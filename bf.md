# SBT113A01

{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT113A01
  title: 이벤트
  menu: "혜택 > 이벤트 메인화면 > 모음형 이벤트"
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
  mainClassList: "pt-none"
</route>
<template>
  <!--
    이벤트 모음형 페이지 (Event Collection Page)
    - 로그인 여부와 관계없이 접근 가능
    - 특정 테마/주제로 묶인 이벤트 제공
    - App, Mobile Web, PC Web에서 동일하게 노출

    1. 히어로 영역 (Hero Area)
      1-1. 서브 타이틀 영역
        - 이벤트 모음형 페이지의 타겟 고객을 정의하는 서브 타이틀 구성
      1-2. 메인 타이틀 영역
        - 모음형 페이지 내 개별 이벤트가 제공하는 혜택을 사용자가 쉽게 인식할 수 있는 문구로 메인 타이틀 구성
      1-3. 모음형 페이지 키비주얼 영역
        - 모음형 페이지의 테마/주제에 적합한 키비주얼 이미지 제공

    2. 이벤트 목록 영역 (Event List Area)
      - 이벤트 모음형 페이지에 매핑된 이벤트 목록 제공
      - 진행중인 이벤트 및 종료된 이벤트 함께 노출
      - 진행중인 이벤트 노출 후, 아래에 종료된 이벤트를 순차적으로 노출
      - 모음형 페이지에 개별 이벤트 매핑은 [디채관 > 이벤트 관리] 화면 참고
      - 정렬 순서: 최신 등록 순
      - 모음형 페이지 내 이벤트 목록 개수 정책
        * 최소: 1개 이상 제공 필요
        * 최대: 제약 없음

      2-1. 참여 가능한 이벤트 개수 정보 표시 영역
        - 해당 모음형 페이지에서 노출 중인 진행중인 이벤트 목록 개수를 제공 (유지)

      2-2. 개별 이벤트 항목
        - 진행중/종료 이벤트 선택 시 해당 이벤트 상세 화면으로 이동
        - 종료 이벤트 썸네일에 "종료" 마크 표시
        - 모음형 페이지에 연결된 개별 이벤트가 종료되어도 별도의 "종료 이벤트 목록"에 노출하지 않고, 모음형 페이지 내에서만 노출
        - 이벤트 등록 관리 시스템에서 연결 해제 시까지 이벤트 이력 유지

      2-3. 맨 위로 가기 버튼
        - 화면이 일정 영역 이상 스크롤될 경우 버튼이 자동으로 표시됨
        - 선택 시 화면 상단으로 자동 스크롤되며, 이후 버튼이 숨겨짐

      2-4. 공유하기 버튼
        - 선택 시 기존 기능과 동일하게 동작

    3. 고지사항 영역 (Notice Area)
      - 모음형 페이지의 공통 고지사항 내용 제공
      - 개별 이벤트 고지사항은 각 이벤트 상세 화면에서 제공
      - 심의필 업데이트
        * 이벤트 목록에 새 이벤트가 추가된 경우에만 심의필 업데이트 필요
        * 기간이 지난 이벤트가 목록에서 제외된 경우 심의필 업데이트 불필요
  -->
  <div class="sc-contents__body sc-event-collection">
    <div class="collection-header">
      <h2
        class="collection-header__title"
        tabindex="0"
        aria-label="해외여행 필수템 캐시백부터 할인까지 여기 다 있ZIP"
      >
        <span class="collection-header__title-sub"> 해외여행 필수템 </span>
        <strong class="collection-header__title-main">
          캐시백부터 할인까지<br />여기 다 있ZIP
        </strong>
      </h2>
      <img
        :src="`${$cdnURL}/images/pages/benefits/main/img_item_collection.svg`"
        alt=""
        class="collection-header__bg"
        aria-hidden="true"
      />
      <!-- <img
        :src="`${$cdnURL}/images/pages/benefits/main/img_coupon_collection.svg`"
        alt=""
        class="collection-header__bg"
        aria-hidden="true"
      /> -->
    </div>
    <div class="collection-body">
      <div class="collection-body__header">
        <ScImageIcon
          iconName="benefis_bg_event_collection"
          width="auto"
          :height="42"
          class="bg_collection-header"
          aria-hidden="true"
          :iconSize="42"
        />
        <h3
          class="collection-body__header-title"
          tabindex="0"
          :aria-label="`진행중 이벤트 ${ongoingEventCount}건`"
        >
          <span aria-hidden="true"
            >진행중 이벤트
            <em>{{ String(ongoingEventCount).padStart(2, "0") }}</em
            >건</span
          >
        </h3>
      </div>
      <div class="collection-inner">
        <div class="category-list__body">
          <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="이벤트 정보" 추가 -->
          <div
            v-for="item in displayedItems"
            :key="item.id"
            class="category-item"
            role="link"
            tabindex="0"
            :aria-label="
              [
                item?.categoryType === '종료 이벤트' ? '종료 이벤트' : null,
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
              :class="{
                'ended-event-item': item.categoryType === '종료 이벤트',
              }"
              aria-hidden="true"
            >
              <template #leftIcon>
                <ScImage
                  :src="item.icon.src"
                  :alt="item.icon.alt"
                  class="category-icon"
                  aria-hidden="true"
                />
                <span
                  v-if="item.categoryType === '종료 이벤트'"
                  class="ended-event-badge"
                >
                  종료
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
      </div>
    </div>
    <CapsuleButton
      variant="outline"
      size="medium"
      text="공유하기"
      :leftIcon="{ iconName: 'Share' }"
      class="sharebtn"
      @click="isShareBottomSheetOpen = true"
    />
  </div>

  <section class="event-collection__notice">
    <Accordion title="꼭! 알아두세요" v-model:isExpanded="isNoticeExpanded">
      <!-- 1뎁스 시작 -->
      <UnorderedList :gap="8">
        <template v-for="(item, index) in noticeItems" :key="index">
          <!-- 1뎁스 아이템 -->
          <UnorderedListItem :variant="item.variant || 'bullet'" size="medium">
            <template v-if="item.title">
              <span>{{ item.title }}</span>
            </template>
            <template v-if="item.text">
              <span>{{ item.text }}</span>
            </template>
            <!-- 2뎁스 시작 -->
            <UnorderedList v-if="item.items && item.items.length > 0" :gap="8">
              <UnorderedListItem
                v-for="(subItem, subIndex) in item.items"
                :key="subIndex"
                :variant="subItem.variant || 'bullet'"
                size="medium"
              >
                <template v-if="subItem.text">
                  <span>{{ subItem.text }}</span>
                </template>
                <template v-else-if="subItem.title">
                  <span>{{ subItem.title }}</span>
                </template>
              </UnorderedListItem>
            </UnorderedList>
            <!-- 2뎁스 끝 -->
          </UnorderedListItem>
        </template>
      </UnorderedList>
      <!-- 1뎁스 끝 -->
    </Accordion>

    <div class="sc-bottom-info__card mt-3xl">
      <p>준법감시 심의필 제20241016-Cpi-011호<br />(2024.10.16~2025.10.15)</p>
    </div>
  </section>

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

  <!-- 공유하기 바텀시트 -->
  <BottomSheet
    v-model="isShareBottomSheetOpen"
    closableDimm
    dimmed
    title="공유하기"
  >
    <ul class="shared-list">
      <li>
        <TextButton
          text="카카오톡"
          ariaLabel="카카오톡으로 공유하기"
          class="kakao-btn"
        >
          <template #leftIcon>
            <ScIcon
              iconName="icon_kakao_brand"
              width="36"
              height="36"
              aria-hidden="true"
            />
          </template>
        </TextButton>
      </li>
      <li>
        <TextButton
          text="문자메세지"
          ariaLabel="문자메세지로 공유하기"
          class="message-btn"
        >
          <template #leftIcon>
            <ScIcon
              iconName="icon_message_brand"
              width="36"
              height="36"
              aria-hidden="true"
            />
          </template>
        </TextButton>
      </li>
      <li>
        <TextButton
          text="링크 복사"
          ariaLabel="링크 복사하기"
          class="link-copy-btn"
        >
          <template #leftIcon>
            <ScIcon iconName="Link" width="36" height="36" aria-hidden="true" />
          </template>
        </TextButton>
      </li>
    </ul>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage, ScImageIcon, ScIcon } from "@shc-nss/ui/shc";
