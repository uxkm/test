
{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT137A02
  title: 쿠폰 검색
  menu: "혜택 > 할인 쿠폰 메인화면 > 쿠폰 전체보기 > 쿠폰검색"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    menu: false
    home: true
  appClassList: "sc-coupon__ongoing-search"
  mainClassList: "coupon-ongoing__main-search"
</route>
<template>
  <div
    :class="[
      'sc-category__group coupon-ongoing__search',
      { 'is-typing': searchKeyword && searchKeyword.length > 0 },
    ]"
  >
    <!-- 
      진행 중 이벤트 인 경우 노출
      검색 필드는 SOLID에서 제공한 UI가 없어서 별도 작업 
    -->
    <div class="category-filter__search full-width">
      <div
        :class="[
          'category-filter__search-field',
          { 'is-focus': isInputFocused },
        ]"
      >
        <IconButton
          iconName="Search"
          size="small"
          :color="false"
          class="category-filter__search-icon"
          aria-label="쿠폰 검색"
          @click="openSearch"
        />
        <div class="category-filter__search-input">
          <div class="category-filter__search-input-inner">
            <label class="custom-input">
              <input
                ref="searchInputRef"
                v-model="searchKeyword"
                type="text"
                placeholder="마이샵, 탑스, 맛있는 쿠폰 검색"
                @focus="isInputFocusedState = true"
                @blur="isInputFocusedState = false"
                @input="handleSearchInput"
                @compositionend="handleSearchInput"
              />
            </label>
            <IconButton
              v-if="searchKeyword"
              iconName="Solid_circle_x"
              size="small"
              :color="false"
              class="category-filter__search-input-clear"
              aria-label="검색어 삭제"
              @click.stop.prevent="clearSearch"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- 최근 검색어 -->
  <KeywordChipGroup
    v-if="!searchKeyword || searchKeyword.length === 0"
    :items="keywordSearchItems"
    size="small"
    color="gray"
    variant="solid"
    :deletable="true"
    control="none"
  />
  <div class="sc-contents__body coupon-ongoing">
    <div class="cupon-contents">
      <div class="cupon-list__wrap">
        <div
          v-if="!searchKeyword || searchKeyword.length === 0"
          class="cupon-list__head list-head"
        >
          <div class="cupon-head__text-left">
            <strong class="cupon-head__text"> 최근 찾아본 쿠폰 </strong>
          </div>
          <div class="cupon-head__text-right">
            <TextButtonUnderline
              text="전체삭제"
              size="xsmall"
              color="secondary"
              @click="openDeleteAllModal"
            />
          </div>
        </div>
        <div class="cupon-list__body">
          <!-- 링크인 경우에만 role="link" 추가 -->
          <div
            v-for="coupon in filteredCoupons"
            :key="coupon.id"
            :class="[
              'cupon-item outline',
              { 'is-label': coupon.label || coupon.expiryDate },
            ]"
            role="link"
          >
            <ListItem align="centered" :left="{ direction: 'reverse' }">
              <template #label v-if="coupon.label || coupon.expiryDate">
                <div class="flex gap-4">
                  <!-- 쿠폰 상태 -->
                  <SolidLabel
                    v-if="coupon.label"
                    :title="coupon.label"
                    :color="coupon.labelColor || 'blue'"
                    class="inline-flex"
                  />
                  <!-- 만료일 -->
                  <TintLabel
                    v-if="coupon.expiryDate"
                    :title="coupon.expiryDate"
                    :color="coupon.expiryDateColor || 'blue'"
                  />
                </div>
              </template>
              <template #leftSubText>
                <span aria-hidden="true">{{ coupon.sub }}</span>
              </template>
              <template #leftMainText>
                <strong
                  aria-hidden="true"
                  class="sv-list__text__main"
                  v-html="highlightText(coupon.main, searchKeyword)"
                ></strong>
              </template>
              <template #rightIcon>
                <img
                  :src="coupon.icon.src"
                  :alt="coupon.icon.alt"
                  class="cupon-icon"
                  aria-hidden="true"
                />
              </template>
              <template
                v-if="!searchKeyword || searchKeyword.length === 0"
                #rightControl
              >
                <IconButton
                  iconName="X"
                  size="16"
                  :aria-label="`${coupon.main} 쿠폰 삭제`"
                  @click="deleteCoupon(coupon.id)"
                />
              </template>
            </ListItem>
          </div>
        </div>
      </div>

      <!-- 검색 결과가 없을 경우 -->
      <NoData v-if="showSearchNoData" :mainText="searchNoDataText" />
    </div>
  </div>

  <!-- 최근 찾아본 쿠폰 기록을 모두 삭제 -->
  <ModalPopup title="" v-model="isOpen" align="center">
    <p class="sc-preline">{{ message }}</p>
    <template #footer>
      <BoxButton @click="isOpen = false" text="취소" color="secondary" />
      <BoxButton @click="deleteAllCoupons" text="계속" />
    </template>
  </ModalPopup>
