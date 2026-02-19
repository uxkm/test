
{% raw %}
```js

<route lang="yaml">
meta:
  id: SMY003A01
  title: 틴즈 도서관
  menu: 마이 > 마이 주니어 > 틴즈도서관 - 안내페이지
  layout: SubLayout
  category: 마이
  publish: 정예린
  publishVersion: 0.8
  status: 작업완료
  header:
    fixed: true
    close: false
    back: true
  qa: 검수완료
  qa2: 검수완료
</route>

<template>
  <div class="my-junior-library-page">
    <div class="tit-top-txt">
      <p>신한카드 X 교보문고</p>
    </div>
    <ScTitle
      mainTitle="10대라면 교보eBook<br />매달 1권 무료!"
      isHero
    />

    <div class="sc-contents__body">
      <div class="section">
        <!-- TBD -->
        <!-- <ScSwiper
          v-bind="argsCard"
          class="pagination-bar sc-swiper--card-select"
        >
          <template #slide="{ item }">
            <div class="swiper-item__card">
              <div class="swiper-item__card__visual">
                <img
                  :src="item.image"
                  alt=""
                />
              </div>
            </div>
          </template>
        </ScSwiper> -->
        <ScLottie
          :animation-link="$cdnURL + '/images/lottie/common/timeline_etc_info01.json'"
          autoPlay
          loop
        />
        <!-- // TBD -->

        <div class="gray-box">
          <UnorderedList :gap="4">
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="이 서비스는 신한 SOL페이 어린이・청소년(만 10세 이상~만 19세 미만)회원만 이용할 수 있는 교보문고 전자도서관 서비스에요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="만 19세 이상이 되면 더이상 틴즈 도서관을 이용할 수 없게 돼요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="매달(1일~말일 기준) 회원 1인 당 도서 1권까지 대여할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="매달 한정된 eBook 수량을 선착순으로 제공하며, 대여 가능한 수량이 조기 소진되면, 도서는 다음달 1일부터 대여할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="일부 도서는 대출 상황에 따라 예약 또는 예약대기를 해야할 수도 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="도서 대여기간은 14일이며, 대여기한이 지나면 자동으로 반납돼요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="이 서비스는 신한카드 및 제휴사의 사정에 따라 예고 없이 변경 또는 종료될 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="회원이 부적절한 방법으로 서비스를 이용했다고 판단할 경우, 예고 없이 이용을 제한할 수 있어요."
            />
            <UnorderedListItem
              variant="bullet"
              size="medium"
              text="틴즈 도서관 이용 관련 문의는 신한카드 고객센터(1544-7000), eBook 콘텐츠(오류・부적절한 콘텐츠 신고 등) 관련 내용은 제휴사인 교보문고 고객센터(1544-1900)에 문의해주세요."
            />
          </UnorderedList>
        </div>
      </div>
    </div>
  </div>

  <BottomActionContainer :scrollDim="true">
    <BoxButtonGroup size="xlarge">
      <BoxButton text="도서관 이용하기" />
    </BoxButtonGroup>
  </BottomActionContainer>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { ScLottie, ScTitle } from "@shc-nss/ui/shc";
import {
  BottomActionContainer,
  BoxButton,
  BoxButtonGroup,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";
import { inject } from "vue";
const { $cdnURL } = inject(AppContextKey);

const slidesCard = [
  {
    id: "slide-1",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-2",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-3",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-4",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
  {
    id: "slide-4",
    image: `${$cdnURL}/images/pages/my/SMY003A01_SWIPER_01.png`,
  },
];

const argsCard = {
  slides: slidesCard,
  slidesPerView: "auto",
  spaceBetween: "-4%",
  pagination: false,
  paginationType: "bullets",
  navigation: false,
  autoplay: false,
  loop: true,
  centeredSlides: true,
  theme: "default",
  speed: 300,
  direction: "horizontal",
};
</script>

<style lang="scss" scoped></style>




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