import {
  ListItem,
  TintLabel,
  FabScrollTop,
  CapsuleButton,
  TextButton,
  BottomSheet,
  Accordion,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, inject, ref, defineModel } from "vue";

// ==========================================
// Inject
// ==========================================
// CDN URL 주입
const { $cdnURL } = inject(AppContextKey);

// ==========================================
// 바텀시트 제어
// ==========================================
const isShareBottomSheetOpen = defineModel({ default: false });

// ==========================================
// 고지사항 아코디언 제어
// ==========================================
const isNoticeExpanded = ref(true);

// ==========================================
// 고지사항 내용
// ==========================================
// 2뎁스까지만 지원하는 구조 (모든 항목은 객체 형태):
// 1뎁스: { text?: string, title?: string, variant?: "bullet" | "dash" | "star", items?: 배열 }
// 2뎁스: { text?: string, title?: string, variant?: "bullet" | "dash" | "star" }
// - variant 옵션: 기본값 1뎁스 "bullet", 2뎁스 "bullet" (variant 옵션 자체가 없으면 기본값 적용)
// - 다른 variant 사용 시: variant: "dash" 또는 variant: "star" 명시
const noticeItems = ref([
  {
    text: "카드별 한도를 설정한 경우, 인증하는 카드에 따라 대출 받을 수 있는 금액이 다를 수 있습니다.",
  },
  {
    text: "카드별 한도를 설정한 경우, 인증하는 카드에 따라 대출 받을 수 있는 금액이 다를 수 있습니다.",
    // variant 옵션 없음 → 기본값 "bullet" 적용
    items: [
      {
        text: "서브 항목 카드별 한도를 설정한 경우, 인증하는 카드에 따라 대출받을 수 있는 금액이 다를 수 있습니다.",
      },
      {
        text: "서브 항목 카드별 한도를 설정한 경우, 인증하는 카드에 따라 대출받을 수 있는 금액이 다를 수 있습니다.",
        // variant: "dash",
      },
      {
        text: "서브 항목 카드별 한도를 설정한 경우, 인증하는 카드에 따라 대출받을 수 있는 금액이 다를 수 있습니다.",
        // variant: "star",
      },
    ],
  },
  {
    text: "카드별 한도를 설정한 경우, 인증하는 카드에 따라 대출 받을 수 있는 금액이 다를 수 있습니다.",
  },
  {
    title: "카드별 한도를 설정한 경우",
    items: [
      {
        text: "인증하는 카드에 따라 대출 받을 수 있는 금액이 다를 수 있습니다.",
      },
    ],
  },
]);

// ==========================================
// 이벤트 데이터
// ==========================================
// 진행 중 이벤트 6개 + 종료 이벤트 2개 = 총 8개
const eventItems = ref([
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
    categoryType: "종료 이벤트",
    chipType: "shopping_culture",
    id: 7,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon7.png`,
      alt: "",
    },
    labelColor: "green",
    sub: "캐시백부터 할인까지 여기 다 있ZIP",
    main: "해외여행 필수템",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "apptech",
    id: 8,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    sub: "SOL페이에 티머니 등록하고",
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
]);

// ==========================================
// Computed Properties
// ==========================================
/**
 * 표시할 이벤트 목록 (8개 고정)
 */
const displayedItems = computed(() => {
  return eventItems.value;
});

/**
 * 진행중인 이벤트 개수
 */
const ongoingEventCount = computed(() => {
  return eventItems.value.filter(
    (item) => item.categoryType === "진행 중 이벤트"
  ).length;
});
</script>



```
{% endraw %}
---
