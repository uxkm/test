
{% raw %}
```js


<route lang="yaml">
meta:
  id: SBT159A01
  title: 혜택
  menu: "혜택 > 혜택 > 퀴즈 등급별 혜택 (BS)"
  layout: MainLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  appClassList: "app_benefits"
  mainClassList: "benefits_main"
</route>
<template>
  <!-- 퀴즈 등급별 혜택 -->
  <BottomSheet
    v-model="isOpen"
    closableDimm
    dimmed
    title="퀴즈 등급별 혜택을 알아보세요"
    class="quiz-level-benefit__sheet"
  >
    <div class="quiz-level-benefit">
      <!-- 
        내 등급
        등급이 없을 경우 LV.0으로 노출
        LV.10 = 퀴즈박사
        LV.20 = 퀴즈왕
        LV.30 = 퀴즈의 신
      -->
      <div
        class="quiz-level-benefit__header"
        tabindex="0"
        :aria-label="headerAriaLabel"
      >
        <div class="quiz-level-benefit__area" aria-hidden="ture">
          <div class="label-group">
            <em class="level-title">내 레벨</em>
            <strong class="level-number">LV.{{ currentLevelName }}</strong>
          </div>
          <SolidLabel color="gray" title="종료 D-23" />
        </div>
        <p class="level-desc" aria-hidden="ture">
          <template v-if="canLevelUp && remainingCount > 0">
            {{ nextLevelName }}까지 <em>{{ remainingCount }}회</em> 남았어요.
          </template>
          <template v-else>
            {{ levelDescription }}
          </template>
        </p>
        <div class="level-progress" aria-hidden="ture">
          <div class="level-progress__bar"></div>
          <div class="level-progress__label">
            <span class="level-progress__text level0"></span>
            <span class="level-progress__text level1">
              <i v-if="currentLevel >= 10" class="is-achieved">
                <Icon name="Check" size="16" color="white" />
              </i>
              <img
                src="/images/pages/benefits/main/Property_level1_status.svg"
                alt="레벨 10"
              />
              <em>퀴즈박사</em>
            </span>
            <span class="level-progress__text level2">
              <i v-if="currentLevel >= 20" class="is-achieved">
                <Icon name="Check" size="16" color="white" />
              </i>
              <img
                src="/images/pages/benefits/main/Property_level2_status.svg"
                alt="레벨 20"
              />
              <em>퀴즈왕</em>
            </span>
            <span class="level-progress__text level3">
              <img
                src="/images/pages/benefits/main/Property_level3_status.svg"
                alt="레벨 30"
              />
              <em>퀴즈의 신</em>
            </span>
          </div>
          <div
            class="level-progress__status"
            :data-level="currentLevel"
            :style="{ '--progress-width': progressWidth }"
          >
            <i class="point-marker-zero"></i>
            <i
              v-if="
                currentLevel > 0 &&
                currentLevel < 30 &&
                currentLevel !== 10 &&
                currentLevel !== 20
              "
              class="point-marker"
            >
              {{ currentLevel }}
            </i>
          </div>
        </div>
      </div>
      <div class="quiz-level-benefit__body">
        <ListItem
          v-for="item in quizLevelItems"
          :key="item.level"
          align="centered"
          class="quiz-level-benefit__item"
          tabindex="0"
          :aria-label="`${item.iconAlt}, ${item.mainText}. ${item.subText}`"
        >
          <template #leftIcon>
            <div class="quiz-level-benefit__item-icon" aria-hidden="true">
              <img :src="`${$cdnURL}${item.iconSrc}`" :alt="item.iconAlt" />
            </div>
          </template>
          <template #leftMainText>
            <strong class="quiz-level-benefit__main-text" aria-hidden="true">
              {{ item.mainText }}
            </strong>
          </template>
          <template #leftSubText>
            <span class="quiz-level-benefit__sub-text" aria-hidden="true">
              {{ item.subText }}
            </span>
          </template>
        </ListItem>
      </div>
      <Divider
        variant="basic"
        color="tertiary"
        size="full"
        orientation="horizontal"
      />
      <div class="quiz-level-benefit__footer">
        <UnorderedList>
          <UnorderedListItem>
            2월에는 월 28회 정답을 맞추면 퀴즈의 신에 등극할 수 있어요.
          </UnorderedListItem>
          <UnorderedListItem>
            이벤트 혜택은 신한카드 사정에 따라 변경될 수 있습니다.
          </UnorderedListItem>
        </UnorderedList>
      </div>
    </div>
  </BottomSheet>
</template>

<script setup>
// ==========================================
// Import
// ==========================================
import { inject, computed } from "vue";
import { defineModel } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import {
  BottomSheet,
  Divider,
  Icon,
  ListItem,
  SolidLabel,
  UnorderedList,
  UnorderedListItem,
} from "@shc-nss/ui/solid";

// ==========================================
// 바텀시트 제어
// ==========================================
const { $cdnURL } = inject(AppContextKey);
const isOpen = defineModel({ default: true });

// ==========================================
// 현재 레벨 및 상태 (예시 데이터)
// ==========================================
const currentLevel = 8; // 현재 정답 횟수 (0~30)
const canLevelUp = true; // 등급 상승 가능 여부
const achievedLevel = null; // 달성한 등급 (10: 퀴즈박사, 20: 퀴즈왕, 30: 퀴즈의 신, null: 없음)

// ==========================================
// 이벤트 정보 (예시 데이터)
// ==========================================
const eventRemainingDays = 23; // 이벤트 남은 기간

// ==========================================
// 현재 등급 이름 (LV.0 또는 LV.퀴즈박사 등)
// achievedLevel이 있으면 그것을 사용하고, 없으면 currentLevel을 기준으로 계산
// ==========================================
const currentLevelName = computed(() => {
  // achievedLevel이 있으면 그것을 사용
  if (achievedLevel === 30) return "퀴즈의 신";
  if (achievedLevel === 20) return "퀴즈왕";
  if (achievedLevel === 10) return "퀴즈박사";

  // achievedLevel이 없으면 currentLevel을 기준으로 계산
  if (currentLevel >= 30) return "퀴즈의 신";
  if (currentLevel >= 20) return "퀴즈왕";
  if (currentLevel >= 10) return "퀴즈박사";
  return "0";
});

// ==========================================
// 다음 등급까지 남은 횟수 계산
// ==========================================
const remainingCount = computed(() => {
  if (achievedLevel === 30) return 0; // 최대 등급 달성
  if (achievedLevel === 20) return 30 - currentLevel;
  if (achievedLevel === 10) return 20 - currentLevel;
  if (achievedLevel === null) {
    // 달성한 등급이 없을 때
    if (currentLevel >= 20) return 30 - currentLevel;
    if (currentLevel >= 10) return 20 - currentLevel;
    return 10 - currentLevel;
  }
  return 10 - currentLevel;
});

// ==========================================
// 다음 등급 이름
// ==========================================
const nextLevelName = computed(() => {
  if (achievedLevel === 30) return "";
  if (achievedLevel === 20) return "퀴즈의 신";
  if (achievedLevel === 10) return "퀴즈왕";
  // 달성한 등급이 없을 때
  if (currentLevel >= 20) return "퀴즈의 신";
  if (currentLevel >= 10) return "퀴즈왕";
  return "퀴즈박사";
});

// ==========================================
// 레벨 설명 텍스트
// 등급 상승 가능 여부와 달성 상태에 따라 다르게 표시
// ==========================================
const levelDescription = computed(() => {
  // 최대 등급 달성 (30) - 등급 상승 가능 여부와 관계없이
  if (currentLevel >= 30 || achievedLevel === 30) {
    return "대단해요! 다음달도 도전해보세요!";
  }

  // 등급 상승 불가능한 경우
  if (!canLevelUp) {
    // 그 외 (달성한 등급 있음/없음)
    return "다음달에 또 퀴즈등급에 도전할 수 있어요.";
  }

  // 등급 상승 가능한 경우
  // 남은 횟수가 있으면 남은 횟수 표시
  if (remainingCount.value > 0) {
    return `${nextLevelName.value}까지 ${remainingCount.value}회 남았어요.`;
  }

  // 남은 횟수가 0인 경우 (현재는 발생하지 않을 것)
  return "";
});

// ==========================================
// aria-label 텍스트
// ==========================================
const headerAriaLabel = computed(() => {
  return `내 레벨 ${currentLevelName.value === "0" ? "0" : currentLevelName.value}, ${levelDescription.value} 이벤트 남은 기간: ${eventRemainingDays}일. 현재횟수: ${currentLevel}회`;
});

// ==========================================
// 진행률 계산
// 각 구간(0~10, 10~20, 20~30)에서 currentLevel까지의 비율로 계산
// 각 level-progress__text의 중앙 위치까지 동적으로 계산
// grid 구조: 65px 56px 1fr 56px 1fr 56px
// level 10일 때 level 1(퀴즈박사) 중앙까지
// level 20일 때 level 2(퀴즈왕) 중앙까지
// level 30일 때 level 3(퀴즈의 신) 중앙까지
// ==========================================
const progressWidth = computed(() => {
  const level = currentLevel;
  if (level <= 0) return "0px";

  let ratio = 0;

  if (level <= 10) {
    // 0~10 구간: level 0 시작점에서 level 1 중앙까지
    // level에 비례하여 계산 (예: level 8이면 0~10 구간에서 8까지 = 80%)
    ratio = level / 10;
    // level 0 시작: 0px
    // level 1 중앙: 93px (65px + 28px)
    // level 10일 때 level 1 중앙(93px)까지 도달
    // level에 비례하여 width 계산
    return `calc(93px * ${ratio})`;
  } else if (level <= 20) {
    // 10~20 구간: level 0 시작점에서 level 2 중앙까지
    ratio = (level - 10) / 10;
    // level 10일 때: level 1 중앙(93px)
    // level 20일 때: level 2 중앙 = 149px + 1fr = 149px + (100% - 65px - 56px * 3) / 2
    // level 1 중앙에서 level 2 중앙까지: 56px + 1fr
    // level 0 시작점에서 level 2 중앙까지: level 1 중앙 + (level 1 중앙에서 level 2 중앙까지) * ratio
    return `calc(93px + 56px * ${ratio} + (100% - 65px - 56px * 3) / 2 * ${ratio})`;
  } else {
    // 20~30 구간: level 0 시작점에서 level 3 중앙까지
    ratio = (level - 20) / 10;
    // level 20일 때: level 2 중앙 = 149px + 1fr
    // level 30일 때: level 3 중앙 = 205px + 2fr = 205px + (100% - 65px - 56px * 3)
    // level 2 중앙에서 level 3 중앙까지: 56px + 1fr
    // level 0 시작점에서 level 3 중앙까지: level 2 중앙 + (level 2 중앙에서 level 3 중앙까지) * ratio
    return `calc(149px + (100% - 65px - 56px * 3) / 2 + 56px * ${ratio} + (100% - 65px - 56px * 3) / 2 * ${ratio})`;
  }
});

// ==========================================
// 퀴즈 등급별 혜택 데이터
// ==========================================
const quizLevelItems = computed(() => [
  {
    level: 30,
    iconSrc: "/images/pages/benefits/main/Property_level3_status.svg",
    iconAlt: "레벨 30",
    mainText: "월 30회 정답 시 퀴즈의 신",
    subText: "최대 10,000P 랜덥포인트 지급",
  },
  {
    level: 20,
    iconSrc: "/images/pages/benefits/main/Property_level2_status.svg",
    iconAlt: "레벨 20",
    mainText: "월 20회 정답 시 퀴즈왕",
    subText: "최대 5,000P 랜덥포인트 지급",
  },
  {
    level: 10,
    iconSrc: "/images/pages/benefits/main/Property_level1_status.svg",
    iconAlt: "레벨 10",
    mainText: "월 10회 정답 시 퀴즈박사",
    subText: "최대 1,000P 랜덥포인트 지급",
  },
]);
</script>



```
{% endraw %}
---
