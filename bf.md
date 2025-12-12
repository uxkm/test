# SBT108A02

{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT108A02
  title: 이벤트
  menu: "혜택 > 이벤트 메인화면 > 이벤트 전체보기: 진행중 이벤트 > 검색"
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업완료
  etc: "SBT108A02(진행중인 이벤트), SBT119A01(이벤트 검색), SBT162A01(이벤트 선택 BS), SBT120A01(조회기간 선택 BS)"
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    home: true
</route>
<template>
  <div class="sc-category__group search-type">
    <div class="category-filter">
      <div class="category-filter__left">
        <TextDropdown
          ref="categoryDropdownRef"
          placeholder="카테고리"
          size="large"
          @click="openCategorySheet"
        >
          <template #value>
            <span :class="['category-filter__label', { 'is-active': true }]">
              {{ selectedCategoryLabel }}
            </span>
          </template>
        </TextDropdown>
      </div>
      <div class="category-filter__right">
        <BoxButton
          text="응모 이력"
          variant="box"
          color="quaternary"
          size="small"
        >
          <template #icon>
            <ScIcon iconName="icon-note" size="16" />
          </template>
        </BoxButton>
      </div>
    </div>

    <!-- 
      검색 필드 노출
      검색 필드는 SOLID에서 제공한 UI가 없어서 별도 작업 
    -->
    <div class="category-filter__search">
      <div
        class="category-filter__search-field"
        :class="{
          'is-focus': isSearchMode,
        }"
      >
        <IconButton
          iconName="Search"
          size="small"
          :color="false"
          class="category-filter__search-icon"
          aria-label="이벤트 검색"
          @click="openSearch"
        />
        <div v-show="isSearchMode" class="category-filter__search-input">
          <div class="category-filter__search-input-inner">
            <label class="custom-input">
              <input
                ref="searchInputRef"
                v-model="searchKeyword"
                type="text"
                placeholder="원하는 이벤트를 검색해보세요"
                @focus="isInputFocused = true"
                @blur="isInputFocused = false"
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
          <TextButton
            text="취소"
            color="secondary"
            size="small"
            class="category-filter__search-cancel"
            @click="closeSearch"
          />
        </div>
      </div>
      <div v-show="!isSearchMode" class="category-filter__search-chip">
        <BasicChipGroup
          control="expand"
          :items="items"
          variant="solid"
          v-model="selectedValue"
        />
      </div>
    </div>
  </div>

  <div class="sc-contents__body">
    <div class="category-contents">
      <div class="category-list__wrap">
        <div class="category-list__body">
          <!-- 링크인 경우에만 role="link" tabindex="0" aria-label="이벤트 정보" 추가 -->
          <div
            v-for="item in displayedItems"
            :key="item.id"
            class="category-item"
            role="link"
            tabindex="0"
            :aria-label="
              [
                item?.categoryType === '종료 이벤트' ? '종료 이벤트' : null,
                item?.label,
                item?.sub,
                item?.main,
                item?.rightLabel,
              ]
                .filter((val) => val != null && val !== '')
                .join(' ')
            "
          >
            <!-- 링크인 경우는 aria-hidden="true" 추가 아닌 경우엔 제거 초점 간소화 -->
            <ListItem
              align="centered"
              :left="{ direction: 'reverse' }"
              :class="{
                'ended-event-item': item.categoryType === '종료 이벤트',
              }"
              aria-hidden="true"
            >
              <template #leftIcon>
                <ScImage
                  :src="item.icon.src"
                  :alt="item.icon.alt"
                  class="category-icon"
                  aria-hidden="true"
                />
                <span
                  v-if="item.categoryType === '종료 이벤트'"
                  class="ended-event-badge"
                >
                  종료
                </span>
              </template>
              <template #leftSubText>
                <TintLabel
                  :title="item.label"
                  :color="item.labelColor || 'green'"
                  v-if="item.label"
                  class="inline-flex"
                />
                <span
                  class="text"
                  v-html="highlightSearchKeyword(item.sub)"
                ></span>
              </template>
              <template #leftMainText>
                <strong v-html="highlightSearchKeyword(item.main)"></strong>
              </template>
              <template #rightControl>
                <TintLabel
                  v-if="item.rightLabel"
                  :title="item.rightLabel"
                  :color="item.rightLabelColor || 'blue'"
                />
              </template>
            </ListItem>
          </div>
        </div>

        <!-- 기본적으로 결과값은 최대 8개 제공, 더보기 선택시 8개식 추가 제공 -->
        <ButtonPagination
          v-if="showMoreButton"
          :current="1"
          iconName="Arrow_refresh"
          title="더보기"
          @click="loadMore"
        />
      </div>

      <!-- 진행 중 이벤트 없음 -->
      <NoData v-if="showOngoingNoData" mainText="진행중인 이벤트가 없습니다." />
      <!-- 진행 중 이벤트 검색 결과 없음 -->
      <NoData v-else-if="showSearchNoData" mainText="검색된 이벤트가 없어요" />

      <!-- 종료 이벤트 없음 -->
      <NoData v-else-if="showEndedNoData" mainText="지난 이벤트가 없습니다." />
    </div>
  </div>

  <!-- floating top button 추가 -->
  <FabScrollTop
    ariaLabel="화면 상단으로 이동"
    :bottom="20"
    :right="20"
    :offset="20"
    :overlayOffset="20"
    :revealDelta="-0.1"
    :showThreshold="0"
    color="primary"
    layoutStrategy="overlaySafeArea"
    overlayActive
    overlayIncludeMargins
    overlayPosition="bottom"
    size="medium"
    class="sc-floating__topbtn"
  />

  <!-- 카테고리 선택 바텀시트 SBT162A01 -->
  <BottomSheet
    closableDimm
    dimmed
    title="이벤트를 선택해주세요"
    v-model="isCategorySheetOpen"
    class="category-sheet not-padding-t"
  >
    <div class="sc-list sc-select__list mark full">
      <div class="select-list__group">
        <div
          v-for="(item, i) in categories"
          :key="`category-${i}`"
          class="select-list__item"
        >
          <BasicCard
            class="select-card select-card__check"
            variant="white"
            :disabled="item.disabled"
            @contentClick="toggleCategoryMark(item)"
            :selected="setCategoryMark(item)"
          >
            <ListItem
              class="select-cardlist__item"
              align="centered"
              :left="{ mainText: item.main }"
              :class="{ 'disabled-item': item.disabled }"
            >
              <template #rightControl>
                <Checkbox
                  :value="item.value"
                  :disabled="item.disabled"
                  variant="mark"
                  align="left"
                  class="select-card__checkbox"
                  :model-value="setCategoryMark(item)"
                  @update:model-value="onCategoryMark(item.value, $event)"
                  @click.stop
                />
              </template>
            </ListItem>
          </BasicCard>
        </div>
      </div>
    </div>
  </BottomSheet>

  <!-- 조회기간 월 선택 바텀시트 SBT120A01 -->
  <BottomSheet
    closableDimm
    dimmed
    title="조회 기간 선택"
    v-model="isMonthSheetOpen"
    class="not-padding-t"
  >
    <!-- 월 조회 필터 -->
    <div class="month-filter__header full-width">
      <DatePicker v-model:viewDate="viewDate" class="month-filter__datepicker">
        <template #header>
          <IconButton
            class="sv-datepicker__header-btn sv-datepicker__header-btn--prev"
            size="large"
            @click="goPrevMonth"
            :aria-label="prevMonthAriaLabel"
          >
            <template #icon>
              <Icon
                name="Chevron_left"
                :fixed-size="false"
                aria-hidden="true"
              />
            </template>
          </IconButton>
          <h2
            class="sv-datepicker__title"
            tabindex="0"
            :aria-label="currentMonthAriaLabel"
          >
            <span class="sv-datepicker__title-content" aria-hidden="true">
              {{ monthTitle }}
            </span>
          </h2>
          <IconButton
            class="sv-datepicker__header-btn sv-datepicker__header-btn--next"
            size="large"
            @click="goNextMonth"
            :aria-label="nextMonthAriaLabel"
          >
            <template #icon>
              <Icon
                name="Chevron_right"
                :fixed-size="false"
                aria-hidden="true"
              />
            </template>
          </IconButton>
        </template>
      </DatePicker>
    </div>
    <div class="month-filter__body">
      <SelectBoxGroup
        :items="monthItems"
        v-model="selectedMonthValue"
        orientation="horizontal"
        @update:model-value="onSelectMonth"
        class="month-filter__grid"
        aria-label="월 선택"
      >
        <template #contents="{ item }">
          <span class="sv-select-box__label" :aria-label="item['aria-label']">{{
            item.displayLabel
          }}</span>
        </template>
      </SelectBoxGroup>
    </div>
    <template #footer>
      <BoxButton
        @click="applyMonth"
        text="확인"
        size="xlarge"
        color="primary"
      />
    </template>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { AppContextKey } from "@/configs/inject/appContext";