</template>

<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import useToastStore from "@/stores/common/toast";
import { ScIcon } from "@shc-nss/ui/shc";
import {
  BoxButton,
  CapsuleButton,
  KeywordChipGroup,
  ListItem,
  SolidLabel,
  TextButtonUnderline,
  TintLabel,
  IconButton,
  ModalPopup,
} from "@shc-nss/ui/solid";
import { computed, inject, onUnmounted, ref } from "vue";

import NoData from "../../_module/NoData.vue";

const { $cdnURL } = inject(AppContextKey);
const { toast, addToast, updateConfig } = useToastStore();

// 팝업 상태 관리
const isOpen = ref(false);

const message = "최근 찾아본 쿠폰 기록을 모두 삭제할까요?";

// 전체 삭제 모달 열기
function openDeleteAllModal() {
  isOpen.value = true;
}

// 전체 쿠폰 삭제
function deleteAllCoupons() {
  // 모든 쿠폰 ID를 삭제 목록에 추가
  deletedCouponIds.value = couponItems.map((coupon) => coupon.id);
  isOpen.value = false;
  addToast("최근 찾아본 쿠폰을 삭제했습니다.", {
    position: "bottom",
    offset: 52,
    color: "dark",
  });
}

// 초기 설정 저장
const initialConfig = {
  defaultColor: "dark",
  offset: 52,
};

// 초기 설정으로 되돌리는 함수
const initConfig = () => {
  updateConfig(initialConfig);
};

const showReceivedOnly = ref(false);
const searchKeyword = ref("");
const isInputFocusedState = ref(false);
const searchInputRef = ref(null);
const deletedCouponIds = ref([]);

// 최근 검색어 데이터
const keywordSearchItems = ref([
  { text: "스타벅스", value: "스타벅스" },
  { text: "배달의민족", value: "배달의민족" },
  { text: "마이샵", value: "마이샵" },
  { text: "탑스", value: "탑스" },
]);

// 인풋에 값이 있으면 is-focus 유지
const isInputFocused = computed(() => {
  return (
    isInputFocusedState.value ||
    (searchKeyword.value && searchKeyword.value.length > 0)
  );
});

const filteredCoupons = computed(() => {
  let base = couponItems;

  if (showReceivedOnly.value) {
    base = base.filter((coupon) => coupon.received);
  }

  // 삭제된 쿠폰 제외
  base = base.filter((coupon) => !deletedCouponIds.value.includes(coupon.id));

  // 검색어 필터링
  if (searchKeyword.value && searchKeyword.value.length > 0) {
    const keyword = searchKeyword.value.toLowerCase();
    base = base.filter(
      (coupon) =>
        coupon.main.toLowerCase().includes(keyword) ||
        coupon.sub.toLowerCase().includes(keyword)
    );
  }

  return base;
});

// 설정 업데이트 함수
const onUpdateConfig = () => {
  updateConfig({
    defaultColor: "light",
  });
};

// 초기 설정 함수
const onInitConfig = () => initConfig();

