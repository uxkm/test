
{% raw %}
```js




<template>
  <!--
    퀴즈팡팡 영역
    - 어드민 > 이벤트 관리 > pLay전용 이벤트 관리에 등록된 퀴즈 이벤트가 있는 경우
      해당 이벤트 기간동안 노출
    - 진행되는 퀴즈 이벤트 없을 경우 해당 영역 히든
    - 문제 풀기 전/후에 따라 UI 다르게 노출
      : 문제 풀기 전: 당일 퀴즈 문항 + 퀴즈 버튼 노출
      : 문제 풀기 후: 등급 현황 + 참여 현황 노출
    - 미로그인 상태에서 퀴즈팡팡 영역 노출
      : 디바이스 정보 DB가 있는 경우 정답 제출 Tap > 마지막 로그인 방식 화면 호출

    [퀴즈 풀기 전]
    1-1. 퀴즈 문제
    - 어드민에 등록된 오늘날짜의 퀴즈유형(OX/객관식-2지선다, 3지선다) 및 문제 출력

    1-2. 퀴즈 유형
    - 이벤트 유형 중 '퀴즈_OX / 퀴즈_객관식'으로 등록된 이벤트가 노출
    - 버튼 비활성화 default, 답 선택 시 선택된 항목 활성화
    - 객관식 항목 텍스트 최대 2줄까지 노출
      : Case1 OX: OX선택 버튼 제공
      : Case2 / Case3 객관식: 라디오버튼+텍스트 제공, 중복선택 불가

    1-3. 힌트 보기 버튼
    - 힌트 보기 버튼 Tap > 어드민에서 해당 날짜, 퀴즈에 등록된 힌트 보기 유형으로 연결
    - 힌트 보기 유형은 타입에 따라 텍스트 or 이미지 or URL방식으로 나뉨
    - 힌트 보기 버튼 Tap > 문제 풀기 전 & 일 1회 & 최초에 한해 1P를 고정지급
    - 힌트 URL 또는 바텀시트 종료 후에 퀴즈로 다시 돌아오면 Toast popup(1-3-1) 노출
      토스트 내용 : 힌트 보너스를 1P 받았어요.
    - 힌트 일 1회 이상 확인 후 1P 배지 미노출

    1-4. 정답 제출 버튼
    - 버튼 비활성화 default, 답 선택 시 버튼 활성화 전환
    - 정답 제출 버튼 Tap > 어드민에 등록된 정답과 화면에서 선택값 일치여부 체크
      : 정답 실패(불일치): 오답 Toast popup(1-4-1) 노출 & 퀴즈 푼 후 화면으로 변경 (화면 refresh)
      토스트 내용 : 1P 획득! 내일은 정답에 도전하세요.
      : 정답 성공(일치): 정답 Toast popup(1-4-2) 노출 & 퀴즈 푼 후 화면으로 변경,
        지급 포인트 적립 (화면 refresh) (어드민 > 포인트 위에 등록된 포인트)
        토스트 내용 : 정답을 맞춰 11P를 받았어요.
      : 포인트 적립 실패: 내부 시스템 오류(인터페이스 실패)등으로 인해 포인트 적립 실패한 경우
        Toast popup(1-4-3) 노출 & 퀴즈풀기 재노출
        토스트 내용 : 앗, 문제가 생겼어요. 다시 해볼까요?

    [퀴즈 푼 후]
    1-1. 내 등급 + 참여 현황 문구
    - 직전 참여일 기준 해당하는 등급 노출 (LV.퀴즈박사, LV.퀴즈왕, LV.퀴즈의 신)
    - 등급 없는 경우 LV.0으로 노출
    - 참여 현황 문구 노출
      : 문구는 해상도에 따라 최대 2줄까지 노출
      : 문제 풀기 전 정답횟수 +1 회 하여 다음 등급까지 남은 횟수 노출
      : 등급 도달시에는 축하 문구 선 노출 후 남은 횟수 문구 노출
    - 내 등급 Tap > [SBT159A01_퀴즈 등급별 혜택 B/S] 호출

    1-2. 이번달 참여 현황 버튼
    - 이번달 참여 현황 버튼에 텍스트로 노출
      : 이번달 {{해당월 일 수}}일 중 {{참여일 수}}일 참여 중
      : ex. 11월에 3번 참여한 경우, '이번달 30일 중 3일 참여 중' 표기
    - 참여 현황 버튼 Tap > [SBT160A01_이달의 참여현황 B/S] 호출

    1-3. 힌트 다시보기 버튼
    - [힌트 다시보기] 버튼 Tap > 퀴즈 풀기 전 힌트보기 버튼과 기능 동일

    1-4. 퀴즈 등급 달성 후 추가 포인트 버튼 <등급 보너스 획득 Case1~3 참고>
    - 퀴즈 등급 달성 시 보너스 받기 버튼 노출
      : 등급 미달성시에는 버튼 미노출
    - {{달성한 등급명}} 보너스 받기 문구 노출
    - 버튼 Tap > 토스트 메시지 노출 후 포인트 적립
      (어드민에서 등록한 포인트 단위 중 랜덤 지급) 보너스 적립 후 버튼 사라짐
    - 등급 도달 후 보너스 받기 버튼 누르지 않고 정답인 경우
      버튼명 변경: 지난 {{달성한 등급명}} 보너스 받기
    - 등급 도달 & 다음 등급 도달까지 보너스 받기 버튼 안누를 경우
      최대 3번까지 연속으로 보너스 받기 가능 (단, 이전 등급 버튼명 분기)
      ex) 퀴즈박사 보너스 안받은 상태로 퀴즈의 신 도달:
        보너스 포인트 받기 버튼 노출 → 보너스 적립(퀴즈박사) →
        보너스 포인트 받기 버튼 노출 → 보너스 적립(퀴즈왕) →
        보너스 포인트 받기 버튼 노출 → 보너스 적립(퀴즈의신) → 버튼 사라짐 
  -->
  <section class="bf-quiz-pangpang">
    <!-- S : 퀴즈팡팡 로딩 -->
    <article
      class="bf-quiz-pangpang__contents skeleton"
      tabindex="0"
      aria-label="로딩중"
    >
      <div class="bf-quiz-pangpang__contents-header" aria-hidden="true">
        <LoadingSkeleton width="100%" :height="54" rounded="small" />
      </div>
      <div class="bf-quiz-pangpang__contents-body" aria-hidden="true">
        <div class="bf-quiz-pangpang__contents-item">
          <LoadingSkeleton width="100%" :height="100" rounded="small" />
        </div>
        <div class="bf-quiz-pangpang__contents-item">
          <LoadingSkeleton width="100%" :height="100" rounded="small" />
        </div>
      </div>
      <div class="bf-quiz-pangpang__contents-footer" aria-hidden="true">
        <div class="bf-quiz-pangpang__contents-item">
          <LoadingSkeleton width="100%" :height="48" rounded="small" />
        </div>
        <div class="bf-quiz-pangpang__contents-item">
          <LoadingSkeleton width="100%" :height="48" rounded="small" />
        </div>
        <div class="bf-quiz-pangpang__contents-item">
          <LoadingSkeleton width="100%" :height="22" rounded="small" />
        </div>
      </div>
    </article>
    <!-- E : 퀴즈팡팡 로딩 -->

    <!-- S : 퀴즈팡팡 콘텐츠 - 문제 풀기 전 -->
    <article class="bf-quiz-pangpang__contents">
      <div class="bf-quiz-pangpang__contents-header">
        <h2 class="bf-quiz-pangpang__title">퀴즈팡팡</h2>
        <!-- 어드민에 등록된 오늘날짜의 퀴즈유형(OX/객관식-2지선다, 3지선다) 및 문제 출력 -->
        <p class="bf-quiz-pangpang__problem-output">
          보기만해도 포인트를 주는 서비스는<br />[포인트 팡팡]이다.
        </p>
        <!-- case 2 - 문제 풀기 전 객관식 3지선다, case 3 - 문제 풀기 전 객관식 2지선다 -->
        <!-- <p class="bf-quiz-pangpang__problem-output">
          보기만해도 포인트를 드리는 포인트<br />즉시적립 서비스명은 무엇일까요?
        </p> -->
      </div>

      <!-- S : OX 퀴즈 -->
      <div class="bf-quiz-pangpang__contents-body">
        <div class="bf-quiz-pangpang__contents-item">
          <SelectBox
            value="true"
            :selected="selectedAnswer === 'true'"
            class="icon-button-true"
            aria-label="그렇다"
            @click="selectedAnswer = 'true'"
          >
            <template #contents>
              <span class="icon-box" aria-hidden="true">
                <ScImageIcon iconName="icon_o" size="32" />
              </span>
              <span class="sv-select-box__label" aria-hidden="true"
                >그렇다</span
              >
            </template>
          </SelectBox>
        </div>
        <div class="bf-quiz-pangpang__contents-item">
          <SelectBox
            value="false"
            :selected="selectedAnswer === 'false'"
            class="icon-button-false"
            aria-label="아니다"
            @click="selectedAnswer = 'false'"
          >
            <template #contents>
              <span class="icon-box" aria-hidden="true">
                <ScImageIcon iconName="icon_x" size="32" />
              </span>
              <span class="sv-select-box__label" aria-hidden="true"
                >아니다</span
              >
            </template>
          </SelectBox>
        </div>
      </div>
      <!-- E : OX 퀴즈 -->

      <!-- S : 문제 풀기 전 객관식 -->
      <div class="bf-quiz-pangpang__contents-body question">
        <RadioCircleGroup
          v-model="selectedQuestion"
          align="left"
          :items="questionItems"
          orientation="vertical"
          class="question-radio__items"
        />
      </div>
      <!-- E : 문제 풀기 전 객관식 -->

      <div class="bf-quiz-pangpang__contents-footer">
        <div class="bf-quiz-pangpang__contents-item">
          <TextBadge
            variant="tint"
            color="gray"
            class="hint-badge"
            aria-label="포인트 1 지급"
          >
            <template #content>
              <span class="hint-badge-image" aria-hidden="true">
                <img
                  :src="`${$cdnURL}/images/pages/base/Coin_Point.png`"
                  alt="포인트"
                />
              </span>
              <em class="hint-badge-text">1P</em>
            </template>
          </TextBadge>
          <BoxButton color="quaternary" text="힌트 보기" />
        </div>
        <div class="bf-quiz-pangpang__contents-item">
          <TextBadge
            variant="tint"
            color="gray"
            class="hint-badge"
            aria-label="포인트 5 지급"
          >
            <template #content>
              <span class="hint-badge-image" aria-hidden="true">
                <img
                  :src="`${$cdnURL}/images/pages/base/Coin_Point.png`"
                  alt="포인트"
                />
              </span>
              <em class="hint-badge-text">5P</em>
            </template>
          </TextBadge>
          <BoxButton
            color="primary"
            text="정답제출"
            :disabled="selectedAnswer === null"
          />
        </div>
        <div class="bf-quiz-pangpang__contents-item">
          <Infobox
            title="기회는 단 한번! 힌트를 꼭 확인해보세요."
            color="info"
            size="small"
            :icon="false"
          />
        </div>
      </div>
    </article>
    <!-- E : 퀴즈팡팡 콘텐츠 - 문제 풀기 전 -->

    <!-- S : 퀴즈팡팡 콘텐츠 - 문제 풀기 후 -->
    <article class="bf-quiz-pangpang__contents-result">
      <div class="bf-quiz-pangpang__contents-header">
        <h2 class="bf-quiz-pangpang__title">내일도 퀴즈에 도전하세요!</h2>
        <TextButton
          text="힌트 다시보기"
          size="xsmall"
          :rightIcon="{ iconName: 'Chevron_right' }"
          color="secondary"
        />
      </div>
      <!--
        내 등급 이미지 경로 및 파일명
        /images/pages/benefits/main/Property_level0_status.svg (LV.0)
        /images/pages/benefits/main/Property_level1_status.svg (LV.10)
        /images/pages/benefits/main/Property_level2_status.svg (LV.20)
        /images/pages/benefits/main/Property_level3_status.svg (LV.30)
        /images/pages/benefits/main/Property_level1_status_disabled.svg (LV.10 disabled)
        /images/pages/benefits/main/Property_level2_status_disabled.svg (LV.20 disabled)
        /images/pages/benefits/main/Property_level3_status_disabled.svg (LV.30 disabled)

        .level-button 클릭시 퀴즈 등급별 혜택 BS 호출 SBT159A01
      -->
      <div class="bf-quiz-pangpang__contents-body">
        <a
          role="button"
          class="level-button"
          aria-label="내 등급 레벨 0, 퀴즈박사까지 2회 남았어요"
        >
          <ListItem align="centered" class="level-item" aria-hidden="true">
            <template #leftIcon>
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/Property_level0_status.svg`"
                alt="레벨 0"
              />
            </template>
            <template #leftMainText>
              <span class="level-content">
                <span class="level-label">
                  <em>LV.0</em>
                  <Icon name="Chevron_right" size="16" />
                </span>
                <span class="level-desc">퀴즈박사까지 2회 남았어요</span>
              </span>
            </template>
          </ListItem>
        </a>
      </div>

      <!-- 등급 달성 - 당일 -->
      <div class="bf-quiz-pangpang__contents-body">
        <a
          role="button"
          class="level-button"
          aria-label="내 등급 레벨 10 퀴즈박사, 퀴즈박사에 등극했어요!"
        >
          <ListItem align="centered" class="level-item" aria-hidden="true">
            <template #leftIcon>
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/Property_level1_status.svg`"
                alt="레벨 10"
              />
            </template>
            <template #leftMainText>
              <span class="level-content">
                <span class="level-label">
                  <em>LV.퀴즈박사</em>
                  <Icon name="Chevron_right" size="16" />
                </span>
                <span class="level-desc">퀴즈박사에 등극했어요!</span>
              </span>
            </template>
          </ListItem>
        </a>
      </div>

      <!-- 등급 달성 - 달성 후 다음 날 -->
      <div class="bf-quiz-pangpang__contents-body">
        <a
          role="button"
          class="level-button"
          aria-label="내 등급 레벨 10 퀴즈박사, 퀴즈왕까지 9회 남았어요"
        >
          <ListItem align="centered" class="level-item" aria-hidden="true">
            <template #leftIcon>
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/Property_level1_status.svg`"
                alt="레벨 10"
              />
            </template>
            <template #leftMainText>
              <span class="level-content">
                <span class="level-label">
                  <em>LV.퀴즈박사</em>
                  <Icon name="Chevron_right" size="16" />
                </span>
                <span class="level-desc">퀴즈왕까지 9회 남았어요</span>
              </span>
            </template>
          </ListItem>
        </a>
      </div>

      <!-- 등급 도달 후 보너스 받기 + 정답 맞춘 경우 -->
      <div class="bf-quiz-pangpang__contents-body">
        <a
          role="button"
          class="level-button"
          aria-label="내 등급 레벨 20 퀴즈왕, 퀴즈신까지 9회 남았어요"
        >
          <ListItem align="centered" class="level-item" aria-hidden="true">
            <template #leftIcon>
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/Property_level2_status.svg`"
                alt="레벨 20"
              />
            </template>
            <template #leftMainText>
              <span class="level-content">
                <span class="level-label">
                  <em>LV.퀴즈왕</em>
                  <Icon name="Chevron_right" size="16" />
                </span>
                <span class="level-desc">퀴즈신까지 9회 남았어요</span>
              </span>
            </template>
          </ListItem>
        </a>
      </div>
      <div class="bf-quiz-pangpang__contents-footer">
        <BoxButton color="quaternary" text="퀴즈박사 보너스 받기" />
        <BoxButton color="quaternary" text="지난 퀴즈박사 보너스 받기" />
        <BoxButton color="quaternary" text="이번달 30일 중 8일 참여" />
      </div>
    </article>
    <!-- E : 퀴즈팡팡 콘텐츠 - 문제 풀기 후 -->

    <!-- S : 퀴즈팡팡 IF 오류시 노출 -->
    <div class="bf-if__error h344">
      <div class="bf-if__error-inner">
        <div class="bf-if__error-icon">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/result_icon.png`"
            alt="IF 오류"
          />
        </div>
        <div class="bf-if__error-text">퀴즈정보를 불러오지 못했어요</div>
        <CapsuleButton
          text="다시 시도하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 퀴즈팡팡 IF 오류시 노출 -->
  </section>
