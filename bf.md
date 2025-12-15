
{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT137A01
  title: 진행 중인 쿠폰
  menu: "혜택 > 할인 쿠폰 메인화면 > 쿠폰 전체보기"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: |
    251215: 홈페이지와 동기화 디자인 변경에 따른 UI 수정
    251118: floating top button 추가 및 이미지 경로 수정
    251117: 링크 및 접근성 관련 aria-label 속성 추가
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    menu: false
    home: true
</route>
<template>
  <div class="sc-category__group coupon-ongoing">
    <div class="category-filter">
      <div class="category-filter__left">
        <TextDropdown
          placeholder="카테고리"
          size="large"
          @click="openCategorySheet"
        >
          <template #value>
            <span
              :class="[
                'category-filter__label',
                { 'is-active': !!selectedCategory },
              ]"
            >
              {{ selectedCategoryLabel }}
            </span>
          </template>
        </TextDropdown>
      </div>
      <div class="category-filter__right">
        <Checkbox
          align="left"
          label="받은 쿠폰만 보기"
          variant="box"
          :model-value="showReceivedOnly"
          @update:model-value="toggleReceivedOnly"
        />
      </div>
    </div>
    <ListTitle :title="`쿠폰 ${filteredCoupons.length}개`" :divider="false">
      <TextButton color="secondary" size="xsmall">
        <template #leftIcon>
          <span aria-hidden="true">
            <ScIcon iconName="Arrow_refresh" size="16" />
          </span>
        </template>
        <template #label>
          <span class="text-tertiary font-weight-300">쿠폰 새로고침</span>
        </template>
      </TextButton>
    </ListTitle>
  </div>
  <div class="sc-contents__body coupon-ongoing">
    <div class="cupon-contents">
      <div class="cupon-list__wrap">
        <div class="cupon-list__body">
          <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="쿠폰 정보" 추가 -->
          <div
            v-for="coupon in filteredCoupons"
            :key="coupon.id"
            class="cupon-item outline"
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
            <ListItem align="centered" :left="{ direction: 'reverse' }">
              <template #leftSubText>
                <span aria-hidden="true">{{ coupon.sub }}</span>
              </template>
              <template #leftMainText>
                <strong aria-hidden="true">{{ coupon.main }}</strong>
              </template>
              <template #rightIcon>
                <img
                  :src="coupon.icon.src"
                  :alt="coupon.icon.alt"
                  class="cupon-icon"
                  aria-hidden="true"
                />
              </template>
            </ListItem>
          </div>
        </div>
      </div>

      <!-- 카테고리 쿠폰 없음 -->
      <NoData v-if="showReceivedNoData" mainText="받은 쿠폰이 없습니다." />

      <NoData
        v-else-if="showFilteredNoData"
        mainText="해당되는 쿠폰이 없습니다."
        subText="카테고리를 다시 설정해 주세요."
      />
    </div>
  </div>
  <div class="search-floating__btn">
    <CapsuleButton size="large" text="쿠폰 검색" variant="tonal">
      <template #leftIcon>
        <Icon name="Search" size="24" aria-hidden="true" />
      </template>
    </CapsuleButton>
  </div>

  <!-- floating top button 추가 -->
  <FabScrollTop
    ariaLabel="화면 상단으로 이동"
    :bottom="20"
    :right="20"
    :offset="20"
    :overlayOffset="20"
    :revealDelta="-0.1"
    :showThreshold="0"
    color="primary"
    layoutStrategy="overlaySafeArea"
    overlayActive
    overlayIncludeMargins
    overlayPosition="bottom"
    size="medium"
    class="sc-floating__topbtn"
  />

  <!-- 카테고리 선택 바텀시트 -->
  <BottomSheet
    title="카테고리"
    v-model="isCategorySheetOpen"
    class="category-sheet"
  >
    <div class="category-sheet__content">
      <RadioCircleGroup
        v-model="nextCategoryValue"
        :items="categories"
        orientation="horizontal"
        labelKey="label"
        valueKey="value"
        class="category-sheet__radio-group"
      />
    </div>
    <template #footer>
      <BoxButtonGroup size="xlarge" variant="35:65">
        <BoxButton text="초기화" color="tertiary" @click="resetCategory" />
        <BoxButton text="적용" @click="applyCategory" />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import useToastStore from "@/stores/common/toast";
import { ScIcon } from "@shc-nss/ui/shc";
import {
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  CapsuleButton,
  Checkbox,
  ListItem,
  ListTitle,
  RadioCircleGroup,
  SolidLabel,
  TextButton,
  TextDropdown,
  TintLabel,
  Icon,
  FabScrollTop,
} from "@shc-nss/ui/solid";
import { computed, inject, ref } from "vue";

