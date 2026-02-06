
{% raw %}
```js

//4868 line

    &.is-error-fallback {
      .coupon-book__card-img {
        width: 48px;
        height: 48px;
        border: 1px solid var(--border-secondary);
        border-radius: var(--radius-xl);
        background-color: var(--bg-gray);
      }
    }


// _utility
  &.isError {
    path[fill="#D0D5DD"] {
      [data-theme="dark"] & {
        fill: var(--fg-disabled);
      }
      @media (prefers-color-scheme: dark) {
        fill: var(--fg-disabled);
      }
    }
  }

<template>
  <!-- S: 할인·쿠폰 -->
  <section class="section bf-discount">
    <div class="bf-section__header">
      <h2 class="title-sub">놓치면 아까운 할인·쿠폰</h2>
    </div>
    <!-- S : 할인·쿠폰 로딩중 스켈레톤 -->
    <div class="cupon-list__body" aria-label="로딩중" tabindex="0">
      <div
        v-for="n in 5"
        :key="n"
        class="cupon-item outline skeleton"
        aria-hidden="true"
      >
        <div class="label">
          <LoadingSkeleton width="40%" :height="22" rounded="small" />
        </div>
        <div class="content">
          <div class="left">
            <LoadingSkeleton width="25%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="26" rounded="small" />
          </div>
          <div class="right">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
        </div>
      </div>
    </div>
    <!-- E : 할인·쿠폰 로딩중 스켈레톤 -->

    <div class="cupon-list__body">
      <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="쿠폰 정보" 추가 -->
      <div
        v-for="coupon in filteredCoupons"
        :key="coupon.id"
        :class="[
          'cupon-item outline',
          { 'is-label': coupon.label || coupon.expiryDate },
          /* 수정 260204: 해당 행 쿠폰 아이콘 이미지 로드 실패 시에만 적용. ScImage @error → onIconError(coupon.id) → iconErrorIds에 추가됨. */
          { 'is-error-fallback': iconErrorIds.includes(coupon.id) },
        ]"
        role="link"
        :aria-label="
          [
            coupon.label ? `쿠폰 상태: ${coupon.label}` : null,
            coupon.expiryDate ? `만료일: ${coupon.expiryDate}` : null,
            coupon.sub,
            coupon.main,
          ]
            .filter(Boolean)
            .join(', ')
        "
      >
        <ListItem align="centered" :left="{ direction: 'reverse' }">
          <template #label v-if="coupon.label || coupon.expiryDate">
            <div class="flex gap-4">
              <!-- 쿠폰 상태 -->
              <SolidLabel
                v-if="coupon.label"
                :title="coupon.label"
                :color="coupon.labelColor || 'blue'"
                class="inline-flex"
              />
              <!-- 만료일 -->
              <TintLabel
                v-if="coupon.expiryDate"
                :title="coupon.expiryDate"
                :color="coupon.expiryDateColor || 'blue'"
              />
            </div>
          </template>
          <template #leftSubText>
            <span aria-hidden="true">{{ coupon.sub }}</span>
          </template>
          <template #leftMainText>
            <strong aria-hidden="true">{{ coupon.main }}</strong>
          </template>
          <template #rightIcon>
            <!-- 수정 260204: img → ScImage.
              - 로드 실패 시: coupon.icon.fallback 있으면 해당 이미지, 없으면 ScImage 기본 ScIcon(empty_image) 노출.
              - @error 시 onIconError로 해당 행에 is-error-fallback 클래스 적용. -->
            <!-- <ScImage
              :src="coupon.icon.src"
              :alt="coupon.icon.alt"
              :fallback="coupon.icon.fallback"
              class="cupon-icon"
              aria-hidden="true"
              @error="onIconError(coupon.id)"
            /> -->
            <ScImage
              :src="coupon.icon.src"
              :alt="coupon.icon.alt"
              class="cupon-icon"
              aria-hidden="true"
              @error="onIconError(coupon.id)"
            />
          </template>
        </ListItem>
      </div>
    </div>

    <div class="bf-section__footer">
      <CapsuleButton
        text="할인·쿠폰 전체보기"
        color="primary"
        variant="outline"
        size="medium"
        :rightIcon="{ iconName: 'Chevron_right' }"
      />
    </div>

    <!-- S : 할인·쿠폰 IF 오류시 노출 -->
    <div class="bf-if__error">
      <div class="bf-if__error-inner">
        <div class="bf-if__error-icon">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/result_icon.png`"
            alt="IF 오류"
          />
        </div>
        <div class="bf-if__error-text">정보를 불러오지 못했어요</div>
        <CapsuleButton
          text="다른 할인·쿠폰 확인하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 할인·쿠폰 IF 오류시 노출 -->
  </section>
  <!-- E: 할인·쿠폰 -->
</template>

<script setup>
import { computed, inject, ref } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  CapsuleButton,
  ListItem,
  LoadingSkeleton,
  SolidLabel,
  TintLabel,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// ========== 수정 260204: 쿠폰 아이콘 이미지 로드 실패 시 해당 행에만 is-error-fallback 클래스 적용 ==========
/** 이미지 로드에 실패한 쿠폰 id 목록. ScImage @error 시 onIconError(coupon.id)로 id가 여기에 추가됨. */
const iconErrorIds = ref([]);
/** ScImage @error 핸들러. 실패한 쿠폰 id를 iconErrorIds에 넣어 해당 행의 :class에서 is-error-fallback이 붙도록 함. */
function onIconError(couponId) {
  if (!iconErrorIds.value.includes(couponId)) {
    iconErrorIds.value = [...iconErrorIds.value, couponId];
  }
}

