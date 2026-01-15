
{% raw %}
```js
// 아이콘이 없을 때 (has-icon 클래스가 있을 때)
          &.has-icon {
            .sc-popover__custom[data-placement="bottom-left"] {
              left: calc((73px / 2) - 34px);
            }
            @media (max-width: 369px) {
              .sc-popover__custom[data-placement="bottom-right"] {
                right: calc((98px / 2) - 6px);
              }
            }
          }


<template>
  <section class="bf-benefit-dashboard" aria-label="혜택 대시보드">
    <!-- S : 로딩 스켈레톤-->
    <div class="dashboard-box">
      <div class="dashboard-box__inner">
        <div class="dashboard-body">
          <div class="dashboard-body__link">
            <span class="dashboard-body__label" aria-hidden="true">
              마이신한포인트
            </span>
            <div class="dashboard-body__value">
              <LoadingSkeleton :width="127" :height="29" rounded="small" />
            </div>
          </div>
          <Divider
            color="tertiary"
            orientation="vertical"
            variant="basic"
            class="dashboard-divider-vertical"
          />
          <div class="dashboard-body__link">
            <span class="dashboard-body__label" aria-hidden="true">
              {{ benefitLabel }}
            </span>
            <div class="dashboard-body__value">
              <LoadingSkeleton :width="127" :height="29" rounded="small" />
            </div>
          </div>
        </div>
        <Divider color="tertiary" variant="basic" class="dashboard-divider" />
        <div class="dashboard-footer">
          <div class="dashboard-footer__list">
            <div class="dashboard-footer__item">
              <TextButton
                text="멤버십"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              >
                <template #leftIcon>
                  <div class="dashboard-membership__icon">
                    <LoadingSkeleton :width="16" :height="16" rounded="small" />
                  </div>
                </template>
              </TextButton>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="내 쿠폰"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="참여한 이벤트"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- E : 로딩 스켈레톤-->

    <!-- 
      2-1. 마이신한포인트 영역
        - 로그인 시 현재 마이신한포인트 잔액 노출
        - 포인트 Tap > 홈페이지 [TBM004_포인트 조회] 화면으로 이동 
    -->
    <!-- case 1 - 금액 기본 멤버십 툴팁 노출 -->
    <div class="dashboard-box">
      <div class="dashboard-box__inner">
        <div class="dashboard-body">
          <a
            rold="link"
            tabindex="0"
            class="dashboard-body__link"
            :aria-label="`마이신한포인트 ${pointValue} 포인드, 더보기`"
          >
            <span class="dashboard-body__label" aria-hidden="true">
              마이신한포인트
              <Icon name="Chevron_right" size="16" />
            </span>
            <p
              class="dashboard-body__value"
              :class="valuteSizeClass"
              aria-hidden="true"
            >
              <em>{{ pointValue }}</em
              >P
            </p>
          </a>
          <Divider
            color="tertiary"
            orientation="vertical"
            variant="basic"
            class="dashboard-divider-vertical"
          />
          <a
            rold="link"
            tabindex="0"
            class="dashboard-body__link"
            :aria-label="`${benefitLabel} ${amountValue} 원, 더보기`"
          >
            <span class="dashboard-body__label" aria-hidden="true">
              {{ benefitLabel }}
              <Icon name="Chevron_right" size="16" />
            </span>
            <p
              class="dashboard-body__value"
              :class="valuteSizeClass"
              aria-hidden="true"
            >
              <em>{{ amountValue }}</em
              >원
            </p>
          </a>
        </div>
        <Divider color="tertiary" variant="basic" class="dashboard-divider" />
        <div class="dashboard-footer">
          <div
            class="dashboard-footer__list"
            :class="{ 'has-icon': !hasMembershipIcon }"
          >
            <div class="dashboard-footer__item">
              <TextButton
                text="멤버십"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
                @click="isMembershipOpen = true"
              >
                <template #leftIcon v-if="hasMembershipIcon">
                  <div class="dashboard-membership__icon">
                    <ScImage
                      :src="`${$cdnURL}/images/pages/benefits/main/icon_membership_b.png`"
                      alt="등급"
                    />
                  </div>
                </template>
              </TextButton>

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div class="sc-popover__custom" data-placement="bottom-left">
                <div class="sc-popover__custom-content">
                  <span>멤버십 등급이 변경됐어요.</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="내 쿠폰"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div
                class="sc-popover__custom"
                data-placement="bottom-center"
                hidden
              >
                <div class="sc-popover__custom-content">
                  <span>유효기간이 곧 끝나는 쿠폰이 있어요!</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="참여한 이벤트"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div
                class="sc-popover__custom"
                data-placement="bottom-right"
                hidden
              >
                <div class="sc-popover__custom-content">
                  <span>이벤트 결과를 확인해보세요.</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- case 2 - 금액 18px 내 쿠폰 툴팁 노출 -->
    <div class="dashboard-box">
      <div class="dashboard-box__inner">
        <div class="dashboard-body">
          <a
            rold="link"
            tabindex="0"
            class="dashboard-body__link"
            :aria-label="`마이신한포인트 ${pointValue2} 포인드, 더보기`"
          >
            <span class="dashboard-body__label" aria-hidden="true">
              마이신한포인트
              <Icon name="Chevron_right" size="16" />
            </span>
            <p
              class="dashboard-body__value"
              :class="valuteSizeClass2"
              aria-hidden="true"
            >
              <em>{{ pointValue2 }}</em
              >P
            </p>
          </a>
          <Divider
            color="tertiary"
            orientation="vertical"
            variant="basic"
            class="dashboard-divider-vertical"
          />
          <a
            rold="link"
            tabindex="0"
            class="dashboard-body__link"
            :aria-label="`${benefitLabel} ${amountValue2} 원, 더보기`"
          >
            <span class="dashboard-body__label" aria-hidden="true">
              {{ benefitLabel }}
              <Icon name="Chevron_right" size="16" />
            </span>
            <p
              class="dashboard-body__value"
              :class="valuteSizeClass2"
              aria-hidden="true"
            >
              <em>{{ amountValue2 }}</em
              >원
            </p>
          </a>
        </div>
        <Divider color="tertiary" variant="basic" class="dashboard-divider" />
        <div class="dashboard-footer">
          <div
            class="dashboard-footer__list"
            :class="{ 'has-icon': !hasMembershipIcon2 }"
          >
            <div class="dashboard-footer__item">
              <TextButton
                text="멤버십"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              >
                <template #leftIcon v-if="hasMembershipIcon2">
                  <div class="dashboard-membership__icon">
                    <ScImage
                      :src="`${$cdnURL}/images/pages/benefits/main/icon_membership_b.png`"
                      alt="등급"
                    />
                  </div>
                </template>
              </TextButton>

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div
                class="sc-popover__custom"
                data-placement="bottom-left"
                hidden
              >
                <div class="sc-popover__custom-content">
                  <span>멤버십 등급이 변경됐어요.</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="내 쿠폰"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div class="sc-popover__custom" data-placement="bottom-center">
                <div class="sc-popover__custom-content">
                  <span>유효기간이 곧 끝나는 쿠폰이 있어요!</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="참여한 이벤트"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div
                class="sc-popover__custom"
                data-placement="bottom-right"
                hidden
              >
                <div class="sc-popover__custom-content">
                  <span>이벤트 결과를 확인해보세요.</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- case 3 - 금액 14px 참여한 이벤트 툴팁 노출 -->
    <div class="dashboard-box">
      <div class="dashboard-box__inner">
        <div class="dashboard-body">
          <a
            rold="link"
            tabindex="0"
            class="dashboard-body__link"
            :aria-label="`마이신한포인트 ${pointValue3} 포인드, 더보기`"
          >
            <span class="dashboard-body__label" aria-hidden="true">
              마이신한포인트
              <Icon name="Chevron_right" size="16" />
            </span>
            <p
              class="dashboard-body__value"
              :class="valuteSizeClass3"
              aria-hidden="true"
            >
              <em>{{ pointValue3 }}</em
              >P
            </p>
          </a>
          <Divider
            color="tertiary"
            orientation="vertical"
            variant="basic"
            class="dashboard-divider-vertical"
          />
          <a
            rold="link"
            tabindex="0"
            class="dashboard-body__link"
            :aria-label="`${benefitLabel} ${amountValue3} 원, 더보기`"
          >
            <span class="dashboard-body__label" aria-hidden="true">
              {{ benefitLabel }}
              <Icon name="Chevron_right" size="16" />
            </span>
            <p
              class="dashboard-body__value"
              :class="valuteSizeClass3"
              aria-hidden="true"
            >
              <em>{{ amountValue3 }}</em
              >원
            </p>
          </a>
        </div>
        <Divider color="tertiary" variant="basic" class="dashboard-divider" />
        <div class="dashboard-footer">
          <div
            class="dashboard-footer__list"
            :class="{ 'has-icon': !hasMembershipIcon3 }"
          >
            <div class="dashboard-footer__item">
              <TextButton
                text="멤버십"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              >
                <template #leftIcon v-if="hasMembershipIcon3">
                  <div class="dashboard-membership__icon">
                    <ScImage
                      :src="`${$cdnURL}/images/pages/benefits/main/icon_membership_b.png`"
                      alt="등급"
                    />
                  </div>
                </template>
              </TextButton>

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div
                class="sc-popover__custom"
                data-placement="bottom-left"
                hidden
              >
                <div class="sc-popover__custom-content">
                  <span>멤버십 등급이 변경됐어요.</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="내 쿠폰"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div
                class="sc-popover__custom"
                data-placement="bottom-center"
                hidden
              >
                <div class="sc-popover__custom-content">
                  <span>유효기간이 곧 끝나는 쿠폰이 있어요!</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="참여한 이벤트"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />

              <!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div class="sc-popover__custom" data-placement="bottom-right">
                <div class="sc-popover__custom-content">
                  <span>이벤트 결과를 확인해보세요.</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- S : IF 오류시 - 멤버십 아이콘 노출 X -->
    <div class="dashboard-box">
      <div class="dashboard-box__inner">
        <div class="dashboard-body__error">
          <span class="dashboard-body__error-text"
            >정보를 불러오지 못했어요</span
          >
          <CapsuleButton
            text="내 포인트 확인하기"
            color="primary"
            variant="outline"
            size="small"
          />
        </div>
        <Divider color="tertiary" variant="basic" class="dashboard-divider" />
        <div class="dashboard-footer">
          <div class="dashboard-footer__list has-icon">
            <div class="dashboard-footer__item">
              <TextButton
                text="멤버십"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              /><!-- 툴팁 - 활성화 시 hidden 속성 제거 -->
              <div class="sc-popover__custom" data-placement="bottom-left">
                <div class="sc-popover__custom-content">
                  <span>멤버십 등급이 변경됐어요.</span>
                </div>
              </div>
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="내 쿠폰"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />
            </div>
            <Divider
              color="tertiary"
              orientation="vertical"
              variant="basic"
              class="dashboard-divider-vertical"
            />
            <div class="dashboard-footer__item">
              <TextButton
                text="참여한 이벤트"
                color="secondary"
                size="small"
                class="dashboard-footer__link"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- E : IF 오류시 -->

    <!-- S : 로그아웃 -->
    <div class="bf-if__login">
      <div class="bf-if__error-inner">
        <div class="bf-if__error-icon">
          <ScImage
            :src="`${$cdnURL}/images/pages/benefits/main/result_icon.png`"
            alt="IF 오류"
          />
        </div>
        <div class="bf-if__error-text">로그인하고 내 혜택을 확인해보세요!</div>
        <CapsuleButton
          text="로그인하기"
          color="primary"
          variant="outline"
          size="small"
        />
      </div>
    </div>
    <!-- E : 로그아웃 -->
  </section>

  <!-- 멤버십 BottomSheet 
   - SBT031A01.vue 개발시 기존 모달 호출하는 형식으로 호출 현재는 UI확인용으로 임시 호출
  -->
  <BottomSheet
    closableDimm
    dimmed
    title="멤버십·리워드​"
    v-model="isMembershipOpen"
    class="sc-membership__bs"
  >
    <div class="sc-membership__list">
      <BasicList
        v-for="item in membershipItems"
        :key="item.id"
        as="div"
        class="sc-membership__item"
      >
        <span class="sc-membership__label">{{ item.label }}</span>
        <template #icon>
          <BoxButton
            color="quaternary"
            size="small"
            text="보기"
            @click.stop="handleViewClick(item)"
          />
        </template>
      </BasicList>
    </div>
  </BottomSheet>
</template>

<script setup>
import { computed, inject, ref, watch, onUnmounted } from "vue";
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  BasicList,
  BottomSheet,
  BoxButton,
  CapsuleButton,
  Divider,
  Icon,
  LoadingSkeleton,
  TextButton,
} from "@shc-nss/ui/solid";

const { $cdnURL } = inject(AppContextKey);

// 마이신한포인트 값 (실제 데이터로 교체 필요)
const pointValue = ref("123,000");
// 이번달 받은 혜택 값 (실제 데이터로 교체 필요)
const amountValue = ref("117,000");
// 혜택 라벨 (이번달/지난달 구분, 실제 데이터로 교체 필요)
const benefitLabel = ref("이번달 받은 혜택"); // 또는 "지난달 받은 혜택"

// 금액 기준으로 폰트 사이즈 클래스 반환
// 둘 중 하나라도 조건에 해당하면 둘 다 같은 폰트 사이즈 적용
// 천만원대 이하 (10,000,000 미만): 18px (large)
// 기본 (10,000,000 ~ 99,999,999): 16px (기본값)
// 1억 이상 (100,000,000 이상): 14px (small)
const getNumericValue = (value) => {
  if (!value) return 0;
  return parseInt(value.toString().replace(/,/g, ""), 10);
};

const getValuteSizeClass = (point, amount) => {
  // 둘 중 하나라도 1억 이상이면 둘 다 small (14px)
  if (point >= 100000000 || amount >= 100000000) {
    return { "dashboard-body__value--small": true };
  }
  // 둘 중 하나라도 천만원대 이하면 둘 다 large (18px)
  if (point < 10000000 || amount < 10000000) {
    return { "dashboard-body__value--large": true };
  }
  // 둘 다 천만원대 이상 1억 미만이면 기본 (16px, 클래스 없음)
  return {};
};

const valuteSizeClass = computed(() => {
  const point = getNumericValue(pointValue.value);
  const amount = getNumericValue(amountValue.value);
  return getValuteSizeClass(point, amount);
});

// 테스트용 데이터 (UI 확인용)
// 기본 금액 (16px) - 천만원대 이상 1억 미만
const pointValue2 = ref("10,000,000");
const amountValue2 = ref("50,000,000");
const pointValue3 = ref("123,000");
const amountValue3 = ref("1,000,000,000");

// 테스트용 폰트 사이즈 클래스 (valuteSizeClass와 별도)
const valuteSizeClass2 = computed(() => {
  const point = getNumericValue(pointValue2.value);
  const amount = getNumericValue(amountValue2.value);
  return getValuteSizeClass(point, amount);
});

const valuteSizeClass3 = computed(() => {
  const point = getNumericValue(pointValue3.value);
  const amount = getNumericValue(amountValue3.value);
  return getValuteSizeClass(point, amount);
});

// case 1 멤버십 아이콘 표시 여부 (실제 데이터로 교체 필요)
const hasMembershipIcon = ref(true);
// case 2 멤버십 아이콘 표시 여부 (실제 데이터로 교체 필요)
const hasMembershipIcon2 = ref(true);
// case 3 멤버십 아이콘 표시 여부 (실제 데이터로 교체 필요)
const hasMembershipIcon3 = ref(false);

// 멤버십 BottomSheet 상태
const isMembershipOpen = ref(false);

// html overflow 제어
watch(isMembershipOpen, (isOpen) => {
  if (typeof document !== "undefined") {
    const htmlElement = document.documentElement;
    if (isOpen) {
      htmlElement.style.overflow = "hidden";
    } else {
      htmlElement.style.overflow = "";
    }
  }
});

// 컴포넌트 언마운트 시 overflow 제거
onUnmounted(() => {
  if (typeof document !== "undefined") {
    document.documentElement.style.overflow = "";
  }
});

// 멤버십 리스트 아이템들
const membershipItems = [
  { id: "sol-membership", label: "SOL 멤버십" },
  { id: "d-club", label: "D-Club" },
  { id: "tops-club", label: "Tops Club" },
  { id: "welcome-gift", label: "웰컴 기프트팩" },
  { id: "friend-referral", label: "친구추천 기프트팩" },
  { id: "welcome-checkin", label: "웰컴체크인" },
];

// 보기 버튼 클릭 핸들러
const handleViewClick = (item) => {
  console.log(`${item.label} 보기 클릭됨`);
  // TODO: 각 항목별 상세 페이지로 이동하는 로직 구현
};
</script>




```
{% endraw %}
---
