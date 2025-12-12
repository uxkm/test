# SBT113A01

{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT158A01
  title: 이벤트
  menu: 혜택 > 웰컴 기프트팩
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: "251215: 이미지 변경 및 배너 타입, 컬러 속성 추가"
  header:
    variant: sub
    fixed: true
    showBack: true
    close: false
    home: true
  mainClassList: pt-none
</route>
<template>
  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body welcome-giftpack">
    <div class="welcome-giftpack__head">
      <h2
        class="welcome-giftpack__title"
        tabindex="0"
        aria-label="신한 쏠페이 고객님께만 드리는 웰컴 기프트팩"
      >
        <img
          :src="`${$cdnURL}/images/symbol/SOLpay.png`"
          alt="신한 SOLpay"
          class="solpay-bi"
          aria-hidden="true"
        />
        <strong aria-hidden="true">고객님께만 드리는<br />웰컴 기프트팩</strong>
      </h2>
    </div>
    <div class="welcome-giftpack__body">
      <h3 class="welcome-giftpack__subtitle">
        다양한 디지털 서비스 혜택을 모아 사용하세요.
      </h3>
      <!-- 페이지 이동 없는 단순 정보 노출 영역 -->
      <!-- 
        [수정 : 251215]이미지 변경 및 다크모드 대응 이미지 CSS로 제어
        라이트/다크 모드 이미지를 모두 렌더링하고 CSS에서 표시/숨김 처리
      -->
      <div class="welcome-giftpack__content">
        <div
          v-for="(item, index) in giftpackItems"
          :key="`giftpack-${index}`"
          class="welcome-giftpack__item"
          tabindex="0"
          :aria-label="`${item.title} ${item.description}`"
        >
          <div class="welcome-giftpack__item-image" aria-hidden="true">
            <img :src="`${$cdnURL}/${item.image.replace(/^\//, '')}`" alt="" />
            <img
              :src="`${$cdnURL}/${item.imageDark.replace(/^\//, '')}`"
              alt=""
            />
          </div>
          <p class="welcome-giftpack__item-text" aria-hidden="true">
            <strong>{{ item.title }}</strong>
            <span>{{ item.description }}</span>
          </p>
        </div>
      </div>

      <!-- 클릭 이동 배너 role="link" 추가, 정보성이면 role="link" 삭제 -->
      <!-- [수정 : 251215]이미지 변경 및 타입, 컬러 속성 추가
        배너 컬러 정의 A Type
        data-color="bg-banner_gray_solid"
        data-color="bg-banner_brand_tint-same"
        data-color="bg-banner_indigo_tint-same"
        data-color="bg-banner_purple_tint-same"
        data-color="bg-banner_gray_solid-same"
        data-color="bg-banner_brand_solid-same"
        data-color="bg-banner_indigo_solid-same"
        data-color="bg-banner_purple_solid-same"
        data-color="seafoam-700"
      -->
      <div
        role="link"
        class="sc-banner rtl"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="a"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img
            :src="`${$cdnURL}/images/pages/benefits/welcome/banner_graphic_myshop.png`"
            alt=""
          />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span>더하면, 알아서 따라오는 할인쿠폰!</span>
        </p>
      </div>
    </div>

    <Divider
      variant="group"
      color="tertiary"
      size="full"
      orientation="horizontal"
    />

    <div class="foot-notice">
      <h3 class="foot-notice__title">유의사항</h3>
      <UnorderedList>
        <UnorderedListItem
          v-for="(item, index) in noticeItems"
          :key="`notice-${index}`"
        >
          {{ item }}
        </UnorderedListItem>
      </UnorderedList>
    </div>

    <Divider
      variant="basic"
      color="secondary"
      size="full"
      orientation="horizontal"
    />

    <div class="sc-bottom-info__card">
      <p>준법감시 심의필 제20241206-Cpi-010호<br />(2024.12.06~2025.12.05)</p>
    </div>
  </div>
</template>

<script setup>
import { Divider, UnorderedList, UnorderedListItem } from "@shc-nss/ui/solid";

// 웰컴 기프트팩 아이템 데이터
const giftpackItems = [
  {
    image: "/images/pages/benefits/welcome/icon_gift_compose.png",
    imageDark: "/images/pages/benefits/welcome/icon_gift_compose_dark.png",
    title: "컴포즈커피",
    description: "2잔에 100원",
  },
  {
    image: "/images/pages/benefits/welcome/icon_gift_emart.png",
    imageDark: "/images/pages/benefits/welcome/icon_gift_emart_dark.png",
    title: "이마트",
    description: "상품권 할인",
  },
  {
    image: "/images/pages/benefits/welcome/icon_gift_mappin.png",
    imageDark: "/images/pages/benefits/welcome/icon_gift_mappin_dark.png",
    title: "위치기반 동의시",
    description: "GS25 캔커피 1원",
  },
  {
    image: "/images/pages/benefits/welcome/icon_gift_cardnotice.png",
    imageDark: "/images/pages/benefits/welcome/icon_gift_cardnotice_dark.png",
    title: "카드사용알림 동의시",
    description: "GS25 박카스 1원",
  },
  {
    image: "/images/pages/benefits/welcome/icon_gift_mycar.png",
    imageDark: "/images/pages/benefits/welcome/icon_gift_mycar_dark.png",
    title: "마이카 내차고 i 등록시",
    description: "1,000Px2 더블포인트!",
  },
  {
    image: "/images/pages/benefits/welcome/icon_gift_mydata.png",
    imageDark: "/images/pages/benefits/welcome/icon_gift_mydata_dark.png",
    title: "마이데이터 미션 달성시",
    description: "4천 포인트 100% 적립",
  },
];

// 유의사항 데이터
const noticeItems = [
  "혜택 별 유의사항 및 조건은 해당 페이지에서 확인 부탁드립니다.",
  "웰컴 기프트백은 해당월에 이용할 수 있습니다.",
];
</script>



```
{% endraw %}
---
