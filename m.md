
{% raw %}
```js

// 분리하여 작업 컴포넌트 호출 방식 ScLottie.vue
<template>
  <!-- a11y: 접근성용 재생/정지 버튼 자동 렌더 (래퍼 + 토글 버튼 포함) -->
  <div
    v-if="a11y"
    class="lottie-animation-container lottie-animation-container--a11y"
    :style="a11yWrapperStyle"
  >
    <div
      ref="lottieContainer"
      class="lottie-animation-container__inner"
      :style="lottieStyle"
    />
    <!-- a11y: 재생/정지 토글 버튼 (네이티브 button으로 클릭 안정성 확보) -->
    <button
      type="button"
      class="lottie-animation-container__toggle"
      :aria-label="isPlaying ? '정지' : '재생'"
      @click="togglePlay"
    >
      <ScIcon
        :icon-name="isPlaying ? 'Control_pause' : 'Control_play'"
        :size="24"
      />
    </button>
  </div>
  <!-- a11y 미사용 시 기존 단일 컨테이너 렌더 -->
  <div
    v-else
    ref="lottieContainer"
    class="lottie-animation-container"
    :style="lottieStyle"
  />
</template>

<script lang="ts">
/**
 * @param {string} animationLink
 * @param {boolean} a11y - true 시 재생/정지 접근성 버튼 자동 렌더
 */
export interface ScLottieProps {
  animationLink: string;
  width?: number | string;
  height?: number | string;
  /** a11y 모드에서 래퍼/버튼 레이아웃에 사용 */
  minHeight?: number | string;
  loop?: boolean;
  autoPlay?: boolean;
  speed?: number;
  delay?: number;
  /** true 시 재생/정지 접근성 버튼 자동 렌더 */
  a11y?: boolean;
}
</script>

<script setup lang="ts">
// a11y 모드: IconButton 대신 네이티브 button + ScIcon 사용 (클릭 이벤트 안정성)
import { ScIcon } from "../icon";
import Lottie, { type AnimationItem } from "lottie-web";
import { computed, nextTick, onMounted, onUnmounted, ref, watch } from "vue";

const props = withDefaults(defineProps<ScLottieProps>(), {
  loop: true,
  autoPlay: true,
  a11y: false,
});

const emit = defineEmits<{
  onAnimationLoaded: [item: AnimationItem];
}>();

const lottieContainer = ref<Element | null>(null); // lottie Container
const lottieInstance = ref<AnimationItem | null>(null); // lottie Instance
/** a11y 모드에서 재생/정지 상태 (토글 버튼 UI 및 aria-label 동기화) */
const isPlaying = ref(props.autoPlay);
let delayTimeoutId: ReturnType<typeof setTimeout> | null = null;

const applyPlayState = (instance: AnimationItem, shouldPlay: boolean) => {
  try {
    shouldPlay ? instance.play() : instance.pause();
  } catch {
    // 일부 로띠에서 play/pause 미지원 시 무시
  }
};

/** a11y: lottie-web togglePause() 호출 후 isPlaying 동기화 */
const togglePlay = () => {
  const instance = lottieInstance.value;
  if (!instance) return;
  instance.togglePause();
  isPlaying.value = !instance.isPaused;
};

const lottieStyle = computed(() => {
  const style: Record<string, string> = {};

  if (props.width)
    style.width = typeof props.width === "number" ? `${props.width}px` : props.width;
  if (props.height)
    style.height = typeof props.height === "number" ? `${props.height}px` : props.height;
  if (props.minHeight)
    style.minHeight =
      typeof props.minHeight === "number" ? `${props.minHeight}px` : props.minHeight;

  return style;
});

/** a11y: 토글 버튼 absolute 포지셔닝을 위한 래퍼 스타일 */
const a11yWrapperStyle = computed(() => {
  const style: Record<string, string> = { position: "relative" };
  if (props.minHeight)
    style.minHeight =
      typeof props.minHeight === "number" ? `${props.minHeight}px` : props.minHeight;
  return style;
});

const initLottie = () => {
  if (!lottieContainer.value) return;

  // a11y: 초기 재생 여부를 isPlaying(내부 상태)로 결정
  const shouldAutoplay = props.a11y ? isPlaying.value : props.autoPlay;

  lottieInstance.value = Lottie.loadAnimation({
    container: lottieContainer.value as unknown as Element,
    renderer: "svg",
    loop: props.loop,
    autoplay: shouldAutoplay,
    path: props.animationLink,
  });

  emit("onAnimationLoaded", lottieInstance.value);

  lottieInstance.value.addEventListener("data_ready", () => {
    const instance = lottieInstance.value;
    if (!instance) return;

    props.speed && (instance.playSpeed = props.speed);

    if (props.delay) {
      applyPlayState(instance, false);
      delayTimeoutId = setTimeout(() => {
        // a11y: delay 후 재생 시 isPlaying 반영
        const shouldPlay = props.a11y ? isPlaying.value : props.autoPlay;
        if (shouldPlay && lottieInstance.value) {
          applyPlayState(lottieInstance.value, true);
        }
        delayTimeoutId = null;
      }, props.delay);
    } else {
      // a11y: data_ready 시점에 isPlaying 반영
      const shouldPlay = props.a11y ? isPlaying.value : props.autoPlay;
      applyPlayState(instance, shouldPlay);
    }
  });
};

// nextTick: v-if(a11y) 분기 시 ref 할당 완료 보장 후 초기화
onMounted(async () => {
  await nextTick();
  initLottie();
});

// a11y: isPlaying 변경 시 / 일반: props.autoPlay 변경 시 play/pause 동기화
watch(
  () => (props.a11y ? isPlaying.value : props.autoPlay),
  (shouldPlay) => {
    const instance = lottieInstance.value;
    if (!instance) return;

    if (delayTimeoutId) {
      clearTimeout(delayTimeoutId);
      delayTimeoutId = null;
    }

    applyPlayState(instance, shouldPlay);
  },
);

onUnmounted(() => {
  if (delayTimeoutId) clearTimeout(delayTimeoutId);
  lottieInstance.value?.destroy();
});
</script>


// 호출하는 부분
<div class="lottie-wrap">
  <ScLottie
    :animation-link="$cdnURL + '/images/lottie/common/timeline_etc_info01.json'"
    :autoPlay="true"
    :loop="true"
    :width="'auto'"
    min-height="344px"
    a11y
  />
</div>
  



// 재생/정지 컴포넌트 케이스 2
<route lang="yaml">
  meta:
    id: SMY003A01
    title: 틴즈 도서관
    menu: 마이 > 마이 주니어 > 틴즈도서관 - 안내페이지
    layout: SubLayout
    category: 마이
    publish: 정예린
    publishVersion: 0.8
    status: 작업완료
    header:
      fixed: true
      close: false
      back: true
    qa: 검수완료
    qa2: 검수완료
  </route>
  
  <template>
    <div class="my-junior-library-page">
      <div class="tit-top-txt">
        <p>신한카드 X 교보문고</p>
      </div>
      <ScTitle
        mainTitle="10대라면 교보eBook<br />매달 1권 무료!"
        isHero
      />
  
      <div class="sc-contents__body">
        <div class="section">
          <!-- TBD -->
          <!-- <ScSwiper
            v-bind="argsCard"
            class="pagination-bar sc-swiper--card-select"
          >
            <template #slide="{ item }">
              <div class="swiper-item__card">
                <div class="swiper-item__card__visual">
                  <img
                    :src="item.image"
                    alt=""
                  />
                </div>
              </div>
            </template>
          </ScSwiper> -->
          <div class="lottie-wrap">
            <ScLottie
              :animation-link="$cdnURL + '/images/lottie/common/timeline_etc_info01.json'"
              :autoPlay="true"
              :loop="true"
              :width="'auto'"
              min-height="344px"
              @onAnimationLoaded="handleAnimationLoaded"
            />
            <IconButton
              class="lottie-wrap__toggle"
              :iconName="isPlaying ? 'Control_pause' : 'Control_play'"
              :aria-label="isPlaying ? '정지' : '재생'"
              :color="false"
              size="small"
              @click="togglePlay"
            />
          </div>
          <!-- // TBD -->
  
          <div class="gray-box">
            <UnorderedList :gap="4">
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="이 서비스는 신한 SOL페이 어린이・청소년(만 10세 이상~만 19세 미만)회원만 이용할 수 있는 교보문고 전자도서관 서비스에요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="만 19세 이상이 되면 더이상 틴즈 도서관을 이용할 수 없게 돼요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="매달(1일~말일 기준) 회원 1인 당 도서 1권까지 대여할 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="매달 한정된 eBook 수량을 선착순으로 제공하며, 대여 가능한 수량이 조기 소진되면, 도서는 다음달 1일부터 대여할 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="일부 도서는 대출 상황에 따라 예약 또는 예약대기를 해야할 수도 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="도서 대여기간은 14일이며, 대여기한이 지나면 자동으로 반납돼요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="이 서비스는 신한카드 및 제휴사의 사정에 따라 예고 없이 변경 또는 종료될 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="회원이 부적절한 방법으로 서비스를 이용했다고 판단할 경우, 예고 없이 이용을 제한할 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="틴즈 도서관 이용 관련 문의는 신한카드 고객센터(1544-7000), eBook 콘텐츠(오류・부적절한 콘텐츠 신고 등) 관련 내용은 제휴사인 교보문고 고객센터(1544-1900)에 문의해주세요."
              />
            </UnorderedList>
          </div>
        </div>
      </div>
    </div>
  
    <BottomActionContainer :scrollDim="true">
      <BoxButtonGroup size="xlarge">
        <BoxButton text="도서관 이용하기" />
      </BoxButtonGroup>
    </BottomActionContainer>
  </template>
  
  <script setup>
  import { AppContextKey } from "@/configs/inject/appContext";
  import { ScLottie, ScTitle } from "@shc-nss/ui/shc";
  import {
    BottomActionContainer,
    BoxButton,
    BoxButtonGroup,
    IconButton,
    UnorderedList,
    UnorderedListItem,
  } from "@shc-nss/ui/solid";
  import { inject, ref } from "vue";
  const { $cdnURL } = inject(AppContextKey);
  const isPlaying = ref(true);
  const lottieInstance = ref(null);

  const handleAnimationLoaded = (instance) => {
    lottieInstance.value = instance;
  };

  const togglePlay = () => {
    isPlaying.value = !isPlaying.value;
    try {
      if (lottieInstance.value) {
        isPlaying.value ? lottieInstance.value.play() : lottieInstance.value.pause();
      }
    } catch {
      // 일부 로띠에서 play/pause 미지원 시 무시
    }
  };

  const slidesCard = [
    {
      id: "slide-1",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-2",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-3",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-4",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-4",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
  ];
  
  const argsCard = {
    slides: slidesCard,
    slidesPerView: "auto",
    spaceBetween: "-4%",
    pagination: false,
    paginationType: "bullets",
    navigation: false,
    autoplay: false,
    loop: true,
    centeredSlides: true,
    theme: "default",
    speed: 300,
    direction: "horizontal",
  };
  </script>
  


// 재생/정지 컴포넌트 케이스
<route lang="yaml">
  meta:
    id: SMY003A01
    title: 틴즈 도서관
    menu: 마이 > 마이 주니어 > 틴즈도서관 - 안내페이지
    layout: SubLayout
    category: 마이
    publish: 정예린
    publishVersion: 0.8
    status: 작업완료
    header:
      fixed: true
      close: false
      back: true
    qa: 검수완료
    qa2: 검수완료
  </route>
  
  <template>
    <div class="my-junior-library-page">
      <div class="tit-top-txt">
        <p>신한카드 X 교보문고</p>
      </div>
      <ScTitle
        mainTitle="10대라면 교보eBook<br />매달 1권 무료!"
        isHero
      />
  
      <div class="sc-contents__body">
        <div class="section">
          <!-- TBD -->
          <!-- <ScSwiper
            v-bind="argsCard"
            class="pagination-bar sc-swiper--card-select"
          >
            <template #slide="{ item }">
              <div class="swiper-item__card">
                <div class="swiper-item__card__visual">
                  <img
                    :src="item.image"
                    alt=""
                  />
                </div>
              </div>
            </template>
          </ScSwiper> -->
          <div class="lottie-wrap">
            <ScLottie
              :animation-link="$cdnURL + '/images/lottie/common/timeline_etc_info01.json'"
              :autoPlay="isPlaying"
              :loop="true"
              :width="'auto'"
              min-height="344px"
            />
            <IconButton
              class="lottie-wrap__toggle"
              :iconName="isPlaying ? 'Control_pause' : 'Control_play'"
              :aria-label="isPlaying ? '정지' : '재생'"
              :color="false"
              size="small"
              @click="isPlaying = !isPlaying"
            />
          </div>
          <!-- // TBD -->
  
          <div class="gray-box">
            <UnorderedList :gap="4">
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="이 서비스는 신한 SOL페이 어린이・청소년(만 10세 이상~만 19세 미만)회원만 이용할 수 있는 교보문고 전자도서관 서비스에요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="만 19세 이상이 되면 더이상 틴즈 도서관을 이용할 수 없게 돼요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="매달(1일~말일 기준) 회원 1인 당 도서 1권까지 대여할 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="매달 한정된 eBook 수량을 선착순으로 제공하며, 대여 가능한 수량이 조기 소진되면, 도서는 다음달 1일부터 대여할 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="일부 도서는 대출 상황에 따라 예약 또는 예약대기를 해야할 수도 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="도서 대여기간은 14일이며, 대여기한이 지나면 자동으로 반납돼요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="이 서비스는 신한카드 및 제휴사의 사정에 따라 예고 없이 변경 또는 종료될 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="회원이 부적절한 방법으로 서비스를 이용했다고 판단할 경우, 예고 없이 이용을 제한할 수 있어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="medium"
                text="틴즈 도서관 이용 관련 문의는 신한카드 고객센터(1544-7000), eBook 콘텐츠(오류・부적절한 콘텐츠 신고 등) 관련 내용은 제휴사인 교보문고 고객센터(1544-1900)에 문의해주세요."
              />
            </UnorderedList>
          </div>
        </div>
      </div>
    </div>
  
    <BottomActionContainer :scrollDim="true">
      <BoxButtonGroup size="xlarge">
        <BoxButton text="도서관 이용하기" />
      </BoxButtonGroup>
    </BottomActionContainer>
  </template>
  
  <script setup>
  import { AppContextKey } from "@/configs/inject/appContext";
  import { ScLottie, ScTitle } from "@shc-nss/ui/shc";
  import {
    BottomActionContainer,
    BoxButton,
    BoxButtonGroup,
    IconButton,
    UnorderedList,
    UnorderedListItem,
  } from "@shc-nss/ui/solid";
  import { inject, ref } from "vue";
  const { $cdnURL } = inject(AppContextKey);
  const isPlaying = ref(true);

  const slidesCard = [
    {
      id: "slide-1",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-2",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-3",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-4",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
    {
      id: "slide-4",
      image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
    },
  ];
  
  const argsCard = {
    slides: slidesCard,
    slidesPerView: "auto",
    spaceBetween: "-4%",
    pagination: false,
    paginationType: "bullets",
    navigation: false,
    autoplay: false,
    loop: true,
    centeredSlides: true,
    theme: "default",
    speed: 300,
    direction: "horizontal",
  };
  </script>
  



// 재생/정지 케이스
<route lang="yaml">
meta:
  id: SMY003A01
  title: 틴즈 도서관
  menu: 마이 > 마이 주니어 > 틴즈도서관 - 안내페이지
  layout: SubLayout
  category: 마이
  publish: 정예린
  publishVersion: 0.8
  status: 작업완료
  header:
    fixed: true
    close: false
    back: true
  qa: 검수완료
  qa2: 검수완료
</route>

<template>
  <div class="my-junior-library-page">
    <div class="tit-top-txt">
      <p>신한카드 X 교보문고</p>
    </div>
    <ScTitle mainTitle="10대라면 교보eBook<br />매달 1권 무료!" isHero />

    <div class="sc-contents__body">
      <div class="section">
        <!-- TBD -->
        <!-- <ScSwiper
          v-bind="argsCard"
          class="pagination-bar sc-swiper--card-select"
        >
          <template #slide="{ item }">
            <div class="swiper-item__card">
              <div class="swiper-item__card__visual">
                <img
                  :src="item.image"
                  alt=""
                />
              </div>
            </div>
          </template>
        </ScSwiper> -->
        <div class="lottie-control-wrap">
          <div
            ref="lottieContainerRef"
            class="teenz_book_lottie"
            aria-hidden="true"
          />
          <!-- 재생/정지 토글 -->
          <div class="lottie-control-actions">
            <IconButton
              class="lottie-control-btn"
              size="small"
              :iconName="isLottiePlaying ? 'Control_pause' : 'Control_play'"
              :aria-label="isLottiePlaying ? '일시정지' : '재생'"
              @click="toggleLottiePlay"
            />
          </div>
        </div>
        <!-- // TBD -->

        <div class="gray-box">
          <UnorderedList :gap="4">
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="이 서비스는 신한 SOL페이 어린이・청소년(만 10세 이상~만 19세 미만)회원만 이용할 수 있는 교보문고 전자도서관 서비스에요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="만 19세 이상이 되면 더이상 틴즈 도서관을 이용할 수 없게 돼요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="매달(1일~말일 기준) 회원 1인 당 도서 1권까지 대여할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="매달 한정된 eBook 수량을 선착순으로 제공하며, 대여 가능한 수량이 조기 소진되면, 도서는 다음달 1일부터 대여할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="일부 도서는 대출 상황에 따라 예약 또는 예약대기를 해야할 수도 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="도서 대여기간은 14일이며, 대여기한이 지나면 자동으로 반납돼요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="이 서비스는 신한카드 및 제휴사의 사정에 따라 예고 없이 변경 또는 종료될 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="회원이 부적절한 방법으로 서비스를 이용했다고 판단할 경우, 예고 없이 이용을 제한할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="틴즈 도서관 이용 관련 문의는 신한카드 고객센터(1544-7000), eBook 콘텐츠(오류・부적절한 콘텐츠 신고 등) 관련 내용은 제휴사인 교보문고 고객센터(1544-1900)에 문의해주세요."
            />
          </UnorderedList>
        </div>
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge">
      <BoxButton text="도서관 이용하기" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { ScTitle } from "@shc-nss/ui/shc";
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  IconButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import lottie from "lottie-web";
import { inject, onMounted, onUnmounted, ref } from "vue";

const { $cdnURL } = inject(AppContextKey);

// 로띠 애니메이션 제어용 (lottie-web 직접 로드 - 재생/정지 동작 보장)
const lottieContainerRef = ref(null);
const lottieAnim = ref(null);

onMounted(() => {
  if (!lottieContainerRef.value) return;
  lottieAnim.value = lottie.loadAnimation({
    container: lottieContainerRef.value,
    renderer: "svg",
    loop: true,
    autoplay: true,
    path: `${$cdnURL}/images/lottie/common/timeline_etc_info01.json`,
  });
});

onUnmounted(() => {
  lottieAnim.value?.destroy();
});
const isLottiePlaying = ref(true);

/** 재생/정지 토글: pause() | play() 호출 및 아이콘 상태 동기화 */
function toggleLottiePlay() {
  if (!lottieAnim.value) return;
  if (isLottiePlaying.value) {
    lottieAnim.value.pause();
    isLottiePlaying.value = false;
  } else {
    lottieAnim.value.play();
    isLottiePlaying.value = true;
  }
}

const slidesCard = [
  {
    id: "slide-1",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-2",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-3",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-4",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-4",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
];

const argsCard = {
  slides: slidesCard,
  slidesPerView: "auto",
  spaceBetween: "-4%",
  pagination: false,
  paginationType: "bullets",
  navigation: false,
  autoplay: false,
  loop: true,
  centeredSlides: true,
  theme: "default",
  speed: 300,
  direction: "horizontal",
};
</script>

<style lang="scss" scoped>
/* 로띠 + 컨트롤 버튼 세로 배치 */
.lottie-control-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;

  .teenz_book_lottie {
    width: 100%;
    min-height: 344px;
  }

  .lottie-control-btn {
    display: flex;
    align-items: center;
    gap: 8px;
  }
}
</style>





<route lang="yaml">
meta:
  id: SMY003A01
  title: 틴즈 도서관
  menu: 마이 > 마이 주니어 > 틴즈도서관 - 안내페이지
  layout: SubLayout
  category: 마이
  publish: 정예린
  publishVersion: 0.8
  status: 작업완료
  header:
    fixed: true
    close: false
    back: true
  qa: 검수완료
  qa2: 검수완료
</route>

<template>
  <div class="my-junior-library-page">
    <div class="tit-top-txt">
      <p>신한카드 X 교보문고</p>
    </div>
    <ScTitle
      mainTitle="10대라면 교보eBook<br />매달 1권 무료!"
      isHero
    />

    <div class="sc-contents__body">
      <div class="section">
        <!-- TBD -->
        <!-- <ScSwiper
          v-bind="argsCard"
          class="pagination-bar sc-swiper--card-select"
        >
          <template #slide="{ item }">
            <div class="swiper-item__card">
              <div class="swiper-item__card__visual">
                <img
                  :src="item.image"
                  alt=""
                />
              </div>
            </div>
          </template>
        </ScSwiper> -->
        <ScLottie
          :animation-link="$cdnURL + '/images/lottie/common/timeline_etc_info01.json'"
          autoPlay
          loop
        />
        <!-- // TBD -->

        <div class="gray-box">
          <UnorderedList :gap="4">
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="이 서비스는 신한 SOL페이 어린이・청소년(만 10세 이상~만 19세 미만)회원만 이용할 수 있는 교보문고 전자도서관 서비스에요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="만 19세 이상이 되면 더이상 틴즈 도서관을 이용할 수 없게 돼요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="매달(1일~말일 기준) 회원 1인 당 도서 1권까지 대여할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="매달 한정된 eBook 수량을 선착순으로 제공하며, 대여 가능한 수량이 조기 소진되면, 도서는 다음달 1일부터 대여할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="일부 도서는 대출 상황에 따라 예약 또는 예약대기를 해야할 수도 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="도서 대여기간은 14일이며, 대여기한이 지나면 자동으로 반납돼요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="이 서비스는 신한카드 및 제휴사의 사정에 따라 예고 없이 변경 또는 종료될 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="회원이 부적절한 방법으로 서비스를 이용했다고 판단할 경우, 예고 없이 이용을 제한할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="틴즈 도서관 이용 관련 문의는 신한카드 고객센터(1544-7000), eBook 콘텐츠(오류・부적절한 콘텐츠 신고 등) 관련 내용은 제휴사인 교보문고 고객센터(1544-1900)에 문의해주세요."
            />
          </UnorderedList>
        </div>
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge">
      <BoxButton text="도서관 이용하기" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { ScLottie, ScTitle } from "@shc-nss/ui/shc";
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { inject } from "vue";
const { $cdnURL } = inject(AppContextKey);

const slidesCard = [
  {
    id: "slide-1",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-2",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-3",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-4",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-4",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
];

const argsCard = {
  slides: slidesCard,
  slidesPerView: "auto",
  spaceBetween: "-4%",
  pagination: false,
  paginationType: "bullets",
  navigation: false,
  autoplay: false,
  loop: true,
  centeredSlides: true,
  theme: "default",
  speed: 300,
  direction: "horizontal",
};
</script>

<style lang="scss" scoped></style>




.bs-calendar {
  .sv-bottom-sheet__body {
    padding-right: 0;
    padding-left: 0;
  }
  .bs-calendar-title {
    @include font-set("title-l", 500);
    font-weight: 500;
    color: var(--text-primary);
  }
}



<route lang="yaml">
meta:
  id: SMY018A01
  title: ""
  menu: 마이 > 마이 주니어 > 눈치게임 - 안내페이지 > 인트로 > 게임 완료 > 실시간 차트 > 날짜선택
  layout: EmptyLayout
  category: 마이
  publish: "정예린(김대민)"
  publishVersion: 0.8
  status: 작업완료
  qa: 검수완료
  qa2: 퍼블완료
  ui: |
    [완료] 260219: 마크업 (페이지 -> BottomSheet로 수정. 디자인 동기화)
    [완료] 260130: 마크업 (날짜 타이틀 수정)
  header:
    back: false
</route>

<template>
  <!-- 260219: 구조 수정 페이지 -> BottomSheet로 수정으로 class 제거 및 변경 -->
  <BottomSheet
    disableMinHeight
    title="날짜를 선택해주세요"
    v-model="isOpen"
    class="bs-calendar"
  >
    <div class="bs-calendar-wrap">
      <CalendarDatePicker
        v-model="modelValue"
        @update:modelValue="onChange"
        @clickDay="onClick"
        header="true"
        :formatters="{ formatCaption: (date) => format(date, 'yyyy년 M월') }"
      >
        <template #header-title="{ title }">
          <div>
            <strong class="bs-calendar-title">{{ title }}</strong>
          </div>
        </template>
      </CalendarDatePicker>
    </div>

    <template #footer>
      <BoxButton
        @click="isOpen = false"
        text="확인"
        size="xlarge"
        color="primary"
      />
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomSheet,
  BoxButton,
  CalendarDatePicker,
} from "@shc-nss/ui/solid";
import { format } from "date-fns";
import { ref } from "vue";

const isOpen = defineModel({ default: true });

const modelValue = ref(new Date());

function onChange(v) {
  alert("update:modelValue => " + v);
}

function onClick(v) {
  alert("clickDay => " + v);
}
</script>



```
{% endraw %}
---