// 쿠폰 리스트 데이터
const couponItems = [
  {
    id: 1,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol01.png`,
      alt: "",
    },
    label: "보유중",
    labelColor: "blue",
    expiryDate: "D-3",
    expiryDateColor: "blue",
    main: "5,000원 캐시백",
    sub: "그리팅몰",
  },
  {
    id: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol02.png`,
      alt: "",
    },
    main: "10,000원 캐시백",
    sub: "CJ더마켓",
  },
  {
    id: 3,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol03.png`,
      alt: "",
    },
    label: "보유중",
    labelColor: "blue",
    expiryDate: "D-3",
    expiryDateColor: "blue",
    main: "5% 캐시백",
    sub: "크록스",
  },
  {
    id: 4,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol04.png`,
      alt: "",
    },
    main: "1,000원 캐시백",
    sub: "파리바게뜨",
  },
  {
    id: 5,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol05.png`,
      alt: "",
    },
    expiryDate: "D-1",
    expiryDateColor: "blue",
    main: "3% 캐시백",
    sub: "구구스",
  },
  // 수정 260204: 이미지 호출 오류 시 UI 확인용. 존재하지 않는 URL → ScImage 로드 실패 → ScIcon(또는 fallback) 노출 및 is-error-fallback 클래스 적용 확인. 확인 후 제거.
  {
    id: 6,
    icon: {
      src: `${$cdnURL}/images/pages/base/__nonexistent_ui_check.png`,
      alt: "",
    },
    main: "이미지 오류 UI 확인용",
    sub: "로드 실패 시 ScIcon 노출",
  },
];

// 필터링된 쿠폰 리스트
const filteredCoupons = computed(() => {
  return couponItems;
});
</script>




// ScImage Component
<template>
  <img
    v-if="!isError"
    ref="imageRef"
    v-bind="$attrs"
    :data-src="src"
    :src="visibleSrc"
    :alt="alt"
    :class="[imageClasses, $attrs.class]"
    :width="width"
    :height="height"
    @load="onLoad"
    @error="onError"
  />
  <!-- 에러 케이스 대체 이미지 -->
  <template v-else>
    <!-- fallback 이미지 제공 -->
    <img
      v-if="fallback"
      v-bind="$attrs"
      :class="['sc-image', 'isFallbackError', $attrs.class]"
      :src="fallback"
      :width="width"
      :height="height"
      alt="이미지를 불러올 수 없습니다."
    />
    <!-- ScIcon은 fragment라 attrs 상속 불가 → span으로 감싸 attrs는 span에만 적용. display:contents로 레이아웃 영향 없음. -->
    <span class="sc-image__error-icon" style="display: contents" v-bind="$attrs">
      <ScIcon
        :class="['sc-image', 'isError', $attrs.class].filter(Boolean).join(' ')"
        iconName="empty_image"
        width="32px"
        height="32px"
      />
    </span>
  </template>
</template>

<script lang="ts">
/**
 * @param {string} src 이미지 실제 URL
 * @param {string} alt 대체 텍스트
 * @param {string | number} width 이미지 너비
 * @param {string | number} height 이미지 높이
 * @param {boolean} lazy lazy loading 적용여부
 * @param {string} fallback Error 대체 이미지
 */
export interface ScImageProps {
  src: string;
  alt?: string;
  width?: string | number;
  height?: string | number;
  lazy?: boolean;
  fallback?: string;
}

/**
 * @param {[event: Event]} load 이미지 loaded 이벤트
 * @param {[event: Event]} error 이미지 error 이벤트
 */
export type ScImageEmits = {
  load: [event: Event];
  error: [event: Event];
};
</script>

<script setup lang="ts">
import { useIntersectionObserver } from "@vueuse/core";
import { type Ref, computed, onMounted, ref, watch } from "vue";
import { ScIcon } from "~/components/shc/icon";
import { ScImageVariants } from "./ScImage.variants";

defineOptions({ inheritAttrs: false });

/** fallback 기본값 없음: 있으면 isFallbackError img 노출, 없으면(undefined) ScIcon(empty_image) 노출 */
const props = withDefaults(defineProps<ScImageProps>(), {
  lazy: true,
});
const emits = defineEmits<ScImageEmits>();

const visibleSrc = ref<string | undefined>(undefined);
const imageRef = ref<HTMLImageElement | null>(null);
const isError = ref(false);

//#region lazy loading
// lazy 옵션 false 일때는 바로 대입
onMounted(() => {
  if (!props.lazy) visibleSrc.value = props.src;
});

const { stop } = useIntersectionObserver(
  imageRef as Ref<HTMLElement | null>,
  ([entry]) => {
    if (entry?.isIntersecting) {
      visibleSrc.value = props.src ?? "";
      stop();
    }
  },
  // 이미지 10% 노출 시 동작
  // lazy 옵션 줄때만 동작
  { threshold: 0.1, immediate: props.lazy }
);
// #endregion

const imageClasses = computed(() =>
  ScImageVariants({
    isError: isError.value,
  })
);

//#region 이벤트 처리
/**
 * Load 이벤트
 * @param {Event} event Load event
 */
const onLoad = (event: Event) => emits("load", event);

/**
 * Error 이벤트
 * @param {Event} event Error Event
 */
const onError = (event: Event) => {
  isError.value = true;
  emits("error", event);
};

watch(
  () => props.src,
  (newValue) => {
    isError.value = false;
    visibleSrc.value = newValue;
  }
);
//#endregion
</script>
























:aria-label="`총 ${couponItems.length}개의 쿠폰을 보유중이에요.`"
:aria-label="`전체쿠폰 ${couponItems.length}개`"

<route lang="yaml">
meta:
  id: SBT021A01
  title: 받은 쿠폰
  menu: "혜택​ > 받은 쿠폰"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: | 
    [추가] 260130: 스켈레톤 추가,
    [접근성 개선]260123: BasicChipGroup control="expand" 옵션추가
    251210: 이미지 ScImage 로 수정
  header:
    variant: sub
    fixed: true
    showBack: true
    home: true
  qa2: 퍼블완료
  ui: | 
    [완료]260120: 마크업 (TBD 아이콘 수정 및 UI 확인용 페이지 추가, SBT021A01-a, SBT021A01-b),
    [완료]260119: 마크업 (상단 네비게이션 우측 close 제거 홈 아이콘 추가 메타정보 수정),
</route>
<template>
  <!-- [수정] UI 확인용: 스켈레톤·본문 둘 다 노출되도록 sc-contents__body 한 겹으로 감쌈. 스켈레톤/본문을 형제가 아닌 동일 body 자식으로 두어 빌드 시 본문이 가려지지 않음 -->
  <div class="sc-contents__body">
    <!-- [추가] 260130: 스켈레톤 추가 -->
    <!-- S : 로딩중 스켈레톤 -->
    <div
      class="card-grid__skeleton coupon-received-loading"
      aria-label="로딩중"
      tabindex="0"
    >
      <!-- card-grid__skeleton 직계 자식 (들여쓰기 1단계) -->
      <div class="cupon-head">
        <LoadingSkeleton :width="304" :height="33" rounded="small" />
      </div>
      <div class="cupon-chip">
        <LoadingSkeleton :width="88" :height="36" rounded="full" />
        <LoadingSkeleton :width="88" :height="36" rounded="full" />
        <LoadingSkeleton :width="88" :height="36" rounded="full" />
      </div>
      <div class="cupon-list__wrap">
        <div class="cupon-list__head">
          <LoadingSkeleton :width="92" :height="24" rounded="small" />
        </div>
        <div class="cupon-list__body">
          <ul class="webzine-list">
            <li 
              v-for="skeletonIndex in 4" :key="`skeleton-${skeletonIndex}`"
              class="webzine-item"
            >
              <div class="webzine-item__thumbnail">
                <LoadingSkeleton
                  :width="48"
                  :height="48"
                />
              </div>
              <div class="webzine-item__content">
                <LoadingSkeleton
                  :width="87"
                  :height="22"
                  rounded="small"
                />
                <LoadingSkeleton
                  :width="200"
                  :height="22"
                  rounded="small"
                />
                <LoadingSkeleton
                  :width="130"
                  :height="22"
                  rounded="small"
                />
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!-- E : 로딩중 스켈레톤 -->

    <!-- 본문: sc-contents__body 직계 자식, 스켈레톤과 형제 -->
    <div class="cupon-contents">
      <!-- S : 모바일상품권 + 할인쿠폰이 있을 경우 -->
      <template v-if="couponItems.length > 0">
        <div
          class="cupon-head"
          tabindex="0"
          aria-label="총 {{ couponItems.length }}개의 쿠폰을 보유중이에요."
        >
          <p aria-hidden="true">
            총 <em class="cupon-count">{{ couponItems.length }}</em
            >개의 쿠폰을 보유중이에요.
          </p>
        </div>
        <div class="cupon-chip">
          <!-- [v0.9 접근성 개선] 260123: control="expand" 옵션추가 -->
          <BasicChipGroup
            :control="chipControl"
            :items="items"
            variant="solid"
            control="expand"
            v-model="selectedValue"
          />
        </div>
      </template>
      <!-- E : 모바일상품권 + 할인쿠폰이 있을 경우 -->

      <!-- S : 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->
      <template v-else>
        <div class="cupon-top__btngroup">
          <BoxButtonGroup variant="50:50">
            <BoxButton size="large" color="tertiary" text="스탬프쿠폰">
              <template #icon>
                <!-- 아이콘 TBD 추 후 변경 -->
                <!-- 260120: 이미지 변경 -->
                <!-- <Icon name="sample-icon" width="34px" height="34px" /> -->
              <img :src="`${$cdnURL}/images/pages/base/img_shinhan.png`" alt="" aria-hidden="true" />
              </template>
            </BoxButton>
            <BoxButton size="large" color="tertiary" text="기프트샵">
              <template #icon>
                <!-- 아이콘 TBD 추 후 변경 -->
                <!-- 260120: 이미지 변경 -->
                <!-- <Icon name="sample-icon" width="34px" height="34px" /> -->
                <img :src="`${$cdnURL}/images/pages/base/img_giftshop.png`" alt="" aria-hidden="true" />
              </template>
            </BoxButton>
          </BoxButtonGroup>

          <Divider
            variant="basic"
            color="tertiary"
            size="full"
            orientation="horizontal"
          />
        </div>
      </template>
      <!-- E : 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->

      <!-- S : 모바일상품권 + 할인쿠폰이 있을 경우 -->
      <template v-if="couponItems.length > 0">
        <div class="cupon-list__wrap">
          <div class="cupon-list__head">
            <strong
              class="cupon-head__text"
              aria-label="전체쿠폰 {{ couponItems.length }}개"
              tabindex="0"
            >
              <span aria-hidden="true"
                >전체쿠폰 <em class="cupon-count">{{ couponItems.length }}</em
                >개</span
              >
            </strong>
            <Tooltip
              :open="false"
              placement="top-left"
              :showClose="true"
              :size="20"
              class="select-type__tooltip"
            >
              <template #content>
                <div class="sc-tooltip__content">
                  <strong class="sc-tooltip-content__title"
                    >쿠폰 개수가 다르다면?</strong
                  >
                  <p>
                    쿠폰별로 받기 또는 사용 반영까지 최대 하루정도 소요될 수
                    있어요
                  </p>
                </div>
              </template>
            </Tooltip>
          </div>
          <div class="cupon-list__body">
            <div
              v-for="coupon in couponItems"
              :key="coupon.id"
              class="cupon-item"
              tabindex="0"
            >
              <ListItem align="centered">
                <template #leftIcon>
                  <ScImage
                    :src="coupon.icon.src"
                    :alt="coupon.icon.alt"
                    class="cupon-icon"
                    aria-hidden="true"
                  />
                </template>
                <template #leftMainText>
                  <span>{{ coupon.mainsub }}</span>
                  <strong>{{ coupon.main }}</strong>
                </template>
                <template #leftSubText>
                  {{ coupon.sub }}
                </template>
              </ListItem>
            </div>
          </div>
        </div>
      </template>
      <!-- E : 모바일상품권 + 할인쿠폰이 있을 경우 -->

      <template v-else>
        <!-- S : 모바일상품권 5장 + 할인쿠폰 0장 인 경우 & 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->
        <div class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- 260120: 이미지 변경 -->
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <ScIcon
                iconName="icon-nodata"
                width="56px"
                height="56px"
              />
            </div>
            <div class="empty__main">
              <p>받은 쿠폰이 없습니다.</p>
            </div>
            <div class="empty__btn">
              <BoxButton
                color="quaternary"
                size="medium"
                text="쿠폰 받으러 가기"
              />
            </div>
          </div>
        </div>
        <!-- E : 모바일상품권 5장 + 할인쿠폰 0장 인 경우 & 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->

        <!-- S : 모바일상품권 0 + 할인쿠폰 3장 인 경우 -->
        <div class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- 260120: 이미지 변경 -->
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <ScIcon
                iconName="icon-nodata"
                width="56px"
                height="56px"
              />
            </div>
            <div class="empty__main">
              <p>보유한 모바일상품권이 없습니다.</p>
            </div>
            <div class="empty__btn">
              <BoxButton
                color="quaternary"
                size="medium"
                text="기프트샵 가기"
              />
            </div>
          </div>
        </div>
        <!-- E : 모바일상품권 0 + 할인쿠폰 3장 인 경우 -->
      </template>
    </div>
  </div>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { inject } from "vue";
import { ref, computed } from "vue";
import {
  BasicChipGroup,
  Tooltip,
  ListItem,
  BoxButton,
  BoxButtonGroup,
  Divider,
  LoadingSkeleton
} from "@shc-nss/ui/solid";
import { ScIcon, ScImage } from "@shc-nss/ui/shc";

const { $cdnURL } = inject(AppContextKey);
// 첫 번째 칩을 선택된 상태로 초기화
const selectedValue = ref("1");
const items = [
  {
    text: "전체",
    value: "1",
  },
  {
    text: "모바일 상품권",
    value: "2",
  },
  {
    text: "할인쿠폰",
    value: "3",
  },
];

// 칩 개수에 따라 control 설정 (기본: none, 많으면: expand)
const chipControl = computed(() => {
  return items.length >= 4 ? "expand" : "none";
});

// 쿠폰 리스트 데이터 (이미지 참조)
const couponItems = [
  {
    id: 1,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    mainsub: "2025.01.01까지",
    main: "마이카플러스 신규 가입 이벤트",
    sub: "배달의 민족 5,000원건",
  },
  {
    id: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    mainsub: "2025.01.01까지",
    main: "스타벅스",
    sub: "[이벤트] 아이스 카페 아메리카노",
  },
  {
    id: 3,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    mainsub: "2025.01.01까지",
    main: "서브웨이",
    sub: "[이벤트] 아이스 카페 아메리카노",
  },
  {
    id: 4,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "스탬프 쿠폰을 찾고 계세요?",
    sub: "신한 Super SOL",
  },
  {
    id: 5,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    mainsub: "관리비 자동납부하고",
    main: "최대 20만원 캐시백 받기",
  },
  {
    id: 6,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    mainsub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "Tops 쿠폰",
  },
  {
    id: 7,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    mainsub: "결제계좌 변경하고",
    main: "신세계 백화점 상품권 포함 5가지 혜택 받기",
  },
  {
    id: 8,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    mainsub: "결제계좌 변경하고",
    main: "스타벅스 쿠폰 받기",
  },
  {
    id: 9,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon7.png`,
      alt: "",
    },
    mainsub: "캐시백부터 할인까지 여기 다 있ZIP",
    main: "해외여행 필수템",
  },
  {
    id: 10,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    mainsub: "SOL페이에 티머니 등록하고",
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
];

