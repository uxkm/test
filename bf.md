
{% raw %}
```js

<route lang="yaml">
meta:
  id: SPY154A01
  title: 신한Pay머니 발급하기
  menu: "페이 > 페이:결제/뱅킹 Tab > 신한 Pay 머니 신청: 약관동의"
  layout: SubLayout
  category: 페이
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  header:
    fixed: true
    back: true
    close: false
</route>
<template>
  <div class="sc-contents__body sc-agree__page">
    <section class="section">
      <div class="sc-agree__list compound" role="region">
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
                <span class="agree-item__label item-label__basic">{{
                  basicItem4.label
                }}</span>
              </template>
            </Checkbox>
          </div>

          <!-- ======================================== -->
          <!-- 1뎁스 영역: 약관 항목들 -->
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
                    <div v-if="item.value === 's4-2'" class="agree-depth">
                      <!-- ======================================== -->
                      <!-- 2뎁스 영역: 개인(신용)정보 필수적 동의 -->
                      <!-- ======================================== -->
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_2"
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
                              <div class="agree-subitem__panel">
                                <!-- 3뎁스 영역: 개인(신용)정보 수집∙이용에 관한 사항 -->
                                <Card
                                  v-if="depth2Item.value === 's4-2-1'"
                                  variant="solid"
                                  color="gray"
                                  class="agree-details card-color__white"
                                >
                                  <ul class="agree-sublist" role="group">
                                    <li
                                      v-for="depth3Item in subItemsDepth3_s4_2_1"
                                      :key="depth3Item.value"
                                      class="agree-subitem agree-subitem__depth3"
                                    >
                                      <div class="agree-item agree-item__sub">
                                        <Checkbox
                                          :value="depth3Item.value"
                                          variant="mark"
                                          align="left"
                                          :model-value="
                                            subAgrees4.includes(
                                              depth3Item.value
                                            )
                                          "
                                          class="agree-item__checkbox item-checkbox__sub"
                                          @update:model-value="
                                            onToggleSub4(
                                              depth3Item.value,
                                              $event
                                            )
                                          "
                                          @click.stop
                                        >
                                          <template #label>
                                            <span
                                              class="agree-item__label item-label__sub"
                                              >{{ depth3Item.label }}</span
                                            >
                                          </template>
                                        </Checkbox>
                                      </div>
                                    </li>
                                  </ul>
                                </Card>

                                <!-- 자세히 보기 링크 -->
                                <div class="agree-depth__link">
                                  <TextButton
                                    class="agree-depth__link"
                                    color="secondary"
                                    size="small"
                                    text="자세히 보기"
                                    showGoTo
                                  />
                                </div>
                              </div>
                            </SolidListAccordion>
                          </template>

                          <!-- 일반 항목 (아코디언 없음) -->
                          <div v-else class="agree-item agree-item__sub">
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
            </div>

            <!-- [필수] 회원 가입 및 발급신청 동의 항목 (s4-3) -->
            <div class="agree-item agree-item__sub">
              <Checkbox
                value="s4-3"
                variant="box"
                align="left"
                :model-value="subAgrees4.includes('s4-3')"
                class="agree-item__checkbox item-checkbox__sub"
                @update:model-value="onToggleSub4('s4-3', $event)"
                @click.stop
              >
                <template #label>
                  <span class="column-line">
                    <span class="agree-item__label item-label__sub"
                      >[필수] 회원 가입 및 발급신청 동의</span
                    >
                    <small class="agree-item-label__description">
                      본인은 카드 실제 소유자와 동일하며, 위 기재된 사실과 다름이 없음을 확인하고 회원가입을 신청합니다.
                    </small>
                  </span>
                </template>
              </Checkbox>
              <IconButton
                iconName="Chevron_right"
                size="small"
                aria-label="[필수] 회원 가입 및 발급신청 동의 상세 보기"
                class="agree-subitem__trigger"
              />
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge" variant="100">
      <BoxButton text="발급하기" :disabled="!basicAgree4" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Card,
  Checkbox,
  IconButton,
  Infobox,
  SolidLabel,
  SolidListAccordion,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { reactive, ref, watch } from "vue";

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환을 위한 타입 정의 (선택사항)

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "개인(신용)정보 필수적 동의",
    value: "s4-2",
    accordion: true,
  },
];

// 2뎁스 항목들 - 개인(신용)정보 필수적 동의 (s4-2)
const subItemsDepth2_s4_2 = [
  {
    label: "[필수] 신한Pay머니 이용약관 동의",
    value: "s4-2-0",
    accordion: false,
  },
  {
    label: "[필수] 개인(신용)정보 수집∙이용 동의",
    value: "s4-2-1",
    accordion: true,
  },
];

// 3뎁스 항목들 - 개인(신용)정보 수집∙이용에 관한 사항 (s4-2-1)
const subItemsDepth3_s4_2_1 = [
  { label: "고유식별정보 수집∙이용 동의", value: "s4-2-1-1" },
  { label: "개인신용정보 수집∙이용 동의", value: "s4-2-1-2" },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-2": false, // 개인(신용)정보 필수적 동의
  "s4-2-1": false, // 개인(신용)정보 수집∙이용에 관한 사항
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산 (1뎁스 + 2뎁스 + 3뎁스)
  const totalItems =
    subItems4.length +
    subItemsDepth2_s4_2.length +
    subItemsDepth3_s4_2_1.length +
    1; // 회원 가입 및 발급신청 동의 항목 (s4-3)
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    // 1뎁스 항목들 + 아코디언 내부의 모든 하위 항목들 (2뎁스 + 3뎁스)
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_2.map((item) => item.value),
      ...subItemsDepth3_s4_2_1.map((item) => item.value),
      "s4-3", // 회원 가입 및 발급신청 동의 항목
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>

<style scoped></style>



<route lang="yaml">
meta:
  id: SPY155A01
  title: 신한Pay머니 발급하기
  menu: "페이 > 페이:결제/뱅킹 Tab > 신한 Pay 머니 신청: 약관동의 > 약관 자세히보기 (FP)"
  layout: SubLayout
  category: 페이
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  header:
    fixed: true
    back: true
    close: false
</route>

<template>
  <FullPopup
    v-model="isOpen"
    title="개인(신용)정보 선택 수집·이용에 관한 동의(선택)"
    class="terms-popup"
  >
    <!-- 약관 내용 영역 (탭 없음) -->
    <div 
      class="terms-panel"
      role="region"
      aria-label="약관 내용"
    >
      <!-- <div class="ondark-empty"> 감싸는 영역은 임시로 추가 실제 개발시 제거하고 사용 -->
      <div class="ondark-empty" style="height: 800px;">
        {{ termsContent }}
      </div>
    </div>
    
    <template #footer>
      <BoxButton 
        color="primary" 
        size="xlarge" 
        text="확인"
        @click="handleConfirm"
      />
    </template>
  </FullPopup>
</template>

<script setup>
import { ref } from "vue";
import { BoxButton, FullPopup } from "@shc-nss/ui/solid";

const isOpen = defineModel({ default: true });

// 약관 내용 데이터
const termsContent = ref("약관 전문");

// 확인 버튼 클릭 핸들러
const handleConfirm = () => {
  // 확인 로직 구현
  console.log("약관 확인");
  isOpen.value = false;
};
</script>




```
{% endraw %}
---
