
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
  status: 재작업
  qa: 검수완료
  etc: |
    [접근성 개선] 접근성 개선 - 검색 필드에 show-label false->true, label 추가,
    [디자인 QA] 배너 이미지 사이즈 수정,
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
        <!-- 260107: 디자인 QA 이미지 사이즈 조정 위한 감싸는 구조로 수정 class명 img 에서 div로 변경 -->
        <div class="discount-coupon__banner-img" aria-hidden="true">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon.png`"
            alt=""
          />
        </div>
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
          <!-- 260107: 디자인 QA 이미지 사이즈 조정 위한 감싸는 구조로 수정 class명 img 에서 div로 변경 -->
          <div class="discount-coupon__banner-img" aria-hidden="true">
            <ScImage
              :src="`${$cdnURL}/images/pages/benefits/coupon/img_coupon_icon02_color.png`"
              alt=""
            />
          </div>
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
              <TextButton
                size="small"
                text="다른 추천받기"
                color="secondary"
                :class="{ 'is-refresh': isRefresh }"
                @click="handleRefresh"
              >
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
        <!-- 260107 : 접근성 개선 - show-label false->true, label 추가  -->
        <InputField
          id="couponSearch"
          name="couponSearch"
          v-model="searchKeyword"
          placeholder="마이샵, 탑스, 맛있는 쿠폰 검색"
          label="진행 중인 쿠폰 검색"
          :show-label="true"
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
import { computed, inject, nextTick, ref } from "vue";

const { $cdnURL } = inject(AppContextKey);

const searchKeyword = ref("");
const isCategorySheetOpen = ref(false);
const nextCategoryValue = ref("all");
const selectedCategory = ref("all");
const isRefresh = ref(false);

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

// 다른 추천받기 버튼 클릭 핸들러
// is-refresh 클래스를 추가하여 아이콘 회전 애니메이션 실행 (1초 후 자동 제거)
function handleRefresh() {
  // 클래스를 제거한 후 다시 추가하여 애니메이션 재시작
  isRefresh.value = false;
  nextTick(() => {
    isRefresh.value = true;
    setTimeout(() => {
      isRefresh.value = false;
    }, 1000);
  });
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




<template>
  <section class="bf-recommend-benefit" aria-label="추천 혜택">
    <!-- S : 로딩 스켈레톤-->
    <div class="bf-recommend-benefit__inner skeleton">
      <LoadingSkeleton :width="290" :height="29" rounded="small" />
      <div class="bf-recommend-benefit__intro">
        <LoadingSkeleton width="100%" :height="162" rounded="small" />
      </div>
    </div>
    <!-- E : 로딩 스켈레톤-->

    <div class="bf-recommend-benefit__inner">
      <h2 class="title-sub px-2xl">출근길 혜택 패키지 도착!</h2>
      <div class="bf-recommend-benefit__intro" :hidden="isBodyVisible">
        <div
          class="bf-recommend-benefit__button"
          role="button"
          tabindex="0"
          @click="handleButtonClick"
          @keydown.enter="handleButtonClick"
          @keydown.space.prevent="handleButtonClick"
        >
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/img_goods.png`"
            alt="추천 혜택"
          />
          <div class="tooltip-recommend-benefit">
            <ScImageIcon
              iconName="bg_tooltip"
              size="128"
              height="66"
              class="bg-tooltip"
              aria-hidden="true"
            />
            <span class="tooltip-custom__text">터치해보세요!</span>
          </div>
        </div>
      </div>
      <div
        class="bf-recommend-benefit__body"
        :class="{ 'is-visible': isBodyVisible }"
        :hidden="!isBodyVisible"
      >
        <ul
          ref="webzineListRef"
          class="webzine-list vertical"
          :tabindex="shouldShowPagination ? 0 : undefined"
          :aria-label="webzineListAriaLabel"
        >
          <li
            v-for="(item, index) in displayedItems"
            :key="`${paginationCurrent}-${index}`"
            :class="{ 'is-visible': isBodyVisible }"
          >
            <BasicList
              as="button"
              class="webzine-item"
              :data-color="item.color"
            >
              <div class="webzine-item__before circle">
                <ScImage :src="item.image" alt="" />
              </div>
              <div class="webzine-item__contents">
                <strong class="webzine-item__label">
                  {{ item.label }}
                </strong>
              </div>
              <div class="webzine-item__after">
                <TextBadge
                  v-if="item.badge"
                  variant="tint"
                  color="gray"
                  :text="item.badge"
                />
              </div>
            </BasicList>
          </li>
        </ul>
        <!-- 
          등록한 혜택 개수에 따라 다른 혜택보기 버튼 노출 
          - 혜택 3개 등록 케이스 : 다른 혜택 보기 버튼 미노출
          - 혜택 6개 등록 케이스 : 다른 헤택 보기 버튼 1/2으로 노출
          - 혜택 9개 등록 케이스 : 다른 혜택 보기 버튼 1/3으로 노출
        -->
        <ButtonPagination
          v-if="shouldShowPagination"
          :total="paginationTotal"
          :current="paginationCurrent"
          iconName="Arrow_refresh"
          title="다른 혜택 보기"
          :class="{
            'is-visible': isBodyVisible && isPaginationVisible,
            'is-refresh': isRefresh,
          }"
          @click="handlePaginationClick"
        />
      </div>
    </div>

    <!-- S : 추천 혜택 IF 오류시 노출 -->
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
          text="다른 혜택 확인하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 추천 혜택 IF 오류시 노출 -->
  </section>