</script>





// 3165 라인

      &.is-error-fallback .sv-list__icon {
        background-color: var(--bg-gray);
        img {
          width: 32px;
          height: 32px;
        }
      }


// discount
<template>
  <!-- S: 할인·쿠폰 -->
  <section class="section bf-discount">
    <div class="bf-section__header">
      <h2 class="title-sub">놓치면 아까운 할인·쿠폰</h2>
    </div>
    <!-- S : 할인·쿠폰 로딩중 스켈레톤 -->
    <div class="cupon-list__body" aria-label="로딩중" tabindex="0">
      <div
        v-for="n in 5"
        :key="n"
        class="cupon-item outline skeleton"
        aria-hidden="true"
      >
        <div class="label">
          <LoadingSkeleton width="40%" :height="22" rounded="small" />
        </div>
        <div class="content">
          <div class="left">
            <LoadingSkeleton width="25%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="26" rounded="small" />
          </div>
          <div class="right">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
        </div>
      </div>
    </div>
    <!-- E : 할인·쿠폰 로딩중 스켈레톤 -->

    <div class="cupon-list__body">
      <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="쿠폰 정보" 추가 -->
      <div
        v-for="coupon in filteredCoupons"
        :key="coupon.id"
        :class="[
          'cupon-item outline',
          { 'is-label': coupon.label || coupon.expiryDate },
          /* 수정 260204: 해당 행의 쿠폰 아이콘 이미지 로드 실패(통신 오류) 시에만 적용.
             ScImage @error 발생 시 onIconError(coupon.id)로 id가 iconErrorIds에 추가됨. */
          { 'is-error-fallback': iconErrorIds.includes(coupon.id) },
        ]"
        role="link"
        :aria-label="
          [
            coupon.label ? `쿠폰 상태: ${coupon.label}` : null,
            coupon.expiryDate ? `만료일: ${coupon.expiryDate}` : null,
            coupon.sub,
            coupon.main,
          ]
            .filter(Boolean)
            .join(', ')
        "
      >
        <ListItem align="centered" :left="{ direction: 'reverse' }">
          <template #label v-if="coupon.label || coupon.expiryDate">
            <div class="flex gap-4">
              <!-- 쿠폰 상태 -->
              <SolidLabel
                v-if="coupon.label"
                :title="coupon.label"
                :color="coupon.labelColor || 'blue'"
                class="inline-flex"
              />
              <!-- 만료일 -->
              <TintLabel
                v-if="coupon.expiryDate"
                :title="coupon.expiryDate"
                :color="coupon.expiryDateColor || 'blue'"
              />
            </div>
          </template>
          <template #leftSubText>
            <span aria-hidden="true">{{ coupon.sub }}</span>
          </template>
          <template #leftMainText>
            <strong aria-hidden="true">{{ coupon.main }}</strong>
          </template>
          <template #rightIcon>
            <!-- 수정 260204: img → ScImage. 통신 오류 시 fallback 이미지 노출, 다크모드 시 fallback 별도 이미지. -->
            <ScImage
              :src="coupon.icon.src"
              :alt="coupon.icon.alt"
              class="cupon-icon"
              aria-hidden="true"
              :fallback="fallbackImageUrl"
              @error="onIconError(coupon.id)"
            />
          </template>
        </ListItem>
      </div>

      <!-- 통신 오류 UI 확인용: 존재하지 않는 이미지 URL로 의도적 404 → ScImage @error 발생 → fallback 노출 및 is-error-fallback 클래스 적용. 확인 후 블록 삭제 가능. -->
      <div
        v-for="coupon in filteredCoupons"
        :key="coupon.id"
        :class="[
          'cupon-item outline',
          { 'is-label': coupon.label || coupon.expiryDate },
          { 'is-error-fallback': iconErrorIds.includes(coupon.id) },
        ]"
        role="link"
        :aria-label="
          [
            coupon.label ? `쿠폰 상태: ${coupon.label}` : null,
            coupon.expiryDate ? `만료일: ${coupon.expiryDate}` : null,
            coupon.sub,
            coupon.main,
          ]
            .filter(Boolean)
            .join(', ')
        "
      >
        <ListItem align="centered" :left="{ direction: 'reverse' }">
          <template #label v-if="coupon.label || coupon.expiryDate">
            <div class="flex gap-4">
              <!-- 쿠폰 상태 -->
              <SolidLabel
                v-if="coupon.label"
                :title="coupon.label"
                :color="coupon.labelColor || 'blue'"
                class="inline-flex"
              />
              <!-- 만료일 -->
              <TintLabel
                v-if="coupon.expiryDate"
                :title="coupon.expiryDate"
                :color="coupon.expiryDateColor || 'blue'"
              />
            </div>
          </template>
          <template #leftSubText>
            <span aria-hidden="true">{{ coupon.sub }}</span>
          </template>
          <template #leftMainText>
            <strong aria-hidden="true">{{ coupon.main }}</strong>
          </template>
          <template #rightIcon>
            <!-- UI확인용: __nonexistent_ui_check.png(404) 사용 → 로드 실패 시 fallback·is-error-fallback 동작 확인. -->
            <ScImage
              :src="`${$cdnURL}/images/pages/base/__nonexistent_ui_check.png`"
              :alt="coupon.icon.alt"
              class="cupon-icon"
              aria-hidden="true"
              :fallback="fallbackImageUrl"
              @error="onIconError(coupon.id)"
            />
          </template>
        </ListItem>
      </div>
    </div>

    <div class="bf-section__footer">
      <CapsuleButton
        text="할인·쿠폰 전체보기"
        color="primary"
        variant="outline"
        size="medium"
        :rightIcon="{ iconName: 'Chevron_right' }"
      />
    </div>

    <!-- S : 할인·쿠폰 IF 오류시 노출 -->
    <div class="bf-if__error">
      <div class="bf-if__error-inner">
        <div class="bf-if__error-icon">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/result_icon.png`"
            alt="IF 오류"
          />
        </div>
        <div class="bf-if__error-text">정보를 불러오지 못했어요</div>
        <CapsuleButton
          text="다른 할인·쿠폰 확인하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 할인·쿠폰 IF 오류시 노출 -->
  </section>
  <!-- E: 할인·쿠폰 -->
</template>

<script setup>
import { computed, inject, onMounted, onUnmounted, ref } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  CapsuleButton,
  ListItem,
  LoadingSkeleton,
  SolidLabel,
  TintLabel,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// ========== 수정 260204: 테마 기반 fallback 이미지 (라이트/다크 분리) ==========
// DOM의 data-theme을 기준으로 하여, 앱 스토어·콘솔·외부 코드 등 어떤 경로로 테마가 바뀌어도 반영되도록 함.
// (이전에는 Pinia 테마 스토어만 참조해, 콘솔에서 setAttribute('data-theme')로 변경 시 반영되지 않던 문제 해결)

/** <html>의 data-theme 속성값 ('light' | 'dark' | null). null이면 시스템 설정(prefers-color-scheme) 따름. */
const dataTheme = ref(null);
/** 테마가 'system'일 때 사용. prefers-color-scheme: dark 미디어 쿼리 결과. */
const systemDark = ref(false);
let observer = null;
let mediaQuery = null;

/** document.documentElement.getAttribute('data-theme')을 읽어 dataTheme에 반영. SSR 대응으로 document 존재 시에만 실행. */
function readDataTheme() {
  if (typeof document === "undefined") return;
  dataTheme.value = document.documentElement.getAttribute("data-theme");
}

onMounted(() => {
  readDataTheme();
  // data-theme 속성 변경 감지 (스토어 토글, 콘솔 setAttribute, 브릿지 등 모든 경로 반영)
  observer = new MutationObserver((mutations) => {
    for (const m of mutations) {
      if (m.attributeName === "data-theme") {
        readDataTheme();
        break;
      }
    }
  });
  observer.observe(document.documentElement, { attributes: true });

  // 시스템 테마(system 모드)용: prefers-color-scheme 변경 시 systemDark 갱신
  mediaQuery = window.matchMedia("(prefers-color-scheme: dark)");
  systemDark.value = mediaQuery.matches;
  const onSystemThemeChange = () => {
    systemDark.value = mediaQuery.matches;
  };
  mediaQuery.addEventListener("change", onSystemThemeChange);
  onUnmounted(() => mediaQuery.removeEventListener("change", onSystemThemeChange));
});

onUnmounted(() => {
  observer?.disconnect();
});

/** 실제 화면에 적용 중인 다크모드 여부. data-theme이 'dark'이거나, (system 모드일 때) systemDark가 true이면 다크. */
const isResolvedDark = computed(
  () =>
    dataTheme.value === "dark" ||
    (dataTheme.value !== "light" && systemDark.value)
);
/** ScImage 로드 실패 시 노출할 대체 이미지 URL. 다크모드일 때 empty_image_dark.svg, 라이트일 때 empty_image.svg 사용. */
const fallbackImageUrl = computed(() =>
  isResolvedDark.value
    ? `${$cdnURL}/images/pages/base/empty_image_dark.svg`
    : `${$cdnURL}/images/pages/base/empty_image.svg`
);

// ========== 수정 260204: 통신 오류 시 해당 행에만 is-error-fallback 클래스 적용 ==========
/** 이미지 로드에 실패한 쿠폰 id 목록. ScImage @error 시 onIconError(coupon.id)로 추가됨. */
const iconErrorIds = ref([]);
/** ScImage의 @error 핸들러. 실패한 쿠폰 id를 iconErrorIds에 넣어 해당 행에만 is-error-fallback 클래스가 붙도록 함. */
function onIconError(couponId) {
  if (!iconErrorIds.value.includes(couponId)) {
    iconErrorIds.value = [...iconErrorIds.value, couponId];
  }
}

// 쿠폰 리스트 데이터
const couponItems = [
  {
    id: 1,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol01.png`,
      alt: "",
    },
    label: "보유중",
    labelColor: "blue",
    expiryDate: "D-3",
    expiryDateColor: "blue",
    main: "5,000원 캐시백",
    sub: "그리팅몰",
  },
  {
    id: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol02.png`,
      alt: "",
    },
    main: "10,000원 캐시백",
    sub: "CJ더마켓",
  },
  {
    id: 3,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol03.png`,
      alt: "",
    },
    label: "보유중",
    labelColor: "blue",
    expiryDate: "D-3",
    expiryDateColor: "blue",
    main: "5% 캐시백",
    sub: "크록스",
  },
  {
    id: 4,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol04.png`,
      alt: "",
    },
    main: "1,000원 캐시백",
    sub: "파리바게뜨",
  },
  {
    id: 5,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol05.png`,
      alt: "",
    },
    expiryDate: "D-1",
    expiryDateColor: "blue",
    main: "3% 캐시백",
    sub: "구구스",
  },
];