import NoData from "../../_module/NoData.vue";

const { $cdnURL } = inject(AppContextKey);
const { toast } = useToastStore();

const categories = [
  {
    label: "전체",
    value: "all",
  },
  {
    label: "카페·다이닝",
    value: "카페 다이닝",
  },
  {
    label: "여가·스포츠",
    value: "여가 스포츠",
  },
  {
    label: "라이프서비스",
    value: "라이프서비스",
  },
  {
    label: "쇼핑",
    value: "쇼핑",
  },
  {
    label: "헬스",
    value: "헬스",
  },
  {
    label: "반려동물",
    value: "반려동물",
  },
  {
    label: "패션·뷰티",
    value: "패션 뷰티",
  },
  {
    label: "여행",
    value: "여행",
  },
  {
    label: "금융·렌탈",
    value: "금융 렌탈",
  },
  {
    label: "자동차",
    value: "자동차",
  },
  {
    label: "육아·교육",
    value: "육아 교육",
  },
  {
    label: "기타",
    value: "기타",
  },
];

const isCategorySheetOpen = ref(false);
const selectedCategory = ref(null);
const nextCategoryValue = ref("all");
const showReceivedOnly = ref(false);

const selectedCategoryLabel = computed(() => {
  if (!selectedCategory.value) {
    return "카테고리";
  }
  const found = categories.find(
    (category) => category.value === selectedCategory.value
  );
  return found ? found.label : "카테고리";
});

const filteredCoupons = computed(() => {
  const activeCategory = selectedCategory.value || "all";
  const base =
    activeCategory === "all"
      ? couponItems
      : couponItems.filter((coupon) => coupon.categoryType === activeCategory);

  return showReceivedOnly.value
    ? base.filter((coupon) => coupon.received)
    : base;
});

function openCategorySheet() {
  nextCategoryValue.value = selectedCategory.value || "all";
  isCategorySheetOpen.value = true;
}

function toggleReceivedOnly(value) {
  showReceivedOnly.value = value;
  if (value) {
    onShowToast();
  }
}

// 토스트 표시 함수
// 받은 쿠폰만 보기 설정되었습니다. / 받은 쿠폰만 보기 해제되었습니다.
const onShowToast = () => {
  toast.info("받은 쿠폰만 보기 설정되었습니다.", {
    position: "bottom",
    color: "dark",
    autoCloseDuration: 3000,
    offset: 52,
  });
};

function resetCategory() {
  nextCategoryValue.value = "all";
}

function applyCategory() {
  selectedCategory.value = nextCategoryValue.value;
  isCategorySheetOpen.value = false;
}

const showReceivedNoData = computed(
  () => showReceivedOnly.value && filteredCoupons.value.length === 0
);

const showFilteredNoData = computed(
  () => !showReceivedOnly.value && filteredCoupons.value.length === 0
);

// 쿠폰 리스트 데이터 (이미지 참조)
const couponItems = [
  {
    categoryType: "카페 다이닝",
    id: 1,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    label: "이벤트",
    labelColor: "blue",
    expiryDate: "D-14",
    expiryDateColor: "blue",
    main: "마이카플러스 신규 가입 이벤트",
    sub: "배달의 민족 5,000원건",
  },
  {
    categoryType: "여가 스포츠",
    id: 2,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    main: "스타벅스",
    sub: "[이벤트] 아이스 카페 아메리카노",
  },
  {
    categoryType: "라이프서비스",
    id: 3,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    expiryDate: "D-14",
    main: "서브웨이",
    sub: "[이벤트] 아이스 카페 아메리카노",
  },
  {
    categoryType: "쇼핑",
    id: 4,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "스탬프 쿠폰을 찾고 계세요?",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "헬스",
    id: 5,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    expiryDate: "D-Day",
    main: "최대 20만원 캐시백 받기",
  },
  {
    categoryType: "반려동물",
    id: 6,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    main: "Tops 쿠폰",
  },
  {
    categoryType: "패션 뷰티",
    id: 7,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    main: "신세계 백화점 상품권 포함 5가지 혜택 받기",
  },
  {
    categoryType: "여행",
    id: 8,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    main: "스타벅스 쿠폰 받기",
  },
  {
    categoryType: "금융 렌탈",
    id: 9,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon7.png`,
      alt: "",
    },
    main: "해외여행 필수템",
  },
  {
    categoryType: "자동차",
    id: 10,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
  {
    categoryType: "육아 교육",
    id: 11,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
  {
    categoryType: "기타",
    id: 12,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
];
</script>




```
{% endraw %}
---
