# test

{% raw %}
```scss
// 251205
// utillity

.modal-tit {
  display: block;
  margin-bottom: var(--spacing-md);
  @include font-set("title-m", 700);
  font-weight: 700;
  color: var(--text-primary);
}
```
{% endraw %}

{% raw %}
```js

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import {
  BasicCard,
  BoxButton,
  BoxButtonGroup,
  Checkbox,
  DataList,
  Icon,
  LineLabel,
  ListItem,
  RadioCircleGroup,
  SelectBoxGroup,
  SolidLabel,
  Tooltip,
} from "@shc-nss/ui/solid";
import { inject, ref } from "vue";

const { $cdnURL } = inject(AppContextKey);
const imgSample1 = `${$cdnURL}/images/pages/demo/img-sample1.png`;
const imgSample2 = `${$cdnURL}/images/pages/demo/img-sample2.png`;
const imgSample3 = `${$cdnURL}/images/pages/demo/img-sample3.png`;

import SelectList from "../../_module/SelectList.vue";

// 유형 1: Select Box (텍스트 옵션) - 기본 리스트 + 인디케이터 사용
const selectBoxItems = [
  { label: "메인텍스트", value: "s1", main: "메인텍스트", sub: "서브텍스트" },
  { label: "메인텍스트", value: "s2", main: "메인텍스트", sub: "서브텍스트" },
  { label: "메인텍스트", value: "s3", main: "메인텍스트", sub: "서브텍스트" },
];

const selectBoxValue = ref("1");

// 유형 2: 상품형 라디오 카드 (SelectBoxGroup items)
const productItems = [
  {
    label: "공무원 신용대출",
    value: "p1",
    badge: "즉시입금",
    details: [
      { title: "메인텍스트", tooltip: "설명", content: "500만원" },
      { title: "메인텍스트", tooltip: "설명", content: "최저 연 3.85%" },
    ],
  },
  {
    label: "공무원 신용대출",
    value: "p2",
    disabled: true,
    details: [
      { title: "메인텍스트", tooltip: "설명", content: "500만원" },
      { title: "메인텍스트", tooltip: "설명", content: "최저 연 3.85%" },
    ],
  },
  {
    label: "공무원 신용대출",
    value: "p3",
    badge: "즉시입금",
    details: [
      { title: "메인텍스트", tooltip: "설명", content: "800만원" },
      { title: "메인텍스트", tooltip: "설명", content: "최저 연 4.10%" },
    ],
  },
];
const radioValue = ref("p1");

// 유형 3: 체크 다중 선택
const checkItems = [
  {
    label: "메인텍스트",
    value: "c1",
    main: "메인텍스트",
    sub: "서브텍스트",
    metaLeft: "서브텍스트",
    metaRight: "메인텍스트",
    iconName: "sample-icon",
    badge: "라벨",
  },
  {
    label: "메인텍스트",
    value: "c2",
    main: "메인텍스트",
    sub: "서브텍스트",
    metaLeft: "서브텍스트",
    metaRight: "메인텍스트",
    iconName: "sample-icon",
    disabled: true,
  },
  {
    label: "메인텍스트",
    value: "c3",
    main: "메인텍스트",
    sub: "서브텍스트",
    metaLeft: "서브텍스트",
    metaRight: "메인텍스트",
    iconName: "sample-icon",
  },
];
const checks = ref(["c1"]);

function onCheck(value, checked) {
  const s = new Set(checks.value);
  if (checked) s.add(value);
  else s.delete(value);
  checks.value = Array.from(s);
}

function selectRadio(item) {
  if (item?.disabled) return;
  radioValue.value = item.value;
}

function toggleCheck(item) {
  if (item?.disabled) return;
  const next = !checks.value.includes(item.value);
  onCheck(item.value, next);
}

// 유형 4: 체크(스몰) 다중 선택
const checkSmallItems = [
  { label: "리스트1", value: "1", showIndicator: true },
  { label: "리스트2", value: "2", showIndicator: true },
  { label: "리스트3", value: "3", showIndicator: true },
  { label: "리스트4", value: "4", showIndicator: true },
];
const checkSmallValue = ref("1");

// 유형 5: 이미지 썸네일 선택
const imageItems = [
  {
    label: "신한 Deep Dream",
    value: "i1",
    main: "신한 Deep Dream",
    sub: "서브텍스트",
    image: imgSample1,
  },
  {
    label: "신한 The Pet",
    value: "i2",
    main: "신한 The Pet",
    sub: "서브텍스트",
    disabled: true,
  },
  {
    label: "신한 The Pet",
    value: "i3",
    main: "신한 The Pet",
    sub: "서브텍스트",
  },
];
const imageValue = ref("i1");

// 유형 6: Choice 리스트 (우측 체크)
const choiceItems = [
  {
    label: "김신한",
    value: "ch1",
    sub: "서브텍스트",
    image: imgSample2,
  },
  {
    label: "이국민",
    value: "ch2",
    sub: "서브텍스트",
    image: imgSample2,
    badge: "만료예정",
    badgeColor: "red",
  },
  {
    label: "이국민",
    value: "ch3",
    sub: "서브텍스트",
    image: imgSample3,
    badge: "만료",
    badgeColor: "gray",
    disabled: true,
  },
];
const choiceValue = ref("ch1");
const markItems0 = [
  {
    value: "c1",
    iconName: "sample-icon",
    main: "메인텍스트",
    selected: true,
    // rightText: "rightText",
  },
  {
    value: "c2",
    iconName: "sample-icon",
    main: "메인텍스트",
  },
  {
    value: "c3",
    main: "메인텍스트",
  },
  {
    value: "c4",
    main: "메인텍스트",
  },
];
const markItems1 = [
  // icon case sample
  {
    value: "c1",
    iconName: "shinhan",
    main: "신한 무지 만능계좌",
    sub: "11024*****32",
    rightText: "240,000원",
    selected: true,
  },
  {
    value: "c2",
    iconName: "sample-icon",
    main: "신한 무지 만능계좌",
    sub: "11024*****32",
    rightText: "240,000원",
  },
  // image case sample
  {
    value: "c3",
    image: imgSample2, // image url
    main: "신한 무지 만능계좌",
    sub: "11024*****32",
    rightText: "240,000원",
  },
  {
    value: "c4",
    image: imgSample3,
    main: "국민은행 급여 계좌",
    sub: "11024*****32",
    rightText: "240,000원",
  },
];
</script>
```
{% endraw %}

---
