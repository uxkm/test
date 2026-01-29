
{% raw %}
```js


// 추가 bottomsheet case
.bs-card-agree.sv-bottom-sheet {
  max-height: 90vh;
  @supports (max-height: min(1px, 2px)) {
    max-height: min(591px, 90vh);
  }
  &.sv-bottom-sheet--variant-none {
    .sv-bottom-sheet__header-inner {
      padding-right: var(--spacing-2xl);
    }
  }
  .sv-bottom-sheet__body {
    padding-bottom: 0;
  }
  .sc-agree__list.agree-outline {
    .outline-label__main {
      @include font-set("title-s");
      font-weight: 500;
    }
    .outline-accordion {
      border-width: 1px;
      padding: calc(var(--spacing-md) - 1px) 0 calc(var(--spacing-lg) - 1px);
      .sv-accordion-item__header {
        padding: var(--spacing-lg) calc(var(--spacing-2xl) - 2px);
      }
      .sv-accordion-item__title {
        min-height: 46px;
      }
    }
    .outline-panel {
      padding: 0;
      padding-left: 30px;
      @include font-set("body-m");
      font-weight: 300;
      color: var(--text-secondary);
    }
    .outline-depth2__item {
      padding: var(--spacing-md) 0 var(--spacing-lg);
    }
    .outline-depth2__item-header {
      display: flex;
      flex-direction: column;
      gap: var(--spacing-xs);
    }
    .outline-depth2__item-label {
      @include font-set("body-m");
      font-weight: 300;
      color: var(--text-primary);
    }
    .outline-depth2__item-grade {
      align-self: flex-start;
    }
    .outline-depth2__item-list {
      display: flex;
      flex-direction: column;
      margin-top: var(--spacing-lg);
    }
    .outline-depth2__list-item {
      display: flex;
      align-items: center;
      gap: var(--spacing-xs);
      color: var(--text-secondary);

      ~ .outline-depth2__list-item {
        margin-top: var(--spacing-md);
      }

      .sv-icon {
        color: var(--icon-secondary);
      }
      .sv-checkbox__label {
        @include font-set("body-s");
        font-weight: 300;
        color: var(--text-tertiary);
      }
      .sv-checkbox {
        flex: 1;
      }
    }
    .agree-depth__link {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      margin-top: var(--spacing-md);
      .sv-button__label {
        @include font-set("body-s");
        font-weight: 500;
        color: var(--text-secondary);
      }
      .sv-button__right-icon {
        color: var(--fg-secondary);
      }
      .agree-depth__link-button {
      }
    }
  }
  .sv-accordion-item--variant-solid
    .sv-accordion-panel
    .sv-accordion-panel__content {
    padding: 0 calc(var(--spacing-2xl) - 2px);
  }
  .img_card_double {
    display: block;
    max-width: 140px;
    margin: 0 auto;
  }
  .outline-label__meta {
    padding-left: var(--spacing-4xl);
  }
  .sc-tooltip__content.agree-grade-tooltip {
    gap: var(--spacing-md);
  }
  .sv-tooltip-base {
    max-width: 264px;
  }
  .agree-grade-tooltip__desc {
    padding-bottom: 10px;
    font-weight: 300;
    color: var(--text-tertiary);
  }
  .sc-bottom-info__card {
    margin-right: 0;
    margin-left: 0;
    padding: var(--spacing-xl);
    .sc-bottom-info__details {
      margin-bottom: 0;
    }
    .sc-bottom-info__inner-title {
      @include font-set("body-s", 300);
      font-weight: 300;
      color: var(--text-secondary);
    }
    .sv-text-list[data-color="quaternary"] {
      color: var(--text-quaternary);
    }
  }
  .agree-contents {
    &__header {
      margin: 0;
    }
    &__body {
      margin-top: var(--spacing-lg);
    }
    &__footer {
      margin-top: var(--spacing-lg);
    }
  }
}


<route lang="yaml">
meta:
  id: SCD001A02
  title: ""
  menu: "카드 > 약관동의(BS)"
  layout: EmptyLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  etc: |
    260128: 약관 동의 BottomSheet 추가(맞춤 카드를 추천받으려면 동의가 필요해요)
</route>
<template>
  <BottomSheet
    variant="none"
    :closableDimm="true"
    :closableDrag="false"
    dimmed
    title="맞춤 카드를 추천받으려면 동의가 필요해요"
    v-model="isOpen"
    class="bs-card-agree"
  >
    <div class="bs-card-agree__contents">
      <div class="agree-contents__header">
        <img
          :src="$cdnURL + '/images/pages/pay/img_card_double.png'"
          alt=""
          class="img_card_double"
          aria-hidden="true"
        />
      </div>
      <div class="agree-contents__body">
        <div class="sc-agree__list agree-outline">
          <div class="agree-list__group">
            <div class="agree-outline__list">
              <SolidListAccordion
                v-for="item in outlineItems"
                :key="item.value"
                :class="[
                  'outline-accordion',
                  { 'is-checked': outlineChecked.includes(item.value) },
                ]"
                :rowClickable="false"
                :value="item.value"
                :prevent-hash="true"
              >
                <template #title>
                  <div class="outline-item check-variant-top">
                    <div class="outline-item__body">
                      <Checkbox
                        :value="item.value"
                        variant="box"
                        align="left"
                        :model-value="outlineChecked.includes(item.value)"
                        class="outline-checkbox"
                        @update:model-value="
                          onToggleoutline(item.value, $event)
                        "
                      >
                        <template #label>
                          <div class="outline-label">
                            <span class="outline-label__main">{{
                              item.label
                            }}</span>
                            <span
                              v-if="item.subText"
                              class="outline-label__subtext"
                              >{{ item.subText }}</span
                            >
                          </div>
                        </template>
                      </Checkbox>
                      <div v-if="item.meta" class="outline-label__meta">
                        <span>{{ item.meta }}</span>
                        <Tooltip
                          placement="top-center"
                          :showClose="true"
                          :closeOnClickOutside="true"
                        >
                          <template #content>
                            <div
                              class="sc-tooltip__content agree-grade-tooltip"
                            >
                              <div class="label-group">
                                <SolidLabel color="cyan" title="안심" />
                                <SolidLabel color="green" title="다소안심" />
                                <SolidLabel color="yellow" title="보통" />
                                <SolidLabel color="orange" title="신중" />
                                <SolidLabel color="red" title="주의" />
                              </div>
                              <p class="agree-grade-tooltip__desc">
                                동의등급제는 개인(신용)정보에 관한 선택적 동의
                                항목에 대해 사생활의 비밀과 자유를 침해할 위험,
                                이익이나 혜택, 동의 내용의 명확성 등을 고려한 뒤
                                5가지 등급을 부여하는 제도예요.
                              </p>
                            </div>
                          </template>
                        </Tooltip>
                      </div>
                    </div>
                  </div>
                </template>
                <div class="outline-panel">
                  <div class="outline-depth2__item">
                    <div class="outline-depth2__item-header">
                      <p class="outline-depth2__item-label">
                        카드 및 금융상품·서비스 안내 및 이용권유를 위한
                        수집·이용
                      </p>
                      <SolidLabel
                        class="outline-depth2__item-grade"
                        color="green"
                        title="다소안심"
                      />
                    </div>
                    <div class="outline-depth2__item-body">
                      <ul class="outline-depth2__item-list">
                        <li class="outline-depth2__list-item">
                          <Checkbox
                            value="agree-outline-2-1"
                            variant="mark"
                            align="left"
                            :model-value="
                              outlineChecked.includes('agree-outline-2-1')
                            "
                            class="outline-depth2__item-checkbox"
                            @update:model-value="
                              onToggleoutline('agree-outline-2-1', $event)
                            "
                            @click.stop
                          >
                            <template #label>
                              <span>고유식별번호 조회 동의</span>
                            </template>
                          </Checkbox>
                        </li>
                        <li class="outline-depth2__list-item">
                          <Checkbox
                            value="agree-outline-2-2"
                            variant="mark"
                            align="left"
                            :model-value="
                              outlineChecked.includes('agree-outline-2-2')
                            "
                            class="outline-depth2__item-checkbox"
                            @update:model-value="
                              onToggleoutline('agree-outline-2-2', $event)
                            "
                            @click.stop
                          >
                            <template #label>
                              <span>개인신용정보 제공 동의</span>
                            </template>
                          </Checkbox>
                        </li>
                      </ul>
                      <div class="agree-depth__link">
                        <TextButton
                          class="agree-depth__link-button"
                          color="secondary"
                          size="small"
                          text="자세히 보기"
                          showGoTo
                        />
                      </div>
                    </div>
                  </div>
                </div>
              </SolidListAccordion>
            </div>
          </div>
        </div>
      </div>
      <div class="agree-contents__footer">
        <div class="sc-bottom-info__card">
          <p class="sc-bottom-info__inner-title">꼭! 알아두세요</p>
          <div class="sc-bottom-info__details">
            <UnorderedList :gap="8">
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="동의를 해제하면 맞춤 카드 관련 안내를 받아볼 수 없어요."
              />
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="개인(신용)정보의 보유 및 이용기간은 계약 종료 시까지에요."
              />
              <UnorderedListItem
                variant="bullet"
                size="small"
                data-color="quaternary"
                text="카드상품과 부수서비스의 안내 및 이용권유에 동의했더라도 신용정보의 이용 및 보호에 관한 법률에 따라 언제든 관련한 연락 중단을 요청할 수 있어요. 요청은 신한카드 고객센터(1544-7000) 또는 홈페이지(www.shinhancard.com)에서 해주세요."
              />
            </UnorderedList>
          </div>
        </div>
      </div>
    </div>
    <!-- 하단 확인 버튼 -->
    <template #footer>
      <BottomActionContainer :scrollDim="true">
        <BoxButtonGroup size="xlarge" variant="35:65">
          <BoxButton text="다음에" color="secondary" />
          <BoxButton text="확인" :disabled="!isConfirmEnabled" />
        </BoxButtonGroup>
      </BottomActionContainer>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomActionContainer,
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  SolidListAccordion,
  SolidLabel,
  TextButton,
  Tooltip,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { computed, ref } from "vue";

const isOpen = defineModel({ default: true });

const outlineItems = [
  {
    label: "[선택] 개인(신용)정보 수집·이용 동의",
    value: "agree-outline-2",
    meta: "동의등급제 안내",
  },
];

const outlineChecked = ref([]);

const outlineChildMap = {
  "agree-outline-2": ["agree-outline-2-1", "agree-outline-2-2"],
};

const isConfirmEnabled = computed(() => outlineChecked.value.length > 0);

function onToggleoutline(value, checked) {
  const set = new Set(outlineChecked.value);
  if (checked) set.add(value);
  else set.delete(value);

  const parentValue = Object.keys(outlineChildMap).find((key) =>
    outlineChildMap[key].includes(value),
  );
  if (parentValue) {
    const childValues = outlineChildMap[parentValue];
    const hasCheckedChild = childValues.some((child) => set.has(child));
    if (hasCheckedChild) set.add(parentValue);
    else set.delete(parentValue);
  }
  outlineChecked.value = Array.from(set);
}
</script>


function getTermsContent(value) {
  const termsMap = {
    "s1-1-1": `신한 마이카 내차고 서비스를 이용하고자 하는 경우 개인정보보호법에 따라 아래의 개인정보 수집•이용 동의가 필요합니다.