// 컴포넌트 언마운트 시 초기 설정으로 복원
onUnmounted(() => initConfig());

const showReceivedNoData = computed(
  () => showReceivedOnly.value && filteredCoupons.value.length === 0
);

const showFilteredNoData = computed(
  () => !showReceivedOnly.value && filteredCoupons.value.length === 0
);

// 검색 결과가 없을 경우
const showSearchNoData = computed(
  () =>
    searchKeyword.value &&
    searchKeyword.value.length > 0 &&
    filteredCoupons.value.length === 0
);

// 검색 결과 없음 메시지 (검색 키워드를 em 태그로 감싸기)
const searchNoDataText = computed(() => {
  if (!searchKeyword.value || searchKeyword.value.length === 0) {
    return "";
  }
  return `'<em>${searchKeyword.value}</em>'에 대한 검색 결과가 없습니다.`;
});

// 검색어 하이라이트 함수
function highlightText(text, keyword) {
  if (!keyword || keyword.length === 0) {
    return text;
  }
  // 공백 없이도 검색어가 매칭되도록 trim하지 않고 사용
  const searchTerm = keyword.replace(/[.*+?^${}()|[\]\\]/g, "\\$&");
  const regex = new RegExp(`(${searchTerm})`, "gi");
  return text.replace(regex, "<em>$1</em>");
}

// 검색 열기 함수
function openSearch() {
  if (searchInputRef.value) {
    searchInputRef.value.focus();
  }
}

// 검색어 삭제 함수
function clearSearch() {
  searchKeyword.value = "";
  if (searchInputRef.value) {
    searchInputRef.value.focus();
  }
}

// 검색어 입력 핸들러 (한글 입력 대응)
function handleSearchInput(event) {
  searchKeyword.value = event.target.value;
}

// 쿠폰 삭제 함수
function deleteCoupon(couponId) {
  deletedCouponIds.value.push(couponId);
  addToast("최근 찾아본 쿠폰을 삭제했습니다.", {
    position: "bottom",
    offset: 52,
    color: "dark",
  });
}

// 쿠폰 리스트 데이터 (이미지 참조)
const couponItems = [
  {
    categoryType: "카페 다이닝",
    id: 1,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    label: "이벤트",
    labelColor: "blue",
    expiryDate: "D-14",
    expiryDateColor: "blue",
    main: "마이카플러스 신규 가입 이벤트마이카플러스 신규 가입 이벤트신규 가입 이벤트",
    sub: "배달의 민족 5,000원건배달의 민족 5,000원건 5,000원건",
  },
  {
    categoryType: "여가 스포츠",
    id: 2,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    main: "[이벤트] 아이스 카페 아메리카노",
    sub: "스타벅스",
  },
  {
    categoryType: "라이프서비스",
    id: 3,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    expiryDate: "D-14",
    main: "[이벤트] 아이스 카페 아메리카노",
    sub: "서브웨이",
  },
  {
    categoryType: "쇼핑",
    id: 4,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "스탬프 쿠폰을 찾고 계세요?",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "헬스",
    id: 5,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    expiryDate: "D-Day",
    main: "최대 20만원 캐시백 받기",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "반려동물",
    id: 6,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    main: "Tops 쿠폰",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "패션 뷰티",
    id: 7,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    main: "신세계 백화점 상품권 포함 5가지 혜택 받기",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "여행",
    id: 8,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    main: "스타벅스 쿠폰 받기",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "금융 렌탈",
    id: 9,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon7.png`,
      alt: "",
    },
    main: "해외여행 필수템",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "자동차",
    id: 10,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "1등 당첨되면 발뮤다 더 토스트",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "육아 교육",
    id: 11,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "1등 당첨되면 발뮤다 더 토스트",
    sub: "신한 Super SOL",
  },
  {
    categoryType: "기타",
    id: 12,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    main: "1등 당첨되면 발뮤다 더 토스트",
    sub: "신한 Super SOL",
  },
];
</script>


```
{% endraw %}
---