// 필터링된 쿠폰 리스트
const filteredCoupons = computed(() => {
  return couponItems;
});
</script>






      // 조건 충족시
      &.is-satisfied {
        border: 1px solid var(--border-secondary);
        background-color: var(--bg-canvas_white);
      }



// sbt160a01
<route lang="yaml">
meta:
  id: SBT160A01
  title: 혜택
  menu: "혜택 > 혜택 > 이달의 참여현황 (BS)"
  layout: MainLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  appClassList: "app_benefits"
  mainClassList: "benefits_main"
</route>
<template>
  <!--
    이달의 참여현황

    [X] 버튼 Tap > 바텀시트 닫힘

    해당 월 일자 별 참여 현황 노출
    - 지난 일자 중 미참여한 경우 미참여 표시 적용
    - 지나지 않은 일자는 참여 여부 미표시 적용
    - 참여 일에 정답, 오답 여부 표시 적용
    - 등급 달성한 날짜에 획득한 등급 메달 노출

    1-1. 퀴즈 정답 시
      - 해당일 표기
      - 문구: 정답

    1-2. 퀴즈 오답 시
      - 해당일 표기
      - 문구: 오답

    1-3. 퀴즈 미참여 시
      - 해당일 표기
      - 문구: 미참여
      - 미참여 조건: 당일 23시59분까지 미참여인 경우, 익일 00시00분에 현황판 미참여 표기
        ex) 22일 23시59분까지 미참여일때 23일 00시00분에 22일 날짜 현황판에 미참여 표기

    1-4. 퀴즈 등급 조건 충족 시
      - 해당일 표기
      - 월 10회 충족 시 동메달 아이콘 노출
      - 월 20회 충족 시 은메달 아이콘 노출
      - 월 30회 충족 시 금메달 아이콘 노출

    1-5. 미도래일
      - 해당일 표기
      - 미도래일 시 비활성화 및 문구 노출 안함

    1-6. 당월 총 적립 포인트 노출
      - 퀴즈팡팡 관련 모든 포인트 합산한 값을 노출
      - (정답 포인트, 오답 포인트, 힌트보기 포인트, 등급별 포인트)

    1-7. 당월 총 정답 일수 노출
  -->
  <BottomSheet
    v-model="isOpen"
    closableDimm
    dimmed
    :title="`${currentMonth}월 참여현황`"
    class="participation-status__sheet"
  >
    <div class="month-schedule__container">
      <div
        v-for="item in scheduleData"
        :key="item.day"
        class="month-schedule__item"
        :class="{
          'is-not-participated': item.status === 'not-participated',
          'is-incorrect': item.status === 'incorrect',
          'is-correct': item.status === 'correct',
          'is-satisfied': item.medal,
          'is-empty': item.status === null && !item.medal,
        }"
        tabindex="0"
        :aria-label="getAriaLabel(item)"
      >
        <!-- 
          v0.9 2600202: 퀴즈 등급 조건 충족 시 추가
          퀴즈 등급 조건 충족 시 이미지만 노출 
          월 10회 참여 시
          월 20회 참여 시
          월 30회 참여 시
        -->
        <div v-if="item.medal" class="month-schedule__medal" aria-hidden="true">
          <img :src="`${$cdnURL}${item.medal.src}`" alt="" />
        </div>
        <template v-else>
          <div class="month-schedule__number" aria-hidden="true">
            {{ item.day }}
          </div>
          <div
            v-if="item.status"
            class="month-schedule__label"
            :class="`is-${item.status}`"
            aria-hidden="true"
          >
            {{ item.label }}
          </div>
        </template>
      </div>
    </div>
    <div class="month-schedule__total">
      <div
        class="month-schedule__total-item"
        tabindex="0"
        aria-label="당월 총 적립 포인트: 239 포인트"
      >
        <strong class="month-schedule__total-label" aria-hidden="true">
          적립 포인트
        </strong>
        <em class="month-schedule__total-value" aria-hidden="true"> 239P </em>
      </div>
      <Divider
        variant="basic"
        color="tertiary"
        size="full"
        orientation="vertical"
      />
      <div
        class="month-schedule__total-item"
        tabindex="0"
        aria-label="당월 총 정답 일수: 24일"
      >
        <strong class="month-schedule__total-label" aria-hidden="true">
          정답 일수
        </strong>
        <em class="month-schedule__total-value" aria-hidden="true"> 24일 </em>
      </div>
    </div>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { BottomSheet, Divider } from "@shc-nss/ui/solid";
