
{% raw %}
```js

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
