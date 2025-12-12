# SBT113A01

{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT105A01
  title: 이벤트
  menu: 혜택 > 이벤트 메인화면
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
    home: true
  appClassList: "sc-bf__events"
  mainClassList: "bf-events__submain"
</route>
<template>
  <!-- S : 로딩중 스켈레톤 -->
  <div class="card-grid__skeleton p_events" aria-label="로딩중" tabindex="0">
    <section aria-hidden="true">
      <div class="collection-card__header">
        <LoadingSkeleton width="65%" :height="29" rounded="small" />
      </div>
      <ul class="collection-card__list">
        <li class="collection-card__item">
          <LoadingSkeleton width="100%" :height="228" rounded="medium" />
        </li>
        <li class="collection-card__item">
          <LoadingSkeleton width="100%" :height="228" rounded="medium" />
        </li>
        <li class="collection-card__item">
          <LoadingSkeleton width="100%" :height="228" rounded="medium" />
        </li>
        <li class="collection-card__item">
          <LoadingSkeleton width="100%" :height="228" rounded="medium" />
        </li>
        <li class="collection-card__item">
          <LoadingSkeleton width="100%" :height="228" rounded="medium" />
        </li>
      </ul>
    </section>
    <section aria-hidden="true">
      <div class="collection-card__header">
        <div class="collection-card__header-left">
          <h2 class="title-sub">
            진행중 이벤트
            <Icon name="Chevron_right" :size="28" />
          </h2>
        </div>
        <div class="collection-card__header-right">
          <LoadingSkeleton :width="54" :height="24" rounded="small" />
        </div>
      </div>
      <ul class="webzine-list">
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
        <li class="webzine-item">
          <div class="webzine-item__thumbnail">
            <LoadingSkeleton :width="48" :height="48" rounded="medium" />
          </div>
          <div class="webzine-item__content">
            <LoadingSkeleton width="70%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
          </div>
        </li>
      </ul>
    </section>
  </div>
  <!-- E : 로딩중 스켈레톤 -->

  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body p_events">
    <!-- 
      이미지는 변경 가능성 있음 현재는 디자인에 있는 부분만 제공됨, 
      카드 배경 타입도 디자인에서 제공된 부분만 반영됨

      2. 모음형 이벤트 영역
      - 표시: 모음형 이벤트는 캐러셀 형식으로 제공
      - 개수: 최소 3개, 최대 5개의 이벤트 표시 가능
      - 표시 여부: 이벤트가 3개 미만인 경우 전체 영역 숨김 처리
      - 노출 로직: "[디지털 채널 > 이벤트 관리 > 모음형 이벤트 관리 > 모음형 이벤트 순서 관리]"에서 설정 저장 후 "[FAN 관리 > 전시 관리 공통 > 이벤트 관리]"에서 "동기화" 수행 시 노출 반영
    -->
    <section v-if="collectionEventItems.length >= 3">
      <div class="collection-card__header">
        <h2 class="title-sub">놓치면 손해 이벤트 모음.zip</h2>
      </div>
      <ul class="collection-card__list">
        <li
          v-for="item in collectionEventItems.slice(0, 5)"
          :key="item.id"
          class="collection-card__item"
          :style="{
            backgroundImage: `url(${item.backgroundImage})`,
          }"
        >
          <!-- 
            링크로 연결이 되는 경우에는 collection-card__item-inner 에 role="link" tabindex="0" 추가
            또는 div 대신 <a> 태그 사용 href를 제공하지 않은 경우에는 role="link" tabindex="0" 추가
          -->
          <div class="collection-card__item-inner">
            <div class="collection-card__item-image" aria-hidden="true">
              <img :src="item.iconImage" :alt="item.iconAlt || ''" />
            </div>
            <div class="collection-card__item-content">
              <strong class="collection-card__text-main">{{
                item.title
              }}</strong>
              <p class="collection-card__text-sub" v-html="item.subtitle"></p>
            </div>
          </div>
        </li>
      </ul>
    </section>

    <!--
      3. 진행중 이벤트 영역
        - 노출: 진행 중인 이벤트 8개 노출
        - 로직: ASIS 로직 준수
        - 정렬: "[이벤트 관리 > 이벤트 순서 관리 > SOL Pay]"에서 지정한 순서대로 표시 및 분배, 별도 순서 지정이 없는 경우 최근 등록순
        - TOBE 제외: ASIS에서 제공하는 카테고리, 슈퍼솔 진입점, "내 이벤트" 영역은 TOBE에서 제공하지 않음

      3-1. 전체 이벤트 보기 버튼
        - 설명: 진행 중인 이벤트의 "더보기" 버튼으로 제공
        - 동작: 선택 시 이벤트 완료 페이지로 이동
        - 목록 참조: 진행 중인 이벤트 목록 URL: https://www.shinhancard.com/mob/MOBFM026N/MOBFM026C01.shc

      3-2. 응모 이력 버튼 (참여한 이벤트)
        - 위치: 진행 중인 이벤트 우측에 고정 버튼으로 제공
        - 동작: 선택 시 "응모한 이벤트" 페이지로 이동
        - 로그인 요구: "응모한 이벤트" 페이지는 로그인 시에만 접근 가능
        - 로그인 리다이렉트: 미로그인 상태에서 접근 시 로그인 화면으로 연결
        - 플랫폼 일관성: App, Mobile Web, PC Web 동일하게 제공
    -->
    <section>
      <div class="collection-card__header">
        <div class="collection-card__header-left">
          <h2 class="title-sub">
            진행 중 이벤트
            <IconButton
              iconName="Chevron_right"
              width="28"
              height="28"
              class="more-btn"
              aria-label="진행 중 이벤트 더보기"
            />
          </h2>
        </div>
        <div class="collection-card__header-right">
          <BoxButton text="참여한 이벤트" color="quaternary" class="more-btn" />
        </div>
      </div>
      <div class="category-list__body section">
        <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="이벤트 정보" 추가 -->
        <div
          v-for="item in displayedItems"
          :key="item.id"
          class="category-item"
          role="link"
          tabindex="0"
          :aria-label="
            [item?.label, item?.sub, item?.main, item?.rightLabel]
              .filter((val) => val != null && val !== '')
              .join(' ')
          "
        >
          <!-- 링크인 경우는 aria-hidden="true" 추가 아닌 경우엔 제거 초점 간소화 -->
          <ListItem
            align="centered"
            :left="{ direction: 'reverse' }"
            aria-hidden="true"
          >
            <template #leftIcon>
              <ScImage
                :src="item.icon.src"
                :alt="item.icon.alt"
                class="category-icon"
                aria-hidden="true"
              />
            </template>
            <template #leftSubText>
              <TintLabel
                :title="item.label"
                :color="item.labelColor || 'green'"
                v-if="item.label"
                class="inline-flex"
              />
              <span class="text" v-html="item.sub"></span>
            </template>
            <template #leftMainText>
              <strong v-html="item.main"></strong>
            </template>
            <template #rightControl>
              <TintLabel
                v-if="item.rightLabel"
                :title="item.rightLabel"
                :color="item.rightLabelColor || 'blue'"
              />
            </template>
          </ListItem>
        </div>
      </div>
    </section>
  </div>
