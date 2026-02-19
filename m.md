
{% raw %}
```js


.bs-calendar {
  .sv-bottom-sheet__body {
    padding-right: 0;
    padding-left: 0;
  }
  .bs-calendar-title {
    @include font-set("title-l", 500);
    font-weight: 500;
    color: var(--text-primary);
  }
}



<route lang="yaml">
meta:
  id: SMY018A01
  title: ""
  menu: 마이 > 마이 주니어 > 눈치게임 - 안내페이지 > 인트로 > 게임 완료 > 실시간 차트 > 날짜선택
  layout: EmptyLayout
  category: 마이
  publish: "정예린(김대민)"
  publishVersion: 0.8
  status: 작업완료
  qa: 검수완료
  qa2: 퍼블완료
  ui: |
    [완료] 260219: 마크업 (페이지 -> BottomSheet로 수정. 디자인 동기화)
    [완료] 260130: 마크업 (날짜 타이틀 수정)
  header:
    back: false
</route>

<template>
  <!-- 260219: 구조 수정 페이지 -> BottomSheet로 수정으로 class 제거 및 변경 -->
  <BottomSheet
    disableMinHeight
    title="날짜를 선택해주세요"
    v-model="isOpen"
    class="bs-calendar"
  >
    <div class="bs-calendar-wrap">
      <CalendarDatePicker
        v-model="modelValue"
        @update:modelValue="onChange"
        @clickDay="onClick"
        header="true"
        :formatters="{ formatCaption: (date) => format(date, 'yyyy년 M월') }"
      >
        <template #header-title="{ title }">
          <div>
            <strong class="bs-calendar-title">{{ title }}</strong>
          </div>
        </template>
      </CalendarDatePicker>
    </div>

    <template #footer>
      <BoxButton
        @click="isOpen = false"
        text="확인"
        size="xlarge"
        color="primary"
      />
    </template>
  </BottomSheet>
</template>

<script setup>
import {
  BottomSheet,
  BoxButton,
  CalendarDatePicker,
} from "@shc-nss/ui/solid";
import { format } from "date-fns";
import { ref } from "vue";

const isOpen = defineModel({ default: true });

const modelValue = ref(new Date());

function onChange(v) {
  alert("update:modelValue => " + v);
}

function onClick(v) {
  alert("clickDay => " + v);
}
</script>



```
{% endraw %}
---
