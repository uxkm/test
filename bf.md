
{% raw %}
```js


<template>
  <!-- S: 이벤트 프로모션 -->
  <section class="bf-promotion" aria-label="이벤트 프로모션">
    <!-- S : 이벤트 프로모션 로딩중 스켈레톤 -->
    <div class="promotion-banner" aria-label="로딩중" tabindex="0" role="text">
      <ul class="webzine-list" aria-hidden="true">
        <li class="webzine-item">
          <div class="webzine-item__before">
            <LoadingSkeleton width="100%" height="100%" rounded="small" />
          </div>
          <div class="webzine-item__contents">
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="26" rounded="small" />
          </div>
          <div class="webzine-item__after">
            <LoadingSkeleton width="100%" :height="25" rounded="small" />
          </div>
        </li>
      </ul>
    </div>
    <!-- E : 이벤트 프로모션 로딩중 스켈레톤 -->

    <!-- S : 인터렉션형 배너 타입 -->
    <div
      ref="promotionBannerContainer"
      class="promotion-banner"
      :class="{ 'sc-swipe-dismissed': isDismissed }"
      :style="{
        backgroundImage: `url(${$cdnURL}/images/dummy/img_promotion_sample.png)`,
      }"
    >
      <div
        ref="promotionBannerInner"
        class="promotion-banner__inner"
        :style="{
          '--inner-width': innerWidth,
          '--inner-opacity': opacity,
          '--transition-duration': isSwiping.value ? '0ms' : '300ms',
          '--is-dismissed': isDismissed ? 1 : 0,
          willChange: isSwiping.value ? 'width' : 'auto',
        }"
      >
        <!-- 260209: 접근성 대응 role="button" 추가 -->
        <!-- 접근성 문구에 액션(내용 더보기) 추가 + 클릭 타겟 확대 -->
        <div
          ref="bannerLink"
          tabindex="0"
          class="banner-link"
          aria-label="제주 리조트 패키지 프로모션 신한카드 고객 대상 특별혜택 내용 더보기"
          role="button"
          @click="handleButtonClick"
        >
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/img_foundation.png`"
            alt=""
            class="promotion-banner__img"
            aria-hidden="true"
          />
          <div class="promotion-banner__contents" aria-hidden="true">
            <span>제주 리조트 패키지 프로모션</span>
            <p class="text-bold">신한카드 고객 대상 특별혜택</p>
          </div>
        </div>
      </div>
      <div
        v-if="!isDismissed"
        ref="promotionBannerHandle"
        class="promotion-banner__handle"
        :style="{
          '--handle-opacity': handleOpacity,
          '--handle-offset': handleButtonOffset,
          '--transition-duration': isSwiping ? '0ms' : '300ms',
        }"
        aria-hidden="true"
      >
        <div
          class="sc-popover__custom"
          :class="{ 'animation-paused': handleOpacity < 0.1 }"
          data-placement="top-center"
        >
          <div class="sc-popover__custom-content">
            <span>당겨보세요!</span>
          </div>
        </div>
        <!-- handle-button은 시각적 핸들 역할만 하므로 button 대신 div 사용 -->
        <div
          ref="handleButton"
          class="handle-button"
          aria-hidden="true"
          @pointerdown="handleButtonPointerDown"
        >
          <Icon name="Arrow_left" size="20" aria-hidden="true" />
        </div>
      </div>
      <CapsuleButton
        v-if="isExpanded"
        ref="promotionBannerButton"
        text="JW 메리어트 제주 리조트 혜택받기"
        color="primary"
        variant="outline"
        size="small"
        :rightIcon="{ iconName: 'Chevron_right' }"
        class="promotion-banner__button"
      />
      <!-- 260113: 버튼 아이콘 사이즈 수정 small -> large -->
      <IconButton
        v-if="isExpanded"
        :color="false"
        :disabled="false"
        size="large"
        aria-label="이전 내용보기"
        class="close-button"
        @click="handleReset"
      >
        <template #icon>
          <Icon name="X" size="20" aria-hidden="true" />
        </template>
      </IconButton>
    </div>
    <!-- S : 인터렉션형 배너 타입 -->

    <!--
      일반형으로 제공하는 경우 
      class="sc-banner" 에 rtl 추가된 경우 아이콘(이미지) 와 텍스트 위치가 좌우 반전
      class="sc-banner" 에 is-reverse 추가된 경우 메인텍스트와 서브텍스트 상하 위치가 반전
      data-type 유형에 따른 배너 선택 data-type=="a" || "b" || "b-image" || "c" || "c-button" || "c-image"
      - a: 텍스트 타입
      - b: 3d,2d 아이콘 그래픽 타입
      - b-image: image 타입
      - c: 3d,2d 아이콘 그래픽 타입 - image
      - c-button: 버튼강조 타입
      - c-image: 배너 + 버튼 조합 타입
      data-color-type="solid" || "tint"
      data-color 에 따라 배경이 다르게 설정됨. 기본은 디자인 가이드에 따라 SOLID, TINT 배경
      data-color="bg-banner_gray_solid"
      data-color="bg-banner_brand_tint-same"
      data-color="bg-banner_indigo_tint-same"
      data-color="bg-banner_purple_tint-same"
      data-color="bg-banner_gray_solid-same"
      data-color="bg-banner_brand_solid-same"
      data-color="bg-banner_indigo_solid-same"
      data-color="bg-banner_purple_solid-same"
      data-color="seafoam-700"

      data-color 값은 관리자에서 등록한 색상으로 표시됨
    -->
    <!-- 260113: 마크업 (promotion - 일반형 배너 제거) -->
    <!-- S : 기본형 배너 a타입 -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
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
      </a>
    </div> -->
    <!-- E : 기본형 배너 a타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner rtl is-reverse"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="b"
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
      </a>
    </div> -->
    <!-- E : 3d,2d 아이콘 그래픽 타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="자동납부 한번에 신청, 정기결제 서비스를 한번에 신청해보세요"
        tabindex="0"
        data-type="b"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/pages/base/Calendar_C.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong class="banner-button">
            자동납부 한번에 신청
            <Icon name="Chevron_right" size="20" />
          </strong>
          <span>정기결제 서비스를 한번에 신청해보세요</span>
        </p>
      </a>
    </div> -->
    <!-- E : 3d,2d 아이콘 그래픽 타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 - image -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner rtl is-reverse"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="b-image"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img
            :src="`${$cdnURL}/images/dummy/img_promotion_sample.png`"
            alt=""
          />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span>더하면, 알아서 따라오는 할인쿠폰!</span>
        </p>
      </a>
    </div> -->
    <!-- E : 3d,2d 아이콘 그래픽 타입 - image -->

    <!-- S : c 타입  -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="c"
        data-color="bg-banner_indigo_solid-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/img_dummy_icon.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span>더하면, 알아서 따라오는 할인쿠폰!</span>
        </p>
      </a>
    </div> -->
    <!-- E : c 타입 -->

    <!-- S : c 타입  -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="매일 새로운 광고가 기다리고 있어요! 광고 보고 포인트 적립하기. 자세히 보기"
        tabindex="0"
        data-type="c"
        data-color="bg-banner_purple_solid"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/img_dummy_icon.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>매일 새로운 광고가 기다리고 있어요!</strong>
          <span class="more-button">
            광고 보고 포인트 적립하기
            <Icon name="Chevron_right" size="16" />
          </span>
        </p>
      </a>
    </div> -->
    <!-- E : c 타입 -->

    <!-- S : c 타입 - 버튼강조  -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="c-button"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/img_dummy_icon.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span class="more-button">
            더하면, 알아서 따라오는 할인쿠폰!
            <Icon name="Chevron_right" size="16" />
          </span>
        </p>
      </a>
    </div> -->
    <!-- E : c 타입 - 버튼강조 -->

    <!-- S : 배너 + 버튼 조합  -->
    <div class="promotion-banner__basic">
      <div class="sc-banner rtl" data-type="c-image" data-color="bg-gray">
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/AD.png`" alt="" />
        </div>
        <p class="sc-banner__text">
          <strong>매일 새로운 광고가<br />기다리고 있어요!</strong>
        </p>
        <BoxButton
          text="광고 보고 포인트 적립하기"
          color="secondary"
          size="large"
          class="footer-button bg-white"
        />
      </div>
    </div>
    <!-- E : 배너 + 버튼 조합 -->
  </section>
  <!-- E: 이벤트 프로모션 -->
</template>

<script setup>
import { computed, inject, nextTick, onMounted, ref, watchEffect } from "vue";
import { useTemplateRef } from "vue";
// [수정 260303] 네이티브 WebView 터치 스와이프 대응: useSwipe(touch) 추가
// 기존:
//   import { usePointerSwipe } from "@vueuse/core";
import { usePointerSwipe, useSwipe } from "@vueuse/core";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  BoxButton,
  CapsuleButton,
  Icon,
  IconButton,
  LoadingSkeleton,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// 프로모션 배너 스와이프 해제 기능
const promotionBannerInner = useTemplateRef("promotionBannerInner");
const promotionBannerContainer = useTemplateRef("promotionBannerContainer");
const promotionBannerHandle = useTemplateRef("promotionBannerHandle");
const handleButton = useTemplateRef("handleButton");
const promotionBannerButton = useTemplateRef("promotionBannerButton");
const bannerLink = useTemplateRef("bannerLink");

// 터치/드래그 민감도 설정
const SENSITIVITY = {
  /**
   * SWIPE_THRESHOLD: usePointerSwipe 시작 임계값 (px)
   * - 설명: 스와이프 이벤트가 시작되기 전에 무시할 최소 이동 거리
   * - 값이 낮을수록: 더 민감하게 반응 (0 = 모든 움직임 감지)
   * - 값이 높을수록: 작은 움직임은 무시하고 큰 움직임만 감지
   * - 사용 위치: usePointerSwipe의 threshold 옵션
   */
  SWIPE_THRESHOLD: 0,

  /**
   * DRAG_DETECTION: 드래그로 인식하는 최소 거리 (px)
   * - 설명: 클릭과 드래그를 구분하기 위한 최소 이동 거리
   * - 값이 낮을수록: 작은 움직임도 드래그로 인식 (민감함)
   * - 값이 높을수록: 어느 정도 움직여야 드래그로 인식 (덜 민감함)
   * - 0으로 설정 시: 터치 시작과 동시에 드래그로 인식하여 즉시 움직임 시작
   * - 사용 위치: onSwipe에서 hasDragged 플래그 설정 시
   */
  DRAG_DETECTION: 0,

  /**
   * CLICK_THRESHOLD: 클릭으로 간주하는 최대 거리 (px)
   * - 설명: 이 거리 미만으로 움직이면 클릭으로 간주
   * - 값이 낮을수록: 작은 움직임도 드래그로 인식
   * - 값이 높을수록: 어느 정도 움직여도 클릭으로 간주
   * - 사용 위치: onSwipeEnd에서 클릭/드래그 구분 시
   */
  CLICK_THRESHOLD: 10,

  /**
   * DISMISS_THRESHOLD: dismiss 임계값 (px)
   * - 설명: promotion-banner__inner를 좌측으로 이 거리만큼 드래그하면 자동으로 dismiss
   * - 값이 낮을수록: 적게 드래그해도 dismiss (민감함)
   * - 값이 높을수록: 많이 드래그해야 dismiss (덜 민감함)
   * - 사용 위치: promotion-banner__inner의 onSwipeEnd에서
   */
  DISMISS_THRESHOLD: 40,

  /**
   * DISMISS_PERCENTAGE: dismiss 임계값 (%)
   * - 설명: promotion-banner__handle를 초기 너비의 이 비율만큼 좌측으로 드래그하면 dismiss
   * - 값이 낮을수록: 적게 드래그해도 dismiss (민감함)
   * - 값이 높을수록: 많이 드래그해야 dismiss (덜 민감함)
   * - 예시: 30% = 초기 너비의 30%만큼 좌측으로 드래그하면 dismiss
   * - 사용 위치: promotion-banner__handle의 onSwipeEnd에서
   */
  DISMISS_PERCENTAGE: 30,

  /**
   * RESET_THRESHOLD: 원래 위치로 복귀하는 임계값 (px)
   * - 설명: 드래그 중 포인터가 벗어났을 때, 이 거리 미만으로 움직였다면 원래 위치로 복귀
   * - 값이 낮을수록: 적게 움직여도 원래 위치로 복귀 (덜 민감함)
   * - 값이 높을수록: 많이 움직여야 원래 위치로 복귀 (민감함)
   * - 사용 위치: resetToInitial 함수에서
   */
  RESET_THRESHOLD: 50,
};

const isDismissed = ref(false);
const innerWidth = ref(null); // promotion-banner__inner의 width 값
const opacity = ref(1);
const isExpanded = ref(false);

// sc-swipe-dismissed 클래스 변경 감지
watchEffect(() => {
  const container = promotionBannerContainer.value;
  if (container) {
    isExpanded.value = container.classList.contains("sc-swipe-dismissed");
  }
});

// handle 영역의 너비 계산
const handleWidth = computed(() => {
  return promotionBannerHandle.value?.offsetWidth ?? 56; // 기본값 56px (CSS에서 설정된 값)
});

// handle-button의 너비 계산 (25px)
const handleButtonWidth = 25;

// promotion-banner__inner의 초기 너비 계산
const initialInnerWidth = computed(() => {
  if (!promotionBannerInner.value) return null;
  return promotionBannerInner.value.offsetWidth;
});

// promotion-banner__handle의 opacity 계산
const handleOpacity = computed(() => {
  if (!initialInnerWidth.value || innerWidth.value === null) return 1;
  const currentWidth =
    parseFloat(String(innerWidth.value).replace("px", "")) ||
    initialInnerWidth.value;
  const initial = initialInnerWidth.value;
  const widthRatio = currentWidth / initial; // 0 ~ 1 사이의 값
  return Math.max(0, widthRatio);
});

// 공통 스와이프 상태
let hasDragged = false;
let startX = 0;

// [수정 260303] 터치·마우스 공통 처리: distance 인자로 받는 핸들러 추출
// 기존:
//   const { distanceX, isSwiping: innerIsSwiping } = usePointerSwipe(
//     promotionBannerInner,
//     {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { hasDragged = true; startX = e.clientX || 0; ... },
//       onSwipe(e) { const distance = distanceX.value; ... },
//       onSwipeEnd() { const isClick = !hasDragged || Math.abs(distanceX.value) < ...; ... },
//     }
//   );
const innerOnSwipeStart = () => {
  hasDragged = true;
  const initialWidth = initialInnerWidth.value;
  if (initialWidth) {
    const widthStr = `${initialWidth}px`;
    if (innerWidth.value === null) {
      innerWidth.value = widthStr;
    }
    const innerEl = promotionBannerInner.value;
    if (innerEl) {
      innerEl.style.transition = "none";
      innerEl.style.width = widthStr;
      innerEl.style.setProperty("--inner-width", widthStr);
    }
  }
};
const innerOnSwipe = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  if (innerWidth.value === null) innerWidth.value = `${initialWidth}px`;
  const newWidth =
    distance > 0
      ? `${Math.max(0, initialWidth - distance)}px`
      : `${initialWidth}px`;
  const innerEl = promotionBannerInner.value;
  if (innerEl) {
    innerEl.style.transition = "none";
    innerEl.style.width = newWidth;
    innerEl.style.setProperty("--inner-width", newWidth);
  }
  innerWidth.value = newWidth;
  opacity.value = 1;
};
const innerOnSwipeEnd = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  const isClick =
    !hasDragged || Math.abs(distance) < SENSITIVITY.CLICK_THRESHOLD;
  const applyDismiss = () => {
    innerWidth.value = "0px";
    opacity.value = 1;
    isDismissed.value = true;
    if (promotionBannerInner.value) {
      promotionBannerInner.value.style.visibility = "hidden";
      promotionBannerInner.value.style.display = "none";
    }
    setTimeout(() => {
      promotionBannerContainer.value?.classList.add("sc-swipe-dismissed");
      isExpanded.value = true;
      nextTick(() => {
        const buttonEl = promotionBannerButton.value?.$el;
        if (buttonEl?.focus) buttonEl.focus();
        else buttonEl?.querySelector?.("button, a, [tabindex]")?.focus();
      });
    }, 600);
  };
  if (isClick) {
    // 클릭 분기에서 조기 return 시 hasDragged가 남지 않도록 즉시 초기화
    hasDragged = false;
    applyDismiss();
    return;
  }
  if (distance >= SENSITIVITY.DISMISS_THRESHOLD) {
    applyDismiss();
  } else {
    innerWidth.value = `${initialWidth}px`;
    opacity.value = 1;
  }
  hasDragged = false;
};

// [수정 260303] inner: 터치(useSwipe, passive:false) + 마우스(usePointerSwipe, pointerTypes:['mouse','pen']) 하이브리드
// 기존:
//   const { distanceX, isSwiping: innerIsSwiping } = usePointerSwipe(
//     promotionBannerInner,
//     {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { ... },
//       onSwipe(e) { const distance = distanceX.value; ... },
//       onSwipeEnd() { ... },
//     }
//   );
const {
  lengthX: innerTouchLengthX,
  isSwiping: innerTouchIsSwiping,
} = useSwipe(promotionBannerInner, {
  threshold: SENSITIVITY.SWIPE_THRESHOLD,
  passive: false,
  onSwipeStart: innerOnSwipeStart,
  onSwipe: () => innerOnSwipe(innerTouchLengthX.value),
  onSwipeEnd: (_, __) => innerOnSwipeEnd(innerTouchLengthX.value),
});
const { distanceX: innerPointerDistanceX, isSwiping: innerPointerIsSwiping } =
  usePointerSwipe(promotionBannerInner, {
    pointerTypes: ["mouse", "pen"],
    disableTextSelect: true,
    threshold: SENSITIVITY.SWIPE_THRESHOLD,
    onSwipeStart: () => {
      startX = 0;
      innerOnSwipeStart();
    },
    onSwipe: () => innerOnSwipe(innerPointerDistanceX.value),
    onSwipeEnd: () => innerOnSwipeEnd(innerPointerDistanceX.value),
  });

// [수정 260303] handle: inner와 동일한 터치·마우스 공통 핸들러 패턴 적용
// 기존:
//   const { distanceX: handleDistanceX, isSwiping: handleIsSwiping } =
//     usePointerSwipe(promotionBannerHandle, {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { ... },
//       onSwipe(e) { const distance = handleDistanceX.value; ... },
//       onSwipeEnd() { ... },
//     });
const handleOnSwipeStart = () => {
  hasDragged = true;
  const initialWidth = initialInnerWidth.value;
  if (initialWidth) {
    const widthStr = `${initialWidth}px`;
    if (innerWidth.value === null) innerWidth.value = widthStr;
    const innerEl = promotionBannerInner.value;
    if (innerEl) {
      innerEl.style.transition = "none";
      innerEl.style.width = widthStr;
      innerEl.style.setProperty("--inner-width", widthStr);
    }
  }
};
const handleOnSwipe = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  if (innerWidth.value === null) innerWidth.value = `${initialWidth}px`;
  const newWidth =
    distance > 0
      ? `${Math.max(0, initialWidth - distance)}px`
      : `${initialWidth}px`;
  const innerEl = promotionBannerInner.value;
  if (innerEl) {
    innerEl.style.transition = "none";
    innerEl.style.width = newWidth;
    innerEl.style.setProperty("--inner-width", newWidth);
  }
  innerWidth.value = newWidth;
  opacity.value = 1;
};
const handleOnSwipeEnd = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  const isClick =
    !hasDragged || Math.abs(distance) < SENSITIVITY.CLICK_THRESHOLD;
  const applyDismiss = () => {
    innerWidth.value = "0px";
    opacity.value = 1;
    isDismissed.value = true;
    if (promotionBannerInner.value) {
      promotionBannerInner.value.style.visibility = "hidden";
      promotionBannerInner.value.style.display = "none";
    }
    setTimeout(() => {
      promotionBannerContainer.value?.classList.add("sc-swipe-dismissed");
      isExpanded.value = true;
      nextTick(() => {
        const buttonEl = promotionBannerButton.value?.$el;
        if (buttonEl?.focus) buttonEl.focus();
        else buttonEl?.querySelector?.("button, a, [tabindex]")?.focus();
      });
    }, 600);
  };
  if (isClick) {
    // 클릭 분기에서 조기 return 시 hasDragged가 남지 않도록 즉시 초기화
    hasDragged = false;
    applyDismiss();
    return;
  }
  if (distance >= SENSITIVITY.DISMISS_THRESHOLD) {
    applyDismiss();
  } else {
    innerWidth.value = `${initialWidth}px`;
    opacity.value = 1;
  }
  hasDragged = false;
};

// [수정 260303] handle: useSwipe + usePointerSwipe 하이브리드
// 기존:
//   const { distanceX: handleDistanceX, isSwiping: handleIsSwiping } =
//     usePointerSwipe(promotionBannerHandle, {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { ... },
//       onSwipe(e) { ... },
//       onSwipeEnd() { ... },
//     });
const { lengthX: handleTouchLengthX, isSwiping: handleTouchIsSwiping } =
  useSwipe(promotionBannerHandle, {
    threshold: SENSITIVITY.SWIPE_THRESHOLD,
    passive: false,
    onSwipeStart: handleOnSwipeStart,
    onSwipe: () => handleOnSwipe(handleTouchLengthX.value),
    onSwipeEnd: (_, __) => handleOnSwipeEnd(handleTouchLengthX.value),
  });
const {
  distanceX: handlePointerDistanceX,
  isSwiping: handlePointerIsSwiping,
} = usePointerSwipe(promotionBannerHandle, {
  pointerTypes: ["mouse", "pen"],
  disableTextSelect: true,
  threshold: SENSITIVITY.SWIPE_THRESHOLD,
  onSwipeStart: () => {
    startX = 0;
    handleOnSwipeStart();
  },
  onSwipe: () => handleOnSwipe(handlePointerDistanceX.value),
  onSwipeEnd: () => handleOnSwipeEnd(handlePointerDistanceX.value),
});

// [수정 260303] isSwiping: inner/handle의 터치·마우스 4개 소스 통합
// 기존:
//   const isSwiping = computed(
//     () => innerIsSwiping.value || handleIsSwiping.value
//   );
const isSwiping = computed(
  () =>
    innerTouchIsSwiping.value ||
    innerPointerIsSwiping.value ||
    handleTouchIsSwiping.value ||
    handlePointerIsSwiping.value
);

// 드래그 중 포인터가 벗어났을 때 상태 리셋
const resetToInitial = () => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (initialWidth && innerWidth.value !== null) {
    const currentWidth =
      parseFloat(String(innerWidth.value).replace("px", "")) || initialWidth;
    // 50px 임계값 미만이면 원래 위치로 복귀
    const dragThreshold = SENSITIVITY.RESET_THRESHOLD;
    const widthReduced = initialWidth - currentWidth;

    if (widthReduced < dragThreshold && widthReduced > 0) {
      // 원래 사이즈로 복귀
      innerWidth.value = `${initialWidth}px`;
      opacity.value = 1;
    }
  }
};

// isSwiping이 false가 되었을 때 상태 리셋
watchEffect(() => {
  if (!isSwiping.value && !isDismissed.value) {
    resetToInitial();
  }
});

// 포인터 이벤트로도 리셋 처리 (드래그 중 포인터가 벗어났을 때)
watchEffect(() => {
  const inner = promotionBannerInner.value;
  const handle = promotionBannerHandle.value;

  if (!inner && !handle) return;

  const handlePointerLeave = () => {
    if (isSwiping.value) {
      // 다음 틱에서 리셋 (onSwipeEnd가 호출될 수 있도록)
      nextTick(() => {
        if (!isSwiping.value && !isDismissed.value) {
          resetToInitial();
        }
      });
    }
  };

  if (inner) {
    inner.addEventListener("pointerleave", handlePointerLeave);
    inner.addEventListener("pointercancel", handlePointerLeave);
  }

  if (handle) {
    handle.addEventListener("pointerleave", handlePointerLeave);
    handle.addEventListener("pointercancel", handlePointerLeave);
  }

  return () => {
    if (inner) {
      inner.removeEventListener("pointerleave", handlePointerLeave);
      inner.removeEventListener("pointercancel", handlePointerLeave);
    }
    if (handle) {
      handle.removeEventListener("pointerleave", handlePointerLeave);
      handle.removeEventListener("pointercancel", handlePointerLeave);
    }
  };
});

// handle-button의 offset 계산 (항상 고정, 드래그 시에도 움직이지 않음)
const handleButtonOffset = computed(() => {
  // [수정 260303] 기존:
  //   if (innerIsSwiping.value || handleIsSwiping.value) return "0px";
  if (isSwiping.value) return "0px";

  // 드래그가 아닐 때도 항상 고정 (움직이지 않음)
  return "0px";
});

// handle-button 스타일 적용 (promotion-banner__inner와 함께 움직임)
watchEffect(() => {
  const button = handleButton.value;
  if (!button) return;

  // 드래그 중: 애니메이션 없음, 드래그 종료 후: ease-out 300ms
  button.style.transition = isSwiping.value
    ? "none"
    : "transform 300ms cubic-bezier(0.4, 0, 0.2, 1)"; // ease-out
});

// handle-button 포인터 다운 핸들러 (스와이프 시작 감지)
const handleButtonPointerDown = (e) => {
  // 스와이프 시작을 위해 hasDragged 초기화
  hasDragged = false;
  startX = e.clientX || 0;
};

// handle-button 클릭 핸들러 (클릭만 처리)
const handleButtonClick = (e) => {
  // 실제 스와이프 진행 중일 때만 클릭 무시
  // banner-link 클릭 전파 시 hasDragged 값이 남아도 탭이 즉시 반응하도록 hasDragged 조건은 제외
  if (isSwiping.value) {
    if (e) {
      e.preventDefault();
      e.stopPropagation();
    }
    return;
  }

  if (isDismissed.value) return;

  const width = handleWidth.value;
  if (!width) return;

  // 클릭 시 dismiss - 사이즈는 즉시 0으로 (딜레이 없음)
  innerWidth.value = "0px";
  opacity.value = 1; // opacity 효과 없음
  isDismissed.value = true;

  // promotion-banner__inner 즉시 숨김 처리
  if (promotionBannerInner.value) {
    promotionBannerInner.value.style.visibility = "hidden";
    promotionBannerInner.value.style.display = "none";
  }

  // 애니메이션 완료(300ms) 후 300ms 딜레이 후 sc-swipe-dismissed 클래스 추가
  setTimeout(() => {
    promotionBannerContainer.value?.classList.add("sc-swipe-dismissed");
    isExpanded.value = true; // 펼쳐진 상태로 설정
    // dismiss 후 promotion-banner__button에 포커스
    nextTick(() => {
      const buttonEl = promotionBannerButton.value?.$el;
      if (buttonEl && typeof buttonEl.focus === "function") {
        buttonEl.focus();
      } else if (buttonEl?.querySelector) {
        const focusableEl = buttonEl.querySelector("button, a, [tabindex]");
        focusableEl?.focus();
      }
    });
  }, 600); // 300ms (애니메이션) + 300ms (추가 딜레이)
};

const handleReset = () => {
  // 원래 사이즈로 복귀
  const initialWidth = initialInnerWidth.value;
  if (initialWidth) {
    const widthStr = `${initialWidth}px`;
    innerWidth.value = widthStr;

    // DOM에 직접 설정하여 원래 위치로 복귀
    const innerEl = promotionBannerInner.value;
    if (innerEl) {
      // transition을 복원하여 애니메이션 적용
      innerEl.style.transition = "";
      innerEl.style.width = widthStr;
      innerEl.style.setProperty("--inner-width", widthStr);
    }
  }
  opacity.value = 1;
  // [260115] isDismissed를 false로 설정하는 시점을 접힘 애니메이션 완료 후로 변경
  // isDismissed.value = false; // 접힘 애니메이션 완료 후로 이동
  isExpanded.value = false; // 펼쳐진 상태 해제

  // 접힘 애니메이션 적용
  // [260115] promotion-banner-collapse 클래스가 제대로 적용되도록 nextTick과 requestAnimationFrame 사용
  // [260115] 접힘 애니메이션 완료 후 promotion-banner__inner와 promotion-banner__handle를 다시 보이도록 수정
  const container = promotionBannerContainer.value;
  if (container) {
    container.classList.remove("sc-swipe-dismissed");

    // DOM 업데이트 후 접힘 애니메이션 클래스 추가
    // [260115] nextTick과 requestAnimationFrame을 사용하여 DOM 업데이트 완료 후 클래스 추가
    nextTick(() => {
      requestAnimationFrame(() => {
        container.classList.add("promotion-banner-collapse");

        // 애니메이션 완료 후 클래스 제거 및 promotion-banner__inner, promotion-banner__handle 다시 보이기
        // [260115] 접힘 애니메이션(200ms) 완료 후 promotion-banner__inner와 promotion-banner__handle를 다시 보이도록 수정
        setTimeout(() => {
          container.classList.remove("promotion-banner-collapse");

          // [260115] 접힘 애니메이션 완료 후 isDismissed를 false로 설정하여 promotion-banner__handle를 다시 보이도록 변경
          isDismissed.value = false;

          // promotion-banner__inner 다시 보이기
          // [260115] 접힘 애니메이션 완료 후에만 promotion-banner__inner를 다시 보이도록 변경
          if (promotionBannerInner.value) {
            promotionBannerInner.value.style.visibility = "visible";
            promotionBannerInner.value.style.display = "";
          }
        }, 200);
      });
    });
  }
  // close-button 클릭 시 banner-link에 포커스
  nextTick(() => {
    bannerLink.value?.focus?.();
  });
};

// 초기 handle-button 위치 설정 (우측에 위치)
const initializeHandleButtonPosition = () => {
  if (isDismissed.value) return;
  // offset이 이미 "0px"로 초기화되어 있으므로 추가 작업 불필요
};

// 컴포넌트 마운트 시 초기 위치 설정
onMounted(async () => {
  await nextTick();
  // DOM이 완전히 렌더링될 때까지 대기
  if (promotionBannerHandle.value) {
    initializeHandleButtonPosition();
  }
  // innerWidth 초기화
  if (promotionBannerInner.value && innerWidth.value === null) {
    const initialWidth = initialInnerWidth.value;
    if (initialWidth) {
      innerWidth.value = `${initialWidth}px`;
    }
  }
});
</script>
<!--
  [개발 처리/요청 사항] promotion-banner 터치 스와이프 동작
  - 배경: 로컬 웹뷰·브라우저에서는 스와이프 동작하나, 네이티브 앱에서는 스크롤 뷰가 터치를 선점하여 동작하지 않음
  - iOS: WebView 상위 UIScrollView의 delaysContentTouches, 제스처 설정 조정하여 배너 영역 수평 터치가 WebView에 전달되도록
  - Android: 배너 영역 터치 시 parent.requestDisallowInterceptTouchEvent(true) 호출하여 상위 스크롤 뷰가 터치를 가로채지 않도록
  - 목표: promotion-banner__inner, promotion-banner__handle 영역의 좌측 스와이프가 WebView까지 전달되어 dismiss 동작
-->







@use "@assets/styles/pay/_benefits" as *;

const args = {
  slides: slides,
  slidesPerView: "1.8",
  spaceBetween: "5%",
  // [추가] 자동재생/정지, 1/n 카운터 옵션 추가 시작
  pagination: true, // 1/n 카운터 + 재생/정지 컨트롤 노출
  paginationType: "fraction", // 블릿 대신 1/n 형식
  autoplay: true, // 자동재생
  autoplayDelay: 3000, // 자동재생 간격(ms)
  // [추가] 자동재생/정지, 1/n 카운터 옵션 추가 끝
  navigation: false,
  loop: true,
  centeredSlides: true,
  theme: "default",
  speed: 300,
  direction: "horizontal",
};


.device_model_sm-f956n .sc-container[data-layout=MainLayout]:after {
  padding-bottom: calc(62px + var(--env-b) + 48px);
}
// sv-bottom-action-container__content: 오직 sv-button-group만 있으면 버튼 그룹에 env-b, 아니면 content에 env-b
.sv-bottom-action-container__content:has(> .sv-button-group:only-child) {
  > .sv-button-group {
    padding-bottom: var(--env-b);
  }
}
.sv-bottom-action-container__content:not(:has(> .sv-button-group:only-child)) {
  padding-bottom: var(--env-b);
}


// 1) nav를 노치 아래부터 배치
  .sv-navigation--fixed .sv-navigation__inner {
    top: var(--env-t);
  }
  // 2) 스크롤 시 노치 영역에 콘텐츠 노출 방지: nav 위에 노치 높이만큼 배경 덮음
  .sv-navigation--fixed .sv-navigation__inner::before {
    content: "";
    position: absolute;
    bottom: 100%;
    left: 0;
    right: 0;
    height: var(--env-t);
    background: inherit;
  }

  // override 처리
  // 상단 고정 네비게이션: 노치 영역을 0으로 두고 노치 아래부터 시작
  .sv-navigation--fixed .sv-navigation__inner {
    top: var(--env-t);
    padding-top: var(--spacing-lg);
  }

// 기본: body에 safe-area padding (footer 없을 때)
    .sv-bottom-sheet_body,
    &.bs-card-agree .sv-bottom-sheet_body {
      padding-bottom: var(--env-b);
    }
    // footer 있을 때: body padding 제거, 하단 CTA 영역에만 적용
    &:has(.sv-popup_footer),
    &.has-footer {
      .sv-bottom-sheet_body,
      &.bs-card-agree .sv-bottom-sheet_body {
        padding-bottom: 0;
      }
      .sv-bottom-action-container__content {
        padding-bottom: var(--env-b);
      }
    }


// android safe area구분

// Android: safe-area 사용 시 영향 제거
// Android에서 env(safe-area-inset-*)가 상단/측면 공간을 만들며 레이아웃이 밀리는 현상 방지
html.os_android {
  --env-t: 0;
  --env-l: 0;
  --env-r: 0;

  // bottomsheet, fullpopup, modalpopup, overlay 상단 영역까지 차지
  .sc-wrap ~ .sv-bottom-sheet,
  .sc-wrap ~ .sv-popup.sv-popup--variant-full,
  .sc-wrap ~ .sv-popup.sv-popup--variant-modal,
  .sc-wrap ~ .sv-overlay {
    padding-top: 0;
  }

  // error-boundary-wrap 상단 패딩 제거
  .error-boundary-wrap {
    padding-top: 0;
  }

  // 상단 고정 네비게이션 패딩 보정 (env-t 제거)
  .error-boundary-wrap .sv-navigation--fixed .sv-navigation__inner {
    padding-top: var(--spacing-lg);
  }
}


// promotion 네이티브 이슈 처리

// import	네이티브 WebView 터치 스와이프 대응: useSwipe(touch) 추가
// inner 공통 핸들러	터치·마우스 공통 처리: distance 인자로 받는 핸들러 추출
// inner useSwipe+usePointerSwipe	터치(useSwipe, passive:false) + 마우스(usePointerSwipe, pointerTypes:['mouse','pen']) 하이브리드
// handle 핸들러	inner와 동일한 터치·마우스 공통 핸들러 패턴 적용
// handle useSwipe+usePointerSwipe	handle: useSwipe + usePointerSwipe 하이브리드
// isSwiping	inner/handle의 터치·마우스 4개 소스 통합
// handleButtonOffset	isSwiping 통합 변수 사용 (기존 innerIsSwiping || handleIsSwiping)

// import – useSwipe 추가
// inner / handle 핸들러 – 공통 핸들러 추출
// useSwipe + usePointerSwipe 하이브리드 – inner, handle 각각 적용
// isSwiping computed – 4개 소스 통합
// handleButtonOffset – isSwiping.value 사용
// 주석 – [수정 260303] 추가


/*
네이티브 앱 확인 체크리스트
1. 터치 스와이프 동작 (핵심)
[ ] inner 영역: 배너 콘텐츠(이미지·텍스트)를 좌측으로 터치 스와이프 시 dismiss
[ ] handle 영역: "당겨보세요!" 버튼 영역을 좌측으로 터치 스와이프 시 dismiss
[ ] 스와이프 후 40px 이상 드래그 시 dismiss
[ ] 스와이프 후 40px 미만이면 원래 위치로 복귀
2. 클릭·버튼 동작
[ ] 짧은 탭(클릭) 시 dismiss
[ ] handle 버튼(화살표) 클릭 시 dismiss
[ ] X 버튼 클릭 시 접힘 애니메이션 후 배너 원래 상태로 복귀
3. 환경별 확인 (가능한 경우)
[ ] iOS (WKWebView): 터치 스와이프 동작
[ ] Android (WebView): 터치 스와이프 동작
4. 동작하지 않을 때 점검 사항
WebView가 들어 있는 스크롤 뷰가 터치를 선점하는지
해당 배너 영역에 requestDisallowInterceptTouchEvent (Android) 적용 여부
터치 이벤트가 WebView까지 전달되는지
요약: 웹에서의 동작과 동일하게, inner·handle 영역의 터치 스와이프가 정상 동작하는지가 네이티브에서 가장 중요한 확인 포인트.
*/
/*
  [네이티브 처리/요청 사항] promotion-banner 터치 스와이프 동작
  - 배경: 로컬 웹뷰·브라우저에서는 스와이프 동작하나, 네이티브 앱에서는 스크롤 뷰가 터치를 선점하여 동작하지 않음
  - iOS: WebView 상위 UIScrollView의 delaysContentTouches, 제스처 설정 조정하여 배너 영역 수평 터치가 WebView에 전달되도록
  - Android: 배너 영역 터치 시 parent.requestDisallowInterceptTouchEvent(true) 호출하여 상위 스크롤 뷰가 터치를 가로채지 않도록
  - 목표: promotion-banner__inner, promotion-banner__handle 영역의 좌측 스와이프가 WebView까지 전달되어 dismiss 동작
*/


<template>
  <!-- S: 이벤트 프로모션 -->
  <section class="bf-promotion" aria-label="이벤트 프로모션">
    <!-- S : 이벤트 프로모션 로딩중 스켈레톤 -->
    <div class="promotion-banner" aria-label="로딩중" tabindex="0" role="text">
      <ul class="webzine-list" aria-hidden="true">
        <li class="webzine-item">
          <div class="webzine-item__before">
            <LoadingSkeleton width="100%" height="100%" rounded="small" />
          </div>
          <div class="webzine-item__contents">
            <LoadingSkeleton width="100%" :height="22" rounded="small" />
            <LoadingSkeleton width="100%" :height="26" rounded="small" />
          </div>
          <div class="webzine-item__after">
            <LoadingSkeleton width="100%" :height="25" rounded="small" />
          </div>
        </li>
      </ul>
    </div>
    <!-- E : 이벤트 프로모션 로딩중 스켈레톤 -->

    <!-- S : 인터렉션형 배너 타입 -->
    <div
      ref="promotionBannerContainer"
      class="promotion-banner"
      :class="{ 'sc-swipe-dismissed': isDismissed }"
      :style="{
        backgroundImage: `url(${$cdnURL}/images/dummy/img_promotion_sample.png)`,
      }"
    >
      <div
        ref="promotionBannerInner"
        class="promotion-banner__inner"
        :style="{
          '--inner-width': innerWidth,
          '--inner-opacity': opacity,
          '--transition-duration': isSwiping.value ? '0ms' : '300ms',
          '--is-dismissed': isDismissed ? 1 : 0,
          willChange: isSwiping.value ? 'width' : 'auto',
        }"
      >
        <!-- 260209: 접근성 대응 role="button" 추가 -->
        <div
          ref="bannerLink"
          tabindex="0"
          class="banner-link"
          aria-label="제주 리조트 패키지 프로모션 신한카드 고객 대상 특별혜택"
          role="button"
        >
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/img_foundation.png`"
            alt=""
            class="promotion-banner__img"
            aria-hidden="true"
          />
          <div class="promotion-banner__contents" aria-hidden="true">
            <span>제주 리조트 패키지 프로모션</span>
            <p class="text-bold">신한카드 고객 대상 특별혜택</p>
          </div>
        </div>
      </div>
      <div
        v-if="!isDismissed"
        ref="promotionBannerHandle"
        class="promotion-banner__handle"
        :style="{
          '--handle-opacity': handleOpacity,
          '--handle-offset': handleButtonOffset,
          '--transition-duration': isSwiping ? '0ms' : '300ms',
        }"
      >
        <div
          class="sc-popover__custom"
          :class="{ 'animation-paused': handleOpacity < 0.1 }"
          data-placement="top-center"
        >
          <div class="sc-popover__custom-content">
            <span>당겨보세요!</span>
          </div>
        </div>
        <button
          ref="handleButton"
          class="handle-button"
          aria-label="내용 더보기"
          @click="handleButtonClick"
          @pointerdown="handleButtonPointerDown"
        >
          <Icon name="Arrow_left" size="20" aria-hidden="true" />
        </button>
      </div>
      <CapsuleButton
        v-if="isExpanded"
        ref="promotionBannerButton"
        text="JW 메리어트 제주 리조트 혜택받기"
        color="primary"
        variant="outline"
        size="small"
        :rightIcon="{ iconName: 'Chevron_right' }"
        class="promotion-banner__button"
      />
      <!-- 260113: 버튼 아이콘 사이즈 수정 small -> large -->
      <IconButton
        v-if="isExpanded"
        :color="false"
        :disabled="false"
        size="large"
        aria-label="이전 내용보기"
        class="close-button"
        @click="handleReset"
      >
        <template #icon>
          <Icon name="X" size="20" aria-hidden="true" />
        </template>
      </IconButton>
    </div>
    <!-- S : 인터렉션형 배너 타입 -->

    <!--
      일반형으로 제공하는 경우 
      class="sc-banner" 에 rtl 추가된 경우 아이콘(이미지) 와 텍스트 위치가 좌우 반전
      class="sc-banner" 에 is-reverse 추가된 경우 메인텍스트와 서브텍스트 상하 위치가 반전
      data-type 유형에 따른 배너 선택 data-type=="a" || "b" || "b-image" || "c" || "c-button" || "c-image"
      - a: 텍스트 타입
      - b: 3d,2d 아이콘 그래픽 타입
      - b-image: image 타입
      - c: 3d,2d 아이콘 그래픽 타입 - image
      - c-button: 버튼강조 타입
      - c-image: 배너 + 버튼 조합 타입
      data-color-type="solid" || "tint"
      data-color 에 따라 배경이 다르게 설정됨. 기본은 디자인 가이드에 따라 SOLID, TINT 배경
      data-color="bg-banner_gray_solid"
      data-color="bg-banner_brand_tint-same"
      data-color="bg-banner_indigo_tint-same"
      data-color="bg-banner_purple_tint-same"
      data-color="bg-banner_gray_solid-same"
      data-color="bg-banner_brand_solid-same"
      data-color="bg-banner_indigo_solid-same"
      data-color="bg-banner_purple_solid-same"
      data-color="seafoam-700"

      data-color 값은 관리자에서 등록한 색상으로 표시됨
    -->
    <!-- 260113: 마크업 (promotion - 일반형 배너 제거) -->
    <!-- S : 기본형 배너 a타입 -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
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
      </a>
    </div> -->
    <!-- E : 기본형 배너 a타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner rtl is-reverse"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="b"
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
      </a>
    </div> -->
    <!-- E : 3d,2d 아이콘 그래픽 타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="자동납부 한번에 신청, 정기결제 서비스를 한번에 신청해보세요"
        tabindex="0"
        data-type="b"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/pages/base/Calendar_C.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong class="banner-button">
            자동납부 한번에 신청
            <Icon name="Chevron_right" size="20" />
          </strong>
          <span>정기결제 서비스를 한번에 신청해보세요</span>
        </p>
      </a>
    </div> -->
    <!-- E : 3d,2d 아이콘 그래픽 타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 - image -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner rtl is-reverse"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="b-image"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img
            :src="`${$cdnURL}/images/dummy/img_promotion_sample.png`"
            alt=""
          />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span>더하면, 알아서 따라오는 할인쿠폰!</span>
        </p>
      </a>
    </div> -->
    <!-- E : 3d,2d 아이콘 그래픽 타입 - image -->

    <!-- S : c 타입  -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="c"
        data-color="bg-banner_indigo_solid-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/img_dummy_icon.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span>더하면, 알아서 따라오는 할인쿠폰!</span>
        </p>
      </a>
    </div> -->
    <!-- E : c 타입 -->

    <!-- S : c 타입  -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="매일 새로운 광고가 기다리고 있어요! 광고 보고 포인트 적립하기. 자세히 보기"
        tabindex="0"
        data-type="c"
        data-color="bg-banner_purple_solid"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/img_dummy_icon.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>매일 새로운 광고가 기다리고 있어요!</strong>
          <span class="more-button">
            광고 보고 포인트 적립하기
            <Icon name="Chevron_right" size="16" />
          </span>
        </p>
      </a>
    </div> -->
    <!-- E : c 타입 -->

    <!-- S : c 타입 - 버튼강조  -->
    <!-- <div class="promotion-banner__basic">
      <a
        role="link"
        class="sc-banner"
        aria-label="MySHOP 더하면, 알아서 따라오는 할인쿠폰!"
        tabindex="0"
        data-type="c-button"
        data-color="bg-banner_brand_tint-same"
      >
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/img_dummy_icon.png`" alt="" />
        </div>
        <p class="sc-banner__text" aria-hidden="true">
          <strong>MySHOP</strong>
          <span class="more-button">
            더하면, 알아서 따라오는 할인쿠폰!
            <Icon name="Chevron_right" size="16" />
          </span>
        </p>
      </a>
    </div> -->
    <!-- E : c 타입 - 버튼강조 -->

    <!-- S : 배너 + 버튼 조합  -->
    <div class="promotion-banner__basic">
      <div class="sc-banner rtl" data-type="c-image" data-color="bg-gray">
        <div class="sc-banner__image" aria-hidden="true">
          <img :src="`${$cdnURL}/images/dummy/AD.png`" alt="" />
        </div>
        <p class="sc-banner__text">
          <strong>매일 새로운 광고가<br />기다리고 있어요!</strong>
        </p>
        <BoxButton
          text="광고 보고 포인트 적립하기"
          color="secondary"
          size="large"
          class="footer-button bg-white"
        />
      </div>
    </div>
    <!-- E : 배너 + 버튼 조합 -->
  </section>
  <!-- E: 이벤트 프로모션 -->
</template>

<script setup>
import { computed, inject, nextTick, onMounted, ref, watchEffect } from "vue";
import { useTemplateRef } from "vue";
// [수정 260303] 네이티브 WebView 터치 스와이프 대응: useSwipe(touch) 추가
// 기존:
//   import { usePointerSwipe } from "@vueuse/core";
import { usePointerSwipe, useSwipe } from "@vueuse/core";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  BoxButton,
  CapsuleButton,
  Icon,
  IconButton,
  LoadingSkeleton,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// 프로모션 배너 스와이프 해제 기능
const promotionBannerInner = useTemplateRef("promotionBannerInner");
const promotionBannerContainer = useTemplateRef("promotionBannerContainer");
const promotionBannerHandle = useTemplateRef("promotionBannerHandle");
const handleButton = useTemplateRef("handleButton");
const promotionBannerButton = useTemplateRef("promotionBannerButton");
const bannerLink = useTemplateRef("bannerLink");

// 터치/드래그 민감도 설정
const SENSITIVITY = {
  /**
   * SWIPE_THRESHOLD: usePointerSwipe 시작 임계값 (px)
   * - 설명: 스와이프 이벤트가 시작되기 전에 무시할 최소 이동 거리
   * - 값이 낮을수록: 더 민감하게 반응 (0 = 모든 움직임 감지)
   * - 값이 높을수록: 작은 움직임은 무시하고 큰 움직임만 감지
   * - 사용 위치: usePointerSwipe의 threshold 옵션
   */
  SWIPE_THRESHOLD: 0,

  /**
   * DRAG_DETECTION: 드래그로 인식하는 최소 거리 (px)
   * - 설명: 클릭과 드래그를 구분하기 위한 최소 이동 거리
   * - 값이 낮을수록: 작은 움직임도 드래그로 인식 (민감함)
   * - 값이 높을수록: 어느 정도 움직여야 드래그로 인식 (덜 민감함)
   * - 0으로 설정 시: 터치 시작과 동시에 드래그로 인식하여 즉시 움직임 시작
   * - 사용 위치: onSwipe에서 hasDragged 플래그 설정 시
   */
  DRAG_DETECTION: 0,

  /**
   * CLICK_THRESHOLD: 클릭으로 간주하는 최대 거리 (px)
   * - 설명: 이 거리 미만으로 움직이면 클릭으로 간주
   * - 값이 낮을수록: 작은 움직임도 드래그로 인식
   * - 값이 높을수록: 어느 정도 움직여도 클릭으로 간주
   * - 사용 위치: onSwipeEnd에서 클릭/드래그 구분 시
   */
  CLICK_THRESHOLD: 10,

  /**
   * DISMISS_THRESHOLD: dismiss 임계값 (px)
   * - 설명: promotion-banner__inner를 좌측으로 이 거리만큼 드래그하면 자동으로 dismiss
   * - 값이 낮을수록: 적게 드래그해도 dismiss (민감함)
   * - 값이 높을수록: 많이 드래그해야 dismiss (덜 민감함)
   * - 사용 위치: promotion-banner__inner의 onSwipeEnd에서
   */
  DISMISS_THRESHOLD: 40,

  /**
   * DISMISS_PERCENTAGE: dismiss 임계값 (%)
   * - 설명: promotion-banner__handle를 초기 너비의 이 비율만큼 좌측으로 드래그하면 dismiss
   * - 값이 낮을수록: 적게 드래그해도 dismiss (민감함)
   * - 값이 높을수록: 많이 드래그해야 dismiss (덜 민감함)
   * - 예시: 30% = 초기 너비의 30%만큼 좌측으로 드래그하면 dismiss
   * - 사용 위치: promotion-banner__handle의 onSwipeEnd에서
   */
  DISMISS_PERCENTAGE: 30,

  /**
   * RESET_THRESHOLD: 원래 위치로 복귀하는 임계값 (px)
   * - 설명: 드래그 중 포인터가 벗어났을 때, 이 거리 미만으로 움직였다면 원래 위치로 복귀
   * - 값이 낮을수록: 적게 움직여도 원래 위치로 복귀 (덜 민감함)
   * - 값이 높을수록: 많이 움직여야 원래 위치로 복귀 (민감함)
   * - 사용 위치: resetToInitial 함수에서
   */
  RESET_THRESHOLD: 50,
};

const isDismissed = ref(false);
const innerWidth = ref(null); // promotion-banner__inner의 width 값
const opacity = ref(1);
const isExpanded = ref(false);

// sc-swipe-dismissed 클래스 변경 감지
watchEffect(() => {
  const container = promotionBannerContainer.value;
  if (container) {
    isExpanded.value = container.classList.contains("sc-swipe-dismissed");
  }
});

// handle 영역의 너비 계산
const handleWidth = computed(() => {
  return promotionBannerHandle.value?.offsetWidth ?? 56; // 기본값 56px (CSS에서 설정된 값)
});

// handle-button의 너비 계산 (25px)
const handleButtonWidth = 25;

// promotion-banner__inner의 초기 너비 계산
const initialInnerWidth = computed(() => {
  if (!promotionBannerInner.value) return null;
  return promotionBannerInner.value.offsetWidth;
});

// promotion-banner__handle의 opacity 계산
const handleOpacity = computed(() => {
  if (!initialInnerWidth.value || innerWidth.value === null) return 1;
  const currentWidth =
    parseFloat(String(innerWidth.value).replace("px", "")) ||
    initialInnerWidth.value;
  const initial = initialInnerWidth.value;
  const widthRatio = currentWidth / initial; // 0 ~ 1 사이의 값
  return Math.max(0, widthRatio);
});

// 공통 스와이프 상태
let hasDragged = false;
let startX = 0;

// [수정 260303] 터치·마우스 공통 처리: distance 인자로 받는 핸들러 추출
// 기존:
//   const { distanceX, isSwiping: innerIsSwiping } = usePointerSwipe(
//     promotionBannerInner,
//     {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { hasDragged = true; startX = e.clientX || 0; ... },
//       onSwipe(e) { const distance = distanceX.value; ... },
//       onSwipeEnd() { const isClick = !hasDragged || Math.abs(distanceX.value) < ...; ... },
//     }
//   );
const innerOnSwipeStart = () => {
  hasDragged = true;
  const initialWidth = initialInnerWidth.value;
  if (initialWidth) {
    const widthStr = `${initialWidth}px`;
    if (innerWidth.value === null) {
      innerWidth.value = widthStr;
    }
    const innerEl = promotionBannerInner.value;
    if (innerEl) {
      innerEl.style.transition = "none";
      innerEl.style.width = widthStr;
      innerEl.style.setProperty("--inner-width", widthStr);
    }
  }
};
const innerOnSwipe = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  if (innerWidth.value === null) innerWidth.value = `${initialWidth}px`;
  const newWidth =
    distance > 0
      ? `${Math.max(0, initialWidth - distance)}px`
      : `${initialWidth}px`;
  const innerEl = promotionBannerInner.value;
  if (innerEl) {
    innerEl.style.transition = "none";
    innerEl.style.width = newWidth;
    innerEl.style.setProperty("--inner-width", newWidth);
  }
  innerWidth.value = newWidth;
  opacity.value = 1;
};
const innerOnSwipeEnd = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  const isClick =
    !hasDragged || Math.abs(distance) < SENSITIVITY.CLICK_THRESHOLD;
  const applyDismiss = () => {
    innerWidth.value = "0px";
    opacity.value = 1;
    isDismissed.value = true;
    if (promotionBannerInner.value) {
      promotionBannerInner.value.style.visibility = "hidden";
      promotionBannerInner.value.style.display = "none";
    }
    setTimeout(() => {
      promotionBannerContainer.value?.classList.add("sc-swipe-dismissed");
      isExpanded.value = true;
      nextTick(() => {
        const buttonEl = promotionBannerButton.value?.$el;
        if (buttonEl?.focus) buttonEl.focus();
        else buttonEl?.querySelector?.("button, a, [tabindex]")?.focus();
      });
    }, 600);
  };
  if (isClick) {
    applyDismiss();
    return;
  }
  if (distance >= SENSITIVITY.DISMISS_THRESHOLD) {
    applyDismiss();
  } else {
    innerWidth.value = `${initialWidth}px`;
    opacity.value = 1;
  }
  hasDragged = false;
};

// [수정 260303] inner: 터치(useSwipe, passive:false) + 마우스(usePointerSwipe, pointerTypes:['mouse','pen']) 하이브리드
// 기존:
//   const { distanceX, isSwiping: innerIsSwiping } = usePointerSwipe(
//     promotionBannerInner,
//     {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { ... },
//       onSwipe(e) { const distance = distanceX.value; ... },
//       onSwipeEnd() { ... },
//     }
//   );
const {
  lengthX: innerTouchLengthX,
  isSwiping: innerTouchIsSwiping,
} = useSwipe(promotionBannerInner, {
  threshold: SENSITIVITY.SWIPE_THRESHOLD,
  passive: false,
  onSwipeStart: innerOnSwipeStart,
  onSwipe: () => innerOnSwipe(innerTouchLengthX.value),
  onSwipeEnd: (_, __) => innerOnSwipeEnd(innerTouchLengthX.value),
});
const { distanceX: innerPointerDistanceX, isSwiping: innerPointerIsSwiping } =
  usePointerSwipe(promotionBannerInner, {
    pointerTypes: ["mouse", "pen"],
    disableTextSelect: true,
    threshold: SENSITIVITY.SWIPE_THRESHOLD,
    onSwipeStart: () => {
      startX = 0;
      innerOnSwipeStart();
    },
    onSwipe: () => innerOnSwipe(innerPointerDistanceX.value),
    onSwipeEnd: () => innerOnSwipeEnd(innerPointerDistanceX.value),
  });

// [수정 260303] handle: inner와 동일한 터치·마우스 공통 핸들러 패턴 적용
// 기존:
//   const { distanceX: handleDistanceX, isSwiping: handleIsSwiping } =
//     usePointerSwipe(promotionBannerHandle, {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { ... },
//       onSwipe(e) { const distance = handleDistanceX.value; ... },
//       onSwipeEnd() { ... },
//     });
const handleOnSwipeStart = () => {
  hasDragged = true;
  const initialWidth = initialInnerWidth.value;
  if (initialWidth) {
    const widthStr = `${initialWidth}px`;
    if (innerWidth.value === null) innerWidth.value = widthStr;
    const innerEl = promotionBannerInner.value;
    if (innerEl) {
      innerEl.style.transition = "none";
      innerEl.style.width = widthStr;
      innerEl.style.setProperty("--inner-width", widthStr);
    }
  }
};
const handleOnSwipe = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  if (innerWidth.value === null) innerWidth.value = `${initialWidth}px`;
  const newWidth =
    distance > 0
      ? `${Math.max(0, initialWidth - distance)}px`
      : `${initialWidth}px`;
  const innerEl = promotionBannerInner.value;
  if (innerEl) {
    innerEl.style.transition = "none";
    innerEl.style.width = newWidth;
    innerEl.style.setProperty("--inner-width", newWidth);
  }
  innerWidth.value = newWidth;
  opacity.value = 1;
};
const handleOnSwipeEnd = (distance) => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (!initialWidth) return;
  const isClick =
    !hasDragged || Math.abs(distance) < SENSITIVITY.CLICK_THRESHOLD;
  const applyDismiss = () => {
    innerWidth.value = "0px";
    opacity.value = 1;
    isDismissed.value = true;
    if (promotionBannerInner.value) {
      promotionBannerInner.value.style.visibility = "hidden";
      promotionBannerInner.value.style.display = "none";
    }
    setTimeout(() => {
      promotionBannerContainer.value?.classList.add("sc-swipe-dismissed");
      isExpanded.value = true;
      nextTick(() => {
        const buttonEl = promotionBannerButton.value?.$el;
        if (buttonEl?.focus) buttonEl.focus();
        else buttonEl?.querySelector?.("button, a, [tabindex]")?.focus();
      });
    }, 600);
  };
  if (isClick) {
    applyDismiss();
    return;
  }
  if (distance >= SENSITIVITY.DISMISS_THRESHOLD) {
    applyDismiss();
  } else {
    innerWidth.value = `${initialWidth}px`;
    opacity.value = 1;
  }
  hasDragged = false;
};

// [수정 260303] handle: useSwipe + usePointerSwipe 하이브리드
// 기존:
//   const { distanceX: handleDistanceX, isSwiping: handleIsSwiping } =
//     usePointerSwipe(promotionBannerHandle, {
//       disableTextSelect: true,
//       threshold: SENSITIVITY.SWIPE_THRESHOLD,
//       onSwipeStart(e) { ... },
//       onSwipe(e) { ... },
//       onSwipeEnd() { ... },
//     });
const { lengthX: handleTouchLengthX, isSwiping: handleTouchIsSwiping } =
  useSwipe(promotionBannerHandle, {
    threshold: SENSITIVITY.SWIPE_THRESHOLD,
    passive: false,
    onSwipeStart: handleOnSwipeStart,
    onSwipe: () => handleOnSwipe(handleTouchLengthX.value),
    onSwipeEnd: (_, __) => handleOnSwipeEnd(handleTouchLengthX.value),
  });
const {
  distanceX: handlePointerDistanceX,
  isSwiping: handlePointerIsSwiping,
} = usePointerSwipe(promotionBannerHandle, {
  pointerTypes: ["mouse", "pen"],
  disableTextSelect: true,
  threshold: SENSITIVITY.SWIPE_THRESHOLD,
  onSwipeStart: () => {
    startX = 0;
    handleOnSwipeStart();
  },
  onSwipe: () => handleOnSwipe(handlePointerDistanceX.value),
  onSwipeEnd: () => handleOnSwipeEnd(handlePointerDistanceX.value),
});

// [수정 260303] isSwiping: inner/handle의 터치·마우스 4개 소스 통합
// 기존:
//   const isSwiping = computed(
//     () => innerIsSwiping.value || handleIsSwiping.value
//   );
const isSwiping = computed(
  () =>
    innerTouchIsSwiping.value ||
    innerPointerIsSwiping.value ||
    handleTouchIsSwiping.value ||
    handlePointerIsSwiping.value
);

// 드래그 중 포인터가 벗어났을 때 상태 리셋
const resetToInitial = () => {
  if (isDismissed.value) return;
  const initialWidth = initialInnerWidth.value;
  if (initialWidth && innerWidth.value !== null) {
    const currentWidth =
      parseFloat(String(innerWidth.value).replace("px", "")) || initialWidth;
    // 50px 임계값 미만이면 원래 위치로 복귀
    const dragThreshold = SENSITIVITY.RESET_THRESHOLD;
    const widthReduced = initialWidth - currentWidth;

    if (widthReduced < dragThreshold && widthReduced > 0) {
      // 원래 사이즈로 복귀
      innerWidth.value = `${initialWidth}px`;
      opacity.value = 1;
    }
  }
};

// isSwiping이 false가 되었을 때 상태 리셋
watchEffect(() => {
  if (!isSwiping.value && !isDismissed.value) {
    resetToInitial();
  }
});

// 포인터 이벤트로도 리셋 처리 (드래그 중 포인터가 벗어났을 때)
watchEffect(() => {
  const inner = promotionBannerInner.value;
  const handle = promotionBannerHandle.value;

  if (!inner && !handle) return;

  const handlePointerLeave = () => {
    if (isSwiping.value) {
      // 다음 틱에서 리셋 (onSwipeEnd가 호출될 수 있도록)
      nextTick(() => {
        if (!isSwiping.value && !isDismissed.value) {
          resetToInitial();
        }
      });
    }
  };

  if (inner) {
    inner.addEventListener("pointerleave", handlePointerLeave);
    inner.addEventListener("pointercancel", handlePointerLeave);
  }

  if (handle) {
    handle.addEventListener("pointerleave", handlePointerLeave);
    handle.addEventListener("pointercancel", handlePointerLeave);
  }

  return () => {
    if (inner) {
      inner.removeEventListener("pointerleave", handlePointerLeave);
      inner.removeEventListener("pointercancel", handlePointerLeave);
    }
    if (handle) {
      handle.removeEventListener("pointerleave", handlePointerLeave);
      handle.removeEventListener("pointercancel", handlePointerLeave);
    }
  };
});

// handle-button의 offset 계산 (항상 고정, 드래그 시에도 움직이지 않음)
const handleButtonOffset = computed(() => {
  // [수정 260303] 기존:
  //   if (innerIsSwiping.value || handleIsSwiping.value) return "0px";
  if (isSwiping.value) return "0px";

  // 드래그가 아닐 때도 항상 고정 (움직이지 않음)
  return "0px";
});

// handle-button 스타일 적용 (promotion-banner__inner와 함께 움직임)
watchEffect(() => {
  const button = handleButton.value;
  if (!button) return;

  // 드래그 중: 애니메이션 없음, 드래그 종료 후: ease-out 300ms
  button.style.transition = isSwiping.value
    ? "none"
    : "transform 300ms cubic-bezier(0.4, 0, 0.2, 1)"; // ease-out
});

// handle-button 포인터 다운 핸들러 (스와이프 시작 감지)
const handleButtonPointerDown = (e) => {
  // 스와이프 시작을 위해 hasDragged 초기화
  hasDragged = false;
  startX = e.clientX || 0;
};

// handle-button 클릭 핸들러 (클릭만 처리)
const handleButtonClick = (e) => {
  // 스와이프 중이면 클릭 무시 (드래그와 클릭 구분)
  if (isSwiping.value || hasDragged) {
    if (e) {
      e.preventDefault();
      e.stopPropagation();
    }
    return;
  }

  if (isDismissed.value) return;

  const width = handleWidth.value;
  if (!width) return;

  // 클릭 시 dismiss - 사이즈는 즉시 0으로 (딜레이 없음)
  innerWidth.value = "0px";
  opacity.value = 1; // opacity 효과 없음
  isDismissed.value = true;

  // promotion-banner__inner 즉시 숨김 처리
  if (promotionBannerInner.value) {
    promotionBannerInner.value.style.visibility = "hidden";
    promotionBannerInner.value.style.display = "none";
  }

  // 애니메이션 완료(300ms) 후 300ms 딜레이 후 sc-swipe-dismissed 클래스 추가
  setTimeout(() => {
    promotionBannerContainer.value?.classList.add("sc-swipe-dismissed");
    isExpanded.value = true; // 펼쳐진 상태로 설정
    // dismiss 후 promotion-banner__button에 포커스
    nextTick(() => {
      const buttonEl = promotionBannerButton.value?.$el;
      if (buttonEl && typeof buttonEl.focus === "function") {
        buttonEl.focus();
      } else if (buttonEl?.querySelector) {
        const focusableEl = buttonEl.querySelector("button, a, [tabindex]");
        focusableEl?.focus();
      }
    });
  }, 600); // 300ms (애니메이션) + 300ms (추가 딜레이)
};

const handleReset = () => {
  // 원래 사이즈로 복귀
  const initialWidth = initialInnerWidth.value;
  if (initialWidth) {
    const widthStr = `${initialWidth}px`;
    innerWidth.value = widthStr;

    // DOM에 직접 설정하여 원래 위치로 복귀
    const innerEl = promotionBannerInner.value;
    if (innerEl) {
      // transition을 복원하여 애니메이션 적용
      innerEl.style.transition = "";
      innerEl.style.width = widthStr;
      innerEl.style.setProperty("--inner-width", widthStr);
    }
  }
  opacity.value = 1;
  // [260115] isDismissed를 false로 설정하는 시점을 접힘 애니메이션 완료 후로 변경
  // isDismissed.value = false; // 접힘 애니메이션 완료 후로 이동
  isExpanded.value = false; // 펼쳐진 상태 해제

  // 접힘 애니메이션 적용
  // [260115] promotion-banner-collapse 클래스가 제대로 적용되도록 nextTick과 requestAnimationFrame 사용
  // [260115] 접힘 애니메이션 완료 후 promotion-banner__inner와 promotion-banner__handle를 다시 보이도록 수정
  const container = promotionBannerContainer.value;
  if (container) {
    container.classList.remove("sc-swipe-dismissed");

    // DOM 업데이트 후 접힘 애니메이션 클래스 추가
    // [260115] nextTick과 requestAnimationFrame을 사용하여 DOM 업데이트 완료 후 클래스 추가
    nextTick(() => {
      requestAnimationFrame(() => {
        container.classList.add("promotion-banner-collapse");

        // 애니메이션 완료 후 클래스 제거 및 promotion-banner__inner, promotion-banner__handle 다시 보이기
        // [260115] 접힘 애니메이션(200ms) 완료 후 promotion-banner__inner와 promotion-banner__handle를 다시 보이도록 수정
        setTimeout(() => {
          container.classList.remove("promotion-banner-collapse");

          // [260115] 접힘 애니메이션 완료 후 isDismissed를 false로 설정하여 promotion-banner__handle를 다시 보이도록 변경
          isDismissed.value = false;

          // promotion-banner__inner 다시 보이기
          // [260115] 접힘 애니메이션 완료 후에만 promotion-banner__inner를 다시 보이도록 변경
          if (promotionBannerInner.value) {
            promotionBannerInner.value.style.visibility = "visible";
            promotionBannerInner.value.style.display = "";
          }
        }, 200);
      });
    });
  }
  // close-button 클릭 시 banner-link에 포커스
  nextTick(() => {
    bannerLink.value?.focus?.();
  });
};

// 초기 handle-button 위치 설정 (우측에 위치)
const initializeHandleButtonPosition = () => {
  if (isDismissed.value) return;
  // offset이 이미 "0px"로 초기화되어 있으므로 추가 작업 불필요
};

// 컴포넌트 마운트 시 초기 위치 설정
onMounted(async () => {
  await nextTick();
  // DOM이 완전히 렌더링될 때까지 대기
  if (promotionBannerHandle.value) {
    initializeHandleButtonPosition();
  }
  // innerWidth 초기화
  if (promotionBannerInner.value && innerWidth.value === null) {
    const initialWidth = initialInnerWidth.value;
    if (initialWidth) {
      innerWidth.value = `${initialWidth}px`;
    }
  }
});
</script>





// SBT128A01


    <!-- 추가 UI -->
    <section class="section giftshop">
      <div class="giftshop__header">
        <h2 class="title-sub">기프트샵</h2>
        <TextButton text="전체보기" color="secondary" size="small" showGoTo />
      </div>
      <div class="giftshop__body">
        <ul class="giftshop__list">
          <li
            v-for="item in giftshopItems"
            :key="item.id"
          >
            <a
              role="link"
              :aria-label="`${item.brand} ${item.productName} 정상가: ${item.originalPrice}, 할인: ${item.discountRate}, 할인가: ${item.salePrice}`"
            >
              <figure class="giftshop__item" aria-hidden="true">
                <div class="giftshop__item-image">
                  <ScImage :src="item.image.src" :alt="item.image.alt" />
                </div>
                <figcaption class="giftshop__item-caption">
                  <strong>{{ item.brand }}</strong>
                  <p>{{ item.productName }}</p>
                  <p><del>{{ item.originalPrice }}</del></p>
                  <p>
                    <em>{{ item.discountRate }}</em>
                    <ins>{{ item.salePrice }}</ins>
                  </p>
                </figcaption>
              </figure>
            </a>
          </li>
        </ul>
      </div>
    </section>

    <section class="section delivery-coupon">
      <div class="delivery-coupon__header">
        <h2 class="title-sub">배달앱 땡겨요 쿠폰</h2>
        <TextButton text="전체보기" color="secondary" size="small" showGoTo />
      </div>
      <div class="delivery-coupon__body">
        <Carousel
          v-if="deliveryCouponSlides.length > 0"
          root-class="delivery-coupon__carousel"
          slides-per-view="1"
          :space-between="0"
          :loop="deliveryCouponSlides.length > 1"
          :pagination="deliveryCouponSlides.length > 1"
          :navigation="deliveryCouponSlides.length > 1"
          :autoplay="deliveryCouponSlides.length > 1"
          :show-autoplay-control="deliveryCouponSlides.length > 1"
          pagination-type="fraction"
          pagination-placement="outside-center"
          number-color="responsiveMode"
          number-size="large"
        >
          <CarouselItem
            v-for="(slide, i) in deliveryCouponSlides"
            :key="slide.id ?? i"
          >
            <a 
              role="link" 
              :href="slide.url || 'javascript:;'" 
              class="delivery-coupon__slide"
              :aria-label="`${slide.image.alt ?? ''}`"
            >
              <ScImage
                v-if="slide.image"
                :src="slide.image.src"
                :alt="slide.image.alt ?? ''"
              />
            </a>
          </CarouselItem>
        </Carousel>
      </div>
    </section>




// 추가 데이터
// 배달앱 땡겨요 쿠폰 캐러셀 슬라이드 (1개면 카운트/재생/정지 미노출)
const deliveryCouponSlides = [
  {
    id: 1,
    url: "javascript:;",
    image: {
      src: `${$cdnURL}/images/dummy/img_giftshop01.png`,
      alt: "도미노피자 배달 메뉴, 최대 11,000원 할인, 기간: 23년 8월1일 부터 23년 8월31일까지",
    },
  },
  {
    id: 2,
    url: "javascript:;",
    image: {
      src: `${$cdnURL}/images/dummy/img_giftshop01.png`,
      alt: "도미노피자 배달 메뉴, 최대 11,000원 할인, 기간: 23년 8월1일 부터 23년 8월31일까지",
    },
  },
];

// 기프트샵 리스트 데이터
const giftshopItems = [
  {
    id: 1,
    brand: "투썸플레이스",
    productName: "따먹는 스토리베리 포콜릿 생크림",
    originalPrice: "7,200원",
    discountRate: "7%",
    salePrice: "6,700원",
    image: {
      src: `${$cdnURL}/images/dummy/img_giftshop01.png`,
      alt: "기프트샵",
    },
  },
  {
    id: 2,
    brand: "투썸플레이스",
    productName: "따먹는 스토리베리 포콜릿 생크림",
    originalPrice: "7,200원",
    discountRate: "7%",
    salePrice: "6,700원",
    image: {
      src: `${$cdnURL}/images/dummy/img_giftshop01.png`,
      alt: "기프트샵",
    },
  },
];



import SBT001A01Service from "./section/SBT001A01-service.vue";


svg {
  path[fill="white"],
  ellipse[fill="white"] {
    fill: var(--bg-canvas_white);

    // card/bank icon 예외
    .card-display & {
      fill: #fff;
    }
    .error &,
    .fail &,
    .intitle &,
    .sc-feedback__notice &,
    .sc-feedback__fail &,
    .sc-feedback__info & {
      fill: #fff;
    }
  }
  &.fixed-color path[fill="white"] {
    fill: #fff;
  }

  path[stroke="white"] {
    .success &,
    .success2 & {
      stroke: var(--bg-canvas_white);
    }
  }
  path[fill="#101828"],
  ellipse[fill="#101828"] {
    fill: var(--text-primary);
  }
  rect[stroke="#101828"],
  path[stroke="#101828"] {
    stroke: var(--text-primary);
  }
  path[fill="#143898"] {
    fill: var(--text-brand);
  }
  path[fill="#344054"] {
    fill: var(--fg-steady);
  }
  path[fill="#0E2A95"] {
    fill: var(--brand-900);
    [data-theme="dark"] & {
      fill: var(--text-blue);
      .coupon-cards:disabled,
      .coupon-cards[disabled] {
        fill: var(--text-disabled-same);
      }
    }
    [data-theme="dark"] .coupon-cards:disabled &,
    [data-theme="dark"] .coupon-cards[disabled] & {
      fill: var(--text-disabled-same);
    }
    html:not([data-theme]) & {
      @media (prefers-color-scheme: dark) {
        & {
          fill: var(--text-blue);
          .coupon-cards:disabled,
          .coupon-cards[disabled] {
            fill: var(--text-disabled-same);
          }
        }
        .coupon-cards:disabled &,
        .coupon-cards[disabled] & {
          fill: var(--text-disabled-same);
        }
      }
    }
  }
  path[fill="#005DF9"] {
    fill: var(--text-brand);
  }
  path[fill-rule="evenodd"][fill="#005DF9"] {
    fill: var(--fg-brand-same);
    .coupon-cards:disabled &,
    .coupon-cards[disabled] & {
      fill: var(--gray-400);
    }
  }
  circle[fill="#101828"] {
    [data-theme="dark"] [iconname="icon-line-car"] & {
      fill: #fff;
    }
    html:not([data-theme]) & {
      @media (prefers-color-scheme: dark) {
        [iconname="icon-line-car"] & {
          fill: #fff;
        }
      }
    }
  }
  path[fill="#000"] {
    [data-theme="dark"] .call & {
      fill: #fff;
    }
    [data-theme="dark"] .convenience & {
      fill: #fff;
    }
    html:not([data-theme]) & {
      @media (prefers-color-scheme: dark) {
        .call & {
          fill: #fff;
        }
        .convenience & {
          fill: #fff;
        }
      }
    }
  }
  &.isError {
    path[fill="#D0D5DD"] {
      [data-theme="dark"] & {
        fill: var(--fg-disabled);
      }
      html:not([data-theme]) & {
        @media (prefers-color-scheme: dark) {
          fill: var(--fg-disabled);
        }
      }
    }
  }
}



.text-price {
      display: flex;
      align-items: center;
      justify-content: flex-start;
      gap: var(--spacing-sm);
      path[fill="#143898"] {
        fill: var(--brand-900);
        [data-theme="dark"] & {
          fill: var(--text-ondark_brand-same);
        }
        html:not([data-theme]) & {
          @media (prefers-color-scheme: dark) {
            fill: var(--text-ondark_brand-same);
          }
        }
      }
    }


&::before,
        &::after {
          content: "";
          position: absolute;
          top: calc(var(--spacing-md, 8px) * -2);
          z-index: 1;
          width: 8px;
          height: 24px;
          border-radius: 100px;
          background: #b1b7c4;
        }



//4868 line

    &.is-error-fallback {
      .coupon-book__card-img {
        width: 48px;
        height: 48px;
        border: 1px solid var(--border-secondary);
        border-radius: var(--radius-xl);
        background-color: var(--bg-gray);
      }
    }


// _utility
  &.isError {
    path[fill="#D0D5DD"] {
      [data-theme="dark"] & {
        fill: var(--fg-disabled);
      }
      @media (prefers-color-scheme: dark) {
        fill: var(--fg-disabled);
      }
    }
  }

<template>
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
          /* 수정 260204: 해당 행 쿠폰 아이콘 이미지 로드 실패 시에만 적용. ScImage @error → onIconError(coupon.id) → iconErrorIds에 추가됨. */
          { 'is-error-fallback': iconErrorIds.includes(coupon.id) },
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
            <!-- 수정 260204: img → ScImage.
              - 로드 실패 시: coupon.icon.fallback 있으면 해당 이미지, 없으면 ScImage 기본 ScIcon(empty_image) 노출.
              - @error 시 onIconError로 해당 행에 is-error-fallback 클래스 적용. -->
            <!-- <ScImage
              :src="coupon.icon.src"
              :alt="coupon.icon.alt"
              :fallback="coupon.icon.fallback"
              class="cupon-icon"
              aria-hidden="true"
              @error="onIconError(coupon.id)"
            /> -->
            <ScImage
              :src="coupon.icon.src"
              :alt="coupon.icon.alt"
              class="cupon-icon"
              aria-hidden="true"
              @error="onIconError(coupon.id)"
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

    <!-- S : 할인·쿠폰 IF 오류시 노출 -->
    <div class="bf-if__error">
      <div class="bf-if__error-inner">
        <div class="bf-if__error-icon">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/result_icon.png`"
            alt="IF 오류"
          />
        </div>
        <div class="bf-if__error-text">정보를 불러오지 못했어요</div>
        <CapsuleButton
          text="다른 할인·쿠폰 확인하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 할인·쿠폰 IF 오류시 노출 -->
  </section>
  <!-- E: 할인·쿠폰 -->