import { ScIcon, ScImage } from "@shc-nss/ui/shc";
import {
  BottomSheet,
  BoxButton,
  Checkbox,
  ListItem,
  TextButton,
  TextDropdown,
  TintLabel,
  FabScrollTop,
  BasicChipGroup,
  IconButton,
  ButtonPagination,
  BasicCard,
  InlineDropdown,
  DatePicker,
  SelectBoxGroup,
  Icon,
} from "@shc-nss/ui/solid";
import { computed, inject, ref, nextTick, watch } from "vue";
import { addMonths, format, startOfMonth, getYear } from "date-fns";
import { ko } from "date-fns/locale";

import NoData from "../../_module/NoData.vue";

// ==========================================
// Inject
// ==========================================
// CDN URL 주입
const { $cdnURL } = inject(AppContextKey);

// ==========================================
// 카테고리 데이터
// ==========================================
// 카테고리 선택 바텀시트에 표시될 카테고리 목록
const categories = [
  {
    value: "ongoing",
    main: "진행 중 이벤트",
    selected: true,
  },
  {
    value: "ended",
    main: "종료 이벤트",
    selected: false,
  },
];

// ==========================================
// 카테고리 필터 상태
// ==========================================
// 카테고리 선택 바텀시트 열림/닫힘 상태
const isCategorySheetOpen = ref(false);
// 현재 선택된 카테고리 값
const selectedCategory = ref(null);
// 바텀시트에서 선택한 임시 카테고리 값 (적용 전)
const nextCategoryValue = ref("ongoing");
// 카테고리 드롭다운 DOM 참조
const categoryDropdownRef = ref(null);
// 월 선택 바텀시트 열림/닫힘 상태
const isMonthSheetOpen = ref(false);
// DatePicker 관련 상태
const today = new Date();
const viewDate = ref(new Date());
// 선택된 월 값 (임시)
const nextMonthValue = ref("5");
// 선택된 월 값 (적용됨)
const selectedMonthValue = ref("5");