import { AppContextKey } from "@/configs/inject/appContext";
import { defineModel, ref, computed, inject } from "vue";

// ==========================================
// 바텀시트 제어
// ==========================================
// 이미지 경로는 CDN URL을 사용
const { $cdnURL } = inject(AppContextKey);
const isOpen = defineModel({ default: true });

// ==========================================
// Props / 데이터
// ==========================================
// 년도와 달
const currentYear = ref(2025);
const currentMonth = ref(12);

// 실제 참여 데이터
// 상태: 'not-participated' | 'incorrect' | 'correct'
const participationData = ref({
  1: { status: "not-participated", label: "미참여" },
  2: { status: "incorrect", label: "오답" },
  3: { status: "correct", label: "정답" },
  4: { status: "correct", label: "정답" },
  5: { status: "correct", label: "정답" },
  6: { status: "not-participated", label: "미참여" },
  7: { status: "incorrect", label: "오답" },
  8: { status: "correct", label: "정답" },
  9: { status: "not-participated", label: "미참여" },
  // 월 10/20/30회 달성일에는 메달 이미지 노출
  10: {
    status: null,
    label: null,
    medal: {
      src: "/images/pages/benefits/main/Property_level1_status.svg",
      alt: "월 10회 참여 달성",
    },
  },
  11: { status: "correct", label: "정답" },
  12: { status: "correct", label: "정답" },
  13: { status: "not-participated", label: "미참여" },
  14: { status: "not-participated", label: "미참여" },
  15: { status: "not-participated", label: "미참여" },
  16: { status: "not-participated", label: "미참여" },
  17: { status: "correct", label: "정답" },
  18: { status: "correct", label: "정답" },
  19: { status: "correct", label: "정답" },
  20: {
    status: null,
    label: null,
    medal: {
      src: "/images/pages/benefits/main/Property_level2_status.svg",
      alt: "월 20회 참여 달성",
    },
  },
  21: { status: "not-participated", label: "미참여" },
  22: { status: "not-participated", label: "미참여" },
  23: { status: "not-participated", label: "미참여" },
  30: {
    status: null,
    label: null,
    medal: {
      src: "/images/pages/benefits/main/Property_level3_status.svg",
      alt: "월 30회 참여 달성",
    },
  },
});

// ==========================================
// Computed
// ==========================================
// 해당 달의 마지막 날짜 계산
const daysInMonth = computed(() => {
  // 예: currentMonth가 11이면 new Date(2025, 12, 0) = 2026년 1월의 0일 = 2025년 12월의 마지막 날
  // new Date(year, month, 0)는 month월의 이전 달 마지막 날을 반환
  // 따라서 new Date(2025, 11, 0) = 2025년 11월의 마지막 날 = 30일
  return new Date(currentYear.value, currentMonth.value, 0).getDate();
});

// 현재 날짜
const today = computed(() => {
  const now = new Date();
  return {
    year: now.getFullYear(),
    month: now.getMonth() + 1,
    day: now.getDate(),
  };
});

// 해당 날짜가 미래인지 확인
const isFutureDate = (day) => {
  if (currentYear.value > today.value.year) return true;
  if (currentYear.value < today.value.year) return false;
  if (currentMonth.value > today.value.month) return true;
  if (currentMonth.value < today.value.month) return false;
  return day > today.value.day;
};

// 스케줄 데이터 생성
const scheduleData = computed(() => {
  const days = [];

  for (let day = 1; day <= daysInMonth.value; day++) {
    // 미래 날짜는 참여현황 없음
    if (isFutureDate(day)) {
      days.push({ day, status: null, label: null });
    } else {
      // 참여 데이터가 있으면 사용, 없으면 null
      const data = participationData.value[day];
      if (data) {
        days.push({
          day,
          status: data.status,
          label: data.label,
          medal: data.medal,
        });
      } else {
        days.push({ day, status: null, label: null });
      }
    }
  }

  return days;
});

// 메달 여부에 따라 접근성 라벨을 분기
const getAriaLabel = (item) => {
  if (item.medal) {
    return `${currentYear.value}년 ${currentMonth.value}월 ${item.day}일 ${item.medal.alt}`;
  }
  return `${currentYear.value}년 ${currentMonth.value}월 ${item.day}일 참여현황: ${
    item.label || "없음"
  }`;
};
</script>






<li v-for="skeletonIndex in 3" :key="`skeleton-${skeletonIndex}`">
  <LoadingSkeleton width="100%" height="100%" />