</template>

<script setup>
import { computed, inject, ref } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  CapsuleButton,
  ListItem,
  LoadingSkeleton,
  SolidLabel,
  TintLabel,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// ========== 수정 260204: 쿠폰 아이콘 이미지 로드 실패 시 해당 행에만 is-error-fallback 클래스 적용 ==========
/** 이미지 로드에 실패한 쿠폰 id 목록. ScImage @error 시 onIconError(coupon.id)로 id가 여기에 추가됨. */
const iconErrorIds = ref([]);
/** ScImage @error 핸들러. 실패한 쿠폰 id를 iconErrorIds에 넣어 해당 행의 :class에서 is-error-fallback이 붙도록 함. */
function onIconError(couponId) {
  if (!iconErrorIds.value.includes(couponId)) {
    iconErrorIds.value = [...iconErrorIds.value, couponId];
  }
}

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
  // 수정 260204: 이미지 호출 오류 시 UI 확인용. 존재하지 않는 URL → ScImage 로드 실패 → ScIcon(또는 fallback) 노출 및 is-error-fallback 클래스 적용 확인. 확인 후 제거.
  {
    id: 6,
    icon: {
      src: `${$cdnURL}/images/pages/base/__nonexistent_ui_check.png`,
      alt: "",
    },
    main: "이미지 오류 UI 확인용",
    sub: "로드 실패 시 ScIcon 노출",
  },
];