아래 사항 확인 후 동의하여 주시기 바랍니다.

(1) 개인정보의 수집, 이용 목적
마이카 차량관리 서비스, 중고차 시세정보 서비스 제공
(2) 개인정보 수집∙이용 항목
일반개인정보 : 성명, 닉네임, 차명, 세부유형, 자동차등록번호, 제원관리번호, 차종, 차대번호, 원동기형식, 용도, 연식, 색상, 최초등록일, 최종소유자, 제작연월일, 주민(법인)등록번호, 사용본거지, 검사유효기간, 등록사항확인일, 폐쇄일, 시세정보, 리콜정보
(3) 개인(신용)정보의 보유, 이용 기간
서비스 이용 동의 철회 , 회원 탈회 또는 채권채무관계 소멸 후 5년 (단, 관련법령의 별도 규정이 명시되어 있는 경우 그 기간을 따름)

위와 같은 개인정보 수집, 이용 동의를 거부할 권리가 있습니다. 그러나 동의를 거부할 경우 마이카 내차고 서비스를 받으실 수 없습니다.`,
    "s1-1-2": `신한 마이카 내차고 서비스 이용을 위하여 제3자에게 개인정보를 제공할 경우 개인정보보호법에 따라 본인이 사전 동의가 필요합니다.
아래 사항 확인 후 동의하여 주시기 바랍니다.

