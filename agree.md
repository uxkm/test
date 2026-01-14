
{% raw %}
```js

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