// 필터링된 쿠폰 리스트
const filteredCoupons = computed(() => {
  return couponItems;
});
</script>




// ScImage Component
<template>
  <img
    v-if="!isError"
    ref="imageRef"
    v-bind="$attrs"
    :data-src="src"
    :src="visibleSrc"
    :alt="alt"
    :class="[imageClasses, $attrs.class]"
    :width="width"
    :height="height"
    @load="onLoad"
    @error="onError"
  />
  <!-- 에러 케이스 대체 이미지 -->
  <template v-else>
    <!-- fallback 이미지 제공 -->
    <img
      v-if="fallback"
      v-bind="$attrs"
      :class="['sc-image', 'isFallbackError', $attrs.class]"
      :src="fallback"
      :width="width"
      :height="height"
      alt="이미지를 불러올 수 없습니다."
    />
    <!-- ScIcon은 fragment라 attrs 상속 불가 → span으로 감싸 attrs는 span에만 적용. display:contents로 레이아웃 영향 없음. -->
    <span class="sc-image__error-icon" style="display: contents" v-bind="$attrs">
      <ScIcon
        :class="['sc-image', 'isError', $attrs.class].filter(Boolean).join(' ')"
        iconName="empty_image"
        width="32px"
        height="32px"
      />
    </span>
  </template>
