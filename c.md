# scss

{% raw %}
```js



// 로티 재생/정지 테스트
<route lang="yaml">
meta:
  id: SBT178A01
  title:
  menu: "혜택 > 앱테크 메인화면 > 지역타겟팅 보물팡팡 플로팅(로띠)"
  layout: EmptyLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.9
</route>
<template>
  <!-- 모달처럼 body 하위 요소에 추가 -->
  <teleport to="body">
    <!-- 상황에 맞게 z-index 조절 필요 -->
    <div class="floating-treasure" style="--z-index: 100">
      <div class="treasure-container">
        <div class="treasure-content">
          <a
            role="link"
            class="treasure-trigger"
            tabindex="0"
            aria-label="보물이에요!"
          >
            <!-- 등장 로티 -->
            <ScLottie
              v-if="prevShow"
              :key="`treasure-enter-${isPaused ? 'paused' : 'play'}`"
              :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_trigger_coin_01.json`"
              :width="118"
              :height="134"
              :loop="false"
              :autoPlay="!isPaused"
              aria-hidden="true"
            />
            <!-- 대기 로티 -->
            <ScLottie
              v-if="nextShow"
              :key="`treasure-wait-${isPaused ? 'paused' : 'play'}`"
              :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_trigger_coin_02.json`"
              :width="118"
              :height="134"
              :loop="true"
              :autoPlay="!isPaused"
              aria-hidden="true"
            />
            <span v-if="nextShow" class="treasure-tooltip" aria-hidden="true"
              >보물이에요!</span
            >
          </a>
        </div>
        <button
          type="button"
          class="treasure-control"
          :aria-pressed="isPaused"
          :aria-label="isPaused ? '로티 재생' : '로티 정지'"
          @click.stop.prevent="togglePlayback"
        >
          <span class="treasure-control-text" aria-hidden="true">
            {{ isPaused ? "재생" : "정지" }}
          </span>
        </button>
        <button type="button" aria-label="닫기" class="treasure-close">
          <span class="treasure-close-icon" aria-hidden="true">
            <ScIcon iconName="X" size="12" />
          </span>
        </button>
      </div>
    </div>
  </teleport>
</template>

<script setup>
import { inject, onBeforeUnmount, onMounted, ref } from "vue";
import { ScIcon, ScLottie } from "@shc-nss/ui/shc";
import { AppContextKey } from "@/configs/inject/appContext";

const appContext = inject(AppContextKey, null);
const cdnURL = appContext?.$cdnURL ?? "";

const prevShow = ref(true);
const nextShow = ref(false);
const isPaused = ref(true);
let swapTimer = null;

function togglePlayback() {
  isPaused.value = !isPaused.value;
}

function scheduleSwap() {
  if (swapTimer) {
    return;
  }
  swapTimer = setTimeout(() => {
    prevShow.value = false;
    nextShow.value = true;
  }, 1000);
}

onMounted(() => {
  scheduleSwap();
});

onBeforeUnmount(() => {
  if (swapTimer) {
    clearTimeout(swapTimer);
  }
});
</script>






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
