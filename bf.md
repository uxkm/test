
{% raw %}
```js


<template>
  <div class="payment-panel payment-panel__daily" aria-label="매일결제">
    <section class="section-head">
      <!-- S : 전일자 카드사용내역 1건 or 다수 인 경우 -->
      <div
        v-if="testValue"
        class="text-daily__title"
        aria-label="지금까지 99,999 포인트 받았어요!"
        tabindex="0"
      >
        <p class="text-daily01" aria-hidden="true">
          <ScImageIcon
            iconName="benefits_welcome_text_daily01"
            width="auto"
            height="18"
            :colorize="false"
            class="svgtext-daily01"
          />
        </p>
        <p class="text-daily02" aria-hidden="true">
          <strong class="text-daily02__point"><em>99,999</em>P</strong>
          <ScImageIcon
            iconName="benefits_welcome_text_daily02"
            width="auto"
            height="28"
            :colorize="false"
            class="svgtext-daily02"
          />
        </p>
      </div>
      <!-- E : 전일자 카드사용내역 1건 or 다수 인 경우 -->

      <!-- S : 포인트 0인 경우(미참여 사용자) -->
      <div
        v-else
        class="text-daily__title"
        aria-label="매일매일 100~1,000 포인트 당첨!"
        tabindex="0"
      >
        <p class="text-daily01" aria-hidden="true">
          <ScImageIcon
            iconName="benefits_welcome_text_daily01-1"
            width="auto"
            height="18"
            :colorize="false"
            class="svgtext-daily01-1"
          />
        </p>
        <p class="text-daily02" aria-hidden="true">
          <strong class="text-daily02__point"><em>100~1,000</em>P</strong>
          <ScImageIcon
            iconName="benefits_welcome_text_daily02-1"
            width="auto"
            height="28"
            :colorize="false"
            class="svgtext-daily02-1"
          />
        </p>
      </div>
      <!-- E : 포인트 0인 경우(미참여 사용자) -->

      <TextButtonUnderline color="secondary" size="medium" text="받은 혜택 확인하기" />
      <div class="img-group" aria-hidden="true">
        <img :src="`${$cdnURL}/images/pages/benefits/welcome/img_daily_main_140x140.png`" alt="" />
      </div>

      <div class="custom-cards__gray-group center">
        <Card
          as="div"
          variant="solid"
          type="basic"
          color="gray"
          class="custom-cards__gray"
          :divider="false"
        >
          <div class="custom-cards__gray-info">
            <p><em>NN</em>일 동안 매일!</p>
            <p>어제 결제했다면, 오늘 포인트가 도착해요</p>
            <p><small>(100~1,000 포인트 랜덤 지급)</small></p>
          </div>
        </Card>
      </div>
    </section>
    <section class="bg-gray">
      <article class="article">
        <div class="custom-cards__group">
          <Card
            v-for="card in dailyCardList"
            :key="card.id"
            as="div"
            color="whiteShadow"
            variant="solid"
            type="basic"
            class="custom-cards"
            :divider="false"
          >
            <div
              class="custom-cards__header"
              tabindex="0"
              :aria-label="`${card.badgeText}. ${card.svgLabel}`"
            >
              <div class="custom-cards__header-title" aria-hidden="true">
                <NumberBadge type="text" :text="card.badgeText" color="gray" inline />
                <ScImageIcon
                  :iconName="card.iconName"
                  width="auto"
                  height="auto"
                  :colorize="false"
                  class="svgtext-custom-cards-title"
                  :aria-label="card.svgLabel"
                />
              </div>
            </div>
            <Divider variant="basic" orientation="horizontal" color="tertiary" aria-hidden="true" />
            <div class="custom-cards__content">
              <div
                v-if="card.isParticipant ?? testValue"
                class="custom-cards__content-item"
                tabindex="0"
                :aria-label="card.participant?.price
                  ? `${card.participant.title}. ${card.participant.price}`
                  : (card.participant?.title ?? '')"
              >
                <span class="custom-cards__title" aria-hidden="true">{{ card.participant?.title }}</span>
                <span
                  v-if="card.participant?.price"
                  class="custom-cards__price"
                  aria-hidden="true"
                >
                  {{ card.participant.price }}
                </span>
              </div>
              <div
                v-else
                class="custom-cards__content-item"
                tabindex="0"
                :aria-label="card.nonParticipantMessage ?? nonParticipantMessage"
              >
                <span class="custom-cards__title" aria-hidden="true">
                  {{ card.nonParticipantMessage ?? nonParticipantMessage }}
                </span>
              </div>
            </div>
            <template #actions>
              <BoxButtonGroup size="large" variant="100">
                <!-- 매일결제 혜택 케이스
                [포인트 받기 전 (조건 충족)]
                버튼명 : 포인트 받기, color : secondary
                [포인트 받 후]
                버튼명 : 받기 완료, disabled : true
                [포인트 만료 시]
                버튼명 : 기간 만료, disabled : true
                [전일자 카드사용내역 5천원 미만]
                버튼명 : 포인트 받기, disabled : true
                -->
                <BoxButton
                  :text="card.button?.text ?? '포인트 받기'"
                  :color="card.button?.color ?? 'secondary'"
                  :disabled="card.button?.disabled ?? !testValue"
                />
              </BoxButtonGroup>

            </template>
          </Card>
        </div>
      </article>
      <div class="custom-divider section-daily bg-gray" aria-hidden="true">
        <ScImageIcon
          iconName="icon-plus-fill"
          width="auto"
          height="auto"
          :colorize="false"
          class="svgicon-plus-fill"
          aria-hidden="true"
        />
      </div>
      <article class="article">
        <div class="custom-cards__group">
          <div class="custom-cards__group-head">
            <div class="group-head__label">
              <NumberBadge type="text" text="기간연장 혜택" color="gray" inline />
            </div>
            <div class="group-head__text" aria-label="통신비 정기결제하면 매일결제 한 달 더!" tabindex="0">
              <!-- S : 전일자 카드사용내역 1건 or 다수 인 경우 -->
              <ScImageIcon
                v-if="testValue"
                iconName="benefits_welcome_text_daily03"
                width="auto"
                height="auto"
                :colorize="false"
                class="svgtext-daily03"
                aria-label="통신비 정기결제하면 매일결제 한 달 더!"
                aria-hidden="true"
              />
              <!-- E : 전일자 카드사용내역 1건 or 다수 인 경우 -->
  
              <!-- S : 포인트 0인 경우(미참여 사용자) -->
              <ScImageIcon
                v-else
                iconName="benefits_welcome_text_daily03-1"
                width="auto"
                height="auto"
                :colorize="false"
                class="svgtext-daily03"
                aria-label="통신비 정기결제 혜택 적용 완료!"
                aria-hidden="true"
              />
              <!-- E : 포인트 0인 경우(미참여 사용자) -->
            </div>
          </div>
          <Card
            as="div"
            color="whiteShadow"
            variant="solid"
            type="basic"
            class="custom-cards"
            :divider="false"
          >
            <div class="custom-cards__content">
              <div class="custom-cards__content-item">
                <img :src="`${$cdnURL}/images/pages/benefits/welcome/img_daily_telecom_140x104.png`" alt="" />
  
                <!-- 포인트 0인경우 (미참여 사용자) -->
                <SolidLabel
                  v-if="!testValue"
                  color="blue"
                  title="혜택 미적용"
                />
                <!-- E : 포인트 0인경우 (미참여 사용자) -->
              </div>
            </div>
            <template #actions>
              <BoxButtonGroup size="large" variant="100">
                <!-- 통신요금 연결 전 -->
                <BoxButton
                  v-if="testValue"
                  text="정기결제 신청하기"
                  color="secondary"
                />
                <!-- E : 통신요금 연결 전 -->
  
                <!-- 통신요금 연결 완료 -->
                <BoxButton
                  v-else
                  text="정기결제 보러가기"
                  color="tertiary"
                />
                <!-- E : 통신요금 연결 완료 -->
              </BoxButtonGroup>
            </template>
          </Card>
        </div>
      </article>  
    </section>
    <section class="section payment-notice">
      <h2 class="title-sub">꼭! 알아두세요</h2>
      <article v-for="section in noticeSections" :key="section.title">
        <h3 class="title-sub__small">{{ section.title }}</h3>
        <UnorderedList :gap="8">
          <template v-for="(item, index) in section.items" :key="index">
            <!-- 일반 아이템 -->
            <UnorderedListItem 
              v-if="typeof item === 'string'"
              variant="bullet"
            >
              <span v-html="item"></span>
            </UnorderedListItem>
            
            <!-- 중첩된 아이템 (이용 예시) -->
            <UnorderedListItem 
              v-else-if="item.type === 'nested'"
              variant="bullet"
            >
              <span>{{ item.title }}</span>
              <UnorderedList :gap="8">
                <UnorderedListItem 
                  v-for="(subItem, subIndex) in item.items" 
                  :key="subIndex"
                  variant="dash"
                >
                  <span>{{ subItem }}</span>
                </UnorderedListItem>
              </UnorderedList>
            </UnorderedListItem>
          </template>
        </UnorderedList>
      </article>
    </section>
  </div>
</template>

<script setup>
import { ScImageIcon } from "@shc-nss/ui/shc";
import {
  BoxButton,
  BoxButtonGroup,
  Card,
  Divider,
  NumberBadge,
  SolidLabel,
  TextButtonUnderline,
  UnorderedList,
  UnorderedListItem
} from "@shc-nss/ui/solid";
import { ref } from "vue";
import { COMMON_NOTICE_SECTION } from "./notice-common";
import { AppContextKey } from "@/configs/inject/appContext";
import { inject } from "vue";
const { $cdnURL } = inject(AppContextKey);

// props로 탭 활성화 상태 받기 (사용하지 않지만 일관성을 위해 정의)
defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

// 임시 UI 확인용 전일자 카드사용내역 1건 or 다수 인 경우 true, 포인트 0인 경우 false
const testValue = ref(true);

const nonParticipantMessage = "오늘 신용카드 쓰고 내일 포인트 받아요!";

// [v0.9] 260127: 참여 이력  포인트 지급 이력 케이스 추가 및 수정
const dailyCardList = [
  // 1. 한번에 5천원 이상 결제
  // 포인트 받기 전(조건 충족)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점을지로파인애비뉴점을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: false
    }
  },
  // 포인트 받은 후
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점을지로파인애비뉴점을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "오늘 N,NNN포인트를 받았어요!",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 없음 (포인트 0/조건 미충족)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    isParticipant: false,
    nonParticipantMessage,
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 결제 금액 5천원 미만
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점",
      price: "1,000원"
    },
    button: {
      text: "5천원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 없음
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    isParticipant: false,
    nonParticipantMessage: "어제 신용카드를 사용하지 않았어요!",
    button: {
      text: "5천원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 있음(만료/혜택 연장 안내)
  {
    id: "daily-card-1",
    badgeText: "1",
    svgLabel: "한번에 5천원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title01",
    participant: {
      title: "을지로파인애비뉴점",
      price: "5,000원"
    },
    button: {
      text: "통신비 정기결제하면 한달 더 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 2. 합쳐서 5만원 이상 결제
  // 포인트 받기 전(조건 충족)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: false
    }
  },
  // 포인트 받은 후
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "오늘 N,NNN포인트를 받았어요!",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 없음 (포인트 0/조건 미충족)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    isParticipant: false,
    nonParticipantMessage,
    button: {
      text: "포인트 받기",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 누적 금액 5만원 미만
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "40,000원"
    },
    button: {
      text: "5만원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 없음
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    isParticipant: false,
    nonParticipantMessage: "어제 신용카드를 사용하지 않았어요!",
    button: {
      text: "5만원 이상 쓰면 포인트 받아요",
      color: "secondary",
      disabled: true
    }
  },
  // 참여 이력 있음 - 전일 결제이력 있음(만료/혜택 연장 안내)
  {
    id: "daily-card-2",
    badgeText: "2",
    svgLabel: "합쳐서 5만원 이상 결제",
    iconName: "benefis_welcome_custom_cards_title02",
    participant: {
      title: "어제 결제 금액",
      price: "500,000원"
    },
    button: {
      text: "통신비 정기결제하면 한달 더 받아요",
      color: "secondary",
      disabled: true
    }
  }
];

// 꼭! 알아두세요 데이터
const noticeSections = [
  {
    title: "매일결제",
    items: [
      "접속일 기준 전날 국내 신한 개인신용카드 승인 이력이 있으면 포인트(마이신한포인트) 지급 대상이 됩니다.",
      "포인트를 지급받기 위해선 '이용권유 방법에 대한 동의'의 전화 혹은 문자 메시지(LMS) 중 1개 이상의 항목과 '혜택정보 수신(이용권유) 동의'의 '카드 및 금융 상품·서비스 안내 및 이용 권유를 위한 수집, 이용' 항목에 대해 모두 동의해야 합니다.",
      "매일결제 혜택은 반갑꾸러미 접속 종료일로부터 30일 전까지 제공되며, 신한SOL페이 앱 기준 통신 3사 요금 정기결제에 등록되어 있거나, 직전 30일 내 통신 3사 정기결제 승인 이력이 있는 경우 혜택 제공 기간이 30일 연장됩니다.",
      "소비기록은 마이데이터 가입 및 자산 연결을 통해 확인할 수 있으며, 마이데이터 가입 및 자산 연결에 대해 제공되는 혜택의 규모와 지급 기준은 연결페이지의 상세 내용을 확인하시기 바랍니다.",
      "반갑꾸러미 접속 대상이더라도 이미 마이데이터 이벤트에 대해 혜택 수혜 이력이 있는 경우에는 해당 혜택은 제공되지 않습니다.",
      "통신사 정기결제에 따라 제공되는 매일결제 혜택 기간 연장 혜택은 최대 1개월간 제공되며, 신청 시점과 무관하게 카드 발급일로부터 2개월 뒤 말일에 혜택 제공이 종료됩니다.",
      "통신사 정기결제에 따라 제공되는 매일결제 혜택기간 연장은 통신사 고객센터를 통해 직접 신청할 경우, 즉시 반영되지않으며 신한 SOL페이 앱을 통한 정기결제가 발생해야 받으실 수 있습니다.",
      {
        type: "nested",
        title: "이용 예시",
        items: [
          "예시 1: 통신사 정기결제 등록 시 혜택 기간 연장",
          "예시 2: 신한 SOL페이 앱을 통한 정기결제 발생 시 혜택 지급",
          "예시 3: 마이데이터 가입 및 자산 연결을 통한 혜택 확인"
        ]
      },
      "계약 체결 전, 상품설명서 및 약관을 확인하시기 바랍니다.",
      "금융소비자는 금융소비자보호법 제19조 제 1항에 따라 해당 금융상품 또는 서비스에 대하여 설명받을 권리가 있습니다.",
      "신용카드 발급이 부적정한 경우(개인신용평점 낮음, 연체(단기 포함) 사유 발생 등), 카드 발급이 제한될 수 있습니다.",
      "카드 이용대금과 이에 수반되는 모든 수수료는 고객님께서 지정하신 결제일에 상환하여야 합니다.",
      "<strong>상환능력 대비 신용카드 사용액 과도 시, 개인신용평점이 하락할 수 있습니다.</strong>",
      "<strong>개인신용평점 하락 시, 금융거래 관련 불이익이 발생할 수 있습니다.</strong>",
      "<strong>일정기간 신용카드 이용대금을 연체할 경우, 결제일이 도래하지 않은 모든 신용카드 이용대금을 변제할 의무가 발생할 수 있습니다.</strong>",
      "준법감시 심의필 제00000000-Cpi-000호<br />(2000.00.00~2000.00.00)"
    ]
  },
  COMMON_NOTICE_SECTION
];
</script>








<BoxButton
    size="xlarge"
    ariaLabel="공유하기"
  >
    <template #label>
      <Popover
        placement="bottom-center"
        content="친구에게 자랑해보세요!"
        :open="true"
        color="gray"
      >
        <span>공유하기</span>
      </Popover>
    </template>
  </BoxButton>
</template>

// 보물찾기
.floating-treasure {
  position: fixed;
  bottom: calc(160px + var(--env-b));
  right: 36px;
  z-index: var(--z-index);
  .treasure-container {
    position: relative;
    width: 118px;
    height: 134px;
  } 
  .treasure-close {
    position: absolute;
    top: 29px;
    right: 0;
    z-index: 1;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    width: 40px;
    height: 40px;
    text-align: right;
    line-height: 1;
    .treasure-close-icon {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 20px;
      height: 20px;
      background-color: var(--bg-white);
      border-radius: var(--radius-full);
      color: var(--fg-primary);
      box-shadow: 0px 2px 4px 0px #16192433;
    }
  }
  .treasure-trigger {
    position: relative;
    display: block;
    width: 118px;
    height: 134px;
  }
  .treasure-tooltip {
    position: absolute;
    top: -5px;
    left: 50%;  
    transform: translateX(-50%);
    display: block;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100% auto;
    background-image: url("#{$cdn-url}/images/pages/benefits/main/bg_treasure_tooltip.png");
    width: 83px;
    height: 36px;
    padding-top: 4px;
    @include font-set(body-s, 500);
    font-weight: 500;
    color: var(--white);
    text-align: center;
    animation: treasureBounce .8s ease-in-out infinite;
    /* @keyframes duration | timing-function | delay | iteration-count | direction | fill-mode | play-state | name */
  }
}
// 보물찾기 위치 확인 로딩
.treasure-modal {
  position: fixed;
  top: calc(0px + var(--env-t));
  left: calc(0px + var(--env-l));
  right: calc(0px + var(--env-r));
  bottom: calc(0px + var(--env-b));
  width: 100%;
  height: 100%;
  // background-color: rgba(0, 0, 0, 0.7);
  background-color: var(--bg-canvas_dark_a60);
  z-index: 600;
  pointer-events: auto;
  &.sv-popup--variant-full {
    background-color: var(--bg-canvas_dark_a60);
    .sv-popup__body {
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0;
    }
  }
  &.sv-popup .sv-popup__title {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    color: transparent;
  }
  .sv-popup__close .sv-icon {
    color: var(--white);
  }
  .treasure-modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100%;
    max-width: 312px;
    margin: 0 auto;
  }
  .treasure-loading-pending {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100%;
    text-align: center;
  }
  .loading-enter {
    margin-top: var(--spacing-md);
  }
  .loading-enter-text {
    margin-bottom: 30px;
    span {
      display: block;
      @include font-set(headline-s, 700);
      font-weight: 700;
      color: var(--white);
      text-align: center;
    }
  }
  .treasure-loading-enter {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    max-width: 312px;
    height: auto;
    margin: 0 auto;
    padding: var(--spacing-4xl) 0;
    text-align: center;
  }
  .treasure-loading-body {
    position: relative;
    width: 100%;
    margin-top: calc((30px + 36px + 56px) * -1);
  }
  .treasure-loading-lottie {
    height: 172px;
    .lottie-animation-container {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      overflow: visible;
      margin: 0 auto;
    }
  }
  .treasure-loading-body-text {
    width: 100%;
    padding-top: calc(30px + 36px);
    color: var(--white);
    @include font-set(headline-s, 700);
    font-weight: 700;
    text-align: center;
  }
  .treasure-loading-point {
    display: inline-block;
    @include font-set(headline-l, 800);
    font-weight: 800;
    color: var(--border-yellow);
    animation: treasurePoint .4s ease-in-out .7s backwards;
  }
}


// treasure(보물찾기) animation
@keyframes treasurePoint {
  0% {
    opacity: 0;
    transform: translateY(20%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes treasureBounce{
  0% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(-5px); }
  100% { transform: translateX(-50%) translateY(0); }
}




```
{% endraw %}
---