</template>

<script lang="ts">
/**
 * @param {string} src 이미지 실제 URL
 * @param {string} alt 대체 텍스트
 * @param {string | number} width 이미지 너비
 * @param {string | number} height 이미지 높이
 * @param {boolean} lazy lazy loading 적용여부
 * @param {string} fallback Error 대체 이미지
 */
export interface ScImageProps {
  src: string;
  alt?: string;
  width?: string | number;
  height?: string | number;
  lazy?: boolean;
  fallback?: string;
}

/**
 * @param {[event: Event]} load 이미지 loaded 이벤트
 * @param {[event: Event]} error 이미지 error 이벤트
 */
export type ScImageEmits = {
  load: [event: Event];
  error: [event: Event];
};
</script>

<script setup lang="ts">
import { useIntersectionObserver } from "@vueuse/core";
import { type Ref, computed, onMounted, ref, watch } from "vue";
import { ScIcon } from "~/components/shc/icon";
import { ScImageVariants } from "./ScImage.variants";

defineOptions({ inheritAttrs: false });

/** fallback 기본값 없음: 있으면 isFallbackError img 노출, 없으면(undefined) ScIcon(empty_image) 노출 */
const props = withDefaults(defineProps<ScImageProps>(), {
  lazy: true,
});
const emits = defineEmits<ScImageEmits>();

