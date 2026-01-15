
{% raw %}
```js

<template>
  <!-- S: 이벤트 프로모션 -->
  <section class="bf-promotion" aria-label="이벤트 프로모션">
    <!-- S : 이벤트 프로모션 로딩중 스켈레톤 -->
    <div class="promotion-banner" aria-label="로딩중" tabindex="0">
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
        <div
          ref="bannerLink"
          tabindex="0"
          class="banner-link"
          aria-label="제주 리조트 패키지 프로모션 신한카드 고객 대상 특별혜택"
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
      <IconButton
        v-if="isExpanded"
        :color="false"
        :disabled="false"
        size="small"
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
    <!-- S : 기본형 배너 a타입 -->
    <div class="promotion-banner__basic">
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
    </div>
    <!-- E : 기본형 배너 a타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 -->
    <div class="promotion-banner__basic">
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
    </div>
    <!-- E : 3d,2d 아이콘 그래픽 타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 -->
    <div class="promotion-banner__basic">
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
    </div>
    <!-- E : 3d,2d 아이콘 그래픽 타입 -->

    <!-- S : 3d,2d 아이콘 그래픽 타입 - image -->
    <div class="promotion-banner__basic">
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
    </div>
    <!-- E : 3d,2d 아이콘 그래픽 타입 - image -->

    <!-- S : c 타입  -->
    <div class="promotion-banner__basic">
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
    </div>
    <!-- E : c 타입 -->

    <!-- S : c 타입  -->
    <div class="promotion-banner__basic">
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
    </div>
    <!-- E : c 타입 -->

    <!-- S : c 타입 - 버튼강조  -->
    <div class="promotion-banner__basic">
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
          <span class="more-button"
            >더하면, 알아서 따라오는 할인쿠폰!
            <Icon name="Chevron_right" size="16" />
          </span>
        </p>
      </a>
    </div>
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
import { usePointerSwipe } from "@vueuse/core";
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

// promotion-banner__inner에 스와이프 이벤트 적용
const { distanceX, isSwiping: innerIsSwiping } = usePointerSwipe(
  promotionBannerInner,
  {
    disableTextSelect: true,
    threshold: SENSITIVITY.SWIPE_THRESHOLD,
    onSwipeStart(e) {
      hasDragged = true; // DRAG_DETECTION이 0이므로 즉시 드래그로 인식
      startX = e.clientX || 0;

      // innerWidth 미리 초기화하여 onSwipe에서 즉시 반응
      const initialWidth = initialInnerWidth.value;
      if (initialWidth) {
        const widthStr = `${initialWidth}px`;
        if (innerWidth.value === null) {
          innerWidth.value = widthStr;
        }

        // transition을 즉시 제거하여 딜레이 없이 움직임
        const innerEl = promotionBannerInner.value;
        if (innerEl) {
          innerEl.style.transition = "none";
          innerEl.style.width = widthStr;
          innerEl.style.setProperty("--inner-width", widthStr);
        }
      }
    },
    onSwipe(e) {
      // 이미 dismiss된 경우 처리하지 않음
      if (isDismissed.value) return;

      const initialWidth = initialInnerWidth.value;
      if (!initialWidth) return;

      // onSwipeStart에서 이미 초기화했지만, 안전을 위해 다시 확인
      if (innerWidth.value === null) {
        innerWidth.value = `${initialWidth}px`;
      }

      // 좌측으로 드래그할 때만 동작 (opacity 효과 없음)
      // 드래그 거리에 따라 width 조절 (최대 전체까지 줄어들 수 있음)
      const distance = distanceX.value;
      const newWidth =
        distance > 0
          ? `${Math.max(0, initialWidth - distance)}px`
          : `${initialWidth}px`;

      // 직접 DOM 조작으로 즉시 반영 (딜레이 없이 곧바로 움직임)
      const innerEl = promotionBannerInner.value;
      if (innerEl) {
        // transition을 명시적으로 제거하여 즉시 반영
        innerEl.style.transition = "none";
        // width를 직접 설정하여 즉시 반영
        innerEl.style.width = newWidth;
        innerEl.style.setProperty("--inner-width", newWidth);
      }

      // Vue 반응성 업데이트 (렌더링 최적화를 위해 나중에 처리)
      innerWidth.value = newWidth;
      opacity.value = 1;
    },
    onSwipeEnd() {
      // 이미 dismiss된 경우 처리하지 않음
      if (isDismissed.value) return;

      const initialWidth = initialInnerWidth.value;
      if (!initialWidth) return;

      // 클릭으로 간주: 드래그가 없었거나 distanceX가 설정된 임계값 미만
      const isClick =
        !hasDragged || Math.abs(distanceX.value) < SENSITIVITY.CLICK_THRESHOLD;

      if (isClick) {
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
              const focusableEl = buttonEl.querySelector(
                "button, a, [tabindex]"
              );
              focusableEl?.focus();
            }
          });
        }, 600); // 300ms (애니메이션) + 300ms (추가 딜레이)
        return;
      }

      // promotion-banner__inner 사이즈의 40px만큼 줄어들었을 때 dismiss
      const dragThreshold = SENSITIVITY.DISMISS_THRESHOLD;

      if (distanceX.value >= dragThreshold) {
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
              const focusableEl = buttonEl.querySelector(
                "button, a, [tabindex]"
              );
              focusableEl?.focus();
            }
          });
        }, 600); // 300ms (애니메이션) + 300ms (추가 딜레이)
      } else {
        // 원래 사이즈로 복귀
        const initialWidth = initialInnerWidth.value;
        if (initialWidth) {
          innerWidth.value = `${initialWidth}px`;
        }
        opacity.value = 1;
      }

      // 스와이프 종료 시 hasDragged 리셋
      hasDragged = false;
    },
  }
);

// promotion-banner__handle에도 스와이프 이벤트 적용 (inner와 동일한 로직)
const { distanceX: handleDistanceX, isSwiping: handleIsSwiping } =
  usePointerSwipe(promotionBannerHandle, {
    disableTextSelect: true,
    threshold: SENSITIVITY.SWIPE_THRESHOLD,
    onSwipeStart(e) {
      hasDragged = true; // DRAG_DETECTION이 0이므로 즉시 드래그로 인식
      startX = e.clientX || 0;

      // innerWidth 미리 초기화하여 onSwipe에서 즉시 반응
      const initialWidth = initialInnerWidth.value;
      if (initialWidth) {
        const widthStr = `${initialWidth}px`;
        if (innerWidth.value === null) {
          innerWidth.value = widthStr;
        }

        // transition을 즉시 제거하여 딜레이 없이 움직임
        const innerEl = promotionBannerInner.value;
        if (innerEl) {
          innerEl.style.transition = "none";
          innerEl.style.width = widthStr;
          innerEl.style.setProperty("--inner-width", widthStr);
        }
      }
    },
    onSwipe(e) {
      // 이미 dismiss된 경우 처리하지 않음
      if (isDismissed.value) return;

      const initialWidth = initialInnerWidth.value;
      if (!initialWidth) return;

      // onSwipeStart에서 이미 초기화했지만, 안전을 위해 다시 확인
      if (innerWidth.value === null) {
        innerWidth.value = `${initialWidth}px`;
      }

      // 좌측으로 드래그할 때만 동작 (opacity 효과 없음)
      // 드래그 거리에 따라 width 조절 (최대 전체까지 줄어들 수 있음)
      const distance = handleDistanceX.value;
      const newWidth =
        distance > 0
          ? `${Math.max(0, initialWidth - distance)}px`
          : `${initialWidth}px`;

      // 직접 DOM 조작으로 즉시 반영 (딜레이 없이 곧바로 움직임)
      const innerEl = promotionBannerInner.value;
      if (innerEl) {
        // transition을 명시적으로 제거하여 즉시 반영
        innerEl.style.transition = "none";
        // width를 직접 설정하여 즉시 반영
        innerEl.style.width = newWidth;
        innerEl.style.setProperty("--inner-width", newWidth);
      }

      // Vue 반응성 업데이트 (렌더링 최적화를 위해 나중에 처리)
      innerWidth.value = newWidth;
      opacity.value = 1;
    },
    onSwipeEnd() {
      // 이미 dismiss된 경우 처리하지 않음
      if (isDismissed.value) return;

      const initialWidth = initialInnerWidth.value;
      if (!initialWidth) return;

      // 클릭으로 간주: 드래그가 없었거나 distanceX가 설정된 임계값 미만
      const isClick =
        !hasDragged ||
        Math.abs(handleDistanceX.value) < SENSITIVITY.CLICK_THRESHOLD;

      if (isClick) {
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
              const focusableEl = buttonEl.querySelector(
                "button, a, [tabindex]"
              );
              focusableEl?.focus();
            }
          });
        }, 600); // 300ms (애니메이션) + 300ms (추가 딜레이)
        return;
      }

      // promotion-banner__inner 사이즈의 40px만큼 줄어들었을 때 dismiss
      const dragThreshold = SENSITIVITY.DISMISS_THRESHOLD;

      if (handleDistanceX.value >= dragThreshold) {
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
              const focusableEl = buttonEl.querySelector(
                "button, a, [tabindex]"
              );
              focusableEl?.focus();
            }
          });
        }, 600); // 300ms (애니메이션) + 300ms (추가 딜레이)
      } else {
        // 원래 사이즈로 복귀
        const initialWidth = initialInnerWidth.value;
        if (initialWidth) {
          innerWidth.value = `${initialWidth}px`;
        }
        opacity.value = 1;
      }

      // 스와이프 종료 시 hasDragged 리셋
      hasDragged = false;
    },
  });

// isSwiping은 두 스와이프 중 하나라도 스와이핑 중이면 true
const isSwiping = computed(() => innerIsSwiping.value || handleIsSwiping.value);

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
  // 드래그 중이면 움직이지 않음 (promotion-banner__inner나 promotion-banner__handle 모두)
  if (innerIsSwiping.value || handleIsSwiping.value) return "0px";

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
  isDismissed.value = false;
  isExpanded.value = false; // 펼쳐진 상태 해제

  // 접힘 애니메이션 적용
  // [260115] promotion-banner-collapse 클래스가 제대로 적용되도록 nextTick과 requestAnimationFrame 사용
  // [260115] 접힘 애니메이션 완료 후 promotion-banner__inner를 다시 보이도록 수정
  const container = promotionBannerContainer.value;
  if (container) {
    container.classList.remove("sc-swipe-dismissed");

    // DOM 업데이트 후 접힘 애니메이션 클래스 추가
    // [260115] nextTick과 requestAnimationFrame을 사용하여 DOM 업데이트 완료 후 클래스 추가
    nextTick(() => {
      requestAnimationFrame(() => {
        container.classList.add("promotion-banner-collapse");

        // 애니메이션 완료 후 클래스 제거 및 promotion-banner__inner 다시 보이기
        // [260115] 접힘 애니메이션(200ms) 완료 후 promotion-banner__inner를 다시 보이도록 수정
        setTimeout(() => {
          container.classList.remove("promotion-banner-collapse");

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





```
{% endraw %}
---
