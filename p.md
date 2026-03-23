
{% raw %}
```js


// _benefits grid 제거
// 1549 line
.level-progress {
  position: relative;
  display: block;
  margin-top: var(--spacing-3xl);
  &__label {
    display: flex;
    align-items: flex-start;
    width: 100%;
  }
  &__text {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 1;
    width: 56px;
    height: 62px;
    text-align: center;
    line-height: 0;
    box-sizing: border-box;
    &.level0 {
      width: 65px;
    }
    &.level2 {
      margin-left: auto;
    }
    &.level3 {
      margin-left: auto;
    }
  }
}


// 2437 line
&__list {
  display: flex;
  column-gap: var(--spacing-lg);
  min-width: 0;
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none; // Firefox
  padding-left: var(--spacing-2xl);
  padding-right: var(--spacing-2xl);
  &::-webkit-scrollbar {
    display: none; // Chrome, Safari
  }
  &.skeleton {
    overflow: hidden;
    margin: 0;
    padding: 0;
    padding-left: var(--container-padding-mobile);
    .collection-card__item {
      margin: 0;
      padding: 0;
      min-width: 160px;
      width: 100%;
    }
  }
}


// 745 line
&__contents-body {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-md);
  margin-top: var(--spacing-3xl);
  margin-bottom: var(--spacing-3xl);
  > .bf-quiz-pangpang__contents-item {
    flex: 1 1 calc(50% - (var(--spacing-md) / 2));
    min-width: 0;
  }
}


// 822 line
&__contents-footer {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-lg) var(--spacing-md);
  position: relative;
  .bf-quiz-pangpang__contents-item {
    flex: 1 1 calc(50% - (var(--spacing-md) / 2));
    min-width: 0;
    &:nth-child(3) {
      flex-basis: 100%;
      width: 100%;
    }
  }
}


// 1373 line
&__container {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-md);
  padding: 0;
}

// 1380 line
&__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  position: relative;
  width: calc((100% - (var(--spacing-md) * 4)) / 5);
  height: 64px;
  padding: var(--spacing-md);
  box-sizing: border-box;
  border-radius: var(--radius-xl);
  background-color: var(--bg-canvas_white);
}

// 1455 line
&__total {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: var(--spacing-lg);
  margin-top: var(--spacing-4xl);
  padding: var(--spacing-xl) var(--spacing-2xl);
  border-radius: var(--radius-xl);
  border: 1px solid var(--border-secondary);
}


// 3641 line
.custum-card__group {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;

  > .sv-button-group {
    width: calc(50% - 4px);
  }

  > .sv-button-group:last-child {
    width: 100%;
  }
}


// 4709 line
&__content {
  display: flex;
  flex-wrap: wrap;
  gap: 0;
  padding: var(--spacing-4xl) 0 var(--spacing-2xl);
}


// 4718 line
&__item {
  flex: 0 0 50%;
  max-width: 50%;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: var(--spacing-3xl) 0;
  border-top: 1px solid var(--border-secondary);
}

// _utility
// 3537 line
.shared-list {
  --shared-list-gap: var(--spacing-xl);
  display: flex;
  flex-wrap: wrap;
  padding: var(--spacing-3xl) var(--spacing-2xl);
  @media (min-width: 360px) {
    --shared-list-gap: var(--spacing-lg);
  }
  @media (min-width: 320px) {
    padding: var(--spacing-3xl) 0;
  }
  li {
    width: calc((100% - (var(--shared-list-gap) * 3)) / 4);
    margin-right: var(--shared-list-gap);
    margin-bottom: var(--shared-list-gap);
    display: flex;
    flex-direction: column;
    align-items: center;
    &:nth-child(4n) {
      margin-right: 0;
    }
    &:nth-last-child(-n + 4) {
      margin-bottom: 0;
    }
  }
  .sv-button--size-m.sv-button--variant-ghost .sv-button__left-icon {
    width: 56px !important;
    height: 56px !important;
  }
  .sv-button--size-m.sv-button--variant-ghost .sv-button__label {
    @include font-set("body-s", 500);
    font-weight: 500;
  }
  .sv-button {
    flex-direction: column;
    gap: var(--spacing-md);
    width: 100%;
    padding: 0;
    .sv-button__left-icon {
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0;
      border-radius: 50%;
      background-color: var(--bg-ongray_graylight_a5);
      .sc-icon {
        width: 36px;
        height: 36px;
      }
    }
    .sv-button__label {
      margin-top: var(--spacing-md);
      margin-left: 0;
      color: var(--text-primary);
    }
    &.link-copy-btn {
      color: var(--fg-primary);
    }
    &.x-btn {
      color: inherit;
      .sv-button__left-icon {
        background-color: var(--bg-informative-same);
      }
    }
    &.kakao-btn {
      svg path[fill="white"] {
        fill: #fff;
      }
    }
    // &.x_transp {
    //   .sv-button__left-icon {
    //     background-color: var(--bg-ongray_graylight_a5);
    //   }
    // }
  }
}

// common
// 767 line
&__grid {
  --month-filter-gap: var(--spacing-md);
  display: flex !important;
  flex-wrap: wrap !important;
  .sv-select-box {
    width: calc((100% - (var(--month-filter-gap) * 2)) / 3);
    box-sizing: border-box;
    margin: 0 var(--month-filter-gap) var(--month-filter-gap) 0 !important;
    &:nth-child(3n) {
      margin-right: 0 !important;
    }
    &:nth-last-child(-n + 3) {
      margin-bottom: 0 !important;
    }
  }
}


// 818 line
.today-list {
  $bg-list-brand: var(--bg-brand) !important;
  $bg-list-cyan: var(--bg-cyan) !important;
  $bg-list-red: var(--bg-red) !important;
  $bg-list-orange: var(--bg-orange) !important;
  $bg-list-crimson: var(--bg-red) !important;

  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-md);

  &__item {
    width: calc((100% - (var(--spacing-md) * 2)) / 3);
  }
}












// fullpopup & page 호출 방식

// ConditionalFullPopup 모듈 예시
<!--
  ConditionalFullPopup: 조건부 FullPopup 래퍼

  wrap=true  → FullPopup으로 slot 감싸기 (풀팝업/모달 형태)
  wrap=false → slot만 렌더링 (페이지 내 인라인 표시)

  FullPopup의 modelValue 기본값이 false이므로,
  명시적으로 modelValue ?? true 전달하여 열린 상태로 표시
-->
<template>
  <FullPopup
    v-if="wrap"
    :model-value="modelValue ?? true"
    @update:model-value="$emit('update:modelValue', $event)"
    :title="title"
    :closeable="closeable"
    @closed="$emit('close')"
  >
    <slot />
  </FullPopup>
  <slot v-else />
</template>

<script setup>
import { FullPopup } from "@shc-nss/ui/solid";

defineProps({
  /** true: FullPopup 래핑, false: slot만 렌더 */
  wrap: { type: Boolean, default: false },
  /** FullPopup 제목 */
  title: { type: String, default: "" },
  /** 닫기 버튼 표시 여부 */
  closeable: { type: Boolean, default: true },
  /**
   * FullPopup open 상태
   * 기본 true - FullPopup modelValue 기본값이 false라 닫힌 상태면 내용이 안 보이므로,
   * 미전달 시 true로 열린 상태 유지
   */
  modelValue: { type: Boolean, default: true },
});

defineEmits(["update:modelValue", "close"]);
</script>




// 화면 예시
<route lang="yaml">
meta:
  id: SBT178A06
  title: "약관동의"
  menu: "혜택 > 앱테크 메인화면 > 지역타겟팅 보물팡팡 > 약관동의 (일반 보물팡팡 수정)"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.9
  status: 작업완료
  etc: | 
    [v0.9] 260130: 풀팝업 -> 페이지 변경
  header:
    fixed: true
    back: true
    close: false
    home: true
</route>
<template>
  <!--
    ConditionalFullPopup: isFullPopup에 따라 FullPopup 래핑 여부 결정
    - wrap=true (풀팝업): FullPopup으로 감싸서 모달 형태로 표시
    - wrap=false (페이지): slot만 렌더링, 별도 래핑 없음
  -->
  <ConditionalFullPopup
    :wrap="isFullPopup"
    v-model="isOpen"
    :title="bodyTitle"
    :closeable="true"
    @close="handleClose"
  >
    <ScTitle mainTitle="실시간 포인트 적립을 위해<br />약관에 동의해주세요." />
    <div class="sc-contents__body sc-agree__page">
      <!--
        페이지인 경우: section 클래스 적용 (레이아웃/스타일용)
        풀팝업인 경우: section 클래스 제거 (FullPopup 내부 레이아웃과 충돌 방지)
      -->
      <section :class="{ section: !isFullPopup }">
        <div
          class="sc-agree__list compound agree_new"
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
            <div
              class="agree-sublist"
              role="group"
            >
              <div
                v-for="item in depth1Items"
                :key="item.value"
                class="agree-subitem"
                :class="{ 'agree-subitem__accordion': Boolean(item.accordion) }"
              >
                <template v-if="item.accordion">
                  <SolidListAccordion
                    class="agree-subitem__accordion"
                    :rowClickable="false"
                    :value="item.value"
                    v-model:isExpanded="subAccordionState4[item.value]"
                  >
                    <template #title>
                      <div
                        class="agree-item agree-item__sub"
                        :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                      >
                        <Checkbox
                          :value="item.value"
                          variant="mark"
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
                      </div>
                    </template>
                    <div class="agree-subitem__panel">
                      <div
                        v-if="item.value === 's4-4'"
                        class="agree-depth"
                      >
                        <ul class="agree-sublist agree-sublist__depth2">
                          <li
                            v-for="depth2Item in subItemsDepth2_s4_4"
                            :key="depth2Item.value"
                            class="agree-subitem agree-subitem__depth2"
                          >
                            <template v-if="depth2Item.accordion">
                              <SolidListAccordion
                                class="agree-subitem__accordion accordion-depth2"
                                :rowClickable="false"
                                :value="depth2Item.value"
                                v-model:isExpanded="subAccordionState4[depth2Item.value]"
                              >
                                <template #title>
                                  <div class="agree-item agree-item__sub">
                                    <Checkbox
                                      :value="depth2Item.value"
                                      variant="mark"
                                      align="left"
                                      :model-value="subAgrees4.includes(depth2Item.value)"
                                      class="agree-item__checkbox item-checkbox__sub"
                                      @update:model-value="onToggleSub4(depth2Item.value, $event)"
                                      @click.stop
                                    >
                                      <template #label>
                                        <span class="agree-item__label item-label__sub">{{
                                          depth2Item.label
                                        }}</span>
                                      </template>
                                    </Checkbox>
                                  </div>
                                </template>
                                <div class="agree-subitem__panel">
                                  <div
                                    v-if="depth2Item.value === 's4-4-5'"
                                    class="agree-depth"
                                  >
                                    <Card
                                      variant="solid"
                                      color="gray"
                                      class="agree-details"
                                    >
                                      <ul
                                        class="agree-sublist"
                                        role="group"
                                      >
                                        <li
                                          v-for="depth3Item in subItemsDepth3_s4_4_5"
                                          :key="depth3Item.value"
                                          class="agree-subitem agree-subitem__depth3"
                                        >
                                          <div class="agree-item agree-item__sub">
                                            <span class="agree-item__label item-label__sub">{{
                                              depth3Item.label
                                            }}</span>
                                            <IconButton
                                              iconName="Chevron_right"
                                              size="small"
                                              :aria-label="`${depth3Item.label} 상세 보기`"
                                              class="agree-subitem__trigger"
                                            />
                                          </div>
                                        </li>
                                      </ul>
                                    </Card>
                                  </div>
                                </div>
                              </SolidListAccordion>
                            </template>
                            <div
                              v-else
                              class="agree-item agree-item__sub"
                            >
                              <Checkbox
                                :value="depth2Item.value"
                                variant="mark"
                                align="left"
                                :model-value="subAgrees4.includes(depth2Item.value)"
                                class="agree-item__checkbox item-checkbox__sub"
                                @update:model-value="onToggleSub4(depth2Item.value, $event)"
                                @click.stop
                              >
                                <template #label>
                                  <span class="agree-item__label item-label__sub">{{
                                    depth2Item.label
                                  }}</span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                :aria-label="`${depth2Item.label} 상세 보기`"
                                class="agree-subitem__trigger"
                              />
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </SolidListAccordion>
                </template>
                <template v-else>
                  <div
                    class="agree-item agree-item__sub"
                    :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                  >
                    <Checkbox
                      :value="item.value"
                      variant="mark"
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
                </template>
              </div>
            </div>
          </div>
        </div>
      </section>
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
  </ConditionalFullPopup>
</template>

<script setup>
import { ScTitle } from "@shc-nss/ui/shc";
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Card,
  Checkbox,
  IconButton,
  SolidListAccordion,
} from "@shc-nss/ui/solid";

import ConditionalFullPopup from "./section/ConditionalFullPopup.vue";
import { computed, reactive, ref, watch } from "vue";
import { useRoute } from "vue-router";

/**
 * @prop {boolean} isFullPopup - 표시 모드
 *   - true: 풀팝업 모드 (FullPopup으로 감싸서 모달 형태)
 *   - false: 페이지 모드 (일반 페이지 레이아웃)
 *   - 부모에서 :is-full-popup="true" 전달 시 풀팝업으로 표시
 */
const props = defineProps({
  isFullPopup: { type: Boolean, default: true },
});

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");

/** FullPopup open/close 상태 (풀팝업 모드에서 닫기 시 false) */
const isOpen = defineModel({ default: true });

/** 풀팝업 닫기 핸들러 */
const handleClose = () => {
  isOpen.value = false;
};

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

const depth1Items = [
  {
    label: "[필수] 신한 슈퍼SOL 이용약관",
    value: "s4-4",
    accordion: true,
  },
];

const subItemsDepth2_s4_4 = [
  { label: "[필수] 신한 모바일 플랫폼 이용약관", value: "s4-4-1" },
  { label: "[필수] 신한금융그룹 통합 포인트 서비스 이용 동의", value: "s4-4-2" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의", value: "s4-4-3" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의(포인트 서비스 제공)", value: "s4-4-4" },
  { label: "[필수] 전자금융서비스 이용동의(신한은행)", value: "s4-4-5", accordion: true },
  { label: "[필수] 그룹 로열티 서비스 이용동의(신한은행)", value: "s4-4-6" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의(신한은행)", value: "s4-4-7" },
];

const subItemsDepth3_s4_4_5 = [
  { label: "전자금융거래 기본약관", value: "s4-4-5-1" },
  { label: "신한온라인서비스 이용약관", value: "s4-4-5-2" },
  { label: "전자통지서비스 이용약관", value: "s4-4-5-3" },
  { label: "개인정보 수집 이용동의(비여신금융거래)", value: "s4-4-5-4" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-4": false,
  "s4-4-5": false,
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  const totalItems = depth1Items.length + subItemsDepth2_s4_4.length;
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    const allItems = [
      ...depth1Items.map((item) => item.value),
      ...subItemsDepth2_s4_4.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>

// 방식 2번째
<route lang="yaml">
meta:
  id: SBT178A06
  title: "약관동의"
  menu: "혜택 > 앱테크 메인화면 > 지역타겟팅 보물팡팡 > 약관동의 (일반 보물팡팡 수정)"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.9
  status: 작업완료
  etc: | 
    [v0.9] 260130: 풀팝업 -> 페이지 변경
  header:
    fixed: true
    back: true
    close: false
    home: true
  # 모드 변경: false=페이지, true=풀팝업 (이 값만 변경하면 wrap/section 자동 반영)
  isFullPopup: false
</route>
<template>
  <!-- wrap: route.meta.isFullPopup 사용, section 클래스는 !wrap과 동기화 -->
  <ConditionalFullPopup
    :wrap="route.meta?.isFullPopup ?? false"
    v-model="isOpen"
    :title="bodyTitle"
    :closeable="true"
    @close="handleClose"
  >
    <ScTitle mainTitle="실시간 포인트 적립을 위해<br />약관에 동의해주세요." />
    <div class="sc-contents__body sc-agree__page">
      <section :class="{ section: !(route.meta?.isFullPopup ?? false) }">
        <div
          class="sc-agree__list compound agree_new"
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
            <div
              class="agree-sublist"
              role="group"
            >
              <div
                v-for="item in depth1Items"
                :key="item.value"
                class="agree-subitem"
                :class="{ 'agree-subitem__accordion': Boolean(item.accordion) }"
              >
                <template v-if="item.accordion">
                  <SolidListAccordion
                    class="agree-subitem__accordion"
                    :rowClickable="false"
                    :value="item.value"
                    v-model:isExpanded="subAccordionState4[item.value]"
                  >
                    <template #title>
                      <div
                        class="agree-item agree-item__sub"
                        :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                      >
                        <Checkbox
                          :value="item.value"
                          variant="mark"
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
                      </div>
                    </template>
                    <div class="agree-subitem__panel">
                      <div
                        v-if="item.value === 's4-4'"
                        class="agree-depth"
                      >
                        <ul class="agree-sublist agree-sublist__depth2">
                          <li
                            v-for="depth2Item in subItemsDepth2_s4_4"
                            :key="depth2Item.value"
                            class="agree-subitem agree-subitem__depth2"
                          >
                            <template v-if="depth2Item.accordion">
                              <SolidListAccordion
                                class="agree-subitem__accordion accordion-depth2"
                                :rowClickable="false"
                                :value="depth2Item.value"
                                v-model:isExpanded="subAccordionState4[depth2Item.value]"
                              >
                                <template #title>
                                  <div class="agree-item agree-item__sub">
                                    <Checkbox
                                      :value="depth2Item.value"
                                      variant="mark"
                                      align="left"
                                      :model-value="subAgrees4.includes(depth2Item.value)"
                                      class="agree-item__checkbox item-checkbox__sub"
                                      @update:model-value="onToggleSub4(depth2Item.value, $event)"
                                      @click.stop
                                    >
                                      <template #label>
                                        <span class="agree-item__label item-label__sub">{{
                                          depth2Item.label
                                        }}</span>
                                      </template>
                                    </Checkbox>
                                  </div>
                                </template>
                                <div class="agree-subitem__panel">
                                  <div
                                    v-if="depth2Item.value === 's4-4-5'"
                                    class="agree-depth"
                                  >
                                    <Card
                                      variant="solid"
                                      color="gray"
                                      class="agree-details"
                                    >
                                      <ul
                                        class="agree-sublist"
                                        role="group"
                                      >
                                        <li
                                          v-for="depth3Item in subItemsDepth3_s4_4_5"
                                          :key="depth3Item.value"
                                          class="agree-subitem agree-subitem__depth3"
                                        >
                                          <div class="agree-item agree-item__sub">
                                            <span class="agree-item__label item-label__sub">{{
                                              depth3Item.label
                                            }}</span>
                                            <IconButton
                                              iconName="Chevron_right"
                                              size="small"
                                              :aria-label="`${depth3Item.label} 상세 보기`"
                                              class="agree-subitem__trigger"
                                            />
                                          </div>
                                        </li>
                                      </ul>
                                    </Card>
                                  </div>
                                </div>
                              </SolidListAccordion>
                            </template>
                            <div
                              v-else
                              class="agree-item agree-item__sub"
                            >
                              <Checkbox
                                :value="depth2Item.value"
                                variant="mark"
                                align="left"
                                :model-value="subAgrees4.includes(depth2Item.value)"
                                class="agree-item__checkbox item-checkbox__sub"
                                @update:model-value="onToggleSub4(depth2Item.value, $event)"
                                @click.stop
                              >
                                <template #label>
                                  <span class="agree-item__label item-label__sub">{{
                                    depth2Item.label
                                  }}</span>
                                </template>
                              </Checkbox>
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                :aria-label="`${depth2Item.label} 상세 보기`"
                                class="agree-subitem__trigger"
                              />
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </SolidListAccordion>
                </template>
                <template v-else>
                  <div
                    class="agree-item agree-item__sub"
                    :class="{ 'is-checked': subAgrees4.includes(item.value) }"
                  >
                    <Checkbox
                      :value="item.value"
                      variant="mark"
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
                </template>
              </div>
            </div>
          </div>
        </div>
      </section>
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
  </ConditionalFullPopup>
</template>

<script setup>
import { ScTitle } from "@shc-nss/ui/shc";
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Card,
  Checkbox,
  IconButton,
  SolidListAccordion,
} from "@shc-nss/ui/solid";

import ConditionalFullPopup from "./section/ConditionalFullPopup.vue";
import { computed, reactive, ref, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
const bodyTitle = computed(() => route.meta?.title || "");

/** FullPopup open/close 상태 (풀팝업 모드에서 닫기 시 false) */
const isOpen = defineModel({ default: true });

/** 풀팝업 닫기 핸들러 */
const handleClose = () => {
  isOpen.value = false;
};

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

const depth1Items = [
  {
    label: "[필수] 신한 슈퍼SOL 이용약관",
    value: "s4-4",
    accordion: true,
  },
];

const subItemsDepth2_s4_4 = [
  { label: "[필수] 신한 모바일 플랫폼 이용약관", value: "s4-4-1" },
  { label: "[필수] 신한금융그룹 통합 포인트 서비스 이용 동의", value: "s4-4-2" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의", value: "s4-4-3" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의(포인트 서비스 제공)", value: "s4-4-4" },
  { label: "[필수] 전자금융서비스 이용동의(신한은행)", value: "s4-4-5", accordion: true },
  { label: "[필수] 그룹 로열티 서비스 이용동의(신한은행)", value: "s4-4-6" },
  { label: "[필수] 개인(신용)정보 수집・이용・제공 동의(신한은행)", value: "s4-4-7" },
];

const subItemsDepth3_s4_4_5 = [
  { label: "전자금융거래 기본약관", value: "s4-4-5-1" },
  { label: "신한온라인서비스 이용약관", value: "s4-4-5-2" },
  { label: "전자통지서비스 이용약관", value: "s4-4-5-3" },
  { label: "개인정보 수집 이용동의(비여신금융거래)", value: "s4-4-5-4" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-4": false,
  "s4-4-5": false,
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  const totalItems = depth1Items.length + subItemsDepth2_s4_4.length;
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    const allItems = [
      ...depth1Items.map((item) => item.value),
      ...subItemsDepth2_s4_4.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>




```
{% endraw %}
---