// ==========================================
// 검색 필드 상태
// ==========================================
// 검색어 입력값
const searchKeyword = ref("");
// 검색 입력 필드 포커스 상태
const isInputFocused = ref(false);
// 검색 입력 필드 DOM 참조
const searchInputRef = ref(null);
// 검색 모드 활성화 여부 (검색 입력 필드 표시/숨김)
const isSearchMode = ref(true);
// 선택된 칩 값 (기본값: "전체")
const selectedValue = ref("all");
// 표시할 항목 수 (기본값: 8개)
const displayedCount = ref(8);

// ==========================================
// 검색 관련 함수
// ==========================================
/**
 * 검색 모드 활성화
 * - 검색 아이콘 버튼 클릭 시 호출
 * - 검색 입력 필드를 표시하고 포커스 이동
 */
function openSearch() {
  isSearchMode.value = true;
  nextTick(() => {
    if (searchInputRef.value) {
      searchInputRef.value.focus();
    }
  });
}

/**
 * 검색 모드 비활성화
 * - 취소 버튼 클릭 시 호출
 * - 검색어 초기화 및 검색 아이콘 버튼으로 포커스 이동
 */
async function closeSearch() {
  isSearchMode.value = false;
  searchKeyword.value = "";
  // 다음 틱에서 검색 아이콘 버튼에 초점 이동
  await nextTick();
  // 검색 아이콘 버튼 요소 찾기
  const searchIconButton = document.querySelector(
    ".category-filter__search-icon button"
  );
  if (searchIconButton instanceof HTMLButtonElement) {
    searchIconButton.focus();
  }
}