const visibleSrc = ref<string | undefined>(undefined);
const imageRef = ref<HTMLImageElement | null>(null);
const isError = ref(false);

//#region lazy loading
// lazy 옵션 false 일때는 바로 대입
onMounted(() => {
  if (!props.lazy) visibleSrc.value = props.src;
});

const { stop } = useIntersectionObserver(
  imageRef as Ref<HTMLElement | null>,
  ([entry]) => {
    if (entry?.isIntersecting) {
      visibleSrc.value = props.src ?? "";
      stop();
    }
  },
  // 이미지 10% 노출 시 동작
  // lazy 옵션 줄때만 동작
  { threshold: 0.1, immediate: props.lazy }
);
// #endregion

const imageClasses = computed(() =>
  ScImageVariants({
    isError: isError.value,
  })
);

//#region 이벤트 처리
/**
 * Load 이벤트
 * @param {Event} event Load event
 */
const onLoad = (event: Event) => emits("load", event);

/**
 * Error 이벤트
 * @param {Event} event Error Event
 */
const onError = (event: Event) => {
  isError.value = true;
  emits("error", event);
};

watch(
  () => props.src,
  (newValue) => {
    isError.value = false;
    visibleSrc.value = newValue;
  }
);
//#endregion
</script>
























:aria-label="`총 ${couponItems.length}개의 쿠폰을 보유중이에요.`"
:aria-label="`전체쿠폰 ${couponItems.length}개`"

