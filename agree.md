
{% raw %}
```js

<route lang="yaml">
meta:
  id: SSN080A01
  title: ""
  menu: "Sign in/up > 앱 잠금해제 > 앱 잠금 안내 > 휴대폰인증: 약관동의(BS)"
  layout: SubLayout
  category: Sign in/up
  publish: 김가영
  publishVersion: 0.8
  status: 작업완료
  etc: SSN103A01
  navbar: false
  header:
    back: false
</route>
<template>
  <BottomSheet title="약관에 동의해주세요." v-model="isOpen">
    <div class="sc-agree__list compound bg-gray" role="region">
      <div class="agree-list__group">
        <!-- ======================================== -->
        <!-- 1뎁스 영역: 기본 약관 항목들 -->
        <!-- ======================================== -->
        <div class="agree-sublist" role="group">
          <div
            v-for="item in subItems4"
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
                    :class="{
                      'is-checked': subAgrees4.includes(item.value),
                    }"
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
                        <span class="agree-item__label item-label__sub">{{
                          item.label
                        }}</span>
                      </template>
                    </Checkbox>
                  </div>
                </template>
                <div class="agree-subitem__panel">
                  <div v-if="item.value === 's4-1'" class="agree-depth">
                    <!-- ======================================== -->
                    <!-- 2뎁스 영역: 서비스 이용약관 -->
                    <!-- ======================================== -->
                    <ul class="agree-sublist agree-sublist__depth2">
                      <li
                        v-for="depth2Item in subItemsDepth2_s4_1"
                        :key="depth2Item.value"
                        class="agree-subitem agree-subitem__depth2"
                      >
                        <!-- 아코디언이 있는 항목 -->
                        <template v-if="depth2Item.accordion">
                          <SolidListAccordion
                            class="agree-subitem__accordion accordion-depth2"
                            :rowClickable="false"
                            :value="depth2Item.value"
                            v-model:isExpanded="
                              subAccordionState4[depth2Item.value]
                            "
                          >
                            <template #title>
                              <div class="agree-item agree-item__sub">
                                <Checkbox
                                  :value="depth2Item.value"
                                  variant="mark"
                                  align="left"
                                  :model-value="
                                    subAgrees4.includes(depth2Item.value)
                                  "
                                  class="agree-item__checkbox item-checkbox__sub"
                                  @update:model-value="
                                    onToggleSub4(depth2Item.value, $event)
                                  "
                                  @click.stop
                                >
                                  <template #label>
                                    <span
                                      class="agree-item__label item-label__sub"
                                      >{{ depth2Item.label }}</span
                                    >
                                  </template>
                                </Checkbox>
                              </div>
                            </template>
                          </SolidListAccordion>
                        </template>

                        <!-- 일반 항목 -->
                        <div v-else class="agree-item agree-item__sub">
                          <Checkbox
                            :value="depth2Item.value"
                            variant="mark"
                            align="left"
                            :model-value="subAgrees4.includes(depth2Item.value)"
                            class="agree-item__checkbox item-checkbox__sub"
                            @update:model-value="
                              onToggleSub4(depth2Item.value, $event)
                            "
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
            <!-- <template v-else>
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
            </template> -->
          </div>
        </div>
      </div>
    </div>

    <template #footer>
      <BottomActionContainer :scrollDim="true">
        <BoxButtonGroup size="xlarge" variant="100">
          <BoxButton text="확인" :disabled="!basicAgree4" />
        </BoxButtonGroup>
      </BottomActionContainer>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BottomSheet,
  BoxButtonGroup,
  Card,
  Checkbox,
  IconButton,
  SolidLabel,
  SolidListAccordion,
  TextButton,
  UnorderedList,
  UnorderedListItem,
  Divider,
} from "@shc-nss/ui/solid";
import { computed, reactive, ref, watch } from "vue";
import { useRoute } from "vue-router";

const isOpen = defineModel({ default: true });
const route = useRoute();
// const bodyTitle = computed(() => route.meta?.title || "");

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의 (아코디언 기능 추가 필요)",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "약관 전체 동의",
    value: "s4-1",
    accordion: true,
  },
];

// 2뎁스 항목들 - 서비스 이용약관 (s4-1)
const subItemsDepth2_s4_1 = [
  { label: "[필수] 앱카드 서비스 이용약관 동의", value: "s4-1-1" },
  { label: "[필수] 개인(신용)정보의 수집 및 이용동의", value: "s4-1-2" },
  { label: "[필수] 고유식별정보처리 동의", value: "s4-1-3" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-1": false, // 서비스 이용약관 2뎁스 아코디언 상태
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // "약관 전체 동의" (s4-1)를 체크한 경우
  if (value === "s4-1") {
    if (checked) {
      // 모든 약관 체크
      const allItems = [
        ...subItems4.map((item) => item.value),
        ...subItemsDepth2_s4_1.map((item) => item.value),
      ];
      subAgrees4.value = allItems;
      basicAgree4.value = true;
    } else {
      // 모든 약관 체크 해제
      subAgrees4.value = [];
      basicAgree4.value = false;
    }
    return;
  }

  // 개별 약관 체크 시 전체 동의 상태 업데이트
  // 전체 항목 수 계산 (1뎁스 + 2뎁스)
  const totalItems = subItems4.length + subItemsDepth2_s4_1.length;
  const currentSet = new Set(subAgrees4.value);

  // 모든 약관이 체크되었는지 확인
  const allItems = [
    ...subItems4.map((item) => item.value),
    ...subItemsDepth2_s4_1.map((item) => item.value),
  ];
  const allChecked = allItems.every((item) => currentSet.has(item));
  basicAgree4.value = allChecked;

  // 모든 약관이 체크되었으면 "약관 전체 동의"도 체크
  if (allChecked && !currentSet.has("s4-1")) {
    currentSet.add("s4-1");
    subAgrees4.value = Array.from(currentSet);
  } else if (!allChecked && currentSet.has("s4-1")) {
    currentSet.delete("s4-1");
    subAgrees4.value = Array.from(currentSet);
  }
}

watch(basicAgree4, (checked) => {
  if (checked) {
    // 1뎁스 항목들
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_1.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>

<style lang="scss" scoped></style>




```
{% endraw %}
---
