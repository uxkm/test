
{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT128A01
  title: 할인・쿠폰
  menu: "혜택 > 할인・쿠폰 메인화면"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    menu: false
    home: true
  appClassList: "sc-discount__coupon"
  mainClassList: "discount-coupon__main"
</route>
<template>
  <!-- S : 로딩중 스켈레톤 -->
  <div
    class="card-grid__skeleton discount-coupon"
    aria-label="로딩중"
    tabindex="0"
  >
    <section class="bg-canvas_gray" aria-hidden="true">
      <div class="couponbook-cards__area">
        <div class="discount-coupon__header">
          <LoadingSkeleton
            width="65%"
            :height="29"
            rounded="small"
            class="left"
          />
          <LoadingSkeleton
            :width="71"
            :height="29"
            rounded="small"
            class="right"
          />
        </div>
        <article class="couponbook-cards">
          <div class="couponbook-cards__head">
            <LoadingSkeleton width="100%" :height="33" rounded="small" />
          </div>
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <LoadingSkeleton width="100%" height="100%" rounded="small" />
            </div>
            <div class="couponbook-cards__content">
              <LoadingSkeleton width="100%" :height="29" rounded="small" />
              <LoadingSkeleton
                width="100%"
                :height="22"
                rounded="small"
                class="p"
              />
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="35:65">
              <LoadingSkeleton width="100%" :height="48" rounded="medium" />
              <LoadingSkeleton width="100%" :height="48" rounded="medium" />
            </BoxButtonGroup>
          </div>
        </article>
      </div>
    </section>
    <section class="section" aria-hidden="true">
      <div class="discount-coupon__header">
        <h2 class="discount-coupon__title">진행 중인 쿠폰</h2>
        <LoadingSkeleton
          :width="71"
          :height="29"
          rounded="small"
          class="right"
        />
      </div>
      <div class="discount-coupon__search">
        <LoadingSkeleton
          width="calc(100% - 32px)"
          :height="56"
          rounded="medium"
          class="left"
        />
        <LoadingSkeleton
          :width="36"
          :height="36"
          rounded="medium"
          class="right"
        />
      </div>
      <article class="discount-coupon__body">
        <div class="cupon-list__body">
          <div class="cupon-item outline skeleton">
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
          <div class="cupon-item outline skeleton">
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
          <div class="cupon-item outline skeleton">
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
          <div class="cupon-item outline skeleton">
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
          <div class="cupon-item outline skeleton">
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
          <div class="cupon-item outline skeleton">
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
          <div class="cupon-item outline skeleton">
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
      </article>
    </section>
  </div>
  <!-- E : 로딩중 스켈레톤 -->

  <!-- 콘텐츠 영영 -->
  <div class="sc-contents__body discount-coupon">
    <!-- 혜택정보수신동의 X - case9 쿠폰북 띠배너(쿠폰북 다 닫았을 경우) -->
    <div class="discount-coupon__banner" data-color="solid-same">
      <!-- href="" 제공을 안하는 경우 role="link" tabindex="0" 추가 제공한 경우는 제거 접근성 초점 발생 해결하기 위함  -->
      <a role="link" tabindex="0" class="banner-link">
        <div class="discount-coupon__banner-contents" aria-hidden="true">
          <strong>4월 쿠폰북 보기</strong>
        </div>
        <ScImage
          :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon.png`"
          alt=""
          class="discount-coupon__banner-img"
          aria-hidden="true"
        />
      </a>
    </div>

    <!-- 혜택정보수신동의 X - case9 쿠폰북 띠배너(쿠폰북 다 닫았을 경우) 영역자체 숨김 section class="bg-canvas_gray" -->
    <section class="bg-canvas_gray">
      <!-- 혜택정보수신동의 O - case4 상단 배너 있는 경우 노출 -->
      <div class="discount-coupon__banner">
        <!-- href="" 제공을 안하는 경우 role="link" tabindex="0" 추가 제공한 경우는 제거 접근성 초점 발생 해결하기 위함  -->
        <a
          role="link"
          tabindex="0"
          class="banner-link"
          aria-label="곧 마감되는 쿠폰이 있어요! 바로 눌러서 확인해보세요"
        >
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon_icon02_color.png`"
            alt=""
            class="discount-coupon__banner-img"
            aria-hidden="true"
          />
          <div class="discount-coupon__banner-contents" aria-hidden="true">
            <strong>곧 마감되는 쿠폰이 있어요!</strong>
            <p>바로 눌러서 확인해보세요</p>
          </div>
        </a>
        <IconButton
          :color="false"
          :disabled="false"
          size="small"
          aria-label="배너 닫기"
          class="circle-type"
        >
          <template #icon>
            <Icon name="X" size="20" aria-hidden="true" />
          </template>
        </IconButton>
      </div>

      <!-- 혜택정보수신동의 O - 혜택 정보 수신동의 Y -->
      <div class="couponbook-cards__area case1">
        <div class="discount-coupon__header">
          <h2 class="discount-coupon__title">맞춤 혜택 도착</h2>
          <TextButton text="전체보기" color="secondary" size="small" showGoTo />
        </div>
        <article class="couponbook-cards">
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/dummy/img_coupon01.png`"
                alt="Mom's Touch"
              />
            </div>
            <div class="couponbook-cards__content">
              <strong>1,000 마이신한포인트</strong>
              <p>맘스터치 X 신한SOL페이</p>
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="100" class="column">
              <BoxButton size="large" text="혜택 확인하기" color="primary" />
              <TextButton size="small" text="다른 추천받기" color="secondary">
                <template #leftIcon>
                  <Icon name="Arrow_refresh" aria-hidden="true" />
                </template>
                <template #rightIcon>
                  <em class="badge-count">3</em>
                </template>
              </TextButton>
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 O - 혜택 정보 수신동의 Y 남은 맞춤 혜택 1개인 경우 -->
      <div class="couponbook-cards__area case2">
        <div class="discount-coupon__header">
          <h2 class="discount-coupon__title">맞춤 혜택 도착</h2>
          <TextButton text="전체보기" color="secondary" size="small" showGoTo />
        </div>
        <article class="couponbook-cards">
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/dummy/img_coupon02.png`"
                alt="GS25"
              />
            </div>
            <div class="couponbook-cards__content">
              <strong
                >GS25 편의점택배 5천원권 모바일쿠폰 GS25 편의점택배 5천원권 GS25
                편의점택배 5천원권</strong
              >
              <p>
                신한카드 디저트Pick 신규 가입 이벤트 신한카드 디저트Pick 신규
                가입 이벤트
              </p>
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="100" class="column">
              <BoxButton size="large" text="혜택 확인하기" color="primary" />
              <TextButtonUnderline
                size="small"
                text="맞춤 혜택 전체보기"
                color="secondary"
              />
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 O - 혜택 정보 수신동의 Y 혜택명/쿠폰명 로드 실패시 -->
      <div class="couponbook-cards__area case3">
        <div class="discount-coupon__header">
          <h2 class="discount-coupon__title">맞춤 혜택 도착</h2>
          <TextButton text="전체보기" color="secondary" size="small" showGoTo />
        </div>
        <article class="couponbook-cards">
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon_icon01.png`"
                alt="쿠폰"
              />
            </div>
            <div class="couponbook-cards__content">
              <strong>바로 확인하기</strong>
              <p>맞춤 혜택</p>
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="100" class="column">
              <BoxButton size="large" text="혜택 확인하기" color="primary" />
              <TextButtonUnderline
                size="small"
                text="맞춤 혜택 전체보기"
                color="secondary"
              />
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 O - 혜택 정보 수신동의 Y 상단 배너 있는 경우 -->
      <div class="couponbook-cards__area case4">
        <div class="discount-coupon__header">
          <h2 class="discount-coupon__title">맞춤 혜택 도착</h2>
          <TextButton text="전체보기" color="secondary" size="small" showGoTo />
        </div>
        <article class="couponbook-cards">
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/dummy/img_coupon01.png`"
                alt="Mom's Touch"
              />
            </div>
            <div class="couponbook-cards__content">
              <strong>1,000 마이신한포인트</strong>
              <p>맘스터치 X 신한SOL페이</p>
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="100" class="column">
              <BoxButton size="large" text="혜택 확인하기" color="primary" />
              <TextButton size="small" text="다른 추천받기" color="secondary">
                <template #leftIcon>
                  <Icon name="Arrow_refresh" aria-hidden="true" />
                </template>
                <template #rightIcon>
                  <em class="badge-count">3</em>
                </template>
              </TextButton>
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 X - 미동의&타겟 쿠폰 없을 시 -->
      <div class="couponbook-cards__area case5">
        <article class="couponbook-cards">
          <div class="couponbook-cards__head">
            <h2 class="couponbook-cards__title">맞춤 혜택 도착</h2>
            <p class="couponbook-cards__description">
              혜택정보수신에 동의하면 맞춤 혜택을 확인할 수 있어요
            </p>
          </div>
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon_icon01.png`"
                alt="쿠폰"
              />
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="35:65">
              <BoxButton size="large" text="닫기" color="secondary" />
              <BoxButton size="large" text="동의하러 가기" color="primary" />
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 X - 미동의&타겟 쿠폰 있을 시 -->
      <div class="couponbook-cards__area case6">
        <article class="couponbook-cards">
          <div class="couponbook-cards__head">
            <h2 class="couponbook-cards__title">맞춤 혜택 도착</h2>
            <p class="couponbook-cards__description">
              혜택정보수신에 동의하면 맞춤 혜택을 확인할 수 있어요
            </p>
          </div>
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/dummy/img_coupon02.png`"
                alt="GS25"
              />
            </div>
            <div class="couponbook-cards__content">
              <strong
                >GS25 편의점택배 5천원권 모바일쿠폰 GS25 편의점택배 5천원권 GS25
                편의점택배 5천원권</strong
              >
              <p>
                신한카드 디저트Pick 신규 가입 이벤트 신한카드 디저트Pick 신규
                가입 이벤트
              </p>
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="35:65">
              <BoxButton size="large" text="닫기" color="secondary" />
              <BoxButton size="large" text="동의하러 가기" color="primary" />
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 X - 마감임박 알림 배너 -->
      <div class="couponbook-cards__area case7">
        <article class="couponbook-cards">
          <div class="couponbook-cards__head">
            <h2 class="couponbook-cards__title">
              곧 사라지는 쿠폰이<br />60장 있어요
            </h2>
          </div>
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon_icon02.png`"
                alt="쿠폰"
              />
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="35:65">
              <BoxButton size="large" text="닫기" color="secondary" />
              <BoxButton size="large" text="받은쿠폰 보기" color="primary" />
            </BoxButtonGroup>
          </div>
        </article>
      </div>

      <!-- 혜택정보수신동의 X - 쿠폰북 배너 -->
      <div class="couponbook-cards__area case8">
        <article class="couponbook-cards">
          <div class="couponbook-cards__head">
            <h2 class="couponbook-cards__title">5월 쿠폰북 도착</h2>
          </div>
          <div class="couponbook-cards__body">
            <div class="couponbook-cards__img">
              <ScImage
                :src="`${$cdnURL}/images/dummy/img_coupon01.png`"
                alt="Mom's Touch"
              />
            </div>
            <div class="couponbook-cards__content">
              <strong>1,000 마이신한포인트</strong>
              <p>맘스터치 X 신한SOL페이</p>
            </div>
          </div>
          <div class="couponbook-cards__foot">
            <BoxButtonGroup variant="35:65">
              <BoxButton size="large" text="닫기" color="secondary" />
              <BoxButton size="large" text="받은쿠폰 보기" color="primary" />
            </BoxButtonGroup>
          </div>
        </article>
      </div>
    </section>

    <section class="section">
      <div class="discount-coupon__header">
        <h2 class="discount-coupon__title">진행 중인 쿠폰</h2>
        <TextButton text="전체보기" color="secondary" size="small" showGoTo />
      </div>
      <div class="discount-coupon__search">
        <InputField
          id="couponSearch"
          name="couponSearch"
          v-model="searchKeyword"
          placeholder="마이샵, 탑스, 맛있는 쿠폰 검색"
          :show-label="false"
          :show-helper="false"
        >
          <template #button>
            <IconButton aria-label="쿠폰 검색">
              <template #icon>
                <Icon name="Search" size="16" aria-hidden="true" />
              </template>
            </IconButton>
          </template>
        </InputField>
        <IconButton
          :color="false"
          :disabled="false"
          size="small"
          aria-label="조회조건 선택"
          class="circle-type"
          @click="isCategorySheetOpen = true"
        >
          <template #icon>
            <Icon name="Sort" size="20" aria-hidden="true" />
          </template>
        </IconButton>
      </div>
      <article class="discount-coupon__body">
        <div class="cupon-list__body">
          <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="쿠폰 정보" 추가 -->
          <div
            v-for="coupon in filteredCoupons"
            :key="coupon.id"
            :class="[
              'cupon-item outline',
              { 'is-label': coupon.label || coupon.expiryDate },
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
      </article>
    </section>
  </div>

  <!-- 카테고리 선택 바텀시트 SBT128A02 -->
  <BottomSheet
    title="카테고리"
    v-model="isCategorySheetOpen"
    class="category-sheet"
  >
    <div class="category-sheet__content p-none">
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
        <BoxButton text="초기화" color="secondary" @click="resetCategory" />
        <BoxButton text="적용" @click="applyCategory" />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Icon,
  IconButton,
  InputField,
  ListItem,
  LoadingSkeleton,
  RadioCircleGroup,
  SolidLabel,
  TextButton,
  TextButtonUnderline,
  TintLabel,
} from "@shc-nss/ui/solid";
import { computed, inject, ref } from "vue";

const { $cdnURL } = inject(AppContextKey);

const searchKeyword = ref("");
const isCategorySheetOpen = ref(false);
const nextCategoryValue = ref("all");
const selectedCategory = ref("all");

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

function resetCategory() {
  nextCategoryValue.value = "all";
  selectedCategory.value = "all";
}

function applyCategory() {
  selectedCategory.value = nextCategoryValue.value;
  isCategorySheetOpen.value = false;
}

// 필터링된 쿠폰 리스트
const filteredCoupons = computed(() => {
  let filtered = couponItems;

  // 카테고리 필터링
  if (selectedCategory.value !== "all") {
    filtered = filtered.filter(
      (coupon) => coupon.categoryType === selectedCategory.value
    );
  }

  // 검색어 필터링
  if (searchKeyword.value.trim()) {
    const keyword = searchKeyword.value.toLowerCase();
    filtered = filtered.filter(
      (coupon) =>
        coupon.main.toLowerCase().includes(keyword) ||
        coupon.sub.toLowerCase().includes(keyword)
    );
  }

  return filtered;
});

// 쿠폰 리스트 데이터 (이미지 참조)
const couponItems = [
  {
    categoryType: "카페 다이닝",
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
    categoryType: "여가 스포츠",
    id: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol02.png`,
      alt: "",
    },
    main: "1,000원 캐시백",
    sub: "CJ더마켓",
  },
  {
    categoryType: "라이프서비스",
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
    categoryType: "쇼핑",
    id: 4,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol04.png`,
      alt: "",
    },
    main: "1,000원 캐시백",
    sub: "파리바게트",
  },
  {
    categoryType: "헬스",
    id: 5,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol01.png`,
      alt: "",
    },
    expiryDate: "D-Day",
    expiryDateColor: "blue",
    main: "5,000원 캐시백",
    sub: "그리팅몰",
  },
  {
    categoryType: "반려동물",
    id: 6,
    icon: {
      src: `${$cdnURL}/images/dummy/img_coupon_symbol02.png`,
      alt: "",
    },
    main: "1,000원 캐시백",
    sub: "CJ더마켓",
  },
  {
    categoryType: "패션 뷰티",
    id: 7,
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
];
</script>



```
{% endraw %}
---
