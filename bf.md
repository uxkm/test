
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
      <div
        class="sc-banner rtl"
        data-type="c-image"
        data-color="bg-gray"
      >
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
  const container = promotionBannerContainer.value;
  if (container) {
    container.classList.remove("sc-swipe-dismissed");
    container.classList.add("promotion-banner-collapse");

    // 애니메이션 완료 후 클래스 제거
    setTimeout(() => {
      container.classList.remove("promotion-banner-collapse");
    }, 200);
  }

  // promotion-banner__inner 다시 보이기
  if (promotionBannerInner.value) {
    promotionBannerInner.value.style.visibility = "visible";
    promotionBannerInner.value.style.display = "";
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






<route lang="yaml">
meta:
  id: SBT159A01
  title: 혜택
  menu: "혜택 > 혜택 > 퀴즈 등급별 혜택 (BS)"
  layout: MainLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  appClassList: "app_benefits"
  mainClassList: "benefits_main"
</route>
<template>
  <!-- 퀴즈 등급별 혜택 -->
  <BottomSheet
    v-model="isOpen"
    closableDimm
    dimmed
    title="퀴즈 등급별 혜택을 알아보세요"
    class="quiz-level-benefit__sheet"
  >
    <div class="quiz-level-benefit">
      <!-- 
        내 등급
        등급이 없을 경우 LV.0으로 노출
        LV.10 = 퀴즈박사
        LV.20 = 퀴즈왕
        LV.30 = 퀴즈의 신
      -->
      <div
        class="quiz-level-benefit__header"
        tabindex="0"
        :aria-label="headerAriaLabel"
      >
        <div class="quiz-level-benefit__area" aria-hidden="ture">
          <div class="label-group">
            <em class="level-title">내 레벨</em>
            <strong class="level-number">LV.{{ currentLevelName }}</strong>
          </div>
          <SolidLabel color="gray" title="종료 D-23" />
        </div>
        <p class="level-desc" aria-hidden="ture">
          <template v-if="canLevelUp && remainingCount > 0">
            {{ nextLevelName }}까지 <em>{{ remainingCount }}회</em> 남았어요.
          </template>
          <template v-else>
            {{ levelDescription }}
          </template>
        </p>
        <div class="level-progress" aria-hidden="ture">
          <div class="level-progress__bar"></div>
          <div class="level-progress__label">
            <span class="level-progress__text level0"></span>
            <span class="level-progress__text level1">
              <i v-if="currentLevel >= 10" class="is-achieved">
                <Icon name="Check" size="16" color="white" />
              </i>
              <img
                :src="
                  currentLevel >= 10
                    ? '/images/pages/benefits/main/Property_level1_status.svg'
                    : '/images/pages/benefits/main/Property_level1_status_disabled.svg'
                "
                alt="레벨 10"
              />
              <em>퀴즈박사</em>
            </span>
            <span class="level-progress__text level2">
              <i v-if="currentLevel >= 20" class="is-achieved">
                <Icon name="Check" size="16" color="white" />
              </i>
              <img
                :src="
                  currentLevel >= 20
                    ? '/images/pages/benefits/main/Property_level2_status.svg'
                    : '/images/pages/benefits/main/Property_level2_status_disabled.svg'
                "
                alt="레벨 20"
              />
              <em>퀴즈왕</em>
            </span>
            <span class="level-progress__text level3">
              <img
                :src="
                  currentLevel >= 30
                    ? '/images/pages/benefits/main/Property_level3_status.svg'
                    : '/images/pages/benefits/main/Property_level3_status_disabled.svg'
                "
                alt="레벨 30"
              />
              <em>퀴즈의 신</em>
            </span>
          </div>
          <div
            class="level-progress__status"
            :data-level="currentLevel"
            :style="{ '--progress-width': progressWidth }"
          >
            <i class="point-marker-zero"></i>
            <i
              v-if="
                currentLevel > 0 &&
                currentLevel < 30 &&
                currentLevel !== 10 &&
                currentLevel !== 20
              "
              class="point-marker"
            >
              {{ currentLevel }}
            </i>
          </div>
        </div>
      </div>
      <div class="quiz-level-benefit__body">
        <ListItem
          v-for="item in quizLevelItems"
          :key="item.level"
          align="centered"
          class="quiz-level-benefit__item"
          tabindex="0"
          :aria-label="`${item.iconAlt}, ${item.mainText}. ${item.subText}`"
        >
          <template #leftIcon>
            <div class="quiz-level-benefit__item-icon" aria-hidden="true">
              <img :src="`${$cdnURL}${item.iconSrc}`" :alt="item.iconAlt" />
            </div>
          </template>
          <template #leftMainText>
            <strong class="quiz-level-benefit__main-text" aria-hidden="true">
              {{ item.mainText }}
            </strong>
          </template>
          <template #leftSubText>
            <span class="quiz-level-benefit__sub-text" aria-hidden="true">
              {{ item.subText }}
            </span>
          </template>
        </ListItem>
      </div>
      <Divider
        variant="basic"
        color="tertiary"
        size="full"
        orientation="horizontal"
      />
      <div class="quiz-level-benefit__footer">
        <UnorderedList>
          <UnorderedListItem>
            2월에는 월 28회 정답을 맞추면 퀴즈의 신에 등극할 수 있어요.
          </UnorderedListItem>
          <UnorderedListItem>
            이벤트 혜택은 신한카드 사정에 따라 변경될 수 있습니다.
          </UnorderedListItem>
        </UnorderedList>
      </div>
    </div>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { inject, computed } from "vue";
import { defineModel } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import {
  BottomSheet,
  Divider,
  Icon,
  ListItem,
  SolidLabel,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";

// ==========================================
// 바텀시트 제어
// ==========================================
const { $cdnURL } = inject(AppContextKey);
const isOpen = defineModel({ default: true });

// ==========================================
// 현재 레벨 및 상태 (예시 데이터)
// ==========================================
const currentLevel = 8; // 현재 정답 횟수 (0~30)
const canLevelUp = true; // 등급 상승 가능 여부
const achievedLevel = null; // 달성한 등급 (10: 퀴즈박사, 20: 퀴즈왕, 30: 퀴즈의 신, null: 없음)

// ==========================================
// 이벤트 정보 (예시 데이터)
// ==========================================
const eventRemainingDays = 23; // 이벤트 남은 기간

// ==========================================
// 현재 등급 이름 (LV.0 또는 LV.퀴즈박사 등)
// achievedLevel이 있으면 그것을 사용하고, 없으면 currentLevel을 기준으로 계산
// ==========================================
const currentLevelName = computed(() => {
  // achievedLevel이 있으면 그것을 사용
  if (achievedLevel === 30) return "퀴즈의 신";
  if (achievedLevel === 20) return "퀴즈왕";
  if (achievedLevel === 10) return "퀴즈박사";

  // achievedLevel이 없으면 currentLevel을 기준으로 계산
  if (currentLevel >= 30) return "퀴즈의 신";
  if (currentLevel >= 20) return "퀴즈왕";
  if (currentLevel >= 10) return "퀴즈박사";
  return "0";
});

// ==========================================
// 다음 등급까지 남은 횟수 계산
// ==========================================
const remainingCount = computed(() => {
  if (achievedLevel === 30) return 0; // 최대 등급 달성
  if (achievedLevel === 20) return 30 - currentLevel;
  if (achievedLevel === 10) return 20 - currentLevel;
  if (achievedLevel === null) {
    // 달성한 등급이 없을 때
    if (currentLevel >= 20) return 30 - currentLevel;
    if (currentLevel >= 10) return 20 - currentLevel;
    return 10 - currentLevel;
  }
  return 10 - currentLevel;
});

// ==========================================
// 다음 등급 이름
// ==========================================
const nextLevelName = computed(() => {
  if (achievedLevel === 30) return "";
  if (achievedLevel === 20) return "퀴즈의 신";
  if (achievedLevel === 10) return "퀴즈왕";
  // 달성한 등급이 없을 때
  if (currentLevel >= 20) return "퀴즈의 신";
  if (currentLevel >= 10) return "퀴즈왕";
  return "퀴즈박사";
});

// ==========================================
// 레벨 설명 텍스트
// 등급 상승 가능 여부와 달성 상태에 따라 다르게 표시
// ==========================================
const levelDescription = computed(() => {
  // 최대 등급 달성 (30) - 등급 상승 가능 여부와 관계없이
  if (currentLevel >= 30 || achievedLevel === 30) {
    return "대단해요! 다음달도 도전해보세요!";
  }

  // 등급 상승 불가능한 경우
  if (!canLevelUp) {
    // 그 외 (달성한 등급 있음/없음)
    return "다음달에 또 퀴즈등급에 도전할 수 있어요.";
  }

  // 등급 상승 가능한 경우
  // 남은 횟수가 있으면 남은 횟수 표시
  if (remainingCount.value > 0) {
    return `${nextLevelName.value}까지 ${remainingCount.value}회 남았어요.`;
  }

  // 남은 횟수가 0인 경우 (현재는 발생하지 않을 것)
  return "";
});

// ==========================================
// aria-label 텍스트
// ==========================================
const headerAriaLabel = computed(() => {
  return `내 레벨 ${currentLevelName.value === "0" ? "0" : currentLevelName.value}, ${levelDescription.value} 이벤트 남은 기간: ${eventRemainingDays}일. 현재횟수: ${currentLevel}회`;
});

// ==========================================
// 진행률 계산
// 각 구간(0~10, 10~20, 20~30)에서 currentLevel까지의 비율로 계산
// 각 level-progress__text의 중앙 위치까지 동적으로 계산
// grid 구조: 65px 56px 1fr 56px 1fr 56px
// level 10일 때 level 1(퀴즈박사) 중앙까지
// level 20일 때 level 2(퀴즈왕) 중앙까지
// level 30일 때 level 3(퀴즈의 신) 중앙까지
// ==========================================
const progressWidth = computed(() => {
  const level = currentLevel;
  if (level <= 0) return "0px";

  let ratio = 0;

  if (level <= 10) {
    // 0~10 구간: level 0 시작점에서 level 1 중앙까지
    // level에 비례하여 계산 (예: level 8이면 0~10 구간에서 8까지 = 80%)
    ratio = level / 10;
    // level 0 시작: 0px
    // level 1 중앙: 93px (65px + 28px)
    // level 10일 때 level 1 중앙(93px)까지 도달
    // level에 비례하여 width 계산
    return `calc(93px * ${ratio})`;
  } else if (level <= 20) {
    // 10~20 구간: level 0 시작점에서 level 2 중앙까지
    ratio = (level - 10) / 10;
    // level 10일 때: level 1 중앙(93px)
    // level 20일 때: level 2 중앙 = 149px + 1fr = 149px + (100% - 65px - 56px * 3) / 2
    // level 1 중앙에서 level 2 중앙까지: 56px + 1fr
    // level 0 시작점에서 level 2 중앙까지: level 1 중앙 + (level 1 중앙에서 level 2 중앙까지) * ratio
    return `calc(93px + 56px * ${ratio} + (100% - 65px - 56px * 3) / 2 * ${ratio})`;
  } else {
    // 20~30 구간: level 0 시작점에서 level 3 중앙까지
    ratio = (level - 20) / 10;
    // level 20일 때: level 2 중앙 = 149px + 1fr
    // level 30일 때: level 3 중앙 = 205px + 2fr = 205px + (100% - 65px - 56px * 3)
    // level 2 중앙에서 level 3 중앙까지: 56px + 1fr
    // level 0 시작점에서 level 3 중앙까지: level 2 중앙 + (level 2 중앙에서 level 3 중앙까지) * ratio
    return `calc(149px + (100% - 65px - 56px * 3) / 2 + 56px * ${ratio} + (100% - 65px - 56px * 3) / 2 * ${ratio})`;
  }
});

// ==========================================
// 퀴즈 등급별 혜택 데이터
// ==========================================
const quizLevelItems = computed(() => [
  {
    level: 30,
    iconSrc: "/images/pages/benefits/main/Property_level3_status.svg",
    iconAlt: "레벨 30",
    mainText: "월 30회 정답 시 퀴즈의 신",
    subText: "최대 10,000P 랜덥포인트 지급",
  },
  {
    level: 20,
    iconSrc: "/images/pages/benefits/main/Property_level2_status.svg",
    iconAlt: "레벨 20",
    mainText: "월 20회 정답 시 퀴즈왕",
    subText: "최대 5,000P 랜덥포인트 지급",
  },
  {
    level: 10,
    iconSrc: "/images/pages/benefits/main/Property_level1_status.svg",
    iconAlt: "레벨 10",
    mainText: "월 10회 정답 시 퀴즈박사",
    subText: "최대 1,000P 랜덥포인트 지급",
  },
]);
</script>





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
          'is-empty': item.status === null,
        }"
        tabindex="0"
        :aria-label="`${currentYear}년 ${currentMonth}월 ${item.day}일 참여현황: ${item.label || '없음'}`"
      >
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
        <em class="month-schedule__total-value" aria-hidden="true">
          239P
        </em>
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
        <em class="month-schedule__total-value" aria-hidden="true">
          24일
        </em>
      </div>
    </div>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { BottomSheet, Divider } from "@shc-nss/ui/solid";
import { defineModel, ref, computed } from "vue";

// ==========================================
// 바텀시트 제어
// ==========================================
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
  10: { status: "not-participated", label: "미참여" },
  11: { status: "correct", label: "정답" },
  12: { status: "correct", label: "정답" },
  13: { status: "not-participated", label: "미참여" },
  14: { status: "not-participated", label: "미참여" },
  15: { status: "not-participated", label: "미참여" },
  16: { status: "not-participated", label: "미참여" },
  17: { status: "correct", label: "정답" },
  18: { status: "correct", label: "정답" },
  19: { status: "correct", label: "정답" },
  20: { status: "incorrect", label: "오답" },
  21: { status: "not-participated", label: "미참여" },
  22: { status: "not-participated", label: "미참여" },
  23: { status: "not-participated", label: "미참여" },
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
        days.push({ day, status: data.status, label: data.label });
      } else {
        days.push({ day, status: null, label: null });
      }
    }
  }

  return days;
});
</script>




```
{% endraw %}
---
