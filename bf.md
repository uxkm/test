
{% raw %}
```js


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
  etc: "251210: 이미지 ScImage 로 수정"
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    home: true
  qa2: 퍼블완료
  ui: |  
    [완료]260120: 마크업 (TBD 아이콘 수정 및 UI 확인용 페이지 추가, SBT021A01-a, SBT021A01-b),
</route>
<template>
  <div class="sc-contents__body">
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
          <BasicChipGroup
            :control="chipControl"
            :items="items"
            variant="solid"
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
              <img :src="`${$cdnURL}/images/pages/base/noData.png`" alt="" class="img-feedback-nodata" />
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
              <img :src="`${$cdnURL}/images/pages/base/noData.png`" alt="" class="img-feedback-nodata" />
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
  Icon,
  Divider,
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




<route lang="yaml">
meta:
  id: SBT021A01-a
  title: 받은 쿠폰
  menu: "혜택​ > 받은 쿠폰"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    home: true
  qa2: 퍼블완료
  ui: |  
    [완료]260120: 마크업 (디자인 요청에 따라 UI 확인용 페이지 작업),
</route>
<template>
  <div class="sc-contents__body">
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
          <BasicChipGroup
            :control="chipControl"
            :items="items"
            variant="solid"
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
        <!-- S : 받은 쿠폰 없음 -->
        <div v-if="emptyType === 'coupon'" class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- 260120: 이미지 변경 -->
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <img :src="`${$cdnURL}/images/pages/base/noData.png`" alt="" class="img-feedback-nodata" />
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
        <!-- E : 받은 쿠폰 없음 -->

        <!-- S : 보유한 모바일상품권 없음 -->
        <div v-else-if="emptyType === 'gift'" class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- 260120: 이미지 변경 -->
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <img :src="`${$cdnURL}/images/pages/base/noData.png`" alt="" class="img-feedback-nodata" />
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
        <!-- E : 보유한 모바일상품권 없음 -->
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
  Icon,
  Divider,
} from "@shc-nss/ui/solid";
import { ScIcon, ScImage } from "@shc-nss/ui/shc";

const { $cdnURL } = inject(AppContextKey);
const emptyType = ref("coupon");
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
const couponItems = [];
</script>






<route lang="yaml">
meta:
  id: SBT021A01-b
  title: 받은 쿠폰
  menu: "혜택​ > 받은 쿠폰"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    home: true
  qa2: 퍼블완료
  ui: |  
    [완료]260120: 마크업 (디자인 요청에 따라 UI 확인용 페이지 작업),
</route>
<template>
  <div class="sc-contents__body">
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
          <BasicChipGroup
            :control="chipControl"
            :items="items"
            variant="solid"
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
      <template v-if="visibleItems.length > 0">
        <div class="cupon-list__wrap">
          <div class="cupon-list__head">
            <strong
              class="cupon-head__text"
              aria-label="전체쿠폰 {{ visibleItems.length }}개"
              tabindex="0"
            >
              <span aria-hidden="true"
                >전체쿠폰 <em class="cupon-count">{{ visibleItems.length }}</em
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
              v-for="coupon in visibleItems"
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
        <div v-if="selectedValue === '3'" class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <img :src="`${$cdnURL}/images/pages/base/noData.png`" alt="" class="img-feedback-nodata" />
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
        <div v-else-if="selectedValue === '2'" class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <img :src="`${$cdnURL}/images/pages/base/noData.png`" alt="" class="img-feedback-nodata" />
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
  Icon,
  Divider,
} from "@shc-nss/ui/solid";
import { ScIcon, ScImage } from "@shc-nss/ui/shc";

const { $cdnURL } = inject(AppContextKey);
// 첫 번째 칩을 선택된 상태로 초기화
const selectedValue = ref("2");
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
];

const visibleItems = computed(() => {
  return selectedValue.value === "1" ? couponItems : [];
});

</script>
  


```
{% endraw %}
---