</template>
<script setup>
// ==========================================
// Import
// ==========================================
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  BoxButton,
  Icon,
  IconButton,
  ListItem,
  LoadingSkeleton,
  TintLabel,
} from "@shc-nss/ui/solid";
import { computed, inject } from "vue";

// ==========================================
// Inject
// ==========================================
// CDN URL 주입
const { $cdnURL } = inject(AppContextKey);

// ==========================================
// 모음형 이벤트 데이터
// ==========================================
// 최소 3개, 최대 5개의 이벤트 표시 가능
// 이벤트가 3개 미만인 경우 전체 영역 숨김 처리
const collectionEventItems = [
  {
    id: 1,
    title: "해외여행 필수템",
    subtitle: "캐시백부터 할인까지<br />여기 다 있ZIP",
    backgroundImage: `${$cdnURL}/images/pages/benefits/main/bg_card1.svg`,
    iconImage: `${$cdnURL}/images/pages/benefits/main/img_item_collection.svg`,
    iconAlt: "",
  },
  {
    id: 2,
    title: "Tops 쿠폰",
    subtitle: "캐시백부터 할인까지<br />꼼꼼히 준비했ZIP",
    backgroundImage: `${$cdnURL}/images/pages/benefits/main/bg_card2.svg`,
    iconImage: `${$cdnURL}/images/pages/benefits/main/img_coupon_collection.svg`,
    iconAlt: "",
  },
  {
    id: 3,
    title: "제주여행 필수템",
    subtitle: "호텔부터 렌트카까지<br />알짜혜택만 모았ZIP",
    backgroundImage: `${$cdnURL}/images/pages/benefits/main/bg_card3.svg`,
    iconImage: `${$cdnURL}/images/pages/benefits/main/img_item_collection.svg`,
    iconAlt: "",
  },
];

// ==========================================
// 진행중 이벤트 데이터
// ==========================================
// 진행 중인 이벤트 8개 노출
// 종료 이벤트 제외
const ongoingItems = [
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 1,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    rightLabel: "D-14",
    rightLabelColor: "blue",
    sub: "IKEA 신한카드로 결제하고",
    main: "최대 10만원 캐시백 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "apptech",
    id: 2,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    rightLabel: "D-Day",
    sub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "최대 20만원 캐시백 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "travel_accommodation",
    id: 3,
    received: false,
    labelColor: "green",
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    sub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "Tops 쿠폰",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "card_payment",
    id: 4,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    sub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "신세계 백화점 상품권 포함 5가지 혜택 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "youth",
    id: 5,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "결제계좌 변경하고",
    main: "스타벅스 쿠폰 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 6,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    rightLabel: "D-7",
    rightLabelColor: "blue",
    sub: "온라인 쇼핑몰에서",
    main: "최대 5만원 할인 쿠폰",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 7,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    rightLabel: "D-10",
    rightLabelColor: "blue",
    sub: "디지털 구독료 결제하면",
    main: "최대 6천원 캐시백",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "apptech",
    id: 8,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "5천원 캐시백으로",
    main: "유튜브 프리미엄도 부담없이",
  },
];

// ==========================================
// Computed Properties
// ==========================================
/**
 * 표시할 진행중 이벤트 목록 (8개 고정)
 * 종료 이벤트 제외
 */
const displayedItems = computed(() => {
  return ongoingItems
    .filter((item) => item.categoryType === "진행 중 이벤트")
    .slice(0, 8);
});
</script>


```
{% endraw %}
---