<route lang="yaml">
meta:
  id: SBT021A01
  title: 받은 쿠폰
  menu: "혜택​ > 받은 쿠폰"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: | 
    [추가] 260130: 스켈레톤 추가,
    [접근성 개선]260123: BasicChipGroup control="expand" 옵션추가
    251210: 이미지 ScImage 로 수정
  header:
    variant: sub
    fixed: true
    showBack: true
    home: true
  qa2: 퍼블완료
  ui: | 
    [완료]260120: 마크업 (TBD 아이콘 수정 및 UI 확인용 페이지 추가, SBT021A01-a, SBT021A01-b),
    [완료]260119: 마크업 (상단 네비게이션 우측 close 제거 홈 아이콘 추가 메타정보 수정),
</route>
<template>
  <!-- [수정] UI 확인용: 스켈레톤·본문 둘 다 노출되도록 sc-contents__body 한 겹으로 감쌈. 스켈레톤/본문을 형제가 아닌 동일 body 자식으로 두어 빌드 시 본문이 가려지지 않음 -->
  <div class="sc-contents__body">
    <!-- [추가] 260130: 스켈레톤 추가 -->
    <!-- S : 로딩중 스켈레톤 -->
    <div
      class="card-grid__skeleton coupon-received-loading"
      aria-label="로딩중"
      tabindex="0"
    >
      <!-- card-grid__skeleton 직계 자식 (들여쓰기 1단계) -->
      <div class="cupon-head">
        <LoadingSkeleton :width="304" :height="33" rounded="small" />
      </div>
      <div class="cupon-chip">
        <LoadingSkeleton :width="88" :height="36" rounded="full" />
        <LoadingSkeleton :width="88" :height="36" rounded="full" />
        <LoadingSkeleton :width="88" :height="36" rounded="full" />
      </div>
      <div class="cupon-list__wrap">
        <div class="cupon-list__head">
          <LoadingSkeleton :width="92" :height="24" rounded="small" />
        </div>
        <div class="cupon-list__body">
          <ul class="webzine-list">
            <li 
              v-for="skeletonIndex in 4" :key="`skeleton-${skeletonIndex}`"
              class="webzine-item"
            >
              <div class="webzine-item__thumbnail">
                <LoadingSkeleton
                  :width="48"
                  :height="48"
                />
              </div>
              <div class="webzine-item__content">
                <LoadingSkeleton
                  :width="87"
                  :height="22"
                  rounded="small"
                />
                <LoadingSkeleton
                  :width="200"
                  :height="22"
                  rounded="small"
                />
                <LoadingSkeleton
                  :width="130"
                  :height="22"
                  rounded="small"
                />
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!-- E : 로딩중 스켈레톤 -->

    <!-- 본문: sc-contents__body 직계 자식, 스켈레톤과 형제 -->
    <div class="cupon-contents">
      <!-- S : 모바일상품권 + 할인쿠폰이 있을 경우 -->
      <template v-if="couponItems.length > 0">
        <div
          class="cupon-head"
          tabindex="0"
          aria-label="총 {{ couponItems.length }}개의 쿠폰을 보유중이에요."
        >
          <p aria-hidden="true">
            총 <em class="cupon-count">{{ couponItems.length }}</em
            >개의 쿠폰을 보유중이에요.
          </p>
        </div>
        <div class="cupon-chip">
          <!-- [v0.9 접근성 개선] 260123: control="expand" 옵션추가 -->
          <BasicChipGroup
            :control="chipControl"
            :items="items"
            variant="solid"
            control="expand"
            v-model="selectedValue"
          />
        </div>
      </template>
      <!-- E : 모바일상품권 + 할인쿠폰이 있을 경우 -->

      <!-- S : 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->
      <template v-else>
        <div class="cupon-top__btngroup">
          <BoxButtonGroup variant="50:50">
            <BoxButton size="large" color="tertiary" text="스탬프쿠폰">
              <template #icon>
                <!-- 아이콘 TBD 추 후 변경 -->
                <!-- 260120: 이미지 변경 -->
                <!-- <Icon name="sample-icon" width="34px" height="34px" /> -->
              <img :src="`${$cdnURL}/images/pages/base/img_shinhan.png`" alt="" aria-hidden="true" />
              </template>
            </BoxButton>
            <BoxButton size="large" color="tertiary" text="기프트샵">
              <template #icon>
                <!-- 아이콘 TBD 추 후 변경 -->
                <!-- 260120: 이미지 변경 -->
                <!-- <Icon name="sample-icon" width="34px" height="34px" /> -->
                <img :src="`${$cdnURL}/images/pages/base/img_giftshop.png`" alt="" aria-hidden="true" />
              </template>
            </BoxButton>
          </BoxButtonGroup>

          <Divider
            variant="basic"
            color="tertiary"
            size="full"
            orientation="horizontal"
          />
        </div>
      </template>
      <!-- E : 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->

      <!-- S : 모바일상품권 + 할인쿠폰이 있을 경우 -->
      <template v-if="couponItems.length > 0">
        <div class="cupon-list__wrap">
          <div class="cupon-list__head">
            <strong
              class="cupon-head__text"
              aria-label="전체쿠폰 {{ couponItems.length }}개"
              tabindex="0"
            >
              <span aria-hidden="true"
                >전체쿠폰 <em class="cupon-count">{{ couponItems.length }}</em
                >개</span
              >
            </strong>
            <Tooltip
              :open="false"
              placement="top-left"
              :showClose="true"
              :size="20"
              class="select-type__tooltip"
            >
              <template #content>
                <div class="sc-tooltip__content">
                  <strong class="sc-tooltip-content__title"
                    >쿠폰 개수가 다르다면?</strong
                  >
                  <p>
                    쿠폰별로 받기 또는 사용 반영까지 최대 하루정도 소요될 수
                    있어요
                  </p>
                </div>
              </template>
            </Tooltip>
          </div>
          <div class="cupon-list__body">
            <div
              v-for="coupon in couponItems"
              :key="coupon.id"
              class="cupon-item"
              tabindex="0"
            >
              <ListItem align="centered">
                <template #leftIcon>
                  <ScImage
                    :src="coupon.icon.src"
                    :alt="coupon.icon.alt"
                    class="cupon-icon"
                    aria-hidden="true"
                  />
                </template>
                <template #leftMainText>
                  <span>{{ coupon.mainsub }}</span>
                  <strong>{{ coupon.main }}</strong>
                </template>
                <template #leftSubText>
                  {{ coupon.sub }}
                </template>
              </ListItem>
            </div>
          </div>
        </div>
      </template>
      <!-- E : 모바일상품권 + 할인쿠폰이 있을 경우 -->

      <template v-else>
        <!-- S : 모바일상품권 5장 + 할인쿠폰 0장 인 경우 & 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->
        <div class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- 260120: 이미지 변경 -->
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <ScIcon
                iconName="icon-nodata"
                width="56px"
                height="56px"
              />
            </div>
            <div class="empty__main">
              <p>받은 쿠폰이 없습니다.</p>
            </div>
            <div class="empty__btn">
              <BoxButton
                color="quaternary"
                size="medium"
                text="쿠폰 받으러 가기"
              />
            </div>
          </div>
        </div>
        <!-- E : 모바일상품권 5장 + 할인쿠폰 0장 인 경우 & 모바일상품권 0 + 할인쿠폰 0 인 경우(기존 유지, 변경예정) -->

        <!-- S : 모바일상품권 0 + 할인쿠폰 3장 인 경우 -->
        <div class="sc-empty-case">
          <div class="empty-type">
            <div class="empty__img fg-informative" aria-hidden="true">
              <!-- 260120: 이미지 변경 -->
              <!-- <ScIcon
                iconName="icon-error-coalition"
                width="68px"
                height="68px"
              /> -->
              <ScIcon
                iconName="icon-nodata"
                width="56px"
                height="56px"
              />
            </div>
            <div class="empty__main">
              <p>보유한 모바일상품권이 없습니다.</p>
            </div>
            <div class="empty__btn">
              <BoxButton
                color="quaternary"
                size="medium"
                text="기프트샵 가기"
              />
            </div>
          </div>
        </div>
        <!-- E : 모바일상품권 0 + 할인쿠폰 3장 인 경우 -->
      </template>
    </div>
  </div>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { inject } from "vue";
import { ref, computed } from "vue";
import {
  BasicChipGroup,
  Tooltip,
  ListItem,
  BoxButton,
  BoxButtonGroup,
  Divider,
  LoadingSkeleton
} from "@shc-nss/ui/solid";
import { ScIcon, ScImage } from "@shc-nss/ui/shc";

const { $cdnURL } = inject(AppContextKey);
// 첫 번째 칩을 선택된 상태로 초기화
const selectedValue = ref("1");
const items = [
  {
    text: "전체",
    value: "1",
  },
  {
    text: "모바일 상품권",
    value: "2",
  },
  {
    text: "할인쿠폰",
    value: "3",
  },
];

// 칩 개수에 따라 control 설정 (기본: none, 많으면: expand)
const chipControl = computed(() => {
  return items.length >= 4 ? "expand" : "none";
});

// 쿠폰 리스트 데이터 (이미지 참조)
const couponItems = [
  {
    id: 1,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    mainsub: "2025.01.01까지",
    main: "마이카플러스 신규 가입 이벤트",
    sub: "배달의 민족 5,000원건",
  },
  {
    id: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    mainsub: "2025.01.01까지",
    main: "스타벅스",
    sub: "[이벤트] 아이스 카페 아메리카노",
  },
  {
    id: 3,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    mainsub: "2025.01.01까지",
    main: "서브웨이",
    sub: "[이벤트] 아이스 카페 아메리카노",
  },
  {
    id: 4,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "스탬프 쿠폰을 찾고 계세요?",
    sub: "신한 Super SOL",
  },
  {
    id: 5,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    mainsub: "관리비 자동납부하고",
    main: "최대 20만원 캐시백 받기",
  },
  {
    id: 6,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    mainsub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "Tops 쿠폰",
  },
  {
    id: 7,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    mainsub: "결제계좌 변경하고",
    main: "신세계 백화점 상품권 포함 5가지 혜택 받기",
  },
  {
    id: 8,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    mainsub: "결제계좌 변경하고",
    main: "스타벅스 쿠폰 받기",
  },
  {
    id: 9,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon7.png`,
      alt: "",
    },
    mainsub: "캐시백부터 할인까지 여기 다 있ZIP",
    main: "해외여행 필수템",
  },
  {
    id: 10,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    mainsub: "SOL페이에 티머니 등록하고",
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
];

</script>





// 3165 라인

      &.is-error-fallback .sv-list__icon {
        background-color: var(--bg-gray);
        img {
          width: 32px;
          height: 32px;
        }
      }


// discount
<template>
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
          /* 수정 260204: 해당 행의 쿠폰 아이콘 이미지 로드 실패(통신 오류) 시에만 적용.
             ScImage @error 발생 시 onIconError(coupon.id)로 id가 iconErrorIds에 추가됨. */
          { 'is-error-fallback': iconErrorIds.includes(coupon.id) },
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
            <!-- 수정 260204: img → ScImage. 통신 오류 시 fallback 이미지 노출, 다크모드 시 fallback 별도 이미지. -->
            <ScImage
              :src="coupon.icon.src"
              :alt="coupon.icon.alt"
              class="cupon-icon"
              aria-hidden="true"
              :fallback="fallbackImageUrl"
              @error="onIconError(coupon.id)"
            />
          </template>
        </ListItem>
      </div>

      <!-- 통신 오류 UI 확인용: 존재하지 않는 이미지 URL로 의도적 404 → ScImage @error 발생 → fallback 노출 및 is-error-fallback 클래스 적용. 확인 후 블록 삭제 가능. -->
      <div
        v-for="coupon in filteredCoupons"
        :key="coupon.id"
        :class="[
          'cupon-item outline',
          { 'is-label': coupon.label || coupon.expiryDate },
          { 'is-error-fallback': iconErrorIds.includes(coupon.id) },
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
            <!-- UI확인용: __nonexistent_ui_check.png(404) 사용 → 로드 실패 시 fallback·is-error-fallback 동작 확인. -->
            <ScImage
              :src="`${$cdnURL}/images/pages/base/__nonexistent_ui_check.png`"
              :alt="coupon.icon.alt"
              class="cupon-icon"
              aria-hidden="true"
              :fallback="fallbackImageUrl"
              @error="onIconError(coupon.id)"
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

    <!-- S : 할인·쿠폰 IF 오류시 노출 -->
    <div class="bf-if__error">
      <div class="bf-if__error-inner">
        <div class="bf-if__error-icon">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/result_icon.png`"
            alt="IF 오류"
          />
        </div>
        <div class="bf-if__error-text">정보를 불러오지 못했어요</div>
        <CapsuleButton
          text="다른 할인·쿠폰 확인하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 할인·쿠폰 IF 오류시 노출 -->
  </section>
  <!-- E: 할인·쿠폰 -->
</template>

<script setup>
import { computed, inject, onMounted, onUnmounted, ref } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  CapsuleButton,
  ListItem,
  LoadingSkeleton,
  SolidLabel,
  TintLabel,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// ========== 수정 260204: 테마 기반 fallback 이미지 (라이트/다크 분리) ==========
// DOM의 data-theme을 기준으로 하여, 앱 스토어·콘솔·외부 코드 등 어떤 경로로 테마가 바뀌어도 반영되도록 함.
// (이전에는 Pinia 테마 스토어만 참조해, 콘솔에서 setAttribute('data-theme')로 변경 시 반영되지 않던 문제 해결)

/** <html>의 data-theme 속성값 ('light' | 'dark' | null). null이면 시스템 설정(prefers-color-scheme) 따름. */
const dataTheme = ref(null);
/** 테마가 'system'일 때 사용. prefers-color-scheme: dark 미디어 쿼리 결과. */
const systemDark = ref(false);
let observer = null;
let mediaQuery = null;

/** document.documentElement.getAttribute('data-theme')을 읽어 dataTheme에 반영. SSR 대응으로 document 존재 시에만 실행. */
function readDataTheme() {
  if (typeof document === "undefined") return;
  dataTheme.value = document.documentElement.getAttribute("data-theme");
}

onMounted(() => {
  readDataTheme();
  // data-theme 속성 변경 감지 (스토어 토글, 콘솔 setAttribute, 브릿지 등 모든 경로 반영)
  observer = new MutationObserver((mutations) => {
    for (const m of mutations) {
      if (m.attributeName === "data-theme") {
        readDataTheme();
        break;
      }
    }
  });
  observer.observe(document.documentElement, { attributes: true });

  // 시스템 테마(system 모드)용: prefers-color-scheme 변경 시 systemDark 갱신
  mediaQuery = window.matchMedia("(prefers-color-scheme: dark)");
  systemDark.value = mediaQuery.matches;
  const onSystemThemeChange = () => {
    systemDark.value = mediaQuery.matches;
  };
  mediaQuery.addEventListener("change", onSystemThemeChange);
  onUnmounted(() => mediaQuery.removeEventListener("change", onSystemThemeChange));
});

onUnmounted(() => {
  observer?.disconnect();
});

/** 실제 화면에 적용 중인 다크모드 여부. data-theme이 'dark'이거나, (system 모드일 때) systemDark가 true이면 다크. */
const isResolvedDark = computed(
  () =>
    dataTheme.value === "dark" ||
    (dataTheme.value !== "light" && systemDark.value)
);
/** ScImage 로드 실패 시 노출할 대체 이미지 URL. 다크모드일 때 empty_image_dark.svg, 라이트일 때 empty_image.svg 사용. */
const fallbackImageUrl = computed(() =>
  isResolvedDark.value
    ? `${$cdnURL}/images/pages/base/empty_image_dark.svg`
    : `${$cdnURL}/images/pages/base/empty_image.svg`
);

// ========== 수정 260204: 통신 오류 시 해당 행에만 is-error-fallback 클래스 적용 ==========
/** 이미지 로드에 실패한 쿠폰 id 목록. ScImage @error 시 onIconError(coupon.id)로 추가됨. */
const iconErrorIds = ref([]);
/** ScImage의 @error 핸들러. 실패한 쿠폰 id를 iconErrorIds에 넣어 해당 행에만 is-error-fallback 클래스가 붙도록 함. */
function onIconError(couponId) {
  if (!iconErrorIds.value.includes(couponId)) {
    iconErrorIds.value = [...iconErrorIds.value, couponId];
  }
}

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
</script>






      // 조건 충족시
      &.is-satisfied {
        border: 1px solid var(--border-secondary);
        background-color: var(--bg-canvas_white);
      }



// sbt160a01
<route lang="yaml">
meta:
  id: SBT160A01
  title: 혜택
  menu: "혜택 > 혜택 > 이달의 참여현황 (BS)"
  layout: MainLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  appClassList: "app_benefits"
  mainClassList: "benefits_main"
</route>
<template>
  <!--
    이달의 참여현황

    [X] 버튼 Tap > 바텀시트 닫힘

    해당 월 일자 별 참여 현황 노출
    - 지난 일자 중 미참여한 경우 미참여 표시 적용
    - 지나지 않은 일자는 참여 여부 미표시 적용
    - 참여 일에 정답, 오답 여부 표시 적용
    - 등급 달성한 날짜에 획득한 등급 메달 노출

    1-1. 퀴즈 정답 시
      - 해당일 표기
      - 문구: 정답

    1-2. 퀴즈 오답 시
      - 해당일 표기
      - 문구: 오답

    1-3. 퀴즈 미참여 시
      - 해당일 표기
      - 문구: 미참여
      - 미참여 조건: 당일 23시59분까지 미참여인 경우, 익일 00시00분에 현황판 미참여 표기
        ex) 22일 23시59분까지 미참여일때 23일 00시00분에 22일 날짜 현황판에 미참여 표기

    1-4. 퀴즈 등급 조건 충족 시
      - 해당일 표기
      - 월 10회 충족 시 동메달 아이콘 노출
      - 월 20회 충족 시 은메달 아이콘 노출
      - 월 30회 충족 시 금메달 아이콘 노출

    1-5. 미도래일
      - 해당일 표기
      - 미도래일 시 비활성화 및 문구 노출 안함

    1-6. 당월 총 적립 포인트 노출
      - 퀴즈팡팡 관련 모든 포인트 합산한 값을 노출
      - (정답 포인트, 오답 포인트, 힌트보기 포인트, 등급별 포인트)

    1-7. 당월 총 정답 일수 노출
  -->
  <BottomSheet
    v-model="isOpen"
    closableDimm
    dimmed
    :title="`${currentMonth}월 참여현황`"
    class="participation-status__sheet"
  >
    <div class="month-schedule__container">
      <div
        v-for="item in scheduleData"
        :key="item.day"
        class="month-schedule__item"
        :class="{
          'is-not-participated': item.status === 'not-participated',
          'is-incorrect': item.status === 'incorrect',
          'is-correct': item.status === 'correct',
          'is-satisfied': item.medal,
          'is-empty': item.status === null && !item.medal,
        }"
        tabindex="0"
        :aria-label="getAriaLabel(item)"
      >
        <!-- 
          v0.9 2600202: 퀴즈 등급 조건 충족 시 추가
          퀴즈 등급 조건 충족 시 이미지만 노출 
          월 10회 참여 시
          월 20회 참여 시
          월 30회 참여 시
        -->
        <div v-if="item.medal" class="month-schedule__medal" aria-hidden="true">
          <img :src="`${$cdnURL}${item.medal.src}`" alt="" />
        </div>
        <template v-else>
          <div class="month-schedule__number" aria-hidden="true">
            {{ item.day }}
          </div>
          <div
            v-if="item.status"
            class="month-schedule__label"
            :class="`is-${item.status}`"
            aria-hidden="true"
          >
            {{ item.label }}
          </div>
        </template>
      </div>
    </div>
    <div class="month-schedule__total">
      <div
        class="month-schedule__total-item"
        tabindex="0"
        aria-label="당월 총 적립 포인트: 239 포인트"
      >
        <strong class="month-schedule__total-label" aria-hidden="true">
          적립 포인트
        </strong>
        <em class="month-schedule__total-value" aria-hidden="true"> 239P </em>
      </div>
      <Divider
        variant="basic"
        color="tertiary"
        size="full"
        orientation="vertical"
      />
      <div
        class="month-schedule__total-item"
        tabindex="0"
        aria-label="당월 총 정답 일수: 24일"
      >
        <strong class="month-schedule__total-label" aria-hidden="true">
          정답 일수
        </strong>
        <em class="month-schedule__total-value" aria-hidden="true"> 24일 </em>
      </div>
    </div>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { BottomSheet, Divider } from "@shc-nss/ui/solid";
