# scss

{% raw %}
```js

// tabs.vue
// Swiper refs
const swiperInstance = ref<SwiperType | null>(null);
// 활성 슬라이드 엘리먼트(높이 변화 감지용)
const activeSlideEl = computed<HTMLElement | null>(() => {
  if (!props.enablePanelSwipe || !swiperInstance.value) return null;

  return (swiperInstance.value.slides?.[swiperInstance.value.activeIndex] as HTMLElement) ?? null;
});

// 초기 로드/콘텐츠 추가 시 높이 고정 문제 방지
const updateSwiperAutoHeight = (): void => {
  if (!props.enablePanelSwipe || !swiperInstance.value) return;

  swiperInstance.value.updateAutoHeight(0);
};

// 활성 슬라이드 높이 변경 시 autoHeight 재계산
useResizeObserver(activeSlideEl, () => {
  updateSwiperAutoHeight();
});

// Swiper event handlers
const onSwiperInit = (swiper: SwiperType): void => {
  swiperInstance.value = swiper;

  // 초기 슬라이드를 activeTab에 맞게 설정
  slideSwiperToActiveTab();

  // 초기 렌더 직후 높이를 다시 계산
  nextTick(() => {
    updateSwiperAutoHeight();
  });
};

const onSlideChange = (swiper: SwiperType): void => {
  // Swiper 슬라이드 변경 시 탭 활성화 업데이트
  const targetValue = findValueBySlideIndex(swiper.activeIndex);

  if (targetValue !== undefined && targetValue !== activeTab.value) {
    setActiveTab(targetValue);
  }

  // 슬라이드 변경 후 높이를 다시 계산
  nextTick(() => {
    updateSwiperAutoHeight();
  });
};





<!doctype html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>SC Loader Preview</title>
    <style>
      body {
        margin: 0;
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        background: #ffffff;
      }

      .sc-loader {
        width: 40px;
        height: 40px;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 6px; /* 점 사이 간격 */
        background: transparent; /* 투명배경 */
      }

      .sc-loader__dot {
        width: 8px;
        height: 8px;
        border-radius: 50%;
        transform: translateY(0);
        animation: scDot 1.33s ease-in-out infinite;
      }

      /* 점 3개 색상 */
      .sc-loader__dot:nth-child(1) {
        background: #ff4d4f;
        animation-delay: 0s;
      }
      .sc-loader__dot:nth-child(2) {
        background: #2f54eb;
        animation-delay: 0.26s;
      }
      .sc-loader__dot:nth-child(3) {
        background: #52c41a;
        animation-delay: 0.52s;
      }

      /* 순서대로 “튀는” 모션 */
      @keyframes scDot {
        0%,
        40%,
        100% {
          transform: translateY(2px) scale(0.92);
        }
        20% {
          transform: translateY(-6px) scale(1.05);
        }
      }

      /* 접근성: 모션 줄이기 */
      @media (prefers-reduced-motion: reduce) {
        .sc-loader__dot {
          animation: none;
        }
      }
    </style>
  </head>
  <body>
    <div class="sc-loader" role="status" aria-label="로딩 중">
      <span class="sc-loader__dot"></span>
      <span class="sc-loader__dot"></span>
      <span class="sc-loader__dot"></span>
    </div>
  </body>
</html>

```
{% endraw %}