</template>

<script setup>
import { inject, nextTick, onMounted, ref, watch } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import {
  BoxButton,
  CapsuleButton,
  Icon,
  IconButton,
  Infobox,
  ListItem,
  LoadingSkeleton,
  RadioCircle,
  RadioCircleGroup,
  SelectBox,
  TextBadge,
  TextButton,
} from "@shc-nss/ui/solid";
import { ScImage, ScImageIcon } from "@shc-nss/ui/shc";

const { $cdnURL } = inject(AppContextKey);
// 퀴즈팡팡 섹션
const selectedAnswer = ref(null);
const questionItems = [
  { label: "포인트 팡팡", value: 1 },
  { label: "텍스트 한 줄 입니다", value: 2 },
  {
    label: "텍스트 입니다 텍스트 입니다 텍스트 입니다 텍스트 입니다",
    value: 3,
  },
];
const selectedQuestion = ref(questionItems[0].value);

// 선택된 항목의 컨테이너에 is-checked 클래스 추가
function updateCheckedClass() {
  nextTick(() => {
    const containers = document.querySelectorAll(
      ".question-radio__items .sv-radio-group__item-container"
    );
    containers.forEach((container) => {
      const radioItem = container.querySelector(
        ".sv-radio-item[data-state='checked']"
      );
      if (radioItem) {
        container.classList.add("is-checked");
      } else {
        container.classList.remove("is-checked");
      }
    });
  });
}

watch(selectedQuestion, () => {
  updateCheckedClass();
});
</script>



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
