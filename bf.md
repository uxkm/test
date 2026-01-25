
{% raw %}
```js

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
  <div class="modal-area">
    <transition name="slide-up">
      <FullPopup
        v-if="fullModal"
        v-model="fullModal"
        class="treasure-modal target-C2025070460731"
      >
        <div class="treasure-box">
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
      </FullPopup>
    </transition>
  </div>
</template>

<script setup>
import { ScLottie } from '@shc-nss/ui/shc'
import { FullPopup } from '@shc-nss/ui/solid'
import { computed, inject, ref } from 'vue'
import { AppContextKey } from '@/configs/inject/appContext'

const appContext = inject(AppContextKey, null)
const cdnURL = computed(() => appContext?.$cdnURL ?? '')

// full modal
const fullModal = defineModel({ default: true })

const anim1 = ref(null)
const anim2 = ref(null)

const handleAnimation1 = (anim) => {
  anim1.value = anim
}

const handleAnimation2 = (anim) => {
  anim2.value = anim
}
</script>



```
{% endraw %}
---
