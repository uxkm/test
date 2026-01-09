
{% raw %}
```js

<route lang="yaml">
meta:
  id: SAT049A03
  title: "약관동의"
  menu: 자산 > 금융추천 > 대출 > 정보계좌 관리 > 금융사 연결현황 > 통합약관동의
  layout: SubLayout
  category: 자산
  publish: 김대민
  publishVersion: 0.8
  status: 재작업
  etc: |
    [개발요청]260109: 페이지 -> 풀팝업 으로 변경. 2depth 우측 상세보기 버튼 추가,
    260105: 디자인 동기화 - 종합포털 바로가기 버튼 크기 수정 small->xsmall,
  header:
    fixed: false
    back: false
    close: true
</route>

<template>
  <FullPopup
    v-model="isOpen"
    title="마이데이터 서비스 이용약관"
    class="sc-agree__page"
  >
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body">
      <section>
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
                              <IconButton
                                iconName="Chevron_right"
                                size="small"
                                :aria-label="`${depth2Item.label} 상세 보기`"
                                class="agree-subitem__trigger"
                                @click="handleDetailClick(depth2Item.value)"
                              />
                            </div>
                          </li>
                        </ul>
                        <!-- 개인정보 처리방침 링크 -->
                        <div class="agree-depth__link">
                          <TextButton
                            class="agree-depth__link"
                            color="secondary"
                            size="small"
                            text="개인정보 처리방침"
                            showGoTo
                          />
                        </div>
                      </div>
                    </div>
                  </SolidListAccordion>
                </template>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>

    <Divider variant="group" color="tertiary" class="mt-4xl" />

    <!-- 하단 고정으로 들어가는 부분 위치 수정 -->
    <div class="sc-contents__foot">
      <div class="sc-bottom-info__inner">
        <h2 class="sc-bottom-info__title">마이데이터 서비스 안내</h2>
        <div class="sc-bottom-info__details">
          <UnorderedList>
            <UnorderedListItem
              variant="bullet"
              text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요."
            />
          </UnorderedList>
        </div>
        <!-- [251027] 마이데이터 서비스 안내 하단 링크 추가 -->
        <div class="agree-depth__link">
          <TextButton
            class="agree-depth__link"
            color="secondary"
            size="xsmall"
            text="종합포털 바로가기"
            showGoTo
          />
        </div>
      </div>
    </div>

    <!-- footer -->
    <template #footer>
      <BottomActionContainer :scrollDim="true">
        <BoxButtonGroup size="xlarge" variant="100">
          <BoxButton text="확인" :disabled="!basicAgree4" />
        </BoxButtonGroup>
      </BottomActionContainer>
    </template>
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
  SolidListAccordion,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { reactive, ref, watch } from "vue";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });

/**
 * 유형 4 : 약관동의 기본형
 */
const basicItem4 = {
  label: "약관 전체 동의",
};

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수] 마이데이터 서비스 이용약관",
    value: "s4-1",
    accordion: true,
  },
];

// 2뎁스 항목들 - 서비스 이용약관 (s4-1)
const subItemsDepth2_s4_1 = [
  {
    label: "[필수] 마이데이터 서비스 개인(신용)정보의 수집 및 이용동의",
    value: "s4-1-1",
  },
];

const basicAgree4 = ref(false);
const subAgrees4 = ref([]);
const subAccordionState4 = reactive({
  "s4-1": true, // 서비스 이용약관 1뎁스 아코디언 상태 (초기 펼침)
});

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);

  // 전체 항목 수 계산 (1뎁스 + 2뎁스)
  const totalItems = subItems4.length + subItemsDepth2_s4_1.length;
  basicAgree4.value = set.size === totalItems;
}

watch(basicAgree4, (checked) => {
  if (checked) {
    // 1뎁스 항목들 + 2뎁스 항목들
    const allItems = [
      ...subItems4.map((item) => item.value),
      ...subItemsDepth2_s4_1.map((item) => item.value),
    ];
    subAgrees4.value = allItems;
  } else {
    subAgrees4.value = [];
  }
});

/**
 * 상세보기 버튼 클릭 핸들러
 */
function handleDetailClick(value) {
  // 상세보기 페이지로 이동하거나 팝업을 열어야 할 경우 여기에 로직 추가
  console.log("상세보기 클릭:", value);
}
</script>



```
{% endraw %}
---
