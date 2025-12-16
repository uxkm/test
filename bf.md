
{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT128A04
  title: 월간 쿠폰북
  menu: "혜택 > 할인 쿠폰 메인화면 > 쿠폰북"
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
  appClassList: "sc-coupon-book"
  mainClassList: "coupon-book__main"
</route>
<template>
  <div class="sc-contents__body coupon-book">
    <h2 class="coupon-book__title">5월 쿠폰북</h2>
    <section v-for="(section, sectionIndex) in sections" :key="sectionIndex">
      <h3 class="coupon-book__title-sub">{{ section.title }}</h3>
      <article>
        <ul class="coupon-book__carousel">
          <li
            v-for="(slide, index) in section.slides"
            :key="index"
            class="coupon-book__card"
          >
            <a
              class="coupon-book__card-item"
              role="link"
              tabindex="0"
              :href="slide.link"
              :aria-label="`${slide.brand} ${slide.reward.replace(/<br\s*\/?>/gi, ' ')}`"
              @focus="handleCardFocus"
            >
              <div class="coupon-book__card-img" aria-hidden="true">
                <ScImage :src="slide.logo" alt="" />
              </div>
              <div class="coupon-book__card-texts">
                <span class="coupon-book__card-brand">{{ slide.brand }}</span>
                <strong class="coupon-book__card-reward" v-html="slide.reward">
                </strong>
              </div>
            </a>
          </li>
        </ul>
      </article>
    </section>
  </div>

  <div class="search-floating__btn">
    <CapsuleButton
      size="large"
      text="쿠폰 검색"
      variant="tonal"
      @click="goToCouponSearch"
    >
      <template #leftIcon>
        <Icon name="Search" size="24" aria-hidden="true" />
      </template>
    </CapsuleButton>
  </div>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import { CapsuleButton, Icon } from "@shc-nss/ui/solid";
import { inject, ref } from "vue";
import { useRouter } from "vue-router";

const { $cdnURL } = inject(AppContextKey);
const router = useRouter();

const goToCouponSearch = () => {
  router.push({ name: "SBT137A02" });
};

const handleCardFocus = (event) => {
  const target = event.currentTarget;
  const cardElement = target.closest(".coupon-book__card");
  const carouselElement = target.closest(".coupon-book__carousel");

  if (cardElement && carouselElement) {
    const cardRect = cardElement.getBoundingClientRect();
    const carouselRect = carouselElement.getBoundingClientRect();

    // 현재 뷰포트에서 카드가 보이는지 확인
    const cardLeft = cardRect.left;
    const cardRight = cardRect.right;
    const carouselLeft = carouselRect.left;
    const carouselRight = carouselRect.right;

    // 카드가 뷰포트 안에 완전히 보이는지 확인
    const isFullyVisible =
      cardLeft >= carouselLeft && cardRight <= carouselRight;

    // 카드가 부분적으로라도 보이는지 확인
    const isPartiallyVisible =
      cardRight > carouselLeft && cardLeft < carouselRight;

    // 카드가 오른쪽에 가려져 있는지 확인
    const isOffscreenRight = cardLeft > carouselRight;

    // 카드가 왼쪽에 가려져 있는지 확인
    const isOffscreenLeft = cardRight < carouselLeft;

    // 스크롤이 필요한 경우만 처리
    if (isFullyVisible) {
      // 완전히 보이면 스크롤하지 않음
      return;
    }

    // 아이템 크기와 간격 계산 (136px + 8px = 144px)
    const spacingMd = parseInt(
      getComputedStyle(document.documentElement).getPropertyValue(
        "--spacing-md"
      ) || "8px",
      10
    );
    const cardWidth = 136;
    const itemSize = cardWidth + spacingMd; // 144px

    const currentScrollLeft = carouselElement.scrollLeft;
    const maxScroll = carouselElement.scrollWidth - carouselElement.clientWidth;

    // 오른쪽에 가려진 경우: 아이템 크기만큼 오른쪽으로 스크롤
    if (cardRight > carouselRight) {
      const newScrollLeft = Math.min(currentScrollLeft + itemSize, maxScroll);
      carouselElement.scrollTo({
        left: newScrollLeft,
        behavior: "smooth",
      });
    }
    // 왼쪽에 가려진 경우: 아이템 크기만큼 왼쪽으로 스크롤
    else if (cardLeft < carouselLeft) {
      const newScrollLeft = Math.max(currentScrollLeft - itemSize, 0);
      carouselElement.scrollTo({
        left: newScrollLeft,
        behavior: "smooth",
      });
    }
  }
};

// 쿠폰북 슬라이드 데이터
const defaultSlides = [
  {
    brand: "올리브영",
    reward: "20,000원<br />캐시백",
    logo: `${$cdnURL}/images/dummy/img_couponbook1.png`,
  },
  {
    brand: "crocs",
    reward: "20,000원<br />캐시백",
    logo: `${$cdnURL}/images/dummy/img_couponbook2.png`,
  },
  {
    brand: "GREAT",
    reward: "20,000원<br />캐시백",
    logo: `${$cdnURL}/images/dummy/img_couponbook1.png`,
  },
  {
    brand: "GREAT",
    reward: "20,000원<br />캐시백",
    logo: `${$cdnURL}/images/dummy/img_couponbook2.png`,
  },
  {
    brand: "GREAT",
    reward: "20,000원<br />캐시백",
    logo: `${$cdnURL}/images/dummy/img_couponbook2.png`,
  },
];

// 섹션 데이터
const sections = [
  {
    title: "5월 마이샵데이 혜택받기!",
    slides: defaultSlides,
  },
  {
    title: "매일의 필수템 다 모였다!",
    slides: defaultSlides,
  },
  {
    title: "따뜻한 날씨만큼 기분 좋은 미식",
    slides: defaultSlides,
  },
  {
    title: "집사들 모여라! 댕냥템 이벤트중",
    slides: defaultSlides,
  },
  {
    title: "Tops 인기쿠폰",
    slides: defaultSlides,
  },
];
</script>



```
{% endraw %}
---