import { AppContextKey } from "@/configs/inject/appContext";
import { defineModel, ref, computed, inject } from "vue";

// ==========================================
// 바텀시트 제어
// ==========================================
// 이미지 경로는 CDN URL을 사용
const { $cdnURL } = inject(AppContextKey);
const isOpen = defineModel({ default: true });

// ==========================================
// Props / 데이터
// ==========================================
// 년도와 달
const currentYear = ref(2025);
const currentMonth = ref(12);

// 실제 참여 데이터
// 상태: 'not-participated' | 'incorrect' | 'correct'
const participationData = ref({
  1: { status: "not-participated", label: "미참여" },
  2: { status: "incorrect", label: "오답" },
  3: { status: "correct", label: "정답" },
  4: { status: "correct", label: "정답" },
  5: { status: "correct", label: "정답" },
  6: { status: "not-participated", label: "미참여" },
  7: { status: "incorrect", label: "오답" },
  8: { status: "correct", label: "정답" },
  9: { status: "not-participated", label: "미참여" },
  // 월 10/20/30회 달성일에는 메달 이미지 노출
  10: {
    status: null,
    label: null,
    medal: {
      src: "/images/pages/benefits/main/Property_level1_status.svg",
      alt: "월 10회 참여 달성",
    },
  },
  11: { status: "correct", label: "정답" },
  12: { status: "correct", label: "정답" },
  13: { status: "not-participated", label: "미참여" },
  14: { status: "not-participated", label: "미참여" },
  15: { status: "not-participated", label: "미참여" },
  16: { status: "not-participated", label: "미참여" },
  17: { status: "correct", label: "정답" },
  18: { status: "correct", label: "정답" },
  19: { status: "correct", label: "정답" },
  20: {
    status: null,
    label: null,
    medal: {
      src: "/images/pages/benefits/main/Property_level2_status.svg",
      alt: "월 20회 참여 달성",
    },
  },
  21: { status: "not-participated", label: "미참여" },
  22: { status: "not-participated", label: "미참여" },
  23: { status: "not-participated", label: "미참여" },
  30: {
    status: null,
    label: null,
    medal: {
      src: "/images/pages/benefits/main/Property_level3_status.svg",
      alt: "월 30회 참여 달성",
    },
  },
});

// ==========================================
// Computed
// ==========================================
// 해당 달의 마지막 날짜 계산
const daysInMonth = computed(() => {
  // 예: currentMonth가 11이면 new Date(2025, 12, 0) = 2026년 1월의 0일 = 2025년 12월의 마지막 날
  // new Date(year, month, 0)는 month월의 이전 달 마지막 날을 반환
  // 따라서 new Date(2025, 11, 0) = 2025년 11월의 마지막 날 = 30일
  return new Date(currentYear.value, currentMonth.value, 0).getDate();
});

// 현재 날짜
const today = computed(() => {
  const now = new Date();
  return {
    year: now.getFullYear(),
    month: now.getMonth() + 1,
    day: now.getDate(),
  };
});

// 해당 날짜가 미래인지 확인
const isFutureDate = (day) => {
  if (currentYear.value > today.value.year) return true;
  if (currentYear.value < today.value.year) return false;
  if (currentMonth.value > today.value.month) return true;
  if (currentMonth.value < today.value.month) return false;
  return day > today.value.day;
};

// 스케줄 데이터 생성
const scheduleData = computed(() => {
  const days = [];

  for (let day = 1; day <= daysInMonth.value; day++) {
    // 미래 날짜는 참여현황 없음
    if (isFutureDate(day)) {
      days.push({ day, status: null, label: null });
    } else {
      // 참여 데이터가 있으면 사용, 없으면 null
      const data = participationData.value[day];
      if (data) {
        days.push({
          day,
          status: data.status,
          label: data.label,
          medal: data.medal,
        });
      } else {
        days.push({ day, status: null, label: null });
      }
    }
  }

  return days;
});

// 메달 여부에 따라 접근성 라벨을 분기
const getAriaLabel = (item) => {
  if (item.medal) {
    return `${currentYear.value}년 ${currentMonth.value}월 ${item.day}일 ${item.medal.alt}`;
  }
  return `${currentYear.value}년 ${currentMonth.value}월 ${item.day}일 참여현황: ${
    item.label || "없음"
  }`;
};
</script>






<li v-for="skeletonIndex in 3" :key="`skeleton-${skeletonIndex}`">
  <LoadingSkeleton width="100%" height="100%" />
</li>

<!-- S : 로딩중 스켈레톤 -->
<div
  class="card-grid__skeleton coupon-book"
  aria-label="로딩중"
  tabindex="0"
>
  <div class="coupon-book__title">
    <LoadingSkeleton :width="150" :height="33" rounded="small" />
  </div>
  <section
    v-for="skeletonSectionIndex in 3"
    :key="`skeleton-section-${skeletonSectionIndex}`"
  >
    <div class="coupon-book__title-sub">
      <LoadingSkeleton :width="195" :height="29" rounded="small" />
    </div>
    <article>
      <ul class="coupon-book__carousel">
        <li
          v-for="cardIndex in 3"
          :key="`skeleton-card-${skeletonSectionIndex}-${cardIndex}`"
          class="coupon-book__card"
        >
          <LoadingSkeleton width="100%" height="100%" />
        </li>
      </ul>
    </article>
  </section>
</div>
<!-- E : 로딩중 스켈레톤 -->




// 힌트 보기 BottomSheet
.picture {
  img {
    max-width: 100%;
    height: auto;
    object-fit: contain;
  }
} 
.hintview-text {
  @include font-set(body-m, 300);
  font-weight: 300;
  color: var(--text-tertiary);
}

<template>
  <BottomSheet
    disableMinHeight
    v-model="isOpen"
    closableDimm
    dimmed
    title="힌트 보기"
    class="bs-hintview__sheet"
  >
    <picture class="picture">
      <img :src="`${$cdnURL}/images/dummy/img_promotion_sample.png`" alt="" />
    </picture>
    <div class="hintview-text">
      터치결제로 결제하면 타임라인에서 랜덤 포인트를 지급하는 페이팡팡 서비스를 이용해보세요.<br />
      결제할 때마다 3P~3,000P까지 랜덤 지급돼요.
    </div>
    <template #footer>
      <BoxButton
        text="확인"
        size="xlarge"
        @click="isOpen = false"
      />
    </template>
  </BottomSheet>
</template>

<script setup>
import { BottomSheet, BoxButton } from "@shc-nss/ui/solid";
import { defineModel } from "vue";

const isOpen = defineModel({ default: true });
</script>

// sbt101a02
<template>
  <FullPopup
    v-model="isOpen"
    :title="bodyTitle"
    :closeable="true"
    @close="handleClose"
  >
    <ScTitle mainTitle="서비스 이용을 위한 약관에<br />동의해주세요." />
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body sc-agree__page">
      <section class="section">
        <div
          class="sc-agree__list compound"
          role="region"
        >
          <div class="agree-list__group">
            <div
              class="agree-item item-basic"
              :class="{ 'is-checked': basicAgree4 }"
            >
              <Checkbox
                v-model="basicAgree4"
                class="agree-item__checkbox item-checkbox__basic"
                variant="box"
                align="left"
              >
                <template #label>
                  <span class="agree-item__label item-label__basic">{{ basicItem4.label }}</span>
                </template>
              </Checkbox>
            </div>

            <!-- ======================================== -->
            <!-- 1뎁스 영역: 기본 약관 항목들 -->
            <!-- ======================================== -->
            <div
              class="agree-sublist"
              role="group"
            >
              <div
                v-for="item in subItems4"
                :key="item.value"
                class="agree-subitem"
              >
                <div
                  class="agree-item agree-item__sub"
                  :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="box"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                    @click.stop
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{ item.label }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    iconName="Chevron_right"
                    size="small"
                    :aria-label="`${item.label} 상세 보기`"
                    class="agree-subitem__trigger"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <Divider
        variant="group"
        color="tertiary"
      />
      <div class="sc-bottom-info__inner">
        <h2 class="sc-bottom-info__title">이용 꿀팁</h2>
        <ListCard variant="solid" as="div" color="gray">
          <ListItem 
            :left="{ 
              mainText: '앱 알림', 
              subText: '적립예정포인트 정보를 실시간으로 받아보세요.',
              direction: 'column'
            }"
          >
            <template #rightControl>
              <ToggleSwitch 
                v-model="appNotificationEnabled"
                @update:modelValue="handleToggleChange('appNotification', $event)"
              />
            </template>
          </ListItem>
        </ListCard>
      </div>
    </div>

    <BottomActionContainer :scrollDim="true">
      <BoxButtonGroup
        size="xlarge"
        variant="100"
      >
        <BoxButton
          text="확인"
          :disabled="!basicAgree4"
        />
      </BoxButtonGroup>
    </BottomActionContainer>
  </FullPopup>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  Divider,
  FullPopup,
  IconButton,
  ListCard,
  ListItem,
  ToggleSwitch,
} from "@shc-nss/ui/solid";
import { computed, ref, watch } from "vue";
import { useRoute } from "vue-router";
import { ScTitle } from "@shc-nss/ui/shc";

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");
const isOpen = defineModel({ default: true });

const handleClose = () => {
  isOpen.value = false;
};

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  { label: "[필수] 개인정보 수집·이용 동의", value: "s4-1" },
  { label: "[필수] 개인정보 제3자 제공동의", value: "s4-2" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);

// 앱 알림 토글 상태
const appNotificationEnabled = ref(true);

/**
 * 동작 로직
 */
function handleToggleChange(type, value) {
  console.log(`${type} toggle changed:`, value);
  // 여기에 토글 변경 시 처리할 로직 추가
}
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산
  basicAgree4.value = set.size === subItems4.length;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    subAgrees4.value = subItems4.map((item) => item.value);
  } else {
    subAgrees4.value = [];
  }
});
</script>