/**
 * 검색어 삭제
 * - 검색 입력 필드 내 삭제 아이콘 클릭 시 호출
 * - 검색어 초기화 및 입력 필드에 포커스 유지
 */
async function clearSearch(event) {
  event?.preventDefault?.();
  event?.stopPropagation?.();
  searchKeyword.value = "";
  // 다음 틱에서 input에 초점 유지
  await nextTick();
  if (searchInputRef.value) {
    searchInputRef.value.focus();
  }
}

// ==========================================
// 칩 그룹 데이터
// ==========================================
// 검색 필터 칩 그룹 아이템 목록
const items = [
  { text: "전체", value: "all" },
  { text: "쇼핑·문화", value: "shopping_culture" },
  { text: "앱테크", value: "apptech" },
  { text: "여행·숙박", value: "travel_accommodation" },
  { text: "카드·결제", value: "card_payment" },
  { text: "청소년", value: "youth" },
];

// ==========================================
// Computed Properties
// ==========================================
/**
 * 선택된 카테고리 라벨
 * - 카테고리 드롭다운에 표시될 텍스트
 * - 선택된 카테고리가 없으면 "진행 중 이벤트" 반환
 */
const selectedCategoryLabel = computed(() => {
  if (!selectedCategory.value) {
    return "진행 중 이벤트";
  }
  const found = categories.find(
    (category) => category.value === selectedCategory.value
  );
  return found ? found.main : "진행 중 이벤트";
});

/**
 * 필터링된 이벤트 목록
 * - 선택된 카테고리 및 받은 이벤트만 보기 필터에 따라 이벤트 목록 필터링
 * - 검색어가 있으면 검색어로 필터링
 */
const filteredItems = computed(() => {
  const activeCategory = selectedCategory.value || "ongoing";
  // 선택된 카테고리에 따라 데이터 소스 선택
  const sourceItems = activeCategory === "ongoing" ? ongoingItems : endedItems;

  let base = sourceItems;

  // 칩 선택 필터링
  if (selectedValue.value && selectedValue.value !== "all") {
    base = base.filter((item) => item.chipType === selectedValue.value);
  }

  // 검색어 필터링
  if (searchKeyword.value && searchKeyword.value.trim()) {
    const keyword = searchKeyword.value.trim().toLowerCase();
    // 검색어를 공백으로 분리하여 각 단어가 포함되어 있는지 확인
    const keywords = keyword.split(/\s+/).filter((k) => k.length > 0);
    base = base.filter((item) => {
      const searchText =
        `${item.main || ""} ${item.sub || ""} ${item.label || ""}`.toLowerCase();
      // 모든 검색어 단어가 포함되어 있는지 확인
      return keywords.every((kw) => searchText.includes(kw));
    });
  }

  return base;
});

/**
 * 표시할 이벤트 목록 (페이지네이션 적용)
 */
const displayedItems = computed(() => {
  return filteredItems.value.slice(0, displayedCount.value);
});

/**
 * 더보기 버튼 표시 여부
 */
const showMoreButton = computed(() => {
  return filteredItems.value.length > displayedCount.value;
});

/**
 * 진행 중 이벤트 없음 데이터 표시 여부
 */
const showOngoingNoData = computed(
  () =>
    (selectedCategory.value === "ongoing" || !selectedCategory.value) &&
    !isSearchMode.value &&
    !searchKeyword.value &&
    filteredItems.value.length === 0
);

/**
 * 종료 이벤트 없음 데이터 표시 여부
 */
const showEndedNoData = computed(
  () =>
    selectedCategory.value === "ended" &&
    !isSearchMode.value &&
    !searchKeyword.value &&
    filteredItems.value.length === 0
);

/**
 * 검색 결과 없음 데이터 표시 여부
 */
