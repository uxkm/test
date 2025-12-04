<route lang="yaml">
meta:
  id: SBT165A01
  title: 진행 중인 쿠폰
  menu: "혜택 > 할인 쿠폰 메인화면 > 쿠폰 전체보기 > 쿠폰카테고리 (BS)"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업대기
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    menu: true
</route>
<template>
  <!-- 카테고리 선택 바텀시트 -->
  <BottomSheet
    title="카테고리"
    :model-value="true"
    class="category-sheet"
  >
    <div class="category-sheet__content">
      <RadioCircleGroup
        v-model="nextCategoryValue"
        :items="categories"
        orientation="horizontal"
        labelKey="label"
        valueKey="value"
        class="category-sheet__radio-group"
      />
    </div>
    <template #footer>
      <BoxButtonGroup
        size="xlarge"
        variant="35:65"
      >
        <BoxButton
          text="초기화"
          color="tertiary"
          @click="resetCategory"
        />
        <BoxButton
          text="적용"
          @click="applyCategory"
        />
      </BoxButtonGroup>
    </template>
  </BottomSheet>
</template>

<script setup>
import { BottomSheet, BoxButton, BoxButtonGroup, RadioCircleGroup } from "@shc-nss/ui/solid";
import { ref } from "vue";

const categories = [
  {
    label: "전체",
    value: "all",
  },
  {
    label: "카페·다이닝",
    value: "카페 다이닝",
  },
  {
    label: "여가·스포츠",
    value: "여가 스포츠",
  },
  {
    label: "라이프서비스",
    value: "라이프서비스",
  },
  {
    label: "쇼핑",
    value: "쇼핑",
  },
  {
    label: "헬스",
    value: "헬스",
  },
  {
    label: "반려동물",
    value: "반려동물",
  },
  {
    label: "패션·뷰티",
    value: "패션 뷰티",
  },
  {
    label: "여행",
    value: "여행",
  },
  {
    label: "금융·렌탈",
    value: "금융 렌탈",
  },
  {
    label: "자동차",
    value: "자동차",
  },
  {
    label: "육아·교육",
    value: "육아 교육",
  },
  {
    label: "기타",
    value: "기타",
  },
];

const nextCategoryValue = ref("all");

function resetCategory() {
  nextCategoryValue.value = "all";
}

function applyCategory() {
  // 적용 로직
  console.log("Selected category:", nextCategoryValue.value);
}
</script>
