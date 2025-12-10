<route lang="yaml">
meta:
  id: select-list
  title: Select list
  menu: Module > Select list Module
  layout: EmptyLayout
  category: Module
  publish: 김대민
  publishVersion: 0.8
  navbar: false
  etc: (공통팀)원정우
</route>

<template>
  <div class="demo-title">유형 : [module] SelectList</div>
  <section class="section">
    <SelectList :items="markItems0" />
  </section>
  <div class="demo-title">유형 1 : Select Box</div>
  <!-- S : 유형 1 : Select Box (SelectBoxGroup 기본 리스트 활용) -->
  <div class="sc-select__list">
    <div class="select-list__group">
      <SelectBoxGroup
        v-model="selectBoxValue"
        :items="selectBoxItems"
        :multiple="true"
        orientation="vertical"
        variant="outline"
        as="div"
      >
        <template #contents="{ item }">
          <ListItem :left="{ mainText: item.main, subText: item.sub }" />
        </template>
      </SelectBoxGroup>
    </div>
  </div>
  <!-- E : 유형 1 : Select Box -->

  <div class="demo-title">유형 1-1 : Select Box + subAccent 텍스트</div>
  <!-- S : 유형 1-1 : Select Box (SelectBoxGroup + subAccent 텍스트) -->
  <div class="sc-select__list">
    <div class="select-list__group">
      <SelectBoxGroup
        v-model="selectBoxValue"
        :items="selectBoxItems"
        :multiple="true"
        orientation="vertical"
        variant="outline"
        as="div"
      >
        <template #contents="{ item }">
          <ListItem :left="{ mainText: item.main, subText: item.sub }">
            <template #leftSubText>
              <div
                class="flex items-center justify-start"
                v-if="!item.disabled"
              >
                <span class="sv-list__text__main"
                  >{{ item.sub
                  }}<span v-if="item.subAccent" class="sv-list__text__accent">{{
                    item.subAccent
                  }}</span></span
                >
              </div>
              <div v-else class="sc-select__disabled-alert">
                <Tooltip placement="center" />
                <span class="sc-list__text-alert">{{ item.sub }}</span>
              </div>
            </template>
          </ListItem>
        </template>
      </SelectBoxGroup>
    </div>
  </div>
  <!-- E : 유형 1-1 : Select Box -->

  <div class="demo-title">유형 1-2 : Select Box (SelectBoxGroup)</div>
  <!-- S : 유형 1-2 : Select Box (SelectBoxGroup) -->
  <div class="sc-select__list">
    <div class="select-list__group">
      <SelectList :items="markItems1" :iconSize="40" />
    </div>
  </div>
  <!-- E : 유형 1 : Select Box -->

  <div class="demo-title">유형 2 : DataList 카드 + Radio (상품)</div>
  <!-- S : 유형 2 : DataList 카드 내부에 Radio (카드 안에 라디오를 형제로 배치) -->
  <div class="sc-select__list">
    <div class="select-list__group">
      <BasicCard
        v-for="(item, i) in productItems"
        :key="`prod-${i}`"
        class="select-card"
        variant="outline"
        :selected="radioValue === item.value"
        :disabled="item.disabled"
        @contentClick="selectRadio(item)"
      >
        <!-- 라디오: 같은 그룹을 공유하도록 v-model 바인딩 -->
        <RadioCircleGroup
          v-model="radioValue"
          :items="[item]"
          orientation="vertical"
          align="left"
          name="product-radio"
        >
          <!-- 라벨 슬롯은 비움: 인디케이터만 활용 -->
          <template #label></template>
        </RadioCircleGroup>

        <!-- 타이틀 영역 -->
        <ListItem align="centered" :left="{ mainText: item.label }">
          <template v-if="item.badge" #label>
            <LineLabel :title="item.badge" color="blue" />
          </template>
        </ListItem>

        <!-- 상세 데이터 리스트 -->
        <div class="sc-data__list">
          <div class="data-list__group">
            <DataList
              v-for="(d, di) in item.details"
              :key="`pi-${di}`"
              align="spaceBetween"
            >
              <template #title>
                <span class="data-list__text">{{ d.title }}</span>
                <Tooltip placement="top-center" :content="d.tooltip" />
              </template>
              <template #content>
                <span class="data-list__text">{{ d.content }}</span>
              </template>
            </DataList>
          </div>
        </div>

        <template #actions>
          <BoxButtonGroup variant="100">
            <BoxButton color="secondary" size="medium" text="상품 설명 보기" />
          </BoxButtonGroup>
        </template>
      </BasicCard>
    </div>
  </div>
  <!-- E : 유형 2 : DataList 카드 + Radio -->

  <div class="demo-title">유형 3 : 카드(Outline) + ListItem + Check</div>
  <div class="sc-select__list">
    <!-- S : 유형 3 : 카드 Outline 내부에 체크 (다중 선택) -->
    <div class="select-list__group">
      <div v-for="(item, i) in checkItems" :key="`check-${i}`">
        <BasicCard
          class="select-card select-card__check"
          variant="outline"
          :selected="checks.includes(item.value)"
          :disabled="item.disabled"
          @contentClick="toggleCheck(item)"
        >
          <ListItem
            class="select-cardlist__item"
            align="top"
            label-orientation="column"
            :left="{
              mainText: item.main,
              subText: item.sub,
              direction: 'column',
            }"
          >
            <template #leftControl>
              <Checkbox
                :value="item.value"
                :disabled="item.disabled"
                variant="box"
                align="left"
                class="select-card__checkbox"
                :model-value="checks.includes(item.value)"
                @update:model-value="onCheck(item.value, $event)"
                @click.stop
              >
                <template #label></template>
              </Checkbox>
            </template>
            <template v-if="item.iconName" #leftIcon>
              <Icon :name="item.iconName" :size="24" aria-hidden="true" />
            </template>
            <template v-if="item.badge" #label>
              <LineLabel :title="item.badge" color="blue" size="small" />
            </template>
          </ListItem>
          <div
            v-if="item.metaLeft || item.metaRight"
            class="select-cardlist__foot"
          >
            <ListItem
              :right="{
                mainText: item.metaRight,
                subText: item.metaLeft,
                direction: 'row-reverse',
              }"
            />
          </div>
        </BasicCard>
      </div>
    </div>
  </div>
  <!-- E : 유형 3 : 카드 Outline + Check -->

  <div class="demo-title">유형 4 : Select Box - Check Icon</div>
  <!-- S : 유형 4 : Select Box - Check Icon (다중 선택) -->
  <div class="sc-select__list">
    <div class="select-list__group">
      <SelectBoxGroup
        v-model="checkSmallValue"
        :items="checkSmallItems"
        orientation="vertical"
        as="div"
      />
    </div>
  </div>
  <!-- E : 유형 4 : Select Box - Check small -->

  <div class="demo-title">유형 5 : Select list image</div>
  <!-- S : 유형 5 : Select list image (SelectBoxGroup 사용) -->
  <div class="sc-select__list">
    <div class="select-list__group select-list__image">
      <SelectBoxGroup
        v-model="imageValue"
        :items="imageItems"
        orientation="vertical"
        variant="outline"
        as="div"
      >
        <template #contents="{ item }">
          <ListItem :left="{ mainText: item.main, subText: item.sub }">
            <template #leftIcon>
              <img v-if="item.image" :src="item.image" alt="" class="thumb" />
              <Icon
                v-else
                :name="item.iconName || 'sample-icon'"
                :size="24"
                aria-hidden="true"
              />
            </template>
          </ListItem>
        </template>
      </SelectBoxGroup>
    </div>
  </div>
  <!-- E : 유형 5 : Select list image -->

  <div class="demo-title">유형 6 : Select list Symbol</div>
  <!-- S : 유형 6 : Select list Symbol -->
  <div class="sc-select__list">
    <div class="select-list__group select-list__symbol">
      <SelectBoxGroup
        v-model="choiceValue"
        :items="choiceItems"
        orientation="vertical"
        variant="outline"
        as="div"
      >
        <template #contents="{ item }">
          <ListItem
            class="select-symbol"
            align="top"
            :left="{ subText: item.sub }"
          >
            <template #leftIcon>
              <img
                v-if="item.image"
                :src="item.image"
                alt=""
                class="symbol-thumb"
              />
              <Icon
                v-else
                :name="item.iconName || 'sample-icon'"
                :size="28"
                aria-hidden="true"
              />
            </template>
            <template #leftMainText>
              <div class="select-symbol__title">
                <span class="select-symbol__name">{{ item.label }}</span>
                <SolidLabel
                  v-if="item.badge"
                  :title="item.badge"
                  :color="item.badgeColor || 'blue'"
                  size="small"
                />
              </div>
            </template>
          </ListItem>
        </template>
      </SelectBoxGroup>
    </div>
  </div>
  <!-- E : 유형 6 : Select list Symbol -->
</template>

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

<style lang="scss" scoped>
@use "@assets/styles/module/_select-list" as *; // Select list 모듈
@use "@assets/styles/module/_data-list" as *; // 유형2 DataList 재사용
</style>