const showSearchNoData = computed(
  () =>
    isSearchMode.value &&
    searchKeyword.value &&
    filteredItems.value.length === 0
);

/**
 * 더보기 버튼 클릭 핸들러
 * - 다음 8개 항목 추가 표시
 * - 새로 로드된 첫 번째 항목에 초점 이동
 */
async function loadMore() {
  const previousCount = displayedCount.value;
  displayedCount.value += 8;

  // DOM 업데이트 후 새로 추가된 첫 번째 항목에 초점 이동
  await nextTick();
  const categoryItems = document.querySelectorAll(".category-item");
  if (categoryItems.length > previousCount) {
    const firstNewItem = categoryItems[previousCount];
    if (firstNewItem instanceof HTMLElement) {
      firstNewItem.focus();
    }
  }
}

/**
 * 필터 변경 시 표시 항목 수 초기화
 */
watch([selectedCategory, selectedValue, searchKeyword], () => {
  displayedCount.value = 8;
});

// ==========================================
// 월 선택 바텀시트 관련
// ==========================================
/**
 * 선택된 월 라벨
 */
const selectedMonthLabel = computed(() => {
  const year = getYear(viewDate.value);
  const month = selectedMonthValue.value;
  return `${year}년 ${month}월`;
});

/**
 * DatePicker 제목 (년도만 표시)
 */
const monthTitle = computed(() => {
  return format(viewDate.value, "yyyy년", { locale: ko });
});

/**
 * 현재 년도 aria-label
 */
const currentMonthAriaLabel = computed(() => {
  return `현재 ${monthTitle.value}`;
});

/**
 * 이전 년도 aria-label
 */
const prevMonthAriaLabel = computed(() => {
  const prevMonth = addMonths(viewDate.value, -1);
  const prevYear = getYear(prevMonth);
  return `이전 ${prevYear}년도 선택`;
});

/**
 * 다음 년도 aria-label
 */
const nextMonthAriaLabel = computed(() => {
  const nextMonth = addMonths(viewDate.value, 1);
  const nextYear = getYear(nextMonth);
  return `다음 ${nextYear}년도 선택`;
});

/**
 * 월 선택 아이템 (1월 ~ 12월)
 */
const monthItems = computed(() => {
  const year = getYear(viewDate.value);
  return [
    {
      value: "1",
      label: "1월",
      displayLabel: "1월",
      "aria-label": `${year}년 1월`,
    },
    {
      value: "2",
      label: "2월",
      displayLabel: "2월",
      "aria-label": `${year}년 2월`,
    },
    {
      value: "3",
      label: "3월",
      displayLabel: "3월",
      "aria-label": `${year}년 3월`,
    },
    {
      value: "4",
      label: "4월",
      displayLabel: "4월",
      "aria-label": `${year}년 4월`,
    },
    {
      value: "5",
      label: "5월",
      displayLabel: "5월",
      "aria-label": `${year}년 5월`,
    },
    {
      value: "6",
      label: "6월",
      displayLabel: "6월",
      "aria-label": `${year}년 6월`,
    },
    {
      value: "7",
      label: "7월",
      displayLabel: "7월",
      "aria-label": `${year}년 7월`,
    },
    {
      value: "8",
      label: "8월",
      displayLabel: "8월",
      "aria-label": `${year}년 8월`,
    },
    {
      value: "9",
      label: "9월",
      displayLabel: "9월",
      "aria-label": `${year}년 9월`,
    },
    {
      value: "10",
      label: "10월",
      displayLabel: "10월",
      "aria-label": `${year}년 10월`,
    },
    {
      value: "11",
      label: "11월",
      displayLabel: "11월",
      "aria-label": `${year}년 11월`,
    },
    {
      value: "12",
      label: "12월",
      displayLabel: "12월",
      "aria-label": `${year}년 12월`,
    },
  ];
});

/**
 * 월 선택 바텀시트 열기
 */
function openMonthSheet() {
  nextMonthValue.value = selectedMonthValue.value;
  // 현재 선택된 월의 년도로 viewDate 설정
  const currentYear = getYear(new Date());
  viewDate.value = new Date(
    currentYear,
    parseInt(selectedMonthValue.value) - 1,
    1
  );
  isMonthSheetOpen.value = true;
}

