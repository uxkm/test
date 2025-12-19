
{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT001A01
  title: 혜택
  menu: "혜택 > 혜택"
  layout: MainLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  appClassList: "app_benefits"
  mainClassList: "benefits_main"
</route>
<template>
  <!-- 스켈레톤 로딩이 로딩이 완료된 모듈부터 콘텐츠 제공  -->
  <div class="sc-contents__body bf-main">
    <!-- S: 앱테크 -->
    <section class="bf-apptech">
      <!--
        추천 앱테크 목록 영역
        1-1. 실시간 참여자 수 
          - 앱테크 메인 페이지의 당일 누적 조회수(page View)를 기반
          - 카운팅 데이터는 실시간 반영이 아닌 지정된 시간에 배치 처리 방식으로 집계
            - 지정 시간 : 07시 / 10시 / 13시 / 16시 / 20시 / 23시
            - 집계 시 누적 조회수가 100이하인 경우 실시간 참여자 수 표시가 아닌 지정 문구 노출
          - 1조회수를 1명 단위로 표기
            - 0~999 : 숫자 그대로 표기
            - 1,000~9,999 : 천단위 쉼표 표시하여 숫자로 표기
            - 10,000 이상 : 만 단위 적용하여 한글 숫자 단위로 표기
            (ex.24,000명 → 2만 4,000명)- 100,000 이상 : 만 단위 + 천단위까지 표기 (ex.153,500명 → 15만 3,500명)
        1-2. 앱테크 리스트 
          앱테크 리스트 3개 노출 (순서대로 노출)
            - 라이브 방송
            - 사다리 타기
            - 룰렛 돌리기
          앱테크 리스트 Tap > 해당 앱테크 상세 화면으로 이동
          (TBD) 리스트형 AD사용하는 경우, 앱테크 리스트 3개 중 마지막 목록에 리스트형 AD노출 (리스트형 AD는 향후 운영에서 반영 예정)
        1-3. ‘앱테크 전체보기’ Tap > [SBT068A01_앱테크 메인] 화면으로 이동 
      -->
      <!-- S: 앱테크 리스트 -->
      <article class="bf-apptech__list">
        <div class="bf-section__header px-5">
          <p class="description">지금 2만 4,000명이 참여 중</p>
          <p class="description">오늘 받을 수 있는 포인트 놓치지 마세요!</p>
          <h2 class="title-sub">SOL쏠하게 모이는 데일리 포인트</h2>
        </div>
        <ul class="sc-point-more__list">
          <li v-for="(item, index) in pointMoreList" :key="index">
            <a
              role="link"
              tabindex="0"
              :aria-label="[item.label, item.sub].filter(Boolean).join(', ')"
              class="point-more__item"
            >
              <ListItem align="centered" aria-hidden="true">
                <template #leftIcon>
                  <div class="point-icon">
                    <ScImage :src="item.icon" alt="" aria-hidden="true" />
                  </div>
                </template>
                <template #leftMainText>
                  <span>{{ item.label }}</span>
                </template>
                <template #leftSubText>
                  <span>{{ item.sub }}</span>
                </template>
              </ListItem>
            </a>
          </li>
        </ul>

        <div class="bf-section__footer">
          <CapsuleButton
            text="앱테크 전체보기"
            color="primary"
            variant="outline"
            size="medium"
            :rightIcon="{ iconName: 'Chevron_right' }"
          />
        </div>
      </article>
      <!-- E: 앱테크 리스트 -->

      <!--
        외부 광고 영역 
        - 외부 광고 배너 노출 
          - 웹 SDK 사용
          - 랜덤 AD 노출
          - 앱 추적 허용(iOS) 미설정 사용자에게는 해당 영역 미노출
        - 게시중인 광고 없는 경우 영역 히든
      -->
      <!-- S: 외부 광고 배너 -->
      <article aria-label="외부 광고 배너">
        <a
          role="link"
          tabindex="0"
          aria-label="익시오 앱 무료 다운로드 이동"
          class="export-banner__link"
        >
          <img
            :src="`${$cdnURL}/images/pages/benefits/main/img_export.png`"
            alt="익시오 앱 무료 다운로드 - 통화녹음&요약 AI앱 익시오 AD Moloco 광고입니다."
            class="export-banner"
          />
        </a>
      </article>
      <!-- E: 외부 광고 배너 -->
    </section>
    <!-- E: 앱테크 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 이벤트 -->
    <section class="bf-event">
      <!--
        - 이벤트 메인화면 설계서 모음형 이벤트 영역 참고
        - 모음형 이벤트만 연속 스크롤링(Continuous Scrolling)으로 제공
        - 최소 3개, 최대 5개까지 게시 가능 - 3개 미만인 경우, 영역 히든 처리
        - [디채관 > 이벤트 관리 > 모음형 이벤트 관리 > 모음형 이벤트 순번관리] 에서 저장 후 [FAN관리 > 전시관리 공통 > 이벤트 관리]에서 ‘동기화' 진행 시, 노출 반영
        - 모음형 이벤트 Tap > [홈페이지 > 모음형 이벤트 상세 화면] 으로 이동 
      -->
      <!-- S: 모음형 이벤트 -->
      <article class="bf-event__collection">
        <div class="bf-section__header">
          <h2 class="title-sub px-5">놓치면 손해 이벤트 모음.zip</h2>
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
                <strong class="collection-card__text-main">
                  {{ item.title }}
                </strong>
                <p class="collection-card__text-sub" v-html="item.subtitle"></p>
              </div>
            </div>
          </li>
        </ul>
      </article>
      <!-- E: 모음형 이벤트 -->

      <!-- S: 이벤트 리스트 -->
      <article class="bf-event__list">
        <div class="bf-section__header px-5">
          <!--
            문구 노출

            이벤트 - 인기 외 카테고리 선택 시 (순위 배지 x)
            - 지금 2만 4,000명이 참여 중

            이벤트 - 당일 누적 조회수 100 이하인 경우 노출 문구 (순위 배지 x, 문구)
            - 관심있는 이벤트만 골라볼 수 있어요


            실시간 참여자 수 
            - 이벤트 메인 페이지의 당일 누적 조회수(page View)를 기반
            - 카운팅 데이터는 실시간 반영이 아닌 지정된 시간에 배치 처리 방식으로 집계
              - 지정 시간 : 07시 / 10시 / 13시 / 16시 / 20시 / 23시
              - 집계 시 누적 조회수가 100이하인 경우 실시간 참여자 수 표시가 아닌 지정 문구 노출
            - 1조회수를 1명 단위로 표기- 0~999 : 숫자 그대로 표기
              - 1,000~9,999 : 천단위 쉼표 표시하여 숫자로 표기
              - 10,000 이상 : 만 단위 적용하여 한글 숫자 단위로 표기(ex.24,000명 → 2만 4,000명)
              - 100,000 이상 : 만 단위 + 천단위까지 표기 (ex.153,500명 → 15만 3,500명)
          -->
          <p class="description">지금 2만 4,000명이 참여 중</p>
          <p class="description">관심있는 이벤트만 골라볼 수 있어요</p>
          <h2 class="title-sub">내게 맞는 이벤트 찾아보기</h2>
        </div>

        <!--
          이벤트 카테고리 
          - 이벤트 카테고리 탭 제공
            - 이벤트 카테고리 [MOBFM026C01]홈페이지 > 이벤트 > 진행중 이벤트 목록과 동일 
            - 인기 / 쇼핑・문화 / 앱테크 / 여행・숙박 / 카드･결제 / 청소년
          - 인기 카테고리: 
            - “전일 기준 조회수 상위(테이블명: MCBSA0157) AND 현재 신한 SOL페이 > 진행 중 이벤트 노출 중” 조건을 만족하는 3개 이벤트 조회수 순서로 노출
            - 단, 위 조건을 만족하는 이벤트 개수가 3개 미만일 경우, 부족한 이벤트 개수만큼 최신 이벤트로 노출하며, 해당건에는 인기순 뱃지 미노출
            - 그 외 카테고리: 해당 카테고리별 이벤트 목록 최신순으로 1위~3위까지 노출
            - 그 외 카테고리에서는 순위 뱃지 미노출
        -->
        <div class="cupon-chip">
          <BasicChipGroup
            control="none"
            variant="solid"
            :items="items"
            v-model="selectedValue"
          />
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
              [
                item?.chipType === 'popular' && item?.rank
                  ? `인기 순위 ${item.rank}위, `
                  : null,
                item?.label,
                item?.sub,
                item?.main,
                item?.rightLabel,
              ]
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
                <!-- 인기만 순위 배지 노출 -->
                <span
                  v-if="item.chipType === 'popular' && item.rank"
                  class="rank-badge"
                >
                  {{ item.rank }}
                </span>
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
        <div class="bf-section__footer">
          <CapsuleButton
            text="이벤트 전체보기"
            color="primary"
            variant="outline"
            size="medium"
            :rightIcon="{ iconName: 'Chevron_right' }"
          />
        </div>
      </article>
      <!-- E: 이벤트 리스트 -->
    </section>
    <!-- E: 이벤트 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 이벤트 프로모션 -->
    <section class="section bf-promotion" aria-label="이벤트 프로모션">
      <!-- 기본형/인터렉션형 배너 노출 -->
      <!-- 임시 처리 작업 중 영역만 이미지로 추가 -->
      <img
        :src="`${$cdnURL}/images/dummy/img_promotion_sample.png`"
        alt=""
        class="img-dummy"
      />
    </section>
    <!-- E: 이벤트 프로모션 -->

    <Divider color="tertiary" variant="group" />

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
      <div class="bf-section__footer">
        <CapsuleButton
          text="할인·쿠폰 전체보기"
          color="primary"
          variant="outline"
          size="medium"
          :rightIcon="{ iconName: 'Chevron_right' }"
        />
      </div>
    </section>
    <!-- E: 할인·쿠폰 -->

    <!-- S: 혜택 서비스 -->
    <section class="section bf-service bg-gray">
      <div class="bf-section__header">
        <h2 class="title-sub">일상의 즐거움을 더하는 혜택 서비스</h2>
      </div>
      <ul class="bf-service__list">
        <li v-for="(item, index) in serviceList" :key="index">
          <a role="link" tabindex="0" class="bf-service__item">
            <div class="bf-service__icon">
              <LoadingSkeleton
                v-if="!imageLoaded[index]"
                width="100%"
                height="100%"
                rounded="small"
              />
              <img
                :src="item.image"
                :alt="item.label"
                :style="{ display: imageLoaded[index] ? 'block' : 'none' }"
                @load="imageLoaded[index] = true"
                @error="imageLoaded[index] = true"
              />
            </div>
            <p class="bf-service__label">{{ item.label }}</p>
          </a>
        </li>
      </ul>
    </section>
    <!-- E: 혜택 서비스 -->
  </div>
</template>

<script setup>
import { computed, inject, reactive, ref } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  BasicChipGroup,
  CapsuleButton,
  Divider,
  ListItem,
  LoadingSkeleton,
  SolidLabel,
  TintLabel,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// 이벤트 모음 카드 데이터
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

// BasicChipGroup 관련 데이터
const selectedValue = ref("1");
const items = [
  {
    text: "인기",
    value: "1",
  },
  {
    text: "쇼핑·문화",
    value: "2",
  },
  {
    text: "앱테크",
    value: "3",
  },
  {
    text: "여행·숙박",
    value: "4",
  },
  {
    text: "카드･결제",
    value: "5",
  },
  {
    text: "청소년",
    value: "6",
  },
];

// 진행중 이벤트 데이터
const ongoingItems = [
  {
    categoryType: "인기",
    chipType: "popular",
    id: 1,
    received: false,
    rank: 1,
    icon: {
      src: `${$cdnURL}/images/dummy/icon_foundation01.png`,
      alt: "",
    },
    sub: "IKEA 신한카드로 결제하고",
    main: "10만원 캐시백 포함 3가지 혜택 받기",
  },
  {
    categoryType: "인기",
    chipType: "popular",
    id: 2,
    received: false,
    rank: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/icon_foundation02.png`,
      alt: "",
    },
    sub: "트릿닷컴에서 예약하고",
    main: "호텔 30% 할인 받기",
  },
  {
    categoryType: "인기",
    chipType: "popular",
    id: 3,
    received: false,
    rank: 3,
    icon: {
      src: `${$cdnURL}/images/dummy/icon_foundation03.png`,
      alt: "",
    },
    sub: "파리바게트 신한카드로 결제하고",
    main: "20,000원 캐시백 받기",
  },
  {
    categoryType: "쇼핑·문화",
    chipType: "shopping_culture",
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
    categoryType: "쇼핑·문화",
    chipType: "shopping_culture",
    id: 5,
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
    categoryType: "쇼핑·문화",
    chipType: "shopping_culture",
    id: 6,
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
    categoryType: "앱테크",
    chipType: "apptech",
    id: 7,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "5천원 캐시백으로",
    main: "유튜브 프리미엄도 부담없이",
  },
  {
    categoryType: "앱테크",
    chipType: "apptech",
    id: 8,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "결제계좌 변경하고",
    main: "스타벅스 쿠폰 받기",
  },
  {
    categoryType: "앱테크",
    chipType: "apptech",
    id: 9,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "앱테크 서비스 이용하고",
    main: "최대 3만원 캐시백",
  },
  {
    categoryType: "여행·숙박",
    chipType: "travel_accommodation",
    id: 10,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    sub: "호텔 예약하고",
    main: "최대 5만원 할인",
  },
  {
    categoryType: "여행·숙박",
    chipType: "travel_accommodation",
    id: 11,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    sub: "항공권 구매하고",
    main: "마일리지 적립",
  },
  {
    categoryType: "여행·숙박",
    chipType: "travel_accommodation",
    id: 12,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    sub: "렌터카 예약하고",
    main: "추가 할인 혜택",
  },
  {
    categoryType: "카드･결제",
    chipType: "card_payment",
    id: 13,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    sub: "카드 결제하고",
    main: "최대 10만원 캐시백",
  },
  {
    categoryType: "카드･결제",
    chipType: "card_payment",
    id: 14,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "자동이체 등록하고",
    main: "추가 혜택 받기",
  },
  {
    categoryType: "카드･결제",
    chipType: "card_payment",
    id: 15,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "결제 수단 변경하고",
    main: "특별 할인",
  },
  {
    categoryType: "청소년",
    chipType: "youth",
    id: 16,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "청소년 특별 혜택",
    main: "최대 3만원 할인",
  },
  {
    categoryType: "청소년",
    chipType: "youth",
    id: 17,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    sub: "학생증 인증하고",
    main: "추가 혜택 받기",
  },
  {
    categoryType: "청소년",
    chipType: "youth",
    id: 18,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    sub: "청소년 전용 서비스",
    main: "특별 할인 쿠폰",
  },
];

const displayedItems = computed(() => {
  const selectedChip = items.find((item) => item.value === selectedValue.value);
  if (!selectedChip) return [];

  const categoryType = selectedChip.text;
  const filtered = ongoingItems.filter(
    (item) => item.categoryType === categoryType
  );

  return filtered.slice(0, 3);
});

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

// 서비스 리스트 데이터
const serviceList = [
  {
    image: `${$cdnURL}/images/pages/benefits/main/icon_service_app1.png`,
    label: "탑스쿠폰",
  },
  {
    image: `${$cdnURL}/images/pages/benefits/main/icon_service_app2.png`,
    label: "마이샵",
  },
  {
    image: `${$cdnURL}/images/pages/benefits/main/icon_service_app3.png`,
    label: "기프트샵",
  },
  {
    image: `${$cdnURL}/images/pages/benefits/main/icon_service_app4.png`,
    label: "땡겨요",
  },
];

// 이미지 로딩 상태 관리
const imageLoaded = reactive({});

const pointMoreList = [
  {
    label: "라이브 방송",
    sub: "방송 알림 신청하고 시청한 후 포인트 받아가세요.",
    icon: `${$cdnURL}/images/pages/benefits/main/icon_point_list01.png`,
    link: "#",
  },
  {
    label: "사다리 타기",
    sub: "사다리 타고 최대 5,000P 받아가세요.",
    icon: `${$cdnURL}/images/pages/benefits/main/icon_point_list02.png`,
    link: "#",
  },
  {
    label: "룰렛 돌리기",
    sub: "룰렛 돌리고 최대 1만P 받아가세요.",
    icon: `${$cdnURL}/images/pages/benefits/main/icon_point_list03.png`,
    link: "#",
  },
];
</script>



```
{% endraw %}
---
