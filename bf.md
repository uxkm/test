
{% raw %}
```js


// 보물찾기
.floating-treasure {
  position: fixed;
  top: 9.5rem;
  right: 2.9rem;
  z-index: 100;
  .btn-delete {
    position: absolute;
    top: 1.7rem;
    right: -2.2rem;
    z-index: 1;
    display: block;
    width: 3.8rem;
    height: 3.8rem;
    // background: url(#{$img-path}/payfan/visual/etc/btn_delete.png) no-repeat;
    background-size: 3.8rem auto;
  }
  .btn-treasure {
    position: relative;
    display: block;
    width: 11.0rem;
    height: 11.0rem;
  }
  .anibox {
    display: block;
    width: 11.0rem;
    height: 11.0rem;
  }
  .text {
    position: absolute;
    top: -3.1rem;
    left: 50%;
    display: block;
    width: 11.7rem;
    height: 6.3rem;
    margin-left: -5.6rem;
    padding-top: 1.7rem;
    padding-right: 0.5rem;
    font-size: 1.3rem;
    line-height: 1.8rem;
    text-align: center;
    color: $white;
    // background: url(#{$img-path}/payfan/visual/etc/bg_treasure_tooltip.png) no-repeat;
    background-size: 11.7rem auto;
    animation: 0.4s ease-in-out 0.7s backwards lottie-text;
    /* @keyframes duration | timing-function | delay | iteration-count | direction | fill-mode | play-state | name */
  }

  //250805 target-C2025070460731 보물팡팡
  &.target-C2025070460731{
    top: auto;
    bottom: 16rem;
    .text{
      width: 9.3rem;//8.3rem;
      height: 4.6rem;//3.6rem;
      // background: url(#{$img-path}/payfan/visual/etc/bg_treasure_tooltip2.png) no-repeat;
      background-size: 100% auto;
      top: -1.8rem;//-1.1rem;
      margin-left: -4.3rem;//-3.9rem;
      padding: .8rem 1rem 0;
      animation: .8s ease-in-out infinite lottie-text2;
    }
  }
}

// 보물찾기 풀팝업 닫기 버튼 숨김
.treasure-modal.sv-popup {
  background: rgba(0, 0, 0, 0.9);
  .sv-popup__close {
    display: none;
  }
}

.modal-area {
  &.ios-top{
    > .full > .modal-dialog > .modal-content{
      > .modal-header {
        padding-top: 3.5rem;
        &+.modal-body {
          padding-top: 9.1rem !important;
        }
      }
    }
  }
  // 하단 floating 버튼 고정시 content height100%로 생기는 스크롤 방지
  &.with-btn {
    .modal .modal-content.no-scroll .modal-body{
      height: calc(100% - 8rem) !important;
    }
  }
  .wide {
    margin: 0 -1rem;
  }
  .footer-shadow {
    .modal-footer {
      box-shadow: 0 0.6rem 1.2rem 0 rgba(22, 25, 36, .5);
    }
  }
  .scroll-move {
    .modal.full .modal-content {
      overflow-y: hidden;
    }
    .scroll-move-area {
      height: calc(100vh - 7.1rem);
      overflow-y: auto;
      margin: 0 -2.4rem;
      padding: 0 2.4rem;
    }
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

// animation
@keyframes lottie-text2 {
  0% { transform: translateY(0); }
  50% { transform: translateY(15%); }
  100% { transform: translateY(0); }
}
@keyframes lottie-text {
  0% {
    opacity: 0;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}





<route lang="yaml">
meta:
  id: SBT178A01
  title: 
  menu: "혜택 > 보물찾기"
  layout: EmptyLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.9
</route>
<template>
  <teleport to="body">
  <div class="floating-treasure target-C2025070460731">
    <div class="btn-treasure">
      <a
        href="javascript:;"
        class="anibox"
      >
        <!-- 등장 로티 -->
        <div>
          <ScLottie
            v-if="prevShow"
            :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_trigger_coin_01.json`"
            :width="118"
            :height="134"
            :loop="false"
            :autoPlay="true"
            @onAnimationLoaded="handleAnimation1"
          />
        </div>
        <!-- 대기 로티 -->
        <div>
          <ScLottie
            v-if="nextShow"
            :animation-link="`${cdnURL}/images/lottie/common/treasure_hunt_trigger_coin_02.json`"
            :width="118"
            :height="134"
            :loop="true"
            :autoPlay="true"
            @onAnimationLoaded="handleAnimation2"
          />
        </div>
      </a>
      <span v-if="nextShow" class="text">보물이에요!</span>
    </div>
    <button
      type="button"
      class="btn-delete"
    >
      <span class="sr-only">삭제</span>
    </button>
  </div>
</template>

<script setup>
import { inject, onBeforeUnmount, onMounted, ref } from "vue";
import { ScLottie } from "@shc-nss/ui/shc";
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