/**
 * 이전 년도로 이동
 */
function goPrevMonth() {
  viewDate.value = startOfMonth(addMonths(viewDate.value, -1));
}

/**
 * 다음 년도로 이동
 */
function goNextMonth() {
  viewDate.value = startOfMonth(addMonths(viewDate.value, 1));
}

/**
 * 월 선택 핸들러
 */
function onSelectMonth(value) {
  nextMonthValue.value = value;
}

/**
 * 월 적용
 */
function applyMonth() {
  selectedMonthValue.value = nextMonthValue.value;
  isMonthSheetOpen.value = false;
}

/**
 * 검색어를 <em> 태그로 감싸서 강조하는 함수
 */
function highlightSearchKeyword(text) {
  if (!text || !searchKeyword.value || !searchKeyword.value.trim()) {
    return text;
  }
  // 검색어를 공백으로 분리하여 각 단어를 개별적으로 강조
  const keywords = searchKeyword.value
    .trim()
    .split(/\s+/)
    .filter((k) => k.length > 0);
  let result = text;

  // 각 검색어 단어를 순차적으로 강조
  keywords.forEach((keyword) => {
    const escapedKeyword = keyword.replace(/[.*+?^${}()|[\]\\]/g, "\\$&");
    // 텍스트 노드만 찾기 (HTML 태그 제외)
    const parts = result.split(/(<[^>]+>)/);
    result = parts
      .map((part) => {
        // HTML 태그는 그대로 유지
        if (part.startsWith("<")) {
          return part;
        }
        // 텍스트 부분에서만 검색어 강조
        const regex = new RegExp(`(${escapedKeyword})`, "gi");
        return part.replace(regex, "<em>$1</em>");
      })
      .join("");
  });

  return result;
}

// ==========================================
// 카테고리 관련 함수
// ==========================================
/**
 * 카테고리 선택 바텀시트 열기
 * - 현재 선택된 카테고리 값을 임시 값으로 설정
 */
function openCategorySheet() {
  nextCategoryValue.value = selectedCategory.value || "ongoing";
  isCategorySheetOpen.value = true;
}

/**
 * 카테고리 체크박스 업데이트
 */
function onCategoryMark(value, checked) {
  if (checked) {
    nextCategoryValue.value = value;
    // 선택 시 바로 적용하고 바텀시트 닫기
    applyCategory();
  } else if (nextCategoryValue.value === value) {
    nextCategoryValue.value = "ongoing";
    applyCategory();
  }
}

/**
 * 카테고리 카드 클릭
 */
function toggleCategoryMark(item) {
  if (item?.disabled) return;
  if (nextCategoryValue.value === item.value) {
    return;
  }
  nextCategoryValue.value = item.value;
  // 선택 시 바로 적용하고 바텀시트 닫기
  applyCategory();
}

/**
 * 카테고리 체크박스 선택 상태 확인
 */
function setCategoryMark(item) {
  if (nextCategoryValue.value === null || nextCategoryValue.value === "") {
    return item.value === "ongoing";
  }
  return nextCategoryValue.value === item.value;
}

/**
 * 카테고리 초기화
 * - 바텀시트에서 초기화 버튼 클릭 시 호출
 */
function resetCategory() {
  nextCategoryValue.value = "ongoing";
}

/**
 * 카테고리 적용
 * - 바텀시트에서 적용 버튼 클릭 시 호출
 * - 임시 카테고리 값을 실제 선택값으로 적용
 */
async function applyCategory() {
  selectedCategory.value = nextCategoryValue.value;
  isCategorySheetOpen.value = false;
  // 바텀시트가 닫힌 후 TextDropdown 버튼에 초점 이동
  await nextTick();
  // 카테고리 드롭다운 버튼 찾기
  const categoryDropdownButton = document.querySelector(
    '.category-filter__left button, .category-filter__left [role="button"]'
  );
  if (categoryDropdownButton instanceof HTMLElement) {
    categoryDropdownButton.focus();
  }
}

