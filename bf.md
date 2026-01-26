
{% raw %}
```js


// 보물찾기
.floating-treasure {
  position: fixed;
  bottom: calc(160px + var(--env-b));
  right: 36px;
  z-index: 100;
  .treasure-container {
    position: relative;
    width: 118px;
    height: 134px;
  } 
  .treasure-close {
    position: absolute;
    top: 29px;
    right: 0;
    z-index: 1;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    width: 40px;
    height: 40px;
    text-align: right;
    line-height: 1;
    .treasure-close-icon {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 20px;
      height: 20px;
      background-color: var(--bg-white);
      border-radius: var(--radius-full);
      color: var(--fg-primary);
      box-shadow: 0px 2px 4px 0px #16192433;
    }
  }
  .treasure-trigger {
    position: relative;
    display: block;
    width: 118px;
    height: 134px;
  }
  .treasure-tooltip {
    position: absolute;
    top: -5px;
    left: 50%;  
    transform: translateX(-50%);
    display: block;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100% auto;
    background-image: url("#{$cdn-url}/images/pages/benefits/main/bg_treasure_tooltip.png");
    width: 83px;
    height: 36px;
    padding-top: 4px;
    @include font-set(body-s, 500);
    font-weight: 500;
    color: var(--white);
    text-align: center;
    animation: .8s ease-in-out infinite lottie-text2;
    /* @keyframes duration | timing-function | delay | iteration-count | direction | fill-mode | play-state | name */
  }
}


// tooltip-recommend-benefit 바운스 애니메이션
@keyframes tooltipBouncy {
  0% {
    transform: translateX(-50%) translateY(0);
  }
  50% {
    transform: translateX(-50%) translateY(5px);
  }
  100% {
    transform: translateX(-50%) translateY(0);
  }
}

// bf-recommend-benefit__body 페이드인 애니메이션
@keyframes bodyFadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

// webzine-list li 페이드인 애니메이션
@keyframes itemFadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

// sv-pagination 페이드인 애니메이션
@keyframes paginationFadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

// treasure(보물찾기) animation
@keyframes lottie-text2 {
  0% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(-5px); }
  100% { transform: translateX(-50%) translateY(0); }
}
@keyframes lottie-text {
  0% {
    opacity: 0;
    transform: translateX(-50%) translateY(0);
  }
  50% {
    opacity: 1;
    transform: translateX(-50%) translateY(-20%);
  }
  100% {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
}




<template>
  <!-- 모달처럼 body 하위 요소에 추가 -->
  <teleport to="body">
    <!-- 상황에 맞게 z-index 조절 필요 -->
    <div class="floating-treasure" style="z-index: 100;">
      <div class="treasure-container">
        <div class="treasure-content">
          <a role="link" class="treasure-trigger" tabindex="0" aria-label="보물이에요!">
            <!-- 등장 로티 -->
            <ScLottie
              v-if="prevShow"
              :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_trigger_coin_01.json`"
              :width="118"
              :height="134"
              :loop="false"
              :autoPlay="true"
              @onAnimationLoaded="handleAnimation1"
              aria-hidden="true"
            />
            <!-- 대기 로티 -->
            <ScLottie
              v-if="nextShow"
              :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_trigger_coin_02.json`"
              :width="118"
              :height="134"
              :loop="true"
              :autoPlay="true"
              @onAnimationLoaded="handleAnimation2"
              aria-hidden="true"
            />
            <span v-if="nextShow" class="treasure-tooltip" aria-hidden="true">보물이에요!</span>
          </a>
        </div>
        <button
          type="button"
          aria-label="닫기"
          class="treasure-close"
        >
          <span
            class="treasure-close-icon"
            aria-hidden="true"
          >
            <ScIcon
              iconName="X"
              width="12"
              height="12"
            />
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
const anim1 = ref(null);
const anim2 = ref(null);
let swapTimer = null;

function scheduleSwap() {
  if (swapTimer) {
    return;
  }
  swapTimer = setTimeout(() => {
    prevShow.value = false;
    nextShow.value = true;
  }, 1000);
}

function handleAnimation1(anim) {
  anim1.value = anim;
  scheduleSwap();
}

function handleAnimation2(anim) {
  anim2.value = anim;
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







<route lang="yaml">
meta:
  id: SBT178A02
  title: 
  menu: "혜택 > 보물찾기"
  layout: EmptyLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.9
</route>
<template>
  <div
    v-if="fullModal"
    class="modal-area"
  >
    <div class="treasure-modal target-C2025070460731">
      <div
        v-if="!isTreasureFound"
        class="treasure-box"
      >
          <div class="loading-lottie">
            <div class="lottie">
              <ScLottie
                :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_loading.json`"
                :width="40"
                :height="40"
                :loop="true"
                :autoPlay="true"
                @onAnimationLoaded="handleAnimation1"
              />
            </div>
          </div>
          <div class="img-box">
            <p class="text">
              위치를 확인 중이에요<br>
              <strong>잠시만 기다려주세요</strong>
            </p>
            <div class="anibox">
              <div>
                <ScLottie
                  :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_compass.json`"
                  :width="200"
                  :height="220"
                  :loop="true"
                  :autoPlay="true"
                  @onAnimationLoaded="handleAnimation2"
                />
              </div>
            </div>
          </div>
        </div>
      <transition name="slide-up">
        <div
          v-if="isTreasureFound"
          ref="modalCont"
          class="treasure-box"
        >
          <button
            type="button"
            class="btn-close"
            aria-label="“닫기”"
            @click="handleClose"
          >
            <ScIcon
              iconName="X"
              size="24"
              color="white"
            />
          </button>
          <!-- 210609 수정 (로티 추가) -->
          <div class="img-box">
            <p class="text">
              축하드려요!
              <em>보물을 찾으셨네요.</em>
            </p>
            <div class="anibox">
              <!-- 등장 로티 -->
              <div>
                <Vue3Lottie
                  v-if="options1.animationData"
                  :animation-data="options1.animationData"
                  :loop="options1.loop"
                  :auto-play="true"
                  :width="360"
                  :height="537"
                  @on-animation-loaded="handleAnimation1"
                />
              </div>
            </div>
            <strong class="point">
              3P
            </strong>
          </div>
          <div class="text-box">
            <a
              href="javascript:;"
              class="link"
            >바로가기</a>
            <p class="text">
              터치결제를 이용하고 더 많은 보물을 <br>찾아보세요!
            </p>
          </div>
          <!-- // 210609 수정 -->
        </div>
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ScIcon, ScLottie } from '@shc-nss/ui/shc'
import { Vue3Lottie } from 'vue3-lottie'
import { computed, inject, onMounted, ref } from 'vue'
import { AppContextKey } from '@/configs/inject/appContext'

const appContext = inject(AppContextKey, null)
const cdnURL = computed(() => appContext?.$cdnURL ?? '')

// full modal
const fullModal = ref(true)
const isTreasureFound = ref(false)

const anim1 = ref(null)
const anim2 = ref(null)
const options1 = ref({
  animationData: null,
  loop: false
})
const options2 = ref({
  animationData: null,
  autoplay: false
})

const buildLottieUrl = (fileName) => {
  const base = cdnURL.value ? cdnURL.value.replace(/\/$/, '') : ''
  return `${base}/images/lottie/common/${fileName}`
}

const loadLottieData = async (fileName, targetOptions) => {
  try {
    const response = await fetch(buildLottieUrl(fileName))
    if (!response.ok) {
      return
    }
    targetOptions.value.animationData = await response.json()
  } catch (error) {
    // ignore fetch errors for publish-only template
  }
}

const handleAnimation1 = (anim) => {
  anim1.value = anim
}

const handleAnimation2 = (anim) => {
  anim2.value = anim
}

const handleClose = () => {
  fullModal.value = false
}

onMounted(() => {
  loadLottieData('etc_treasure_enter.json', options1)
  loadLottieData('etc_treasure_waiting.json', options2)
  setTimeout(() => {
    isTreasureFound.value = true
  }, 3000)
})
</script>





```
{% endraw %}
---