<template>
  <div class="payment-panel payment-panel__daily" aria-label="매일결제">
    <section class="section-head">
      <!-- S : 전일자 카드사용내역 1건 or 다수 인 경우 -->
      <div
        v-if="testValue"
        class="text-daily__title"
        aria-label="지금까지 99,999 포인트 받았어요!"
        tabindex="0"
      >
        <p class="text-daily01" aria-hidden="true">
          <ScImageIcon
            iconName="benefits_welcome_text_daily01"
            width="auto"
            height="18"
            :colorize="false"
            class="svgtext-daily01"
          />
        </p>
        <p class="text-daily02" aria-hidden="true">
          <strong class="text-daily02__point"><em>99,999</em>P</strong>
          <ScImageIcon
            iconName="benefits_welcome_text_daily02"
            width="auto"
            height="28"
            :colorize="false"
            class="svgtext-daily02"
          />
        </p>
      </div>
      <!-- E : 전일자 카드사용내역 1건 or 다수 인 경우 -->

      <!-- S : 포인트 0인 경우(미참여 사용자) -->
      <div
        v-else
        class="text-daily__title"
        aria-label="매일매일 100~1,000 포인트 당첨!"
        tabindex="0"
      >
        <p class="text-daily01" aria-hidden="true">
          <ScImageIcon
            iconName="benefits_welcome_text_daily01-1"
            width="auto"
            height="18"
            :colorize="false"
            class="svgtext-daily01-1"
          />
        </p>
        <p class="text-daily02" aria-hidden="true">
          <strong class="text-daily02__point"><em>100~1,000</em>P</strong>
          <ScImageIcon
            iconName="benefits_welcome_text_daily02-1"
            width="auto"
            height="28"
            :colorize="false"
            class="svgtext-daily02-1"
          />
        </p>
      </div>
      <!-- E : 포인트 0인 경우(미참여 사용자) -->

      <TextButtonUnderline color="secondary" size="medium" text="받은 혜택 확인하기" />
      <div class="img-group" aria-hidden="true">
        <img :src="`${$cdnURL}/images/pages/benefits/welcome/img_daily_main_140x140.png`" alt="" />
      </div>

      <div class="custom-cards__gray-group center">
        <Card
          as="div"
          variant="solid"
          type="basic"
          color="gray"
          class="custom-cards__gray"
          :divider="false"
        >
          <div class="custom-cards__gray-info">
            <p><em>NN</em>일 동안 매일!</p>
            <p>어제 결제했다면, 오늘 포인트가 도착해요</p>
            <p><small>(100~1,000 포인트 랜덤 지급)</small></p>
          </div>
        </Card>
      </div>
    </section>
    <section class="bg-gray">
      <article class="article">
        <div class="custom-cards__group">
          <Card
            v-for="card in dailyCardList"
            :key="card.id"
            as="div"
            color="whiteShadow"
            variant="solid"
            type="basic"
            class="custom-cards"
            :divider="false"
          >
            <div
              class="custom-cards__header"
              tabindex="0"
              :aria-label="`${card.badgeText}. ${card.svgLabel}`"
            >
              <div class="custom-cards__header-title" aria-hidden="true">
                <NumberBadge type="text" :text="card.badgeText" color="gray" inline />
                <ScImageIcon
                  :iconName="card.iconName"
                  width="auto"
                  height="auto"
                  :colorize="false"
                  class="svgtext-custom-cards-title"
                  :aria-label="card.svgLabel"
                />
              </div>
            </div>
            <Divider variant="basic" orientation="horizontal" color="tertiary" aria-hidden="true" />
            <div class="custom-cards__content">
              <div
                v-if="card.isParticipant ?? testValue"
                class="custom-cards__content-item"
                tabindex="0"
                :aria-label="card.participant?.price
                  ? `${card.participant.title}. ${card.participant.price}`
                  : (card.participant?.title ?? '')"
              >
                <span class="custom-cards__title" aria-hidden="true">{{ card.participant?.title }}</span>
                <span
                  v-if="card.participant?.price"
                  class="custom-cards__price"
                  aria-hidden="true"
                >
                  {{ card.participant.price }}
                </span>
              </div>
              <div
                v-else
                class="custom-cards__content-item"
                tabindex="0"
                :aria-label="card.nonParticipantMessage ?? nonParticipantMessage"
              >
                <span class="custom-cards__title" aria-hidden="true">
                  {{ card.nonParticipantMessage ?? nonParticipantMessage }}
                </span>
              </div>
            </div>
            <template #actions>
              <BoxButtonGroup size="large" variant="100">
                <!-- 매일결제 혜택 케이스
                [포인트 받기 전 (조건 충족)]
                버튼명 : 포인트 받기, color : secondary
                [포인트 받 후]
                버튼명 : 받기 완료, disabled : true
                [포인트 만료 시]
                버튼명 : 기간 만료, disabled : true
                [전일자 카드사용내역 5천원 미만]
                버튼명 : 포인트 받기, disabled : true
                -->
                <BoxButton
                  :text="card.button?.text ?? '포인트 받기'"
                  :color="card.button?.color ?? 'secondary'"
                  :disabled="card.button?.disabled ?? !testValue"
                />
              </BoxButtonGroup>

            </template>
          </Card>
        </div>
      </article>
      <div class="custom-divider section-daily bg-gray" aria-hidden="true">
        <ScImageIcon
          iconName="icon-plus-fill"
          width="auto"
          height="auto"
          :colorize="false"
          class="svgicon-plus-fill"
          aria-hidden="true"
        />
      </div>
      <article class="article">
        <div class="custom-cards__group">
          <div class="custom-cards__group-head">
            <div class="group-head__label">
              <NumberBadge type="text" text="기간연장 혜택" color="gray" inline />
            </div>
            <div class="group-head__text" aria-label="통신비 정기결제하면 매일결제 한 달 더!" tabindex="0">
              <!-- S : 전일자 카드사용내역 1건 or 다수 인 경우 -->
              <ScImageIcon
                v-if="testValue"
                iconName="benefits_welcome_text_daily03"
                width="auto"
                height="auto"
                :colorize="false"
                class="svgtext-daily03"
                aria-label="통신비 정기결제하면 매일결제 한 달 더!"
                aria-hidden="true"
              />
              <!-- E : 전일자 카드사용내역 1건 or 다수 인 경우 -->
  
              <!-- S : 포인트 0인 경우(미참여 사용자) -->
              <ScImageIcon
                v-else
                iconName="benefits_welcome_text_daily03-1"
                width="auto"
                height="auto"
                :colorize="false"
                class="svgtext-daily03"
                aria-label="통신비 정기결제 혜택 적용 완료!"
                aria-hidden="true"
              />
              <!-- E : 포인트 0인 경우(미참여 사용자) -->
            </div>
          </div>
          <Card
            as="div"
            color="whiteShadow"
            variant="solid"
            type="basic"
            class="custom-cards"
            :divider="false"
          >
            <div class="custom-cards__content">
              <div class="custom-cards__content-item">
                <img :src="`${$cdnURL}/images/pages/benefits/welcome/img_daily_telecom_140x104.png`" alt="" />
  
                <!-- 포인트 0인경우 (미참여 사용자) -->
                <SolidLabel
                  v-if="!testValue"
                  color="blue"
                  title="혜택 미적용"
                />
                <!-- E : 포인트 0인경우 (미참여 사용자) -->
              </div>
            </div>
            <template #actions>
              <BoxButtonGroup size="large" variant="100">
                <!-- 통신요금 연결 전 -->
                <BoxButton
                  v-if="testValue"
                  text="정기결제 신청하기"
                  color="secondary"
                />
                <!-- E : 통신요금 연결 전 -->
  
                <!-- 통신요금 연결 완료 -->
                <BoxButton
                  v-else
                  text="정기결제 보러가기"
                  color="tertiary"
                />
                <!-- E : 통신요금 연결 완료 -->
              </BoxButtonGroup>
            </template>
          </Card>
        </div>
      </article>  
    </section>
    <section class="section payment-notice">
      <h2 class="title-sub">꼭! 알아두세요</h2>
      <article v-for="section in noticeSections" :key="section.title">
        <h3 class="title-sub__small">{{ section.title }}</h3>
        <UnorderedList :gap="8">
          <template v-for="(item, index) in section.items" :key="index">
            <!-- 일반 아이템 -->
            <UnorderedListItem 
              v-if="typeof item === 'string'"
              variant="bullet"
            >
              <span v-html="item"></span>
            </UnorderedListItem>
            
            <!-- 중첩된 아이템 (이용 예시) -->
            <UnorderedListItem 
              v-else-if="item.type === 'nested'"
              variant="bullet"
            >
              <span>{{ item.title }}</span>
              <UnorderedList :gap="8">
                <UnorderedListItem 
                  v-for="(subItem, subIndex) in item.items" 
                  :key="subIndex"
                  variant="dash"
                >
                  <span>{{ subItem }}</span>
                </UnorderedListItem>
              </UnorderedList>
            </UnorderedListItem>
          </template>
        </UnorderedList>
      </article>
    </section>
  </div>
</template>

<script setup>
import { ScImageIcon } from "@shc-nss/ui/shc";
import {
  BoxButton,
  BoxButtonGroup,
  Card,
  Divider,
  NumberBadge,
  SolidLabel,
  TextButtonUnderline,
  UnorderedList,
  UnorderedListItem
} from "@shc-nss/ui/solid";
import { ref } from "vue";
import { COMMON_NOTICE_SECTION } from "./notice-common";
import { AppContextKey } from "@/configs/inject/appContext";
import { inject } from "vue";
const { $cdnURL } = inject(AppContextKey);

// props로 탭 활성화 상태 받기 (사용하지 않지만 일관성을 위해 정의)
defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

// 임시 UI 확인용 전일자 카드사용내역 1건 or 다수 인 경우 true, 포인트 0인 경우 false
const testValue = ref(true);

const nonParticipantMessage = "오늘 신용카드 쓰고 내일 포인트 받아요!";

// [v0.9] 260127: 참여 이력  포인트 지급 이력 케이스 추가 및 수정
const dailyCardList = [
  // 1. 한번에 5천원 이상 결제
  // 포인트 받기 전(조건 충족)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점을지로파인애비뉴점을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: false
    }
  },
  // 포인트 받은 후
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점을지로파인애비뉴점을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "오늘 N,NNN포인트를 받았어요!",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 없음 (포인트 0/조건 미충족)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    isParticipant: false,
    nonParticipantMessage,
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 결제 금액 5천원 미만
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점",
      price: "1,000원"
    },
    button: {
      text: "5천원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 없음
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    isParticipant: false,
    nonParticipantMessage: "어제 신용카드를 사용하지 않았어요!",
    button: {
      text: "5천원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 있음(만료/혜택 연장 안내)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "통신비 정기결제하면 한달 더 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 2. 합쳐서 5만원 이상 결제
  // 포인트 받기 전(조건 충족)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: false
    }
  },
  // 포인트 받은 후
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "오늘 N,NNN포인트를 받았어요!",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 없음 (포인트 0/조건 미충족)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    isParticipant: false,
    nonParticipantMessage,
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 누적 금액 5만원 미만
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "40,000원"
    },
    button: {
      text: "5만원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 없음
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    isParticipant: false,
    nonParticipantMessage: "어제 신용카드를 사용하지 않았어요!",
    button: {
      text: "5만원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 있음(만료/혜택 연장 안내)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "통신비 정기결제하면 한달 더 받아요",
      color: "secondary",
      disabled: true
    }
  }
];

// 꼭! 알아두세요 데이터
const noticeSections = [
  {
    title: "매일결제",
    items: [
      "접속일 기준 전날 국내 신한 개인신용카드 승인 이력이 있으면 포인트(마이신한포인트) 지급 대상이 됩니다.",
      "포인트를 지급받기 위해선 '이용권유 방법에 대한 동의'의 전화 혹은 문자 메시지(LMS) 중 1개 이상의 항목과 '혜택정보 수신(이용권유) 동의'의 '카드 및 금융 상품·서비스 안내 및 이용 권유를 위한 수집, 이용' 항목에 대해 모두 동의해야 합니다.",
      "매일결제 혜택은 반갑꾸러미 접속 종료일로부터 30일 전까지 제공되며, 신한SOL페이 앱 기준 통신 3사 요금 정기결제에 등록되어 있거나, 직전 30일 내 통신 3사 정기결제 승인 이력이 있는 경우 혜택 제공 기간이 30일 연장됩니다.",
      "소비기록은 마이데이터 가입 및 자산 연결을 통해 확인할 수 있으며, 마이데이터 가입 및 자산 연결에 대해 제공되는 혜택의 규모와 지급 기준은 연결페이지의 상세 내용을 확인하시기 바랍니다.",
      "반갑꾸러미 접속 대상이더라도 이미 마이데이터 이벤트에 대해 혜택 수혜 이력이 있는 경우에는 해당 혜택은 제공되지 않습니다.",
      "통신사 정기결제에 따라 제공되는 매일결제 혜택 기간 연장 혜택은 최대 1개월간 제공되며, 신청 시점과 무관하게 카드 발급일로부터 2개월 뒤 말일에 혜택 제공이 종료됩니다.",
      "통신사 정기결제에 따라 제공되는 매일결제 혜택기간 연장은 통신사 고객센터를 통해 직접 신청할 경우, 즉시 반영되지않으며 신한 SOL페이 앱을 통한 정기결제가 발생해야 받으실 수 있습니다.",
      {
        type: "nested",
        title: "이용 예시",
        items: [
          "예시 1: 통신사 정기결제 등록 시 혜택 기간 연장",
          "예시 2: 신한 SOL페이 앱을 통한 정기결제 발생 시 혜택 지급",
          "예시 3: 마이데이터 가입 및 자산 연결을 통한 혜택 확인"
        ]
      },
      "계약 체결 전, 상품설명서 및 약관을 확인하시기 바랍니다.",
      "금융소비자는 금융소비자보호법 제19조 제 1항에 따라 해당 금융상품 또는 서비스에 대하여 설명받을 권리가 있습니다.",
      "신용카드 발급이 부적정한 경우(개인신용평점 낮음, 연체(단기 포함) 사유 발생 등), 카드 발급이 제한될 수 있습니다.",
      "카드 이용대금과 이에 수반되는 모든 수수료는 고객님께서 지정하신 결제일에 상환하여야 합니다.",
      "<strong>상환능력 대비 신용카드 사용액 과도 시, 개인신용평점이 하락할 수 있습니다.</strong>",
      "<strong>개인신용평점 하락 시, 금융거래 관련 불이익이 발생할 수 있습니다.</strong>",
      "<strong>일정기간 신용카드 이용대금을 연체할 경우, 결제일이 도래하지 않은 모든 신용카드 이용대금을 변제할 의무가 발생할 수 있습니다.</strong>",
      "준법감시 심의필 제00000000-Cpi-000호<br />(2000.00.00~2000.00.00)"
    ]
  },
  COMMON_NOTICE_SECTION
];
</script>








<BoxButton
    size="xlarge"
    ariaLabel="공유하기"
  >
    <template #label>
      <Popover
        placement="bottom-center"
        content="친구에게 자랑해보세요!"
        :open="true"
        color="gray"
      >
        <span>공유하기</span>
      </Popover>
    </template>
  </BoxButton>
</template>

// 보물찾기
.floating-treasure {
  position: fixed;
  bottom: calc(160px + var(--env-b));
  right: 36px;
  z-index: var(--z-index);
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
    animation: treasureBounce .8s ease-in-out infinite;
    /* @keyframes duration | timing-function | delay | iteration-count | direction | fill-mode | play-state | name */
  }
}
// 보물찾기 위치 확인 로딩
.treasure-modal {
  position: fixed;
  top: calc(0px + var(--env-t));
  left: calc(0px + var(--env-l));
  right: calc(0px + var(--env-r));
  bottom: calc(0px + var(--env-b));
  width: 100%;
  height: 100%;
  // background-color: rgba(0, 0, 0, 0.7);
  background-color: var(--bg-canvas_dark_a60);
  z-index: 600;
  pointer-events: auto;
  &.sv-popup--variant-full {
    background-color: var(--bg-canvas_dark_a60);
    .sv-popup__body {
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0;
    }
  }
  &.sv-popup .sv-popup__title {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    color: transparent;
  }
  .sv-popup__close .sv-icon {
    color: var(--white);
  }
  .treasure-modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100%;
    max-width: 312px;
    margin: 0 auto;
  }
  .treasure-loading-pending {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100%;
    text-align: center;
  }
  .loading-enter {
    margin-top: var(--spacing-md);
  }
  .loading-enter-text {
    margin-bottom: 30px;
    span {
      display: block;
      @include font-set(headline-s, 700);
      font-weight: 700;
      color: var(--white);
      text-align: center;
    }
  }
  .treasure-loading-enter {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    max-width: 312px;
    height: auto;
    margin: 0 auto;
    padding: var(--spacing-4xl) 0;
    text-align: center;
  }
  .treasure-loading-body {
    position: relative;
    width: 100%;
    margin-top: calc((30px + 36px + 56px) * -1);
  }
  .treasure-loading-lottie {
    height: 172px;
    .lottie-animation-container {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      overflow: visible;
      margin: 0 auto;
    }
  }
  .treasure-loading-body-text {
    width: 100%;
    padding-top: calc(30px + 36px);
    color: var(--white);
    @include font-set(headline-s, 700);
    font-weight: 700;
    text-align: center;
  }
  .treasure-loading-point {
    display: inline-block;
    @include font-set(headline-l, 800);
    font-weight: 800;
    color: var(--border-yellow);
    animation: treasurePoint .4s ease-in-out .7s backwards;
  }
}


// treasure(보물찾기) animation
@keyframes treasurePoint {
  0% {
    opacity: 0;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes treasureBounce{
  0% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(-5px); }
  100% { transform: translateX(-50%) translateY(0); }
}




```
{% endraw %}
---