// ==========================================
// 이벤트 데이터
// ==========================================
// 진행 중 이벤트 데이터
const ongoingItems = [
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 1,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    rightLabel: "D-14",
    rightLabelColor: "blue",
    sub: "IKEA 신한카드로 결제하고",
    main: "최대 10만원 캐시백 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "apptech",
    id: 2,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    rightLabel: "D-Day",
    sub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "최대 20만원 캐시백 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "travel_accommodation",
    id: 3,
    received: false,
    label: "이벤트 모음.zip",
    labelColor: "green",
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    sub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "Tops 쿠폰",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "card_payment",
    id: 4,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    sub: "캐시백부터 할인까지 꼼꼼히 준비했ZIP",
    main: "신세계 백화점 상품권 포함 5가지 혜택 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "youth",
    id: 5,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "결제계좌 변경하고",
    main: "스타벅스 쿠폰 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 6,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    rightLabel: "D-7",
    rightLabelColor: "blue",
    sub: "온라인 쇼핑몰에서",
    main: "최대 5만원 할인 쿠폰",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "apptech",
    id: 7,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "앱에서 결제하고",
    main: "추가 적립 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "travel_accommodation",
    id: 8,
    received: false,
    label: "이벤트 모음.zip",
    labelColor: "green",
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    sub: "여행 예약하고",
    main: "호텔 할인 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "card_payment",
    id: 9,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon6.png`,
      alt: "",
    },
    sub: "카드로 결제하고",
    main: "캐시백 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "youth",
    id: 10,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    rightLabel: "D-3",
    rightLabelColor: "blue",
    sub: "청소년 특별 혜택",
    main: "영화 할인 쿠폰",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 11,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    sub: "문화센터 이용하고",
    main: "강좌 수강료 할인",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "apptech",
    id: 12,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "앱 다운로드하고",
    main: "신규 가입 혜택",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "travel_accommodation",
    id: 13,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    rightLabel: "D-10",
    rightLabelColor: "blue",
    sub: "렌터카 예약하고",
    main: "추가 할인 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "card_payment",
    id: 14,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    sub: "카드 혜택 받고",
    main: "추가 적립 받기",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "youth",
    id: 15,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "청소년 특가",
    main: "도서 구매 할인",
  },
  {
    categoryType: "진행 중 이벤트",
    chipType: "shopping_culture",
    id: 16,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    label: "이벤트 모음.zip",
    labelColor: "green",
    sub: "문화 생활 즐기고",
    main: "공연 할인 받기",
  },
];

// 종료 이벤트 데이터
const endedItems = [
  {
    categoryType: "종료 이벤트",
    chipType: "shopping_culture",
    id: 1,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon7.png`,
      alt: "",
    },
    label: "이벤트 모음.zip",
    labelColor: "green",
    sub: "캐시백부터 할인까지 여기 다 있ZIP",
    main: "해외여행 필수템",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "apptech",
    id: 2,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    sub: "SOL페이에 티머니 등록하고",
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "travel_accommodation",
    id: 3,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    sub: "SOL페이에 티머니 등록하고",
    main: "1등 당첨되면 발뮤다 더 토스트",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "card_payment",
    id: 4,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon3.png`,
      alt: "",
    },
    sub: "카드 발급하고",
    main: "신규 발급 혜택",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "youth",
    id: 5,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon2.png`,
      alt: "",
    },
    sub: "청소년 특별 이벤트",
    main: "도서 구매 할인",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "shopping_culture",
    id: 6,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon1.png`,
      alt: "",
    },
    sub: "백화점에서 쇼핑하고",
    main: "추가 할인 받기",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "apptech",
    id: 7,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon4.png`,
      alt: "",
    },
    sub: "앱 업데이트하고",
    main: "이벤트 참여하기",
  },
  {
    categoryType: "종료 이벤트",
    chipType: "travel_accommodation",
    id: 8,
    received: false,
    icon: {
      src: `${$cdnURL}/images/dummy/thumb_benefit_cupon5.png`,
      alt: "",
    },
    sub: "항공권 예약하고",
    main: "마일리지 적립",
  },
];
</script>


```
{% endraw %}
---