</template>

<script setup>
import { computed, inject, nextTick, ref } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage, ScImageIcon } from "@shc-nss/ui/shc";
import {
  BasicList,
  ButtonPagination,
  CapsuleButton,
  IconButton,
  LoadingSkeleton,
  TextBadge,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// 상태 관리
const isBodyVisible = ref(false);
const isPaginationVisible = ref(false);
const isRefresh = ref(false);

// 전체 혜택 아이템 데이터
const allBenefitItems = ref([
  {
    id: 1,
    image: `${$cdnURL}/images/dummy/img_coupon_symbol04.png`,
    label: "파리바케트 아메리카노",
    badge: "34% 할인",
  },
  {
    id: 2,
    image: `${$cdnURL}/images/dummy/img_dummy_car.png`,
    label: "하이팻 이용하기",
    badge: "최대 2만원 캐시백",
  },
  {
    id: 3,
    image: `${$cdnURL}/images/dummy/img_dummy_giftbox.png`,
    label: "버튼 누르기",
    badge: "최대 10포인트",
  },
  {
    id: 4,
    image: `${$cdnURL}/images/dummy/img_coupon_symbol04.png`,
    label: "파리바케트 아메리카노",
    badge: "34% 할인",
  },
  {
    id: 5,
    image: `${$cdnURL}/images/dummy/img_dummy_car.png`,
    label: "하이팻 이용하기",
    badge: "최대 2만원 캐시백",
  },
  {
    id: 6,
    image: `${$cdnURL}/images/dummy/img_dummy_giftbox.png`,
    label: "버튼 누르기",
    badge: "최대 10포인트",
  },
  {
    id: 7,
    image: `${$cdnURL}/images/dummy/img_coupon_symbol04.png`,
    label: "파리바케트 아메리카노",
    badge: "34% 할인",
  },
  {
    id: 8,
    image: `${$cdnURL}/images/dummy/img_dummy_car.png`,
    label: "하이팻 이용하기",
    badge: "최대 2만원 캐시백",
  },
  {
    id: 9,
    image: `${$cdnURL}/images/dummy/img_dummy_giftbox.png`,
    label: "버튼 누르기",
    badge: "최대 10포인트",
  },
]);

// 고정 컬러 순서
const fixedColors = [
  "--palette-blue-100",
  "--palette-monotone-100",
  "--palette-indigo-100",
];

// 전체 항목을 3개씩 그룹화한 배열
const groupedItems = ref([]);

// 항목을 순서대로 3개씩 그룹화하는 함수 (color는 고정)
const initializeItems = () => {
  const groups = [];
  const items = [...allBenefitItems.value];

  // 순서대로 3개씩 그룹화하고 각 그룹의 color를 고정 순서로 할당
  for (let i = 0; i < items.length; i += 3) {
    const group = items.slice(i, i + 3).map((item, index) => ({
      ...item,
      color: fixedColors[index], // color는 고정 순서로 할당
    }));
    groups.push(group);
  }

  groupedItems.value = groups;
};

// 항목을 랜덤으로 섞고 3개씩 그룹화하는 함수 (color는 고정)
const shuffleAndGroupItems = () => {
  const groups = [];
  const items = [...allBenefitItems.value];

  // 데이터만 랜덤으로 섞기 (color 제외)
  const shuffled = items.sort(() => Math.random() - 0.5);

  // 3개씩 그룹화하고 각 그룹의 color를 고정 순서로 할당
  for (let i = 0; i < shuffled.length; i += 3) {
    const group = shuffled.slice(i, i + 3).map((item, index) => ({
      ...item,
      color: fixedColors[index], // color는 고정 순서로 할당
    }));
    groups.push(group);
  }

  groupedItems.value = groups;
};

// 현재 표시할 항목들 (현재 페이지의 3개)
const displayedItems = computed(() => {
  const currentPage = paginationCurrent.value - 1;
  if (currentPage >= 0 && currentPage < groupedItems.value.length) {
    return groupedItems.value[currentPage];
  }
  return [];
});

// 혜택 개수
const totalBenefits = computed(() => allBenefitItems.value.length);

// 페이지네이션 표시 여부 (3개일 때는 미노출)
const shouldShowPagination = computed(() => totalBenefits.value > 3);

// 페이지네이션 total 계산 (3개씩 묶어서 표시)
const paginationTotal = computed(() => {
  if (totalBenefits.value <= 3) return 0;
  return Math.ceil(totalBenefits.value / 3);
});

// 페이지네이션 current (현재 페이지)
const paginationCurrent = ref(1);

// webzine-list ref
const webzineListRef = ref(null);

// webzine-list aria-label (6개 이상일 때만)
const webzineListAriaLabel = computed(() => {
  if (!shouldShowPagination.value) return undefined;

  const total = paginationTotal.value;
  const current = paginationCurrent.value;
  const currentText =
    current === 1 ? "1번째" : current === 2 ? "2번째" : "3번째";

  return `혜택 리스트 총 ${total}개 페이지 중 현재 페이지 ${currentText}`;
});

// 버튼 클릭 핸들러
const handleButtonClick = async () => {
  if (isBodyVisible.value) return; // 이미 열려있으면 무시

  // 처음 로드 시 순서대로 그룹화 (첫 3개는 순서대로)
  initializeItems();

  // 첫 페이지로 초기화
  paginationCurrent.value = 1;

  // body 표시 (CSS에서 타이밍 제어)
  isBodyVisible.value = true;

  // 6개 이상일 때 webzine-list에 포커스 (첫 그룹 진입 시)
  if (shouldShowPagination.value) {
    await nextTick();
    setTimeout(() => {
      webzineListRef.value?.focus();
    }, 100); // DOM 렌더링 대기
  }

  // pagination 타이밍 계산
  setTimeout(() => {
    isPaginationVisible.value = true;
  }, 3000);
};

// 페이지네이션 클릭 핸들러
// is-refresh 클래스를 추가하여 아이콘 회전 애니메이션 실행 (1초 후 자동 제거)
const handlePaginationClick = async () => {
  // 애니메이션 트리거
  isRefresh.value = false;
  await nextTick();
  isRefresh.value = true;
  setTimeout(() => {
    isRefresh.value = false;
  }, 1000);

  // 다음 페이지로 이동 (총 페이지 수를 넘지 않도록)
  if (paginationCurrent.value < paginationTotal.value) {
    paginationCurrent.value += 1;
  } else {
    // 마지막 페이지에서 다시 클릭하면 첫 페이지로 돌아가고 랜덤 재섞기
    shuffleAndGroupItems();
    paginationCurrent.value = 1;
  }

  // isBodyVisible은 한 번 true가 되면 계속 유지 (클릭 시 추가/제거 안 함)
  await nextTick();
  // webzine-list에 포커스 (6개 이상일 때만)
  if (shouldShowPagination.value && webzineListRef.value) {
    setTimeout(() => {
      webzineListRef.value?.focus();
    }, 100); // DOM 렌더링 대기
  }
};
</script>




```
{% endraw %}
---