</li>

<!-- S : 로딩중 스켈레톤 -->
<div
  class="card-grid__skeleton coupon-book"
  aria-label="로딩중"
  tabindex="0"
>
  <div class="coupon-book__title">
    <LoadingSkeleton :width="150" :height="33" rounded="small" />
  </div>
  <section
    v-for="skeletonSectionIndex in 3"
    :key="`skeleton-section-${skeletonSectionIndex}`"
  >
    <div class="coupon-book__title-sub">
      <LoadingSkeleton :width="195" :height="29" rounded="small" />
    </div>
    <article>
      <ul class="coupon-book__carousel">
        <li
          v-for="cardIndex in 3"
          :key="`skeleton-card-${skeletonSectionIndex}-${cardIndex}`"
          class="coupon-book__card"
        >
          <LoadingSkeleton width="100%" height="100%" />
        </li>
      </ul>
    </article>
  </section>
</div>
<!-- E : 로딩중 스켈레톤 -->




// 힌트 보기 BottomSheet
.picture {
  img {
    max-width: 100%;
    height: auto;
    object-fit: contain;
  }
} 
.hintview-text {
  @include font-set(body-m, 300);
  font-weight: 300;
  color: var(--text-tertiary);
}

<template>
  <BottomSheet
    disableMinHeight
    v-model="isOpen"
    closableDimm
    dimmed
    title="힌트 보기"
    class="bs-hintview__sheet"
  >
    <picture class="picture">
      <img :src="`${$cdnURL}/images/dummy/img_promotion_sample.png`" alt="" />
    </picture>
    <div class="hintview-text">
      터치결제로 결제하면 타임라인에서 랜덤 포인트를 지급하는 페이팡팡 서비스를 이용해보세요.<br />
      결제할 때마다 3P~3,000P까지 랜덤 지급돼요.
    </div>
    <template #footer>
      <BoxButton
        text="확인"
        size="xlarge"
        @click="isOpen = false"
      />
    </template>
  </BottomSheet>
</template>

<script setup>
import { BottomSheet, BoxButton } from "@shc-nss/ui/solid";
import { defineModel } from "vue";

const isOpen = defineModel({ default: true });
</script>

// sbt101a02
<template>
  <FullPopup
    v-model="isOpen"
    :title="bodyTitle"
    :closeable="true"
    @close="handleClose"
  >
    <ScTitle mainTitle="서비스 이용을 위한 약관에<br />동의해주세요." />
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body sc-agree__page">
      <section class="section">
        <div
          class="sc-agree__list compound"
          role="region"
        >
          <div class="agree-list__group">
            <div
              class="agree-item item-basic"
              :class="{ 'is-checked': basicAgree4 }"
            >
              <Checkbox
                v-model="basicAgree4"
                class="agree-item__checkbox item-checkbox__basic"
                variant="box"
                align="left"
              >
                <template #label>
                  <span class="agree-item__label item-label__basic">{{ basicItem4.label }}</span>
                </template>
              </Checkbox>
            </div>

            <!-- ======================================== -->
            <!-- 1뎁스 영역: 기본 약관 항목들 -->
            <!-- ======================================== -->
            <div
              class="agree-sublist"
              role="group"
            >
              <div
                v-for="item in subItems4"
                :key="item.value"
                class="agree-subitem"
              >
                <div
                  class="agree-item agree-item__sub"
                  :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="box"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                    @click.stop
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{ item.label }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    :aria-label="`${item.label} 상세 보기`"
                    class="agree-subitem__trigger"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <Divider
        variant="group"
        color="tertiary"
      />
      <div class="sc-bottom-info__inner">
        <h2 class="sc-bottom-info__title">이용 꿀팁</h2>
        <ListCard variant="solid" as="div" color="gray">
          <ListItem 
            :left="{ 
              mainText: '앱 알림', 
              subText: '적립예정포인트 정보를 실시간으로 받아보세요.',
              direction: 'column'
            }"
          >
            <template #rightControl>
              <ToggleSwitch 
                v-model="appNotificationEnabled"
                @update:modelValue="handleToggleChange('appNotification', $event)"
              />
            </template>
          </ListItem>
        </ListCard>
      </div>
    </div>

    <BottomActionContainer :scrollDim="true">
      <BoxButtonGroup
        size="xlarge"
        variant="100"
      >
        <BoxButton
          text="확인"
          :disabled="!basicAgree4"
        />
      </BoxButtonGroup>
    </BottomActionContainer>
  </FullPopup>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  Divider,
  FullPopup,
  IconButton,
  ListCard,
  ListItem,
  ToggleSwitch,
} from "@shc-nss/ui/solid";
import { computed, ref, watch } from "vue";
import { useRoute } from "vue-router";
import { ScTitle } from "@shc-nss/ui/shc";

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");
const isOpen = defineModel({ default: true });

const handleClose = () => {
  isOpen.value = false;
};

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  { label: "[필수] 개인정보 수집·이용 동의", value: "s4-1" },
  { label: "[필수] 개인정보 제3자 제공동의", value: "s4-2" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);

// 앱 알림 토글 상태
const appNotificationEnabled = ref(true);

/**
 * 동작 로직
 */
function handleToggleChange(type, value) {
  console.log(`${type} toggle changed:`, value);
  // 여기에 토글 변경 시 처리할 로직 추가
}
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산
  basicAgree4.value = set.size === subItems4.length;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    subAgrees4.value = subItems4.map((item) => item.value);
  } else {
    subAgrees4.value = [];
  }
});
</script>