(1) 개인정보를 제공받는 자
나이스평가정보㈜
(2) 제공대상 개인정보
일반개인정보 : 성명, 자동차번호
(3) 제공받는자의 이용목적
자동차 정보 및 중고차 시세 조회 / 제공
(4) 보유 및 이용기간
서비스 이용 동의 철회 , 회원 탈회 또는 채권채무관계 소멸 후 5년 (단, 관련법령의 별도 규정이 명시되어 있는 경우 그 기간을 따름)

위와 같은 개인정보 수집, 이용 동의를 거부할 권리가 있습니다. 그러나 동의를 거부할 경우 마이카 내차고 서비스를 받으실 수 없습니다.`,
  };

  // TODO: 실제 API 호출로 변경
  // 예: return await fetchTermsContent(value);
  return termsMap[value] || "";
}






// v0.9 또는 0.8에서 신규로 추가된 부분부터 1뎁스 항목체크 모양은 box->mark로 수정 2뎁스항목은 좌측 들여쓰기 구조 class agree_new 추가
.sc-agree__list.agree_new {
  .agree-subitem {
    .sv-accordion-item--variant-solid  {
      > .sv-accordion-panel {
        > .sv-accordion-panel__content {
          padding-left: calc(var(--spacing-3xl) + var(--spacing-2xl));
        }
      }
    }
  }
}


// 체크항목 없는 유형
<template>
  <BottomSheet
    v-model="isOpen"
    title="자산 연결하기 전에 동의가 필요해요"
    variant="closeButton"
    class="sc-terms__popup px-none"
  >
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body sc-agree__page">
      <section>
        <div class="sc-agree__list compound" role="region">
          <div class="agree-list__group">
            <!-- ======================================== -->
            <!-- 1뎁스 영역: 기본 약관 항목들 -->
            <!-- ======================================== -->
            <!-- 260116: 좌측 체크항목 제거 후 item-label__sub 에 class flex-auto 추가 -->
            <div class="agree-sublist" role="group">
              <div
                v-for="item in subItems4"
                :key="item.value"
                class="agree-subitem"
              >
                <div class="agree-item agree-item__sub">
                  <span class="agree-item__label item-label__sub flex-auto">{{
                    item.label
                  }}</span>
                  <IconButton
                    size="small"
                    icon-name="Chevron_right"
                    :aria-label="`${item.label} 상세보기`"
                    @click="handleDetailClick(item)"
                  />
                </div>
              </div>
              <!-- 개인정보 처리방침 링크 -->
              <div class="agree-depth__link pr-2xl">
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
        </div>
      </section>
    </div>

    <Divider variant="group" color="tertiary" class="mb-4xl" />

    <div class="sc-contents__foot">
      <div class="sc-bottom-info__inner">
        <div class="sc-bottom-info__details">
          <UnorderedList :gap="8" data-color="quaternary">
            <UnorderedListItem
              text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요."
            />
            <UnorderedListItem
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

    <template #footer>
      <BoxButtonGroup size="xlarge" variant="35:65">
        <BoxButton text="괜찮아요" color="secondary" @click="isOpen = false" />
        <BoxButton text="좋아요" color="primary" />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Divider,
  IconButton,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수] 마이데이터 서비스 이용약관",
    value: "s4-1",
  },
  {
    label: "[필수] 마이데이터 서비스 수집이용동의",
    value: "s4-1-2",
  },
];

/**
 * 상세보기 클릭 핸들러
 */
function handleDetailClick(item) {
  // TODO: 상세보기 페이지로 이동하거나 모달 표시
  console.log("상세보기 클릭:", item);
}
</script>























// 체크항목 있는 유형

<template>
  <BottomSheet
    v-model="isOpen"
    title="자산 연결하기 전에 동의가 필요해요"
    variant="closeButton"
    class="sc-terms__popup px-none"
  >
    <!-- 콘텐츠 영역 -->
    <div class="sc-contents__body sc-agree__page">
      <section>
        <div class="sc-agree__list compound" role="region">
          <div class="agree-list__group">
            <!-- ======================================== -->
            <!-- 1뎁스 영역: 기본 약관 항목들 -->
            <!-- ======================================== -->
            <div class="agree-sublist" role="group">
              <div
                v-for="item in subItems4"
                :key="item.value"
                class="agree-subitem"
              >
                <div
                  class="agree-item agree-item__sub"
                  :class="{
                    'is-checked': subAgrees4.includes(item.value),
                  }"
                >
                  <Checkbox
                    :value="item.value"
                    variant="mark"
                    align="left"
                    :model-value="subAgrees4.includes(item.value)"
                    class="agree-item__checkbox item-checkbox__sub"
                    @update:model-value="onToggleSub4(item.value, $event)"
                  >
                    <template #label>
                      <span class="agree-item__label item-label__sub">{{
                        item.label
                      }}</span>
                    </template>
                  </Checkbox>
                  <IconButton
                    size="small"
                    icon-name="Chevron_right"
                    :aria-label="`${item.label} 상세보기`"
                    @click="handleDetailClick(item)"
                  />
                </div>
              </div>
              <!-- 개인정보 처리방침 링크 -->
              <div class="agree-depth__link pr-2xl">
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
        </div>
      </section>
    </div>

    <Divider variant="group" color="tertiary" class="mb-4xl" />

    <div class="sc-contents__foot">
      <div class="sc-bottom-info__inner">
        <div class="sc-bottom-info__details">
          <UnorderedList :gap="8" data-color="quaternary">
            <UnorderedListItem text="잘 이용하지 않는 서비스는 탈퇴 후 내 정보를 삭제할 수 있어요." />
            <UnorderedListItem text="나의 마이데이터 서비스 가입현황은 마이데이터 종합포털에서 확인할 수 있어요." />
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

    <template #footer>
      <BoxButtonGroup size="xlarge" variant="35:65">
        <BoxButton text="괜찮아요" color="secondary" @click="isOpen = false" />
        <BoxButton
          text="좋아요"
          color="primary"
        />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomSheet,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  Divider,
  IconButton,
  TextButton,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { ref } from "vue";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });

// JavaScript/TypeScript 호환 배열
const subItems4 = [
  {
    label: "[필수] 마이데이터 서비스 이용약관",
    value: "s4-1",
  },
  {
    label: "[필수] 마이데이터 서비스 수집이용동의",
    value: "s4-1-2",
  },
];

const subAgrees4 = ref([]);

/**
 * 동작 로직
 */
function onToggleSub4(value, checked) {
  const set = new Set(subAgrees4.value);
  if (checked) set.add(value);
  else set.delete(value);
  subAgrees4.value = Array.from(set);
}

/**
 * 상세보기 클릭 핸들러
 */
function handleDetailClick(item) {
  // TODO: 상세보기 페이지로 이동하거나 모달 표시
  console.log("상세보기 클릭:", item);
}



```
{% endraw %}
---
