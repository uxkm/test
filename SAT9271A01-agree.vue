<template>
  <ScTitle
    mainTitle="예상한도와 금리 조회를 위해<br />다음 항목에 동의해주세요."
    description="대출신청 가능여부 확인을 위한 신용조회는<br />고객님의 개인신용평점에 영향을 주지 않습니다. "
  />
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

          <!-- 1뎁스 약관 항목 -->
          <div
            class="agree-sublist"
            role="group"
          >
            <div
              v-for="item in subItems4"
              :key="item.value"
              class="agree-subitem"
              :class="{ 'agree-subitem__accordion': Boolean(item.accordion) }"
            >
              <!-- 아코디언 항목 -->
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
                    </div>
                  </template>
                  <div class="agree-subitem__panel">
                    <!-- 2뎁스 하위 항목 -->
                    <div
                      v-if="item.value === 's4-5'"
                      class="agree-depth"
                    >
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_5"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
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
                    <div
                      v-else-if="item.value === 's4-6'"
                      class="agree-depth"
                    >
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_6"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
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
                    <div
                      v-else-if="item.value === 's4-7'"
                      class="agree-depth"
                    >
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_7"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
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
                    <div
                      v-else-if="item.value === 's4-10'"
                      class="agree-depth"
                    >
                      <ul class="agree-sublist agree-sublist__depth2">
                        <li
                          v-for="depth2Item in subItemsDepth2_s4_10"
                          :key="depth2Item.value"
                          class="agree-subitem agree-subitem__depth2"
                        >
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

              <!-- 일반 항목 (아코디언 없음) -->
              <template v-else>
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
</template>

<script setup>
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  IconButton,
  SolidListAccordion,
} from "@shc-nss/ui/solid";
import { ScTitle } from "@shc-nss/ui/shc";
import { reactive, ref, watch } from "vue";

// 약관 전체 동의
const basicItem4 = {
  label: "전체 동의",
};

// 1뎁스 항목들
const subItems4 = [
  {
    label: "[필수] (대환)대출 비교 서비스 이용 약관",
    value: "s4-1",
  },
  {
    label: "[필수] 신한카드 개인(신용)정보 수집·이용 동의",
    value: "s4-2",
  },
  {
    label: "[필수] 신한카드 고유식별정보 수집·이용 동의",
    value: "s4-3",
  },
  {
    label: "[필수] 신한카드 (개인) 신용정보 제3자 제공동의(금융결제원)",
    value: "s4-4",
  },
  {
    label: "[필수] 금융사 개인(신용)정보 수집·이용 동의",
    value: "s4-5",
    accordion: true,
  },
  {
    label: "[필수] 금융사 개인(신용)정보 조회 동의",
    value: "s4-6",
    accordion: true,
  },
  {
    label: "[필수] 금융사 개인(신용)정보 제3자 제공 동의",
    value: "s4-7",
    accordion: true,
  },
  {
    label: "[필수] 금융결제원 대출정보 열람청구 위임 동의",
    value: "s4-8",
  },
  {
    label: "[필수] 비대면 서류 제출 자동화(스크래핑) 서비스 이용동의",
    value: "s4-9",
  },
  {
    label: "[필수] 휴대폰 본인확인 이용 동의",
    value: "s4-10",
    accordion: true,
  },
];

// 2뎁스 항목들 - 금융사 개인(신용)정보 수집·이용 동의 (s4-5)
const subItemsDepth2_s4_5 = [
  { label: "개인(신용)정보 수집·이용 동의", value: "s4-5-1" },
  { label: "고유식별정보 수집·이용 동의", value: "s4-5-2" },
];

// 2뎁스 항목들 - 금융사 개인(신용)정보 조회 동의 (s4-6)
const subItemsDepth2_s4_6 = [
  { label: "개인(신용)정보 조회 동의", value: "s4-6-1" },
  { label: "고유식별정보 조회 동의", value: "s4-6-2" },
];

// 2뎁스 항목들 - 금융사 개인(신용)정보 제3자 제공 동의 (s4-7)
const subItemsDepth2_s4_7 = [
  { label: "개인(신용)정보 제공 동의", value: "s4-7-1" },
  { label: "고유식별정보 제공 동의", value: "s4-7-2" },
];

// 2뎁스 항목들 - 휴대폰 본인확인 이용 동의 (s4-10)
const subItemsDepth2_s4_10 = [
  { label: "개인정보이용 및 활용 동의", value: "s4-10-1" },
  { label: "휴대폰 본인확인 이용동의", value: "s4-10-2" },
  { label: "고유식별정보 처리동의", value: "s4-10-3" },
];

// 전체 동의 상태
const basicAgree4 = ref(false);

// 개별 동의 상태
const subAgrees4 = ref([]);

// 아코디언 확장/축소 상태
const subAccordionState4 = reactive({
  "s4-5": false,
  "s4-6": false,
  "s4-7": false,
  "s4-10": false,
});

// 개별 항목 토글 시 전체 동의 상태 업데이트
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산 (1뎁스 + 2뎁스)
  const totalItems =
    subItems4.length +
    subItemsDepth2_s4_5.length +
    subItemsDepth2_s4_6.length +
    subItemsDepth2_s4_7.length +
    subItemsDepth2_s4_10.length;
  basicAgree4.value = set.size === totalItems;
}

// 전체 동의 토글 시 모든 항목 선택/해제
watch(basicAgree4, (checked) => {
  if (checked) {
    // 모든 항목 선택
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_5.map((item) => item.value),
      ...subItemsDepth2_s4_6.map((item) => item.value),
      ...subItemsDepth2_s4_7.map((item) => item.value),
      ...subItemsDepth2_s4_10.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});
</script>

<style lang="scss" scoped></style>