<template>
  <div class="payment-panel payment-panel__daily" aria-label="매일결제">
    <section class="section-head">
      <!-- S : 전일자 카드사용내역 1건 or 다수 인 경우 -->
      <div
        v-if="testValue"
        class="text-daily__title"
        aria-label="지금까지 99,999 포인트 받았어요!"
        tabindex="0"
      >
        <p class="text-daily01" aria-hidden="true">
          <ScImageIcon
            iconName="benefits_welcome_text_daily01"
            width="auto"
            height="18"
            :colorize="false"
            class="svgtext-daily01"
          />
        </p>
        <p class="text-daily02" aria-hidden="true">
          <strong class="text-daily02__point"><em>99,999</em>P</strong>
          <ScImageIcon
            iconName="benefits_welcome_text_daily02"
            width="auto"
            height="28"
            :colorize="false"
            class="svgtext-daily02"
          />
        </p>
      </div>
      <!-- E : 전일자 카드사용내역 1건 or 다수 인 경우 -->

      <!-- S : 포인트 0인 경우(미참여 사용자) -->
      <div
        v-else
        class="text-daily__title"
        aria-label="매일매일 100~1,000 포인트 당첨!"
        tabindex="0"
      >
        <p class="text-daily01" aria-hidden="true">
          <ScImageIcon
            iconName="benefits_welcome_text_daily01-1"
            width="auto"
            height="18"
            :colorize="false"
            class="svgtext-daily01-1"
          />
        </p>
        <p class="text-daily02" aria-hidden="true">
          <strong class="text-daily02__point"><em>100~1,000</em>P</strong>
          <ScImageIcon
            iconName="benefits_welcome_text_daily02-1"
            width="auto"
            height="28"
            :colorize="false"
            class="svgtext-daily02-1"
          />
        </p>
      </div>
      <!-- E : 포인트 0인 경우(미참여 사용자) -->

      <TextButtonUnderline color="secondary" size="medium" text="받은 혜택 확인하기" />
      <div class="img-group" aria-hidden="true">
        <img :src="`${$cdnURL}/images/pages/benefits/welcome/img_daily_main_140x140.png`" alt="" />
      </div>

      <div class="custom-cards__gray-group center">
        <Card
          as="div"
          variant="solid"
          type="basic"
          color="gray"
          class="custom-cards__gray"
          :divider="false"
        >
          <div class="custom-cards__gray-info">
            <p><em>NN</em>일 동안 매일!</p>
            <p>어제 결제했다면, 오늘 포인트가 도착해요</p>
            <p><small>(100~1,000 포인트 랜덤 지급)</small></p>
          </div>
        </Card>
      </div>
    </section>
    <section class="bg-gray">
      <article class="article">
        <div class="custom-cards__group">
          <Card
            v-for="card in dailyCardList"
            :key="card.id"
            as="div"
            color="whiteShadow"
            variant="solid"
            type="basic"
            class="custom-cards"
            :divider="false"
          >
            <div
              class="custom-cards__header"
              tabindex="0"
              :aria-label="`${card.badgeText}. ${card.svgLabel}`"
            >
              <div class="custom-cards__header-title" aria-hidden="true">
                <NumberBadge type="text" :text="card.badgeText" color="gray" inline />
                <ScImageIcon
                  :iconName="card.iconName"
                  width="auto"
                  height="auto"
                  :colorize="false"
                  class="svgtext-custom-cards-title"
                  :aria-label="card.svgLabel"
                />
              </div>
            </div>
            <Divider variant="basic" orientation="horizontal" color="tertiary" aria-hidden="true" />
            <div class="custom-cards__content">
              <div
                v-if="card.isParticipant ?? testValue"
                class="custom-cards__content-item"
                tabindex="0"
                :aria-label="card.participant?.price
                  ? `${card.participant.title}. ${card.participant.price}`
                  : (card.participant?.title ?? '')"
              >
                <span class="custom-cards__title" aria-hidden="true">{{ card.participant?.title }}</span>
                <span
                  v-if="card.participant?.price"
                  class="custom-cards__price"
                  aria-hidden="true"
                >
                  {{ card.participant.price }}
                </span>
              </div>
              <div
                v-else
                class="custom-cards__content-item"
                tabindex="0"
                :aria-label="card.nonParticipantMessage ?? nonParticipantMessage"
              >
                <span class="custom-cards__title" aria-hidden="true">
                  {{ card.nonParticipantMessage ?? nonParticipantMessage }}
                </span>
              </div>
            </div>
            <template #actions>
              <BoxButtonGroup size="large" variant="100">
                <!-- 매일결제 혜택 케이스
                [포인트 받기 전 (조건 충족)]
                버튼명 : 포인트 받기, color : secondary
                [포인트 받 후]
                버튼명 : 받기 완료, disabled : true
                [포인트 만료 시]
                버튼명 : 기간 만료, disabled : true
                [전일자 카드사용내역 5천원 미만]
                버튼명 : 포인트 받기, disabled : true
                -->
                <BoxButton
                  :text="card.button?.text ?? '포인트 받기'"
                  :color="card.button?.color ?? 'secondary'"
                  :disabled="card.button?.disabled ?? !testValue"
                />
              </BoxButtonGroup>

            </template>
          </Card>
        </div>
      </article>
      <div class="custom-divider section-daily bg-gray" aria-hidden="true">
        <ScImageIcon
          iconName="icon-plus-fill"
          width="auto"
          height="auto"
          :colorize="false"
          class="svgicon-plus-fill"
          aria-hidden="true"
        />
      </div>
      <article class="article">
        <div class="custom-cards__group">
          <div class="custom-cards__group-head">
            <div class="group-head__label">
              <NumberBadge type="text" text="기간연장 혜택" color="gray" inline />
            </div>
            <div class="group-head__text" aria-label="통신비 정기결제하면 매일결제 한 달 더!" tabindex="0">
              <!-- S : 전일자 카드사용내역 1건 or 다수 인 경우 -->
              <ScImageIcon
                v-if="testValue"
                iconName="benefits_welcome_text_daily03"
                width="auto"
                height="auto"
                :colorize="false"
                class="svgtext-daily03"
                aria-label="통신비 정기결제하면 매일결제 한 달 더!"
                aria-hidden="true"
              />
              <!-- E : 전일자 카드사용내역 1건 or 다수 인 경우 -->
  
              <!-- S : 포인트 0인 경우(미참여 사용자) -->
              <ScImageIcon
                v-else
                iconName="benefits_welcome_text_daily03-1"
                width="auto"
                height="auto"
                :colorize="false"
                class="svgtext-daily03"
                aria-label="통신비 정기결제 혜택 적용 완료!"
                aria-hidden="true"
              />
              <!-- E : 포인트 0인 경우(미참여 사용자) -->
            </div>
          </div>
          <Card
            as="div"
            color="whiteShadow"
            variant="solid"
            type="basic"
            class="custom-cards"
            :divider="false"
          >
            <div class="custom-cards__content">
              <div class="custom-cards__content-item">
                <img :src="`${$cdnURL}/images/pages/benefits/welcome/img_daily_telecom_140x104.png`" alt="" />
  
                <!-- 포인트 0인경우 (미참여 사용자) -->
                <SolidLabel
                  v-if="!testValue"
                  color="blue"
                  title="혜택 미적용"
                />
                <!-- E : 포인트 0인경우 (미참여 사용자) -->
              </div>
            </div>
            <template #actions>
              <BoxButtonGroup size="large" variant="100">
                <!-- 통신요금 연결 전 -->
                <BoxButton
                  v-if="testValue"
                  text="정기결제 신청하기"
                  color="secondary"
                />
                <!-- E : 통신요금 연결 전 -->
  
                <!-- 통신요금 연결 완료 -->
                <BoxButton
                  v-else
                  text="정기결제 보러가기"
                  color="tertiary"
                />
                <!-- E : 통신요금 연결 완료 -->
              </BoxButtonGroup>
            </template>
          </Card>
        </div>
      </article>  
    </section>
    <section class="section payment-notice">
      <h2 class="title-sub">꼭! 알아두세요</h2>
      <article v-for="section in noticeSections" :key="section.title">
        <h3 class="title-sub__small">{{ section.title }}</h3>
        <UnorderedList :gap="8">
          <template v-for="(item, index) in section.items" :key="index">
            <!-- 일반 아이템 -->
            <UnorderedListItem 
              v-if="typeof item === 'string'"
              variant="bullet"
            >
              <span v-html="item"></span>
            </UnorderedListItem>
            
            <!-- 중첩된 아이템 (이용 예시) -->
            <UnorderedListItem 
              v-else-if="item.type === 'nested'"
              variant="bullet"
            >
              <span>{{ item.title }}</span>
              <UnorderedList :gap="8">
                <UnorderedListItem 
                  v-for="(subItem, subIndex) in item.items" 
                  :key="subIndex"
                  variant="dash"
                >
                  <span>{{ subItem }}</span>
                </UnorderedListItem>
              </UnorderedList>
            </UnorderedListItem>
          </template>
        </UnorderedList>
      </article>
    </section>
  </div>
</template>

<script setup>
import { ScImageIcon } from "@shc-nss/ui/shc";
import {
  BoxButton,
  BoxButtonGroup,
  Card,
  Divider,
  NumberBadge,
  SolidLabel,
  TextButtonUnderline,
  UnorderedList,
  UnorderedListItem
} from "@shc-nss/ui/solid";
import { ref } from "vue";
import { COMMON_NOTICE_SECTION } from "./notice-common";
import { AppContextKey } from "@/configs/inject/appContext";
import { inject } from "vue";
const { $cdnURL } = inject(AppContextKey);

// props로 탭 활성화 상태 받기 (사용하지 않지만 일관성을 위해 정의)
defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

// 임시 UI 확인용 전일자 카드사용내역 1건 or 다수 인 경우 true, 포인트 0인 경우 false
const testValue = ref(true);

const nonParticipantMessage = "오늘 신용카드 쓰고 내일 포인트 받아요!";

// [v0.9] 260127: 참여 이력  포인트 지급 이력 케이스 추가 및 수정
const dailyCardList = [
  // 1. 한번에 5천원 이상 결제
  // 포인트 받기 전(조건 충족)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점을지로파인애비뉴점을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: false
    }
  },
  // 포인트 받은 후
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점을지로파인애비뉴점을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "오늘 N,NNN포인트를 받았어요!",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 없음 (포인트 0/조건 미충족)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    isParticipant: false,
    nonParticipantMessage,
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 결제 금액 5천원 미만
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점",
      price: "1,000원"
    },
    button: {
      text: "5천원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 없음
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    isParticipant: false,
    nonParticipantMessage: "어제 신용카드를 사용하지 않았어요!",
    button: {
      text: "5천원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 있음(만료/혜택 연장 안내)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "통신비 정기결제하면 한달 더 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 2. 합쳐서 5만원 이상 결제
  // 포인트 받기 전(조건 충족)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: false
    }
  },
  // 포인트 받은 후
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "오늘 N,NNN포인트를 받았어요!",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 없음 (포인트 0/조건 미충족)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    isParticipant: false,
    nonParticipantMessage,
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 누적 금액 5만원 미만
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "40,000원"
    },
    button: {
      text: "5만원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 없음
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    isParticipant: false,
    nonParticipantMessage: "어제 신용카드를 사용하지 않았어요!",
    button: {
      text: "5만원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 있음(만료/혜택 연장 안내)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "통신비 정기결제하면 한달 더 받아요",
      color: "secondary",
      disabled: true
    }
  }
];

// 꼭! 알아두세요 데이터
const noticeSections = [
  {
    title: "매일결제",
    items: [
      "접속일 기준 전날 국내 신한 개인신용카드 승인 이력이 있으면 포인트(마이신한포인트) 지급 대상이 됩니다.",
      "포인트를 지급받기 위해선 '이용권유 방법에 대한 동의'의 전화 혹은 문자 메시지(LMS) 중 1개 이상의 항목과 '혜택정보 수신(이용권유) 동의'의 '카드 및 금융 상품·서비스 안내 및 이용 권유를 위한 수집, 이용' 항목에 대해 모두 동의해야 합니다.",
      "매일결제 혜택은 반갑꾸러미 접속 종료일로부터 30일 전까지 제공되며, 신한SOL페이 앱 기준 통신 3사 요금 정기결제에 등록되어 있거나, 직전 30일 내 통신 3사 정기결제 승인 이력이 있는 경우 혜택 제공 기간이 30일 연장됩니다.",
      "소비기록은 마이데이터 가입 및 자산 연결을 통해 확인할 수 있으며, 마이데이터 가입 및 자산 연결에 대해 제공되는 혜택의 규모와 지급 기준은 연결페이지의 상세 내용을 확인하시기 바랍니다.",
      "반갑꾸러미 접속 대상이더라도 이미 마이데이터 이벤트에 대해 혜택 수혜 이력이 있는 경우에는 해당 혜택은 제공되지 않습니다.",
      "통신사 정기결제에 따라 제공되는 매일결제 혜택 기간 연장 혜택은 최대 1개월간 제공되며, 신청 시점과 무관하게 카드 발급일로부터 2개월 뒤 말일에 혜택 제공이 종료됩니다.",
      "통신사 정기결제에 따라 제공되는 매일결제 혜택기간 연장은 통신사 고객센터를 통해 직접 신청할 경우, 즉시 반영되지않으며 신한 SOL페이 앱을 통한 정기결제가 발생해야 받으실 수 있습니다.",
      {
        type: "nested",
        title: "이용 예시",
        items: [
          "예시 1: 통신사 정기결제 등록 시 혜택 기간 연장",
          "예시 2: 신한 SOL페이 앱을 통한 정기결제 발생 시 혜택 지급",
          "예시 3: 마이데이터 가입 및 자산 연결을 통한 혜택 확인"
        ]
      },
      "계약 체결 전, 상품설명서 및 약관을 확인하시기 바랍니다.",
      "금융소비자는 금융소비자보호법 제19조 제 1항에 따라 해당 금융상품 또는 서비스에 대하여 설명받을 권리가 있습니다.",
      "신용카드 발급이 부적정한 경우(개인신용평점 낮음, 연체(단기 포함) 사유 발생 등), 카드 발급이 제한될 수 있습니다.",
      "카드 이용대금과 이에 수반되는 모든 수수료는 고객님께서 지정하신 결제일에 상환하여야 합니다.",
      "<strong>상환능력 대비 신용카드 사용액 과도 시, 개인신용평점이 하락할 수 있습니다.</strong>",
      "<strong>개인신용평점 하락 시, 금융거래 관련 불이익이 발생할 수 있습니다.</strong>",
      "<strong>일정기간 신용카드 이용대금을 연체할 경우, 결제일이 도래하지 않은 모든 신용카드 이용대금을 변제할 의무가 발생할 수 있습니다.</strong>",
      "준법감시 심의필 제00000000-Cpi-000호<br />(2000.00.00~2000.00.00)"
    ]
  },
  COMMON_NOTICE_SECTION
];
</script>








<BoxButton
    size="xlarge"
    ariaLabel="공유하기"
  >
    <template #label>
      <Popover
        placement="bottom-center"
        content="친구에게 자랑해보세요!"
        :open="true"
        color="gray"
      >
        <span>공유하기</span>
      </Popover>
    </template>
  </BoxButton>
</template>

// 보물찾기
.floating-treasure {
  position: fixed;
  bottom: calc(160px + var(--env-b));
  right: 36px;
  z-index: var(--z-index);
  .treasure-container {
    position: relative;
    width: 118px;
    height: 134px;
  } 
  .treasure-close {
    position: absolute;
    top: 29px;
    right: 0;
    z-index: 1;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    width: 40px;
    height: 40px;
    text-align: right;
    line-height: 1;
    .treasure-close-icon {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 20px;
      height: 20px;
      background-color: var(--bg-white);
      border-radius: var(--radius-full);
      color: var(--fg-primary);
      box-shadow: 0px 2px 4px 0px #16192433;
    }
  }
  .treasure-trigger {
    position: relative;
    display: block;
    width: 118px;
    height: 134px;
  }
  .treasure-tooltip {
    position: absolute;
    top: -5px;
    left: 50%;  
    transform: translateX(-50%);
    display: block;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100% auto;
    background-image: url("#{$cdn-url}/images/pages/benefits/main/bg_treasure_tooltip.png");
    width: 83px;
    height: 36px;
    padding-top: 4px;
    @include font-set(body-s, 500);
    font-weight: 500;
    color: var(--white);
    text-align: center;
    animation: treasureBounce .8s ease-in-out infinite;
    /* @keyframes duration | timing-function | delay | iteration-count | direction | fill-mode | play-state | name */
  }
}
// 보물찾기 위치 확인 로딩
.treasure-modal {
  position: fixed;
  top: calc(0px + var(--env-t));
  left: calc(0px + var(--env-l));
  right: calc(0px + var(--env-r));
  bottom: calc(0px + var(--env-b));
  width: 100%;
  height: 100%;
  // background-color: rgba(0, 0, 0, 0.7);
  background-color: var(--bg-canvas_dark_a60);
  z-index: 600;
  pointer-events: auto;
  &.sv-popup--variant-full {
    background-color: var(--bg-canvas_dark_a60);
    .sv-popup__body {
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0;
    }
  }
  &.sv-popup .sv-popup__title {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    color: transparent;
  }
  .sv-popup__close .sv-icon {
    color: var(--white);
  }
  .treasure-modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100%;
    max-width: 312px;
    margin: 0 auto;
  }
  .treasure-loading-pending {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100%;
    text-align: center;
  }
  .loading-enter {
    margin-top: var(--spacing-md);
  }
  .loading-enter-text {
    margin-bottom: 30px;
    span {
      display: block;
      @include font-set(headline-s, 700);
      font-weight: 700;
      color: var(--white);
      text-align: center;
    }
  }
  .treasure-loading-enter {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    max-width: 312px;
    height: auto;
    margin: 0 auto;
    padding: var(--spacing-4xl) 0;
    text-align: center;
  }
  .treasure-loading-body {
    position: relative;
    width: 100%;
    margin-top: calc((30px + 36px + 56px) * -1);
  }
  .treasure-loading-lottie {
    height: 172px;
    .lottie-animation-container {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      overflow: visible;
      margin: 0 auto;
    }
  }
  .treasure-loading-body-text {
    width: 100%;
    padding-top: calc(30px + 36px);
    color: var(--white);
    @include font-set(headline-s, 700);
    font-weight: 700;
    text-align: center;
  }
  .treasure-loading-point {
    display: inline-block;
    @include font-set(headline-l, 800);
    font-weight: 800;
    color: var(--border-yellow);
    animation: treasurePoint .4s ease-in-out .7s backwards;
  }
}


// treasure(보물찾기) animation
@keyframes treasurePoint {
  0% {
    opacity: 0;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes treasureBounce{
  0% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(-5px); }
  100% { transform: translateX(-50%) translateY(0); }
}




```
{% endraw %}
---
