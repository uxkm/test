# SBT068A01

{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT068A01
  title: 앱테크
  menu: 혜택 > 앱테크 메인화면
  layout: SubLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  header:
    variant: sub
    fixed: true
    back: true
    close: false
    home: true
  appClassList: "sc-bf__apptech"
  mainClassList: "bf-apptech__submain"
</route>
<template>
  <!-- 
   앱테크 메인화면 정의
    - 화면 진입 시 스켈레톤 UI 적용
    - 로딩 시 화면 내 모듈별 독립적으로 로딩
    - 로딩 시 공통 스피너 UI 적용
    - 이미지 영역에 이미지 정상적으로 호출하지 못할 경우 디폴트 이미지 노출 (단, 외부광고 배너 제외)
  -->
  <!-- S : 로딩중 스켈레톤 -->
  <div
    class="card-grid__skeleton apptech"
    aria-label="로딩중"
    tabindex="0"
  >
    <section aria-hidden="true">
      <article class="px-2xl">
        <LoadingSkeleton
          width="100%"
          :height="100"
          rounded="small"
        />
      </article>
      <article class="apptech-today">
        <div class="apptech-today__header">
          <h2 class="apptech-title">오늘의 앱테크</h2>
          <div class="apptech-today__actions">
            <div class="action-btn action-btn__detail">
              <LoadingSkeleton
                :width="20"
                :height="20"
                rounded="small"
              />
              <span
                class="action-btn__text"
                aria-hidden="true"
                >포인트 상세</span
              >
            </div>
            <Divider
              variant="basic"
              orientation="vertical"
              color="tertiary"
              size="full"
            />
            <div class="action-btn action-btn__settings">
              <span
                class="action-btn__text"
                aria-hidden="true"
                >설정</span
              >
            </div>
          </div>
        </div>
        <div class="apptech-today__body">
          <ul class="today-list">
            <li
              v-for="i in 6"
              :key="i"
              class="today-list__item"
            >
              <LoadingSkeleton
                width="100%"
                :height="86"
                rounded="medium"
              />
            </li>
          </ul>
        </div>
      </article>
      <article class="today-mission">
        <div class="banner-item">
          <LoadingSkeleton
            width="100%"
            :height="82"
            rounded="medium"
          />
        </div>
      </article>
      <article class="inlifle-banner">
        <div class="banner-item">
          <LoadingSkeleton
            width="100%"
            :height="82"
            rounded="medium"
          />
        </div>
        <div class="adpicon-banner">
          <div class="adpicon-banner__carousel">
            <figure class="adpicon-banner__card-inner">
              <div class="adpicon-banner__card-visual">
                <LoadingSkeleton
                  width="100%"
                  :height="200"
                  rounded="large"
                />
              </div>
              <figcaption class="adpicon-banner__content">
                <LoadingSkeleton
                  width="50%"
                  :height="26"
                  rounded="small"
                />
                <LoadingSkeleton
                  width="100%"
                  :height="44"
                  rounded="small"
                />
                <div class="adpicon-banner__actions">
                  <LoadingSkeleton
                    width="30%"
                    :height="26"
                    rounded="small"
                  />
                </div>
              </figcaption>
            </figure>
          </div>
          <div class="adpicon-banner__controls">
            <LoadingSkeleton
              width="30%"
              :height="8"
              rounded="small"
            />
          </div>
          <div class="adpicon-banner__more">
            <LoadingSkeleton
              width="100%"
              height="100%"
              rounded="small"
            />
          </div>
        </div>
      </article>
    </section>
    <Divider
      variant="group"
      color="tertiary"
    />
    <section aria-hidden="true">
      <h2 class="apptech-title">포인트 더 받기</h2>
      <ul class="sc-point-more__list">
        <li
          v-for="i in 6"
          :key="i"
        >
          <ListItem align="centered">
            <template #leftIcon>
              <div class="point-icon">
                <LoadingSkeleton
                  :width="48"
                  :height="48"
                  rounded="large"
                />
              </div>
            </template>
            <template #leftMainText>
              <LoadingSkeleton
                width="100%"
                :height="22"
                rounded="small"
              />
            </template>
          </ListItem>
        </li>
      </ul>
    </section>
  </div>
  <!-- E : 로딩중 스켈레톤 -->

  <!-- 콘텐츠 영역 -->
  <div class="sc-contents__body apptech">
    <section>
      <!-- 
        외부광고 배너 영역
        - 통이미지 노출
        - 자동전시영역 (어드민 전시관리 대상아님)
        - 배너 Tap > 아웃링크 연결 (디바이스에 따라 크롬, 사파리 등 외부 브라우저로 해당 url 연결)
        - 로딩 중 타임아웃, 로딩지연 시 영역 히든
        - 등록된 외부 광고 없는 경우 앱테크 배너 노출
        - 별도 refresh 정책 적용
      -->
      <article aria-label="외부 광고 배너">
        <a
          rol="link"
          aria-label="익시오 앱 무료 다운로드 이동"
        >
          <img
            :src="`${$cdnURL}/images/pages/benefits/main/img_export.png`"
            alt="익시오 앱 무료 다운로드 - 통화녹음&요약 AI앱 익시오 AD Moloco 광고입니다."
            class="export-banner"
          />
        </a>
      </article>

      <!-- 
        3. 오늘의 앱테크 영역
        - 게임 서비스 & 오늘의 미션 하드코딩 영역
        - 어드민 전시관리 대상영역 아님, 변경점 발생 시 CSR 작성
        - 획득한 포인트는 익일 적립 (포인트팡팡과 동일방식)
        
        3-1. 타이틀
        - 오늘의 앱테크 (고정)
        
        3-2. 포인트상세
        - 로그아웃 상태에서 Tap > 마지막으로 로그인한 로그인 수단 노출
        - '포인트상세' Tap > [혜택 > 앱테크 > 포인트 상세] 화면으로 이동
        
        3-3. 설정
        - 로그아웃 상태에서 Tap > 마지막으로 로그인한 로그인 수단 노출
        - 앱테크 서비스 중 약관에 동의한 서비스가 있는 경우 버튼 노출
        - '설정' Tap > [혜택 > 앱테크 > 설정] 화면으로 이동
        
        3-4. 게임하고 매일 랜덤 포인트
        - 게임 선택 시 개별 화면으로 연결
        - 통이미지 적용 - 디자인에 맞추어서 아이콘만 제공 bg는 css처리 (뱃지 제외)
        
        [룰렛돌리기]
        - Tap > 링크: https://apptech-dev.sh-adtech.com/#/rouletteread
        
        [가위바위보]
        - Tap > 링크: https://apptech-dev.sh-adtech.com/#/rpsrouletteread/2
        
        [사다리타기]
        - Tap > 링크: https://dev-web.anick.io/shinhan/ladder?userKey=test&clientCode=shinhancard&adid=c855f53c-d6c-407c-9932-af448bf6f792&productCode=LADDER
        - (11월 말 url 변경 예정)
        
        [무료사주]
        - Tap > 링크: https://apptech-dev.sh-adtech.com/#/todaytarocard
        
        [쿠팡 혜택]
        - 로그아웃 상태에서 Tap > 마지막으로 로그인한 로그인 수단 노출
        - 로그인 상태에서 Tap >
          - 약관 미동의한 경우 약관 동의 화면으로 이동
          - 약관 동의한 경우 쇼핑 적립 화면(제휴사 화면)으로 이동
        - 링크: https://pay.shinhancard.com/pay/PAYFM006N/PAYFM006001.shc?afoCd=BO&menuCd=0
        
        [포인트박스]
        - Tap > 링크: https://dev-web.anick.io/shinhan?userKey=test&clientCode=shinhancard&adid=c855f53c-5d6c-407c-9932-af448bf6f792
        - (11월 말 url 변경 예정)
      -->
      <article
        class="apptech-today"
        aria-label="오늘의 앱테크"
      >
        <div class="apptech-today__header">
          <h2 class="apptech-title">오늘의 앱테크</h2>
          <div class="apptech-today__actions">
            <a
              role="link"
              class="action-btn action-btn__detail"
              aria-label="포인트 상세 화면으로 이동"
            >
              <ScImage
                src="/images/pages/benefits/main/Coin_Point.svg"
                alt=""
                aria-hidden="true"
                class="action-btn__icon"
              />
              <span
                class="action-btn__text"
                aria-hidden="true"
                >포인트 상세</span
              >
            </a>
            <Divider
              variant="basic"
              orientation="vertical"
              color="tertiary"
              size="full"
            />
            <a
              role="link"
              class="action-btn action-btn__settings"
              aria-label="설정 화면으로 이동"
            >
              <span
                class="action-btn__text"
                aria-hidden="true"
                >설정</span
              >
            </a>
          </div>
        </div>
        <div class="apptech-today__body">
          <ul class="today-list">
            <li
              v-for="(game, index) in todayGameList"
              :key="index"
              class="today-list__item"
            >
              <a
                role="link"
                :class="['today-list__link', game.bgClass]"
                :aria-label="game.label"
              >
                <TextBadge
                  v-if="game.badge"
                  :color="game.badge === 'is-hot' ? 'blue' : 'red'"
                  :text="game.badge === 'is-hot' ? 'HOT' : 'NEW'"
                  variant="solid"
                  class="today-list__badge"
                />
                <ScImage
                  :src="game.icon"
                  alt=""
                  aria-hidden="true"
                />
                <span
                  class="today-list__label"
                  aria-hidden="true"
                  >{{ game.label }}</span
                >
              </a>
            </li>
          </ul>
        </div>
      </article>

      <!-- 
        1. 오늘의 미션 영역
        
        배너 Tap
        - 로그아웃 상태에서 Tap > 마지막으로 로그인한 로그인 수단 노출
        - 약관 미동의한 경우 약관 동의 화면으로 이동
        - 약관 동의한 경우 [혜택 > 앱테크 > 오늘의 미션] 화면으로 이동
        - 링크: https://apptech-dev.sh-adtech.com/#/todaymission
      -->
      <article
        class="today-mission"
        aria-label="오늘의 미션"
      >
        <div class="banner-item">
          <a
            role="link"
            aria-label="매일 새로운 미션 포인트 도착! 최대 70만 포인트"
            class="banner-item__link"
          >
            <div
              class="banner-item__img"
              aria-hidden="true"
            >
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/icon_bn01.png`"
                alt=""
              />
            </div>
            <div
              class="banner-item__label"
              aria-hidden="true"
            >
              <span>매일 새로운</span>
              <strong>미션 포인트 도착!</strong>
            </div>
            <div class="banner-item__actions">
              <div
                class="point-badge"
                aria-hidden="true"
              >
                <img
                  :src="`${$cdnURL}/images/pages/benefits/main/icon_point_yellow-18.png`"
                  alt=""
                />
                <span>최대 999만</span>
              </div>
            </div>
          </a>
        </div>
      </article>

      <!-- 
        2. 포인트 눌러서 바로 적립 영역
        - 자동전시영역 (어드민 전시관리 대상 아님)
        - 화면진입 케이스에 따라 아래와 같이 분기처리
          - 앱회원 & 로그아웃: 마지막으로 로그인한 로그인 수단 노출
          - 앱회원 & 로그인 & 이용약관 미동의: 약관 동의 화면 노출
          - 앱회원 & 로그인 & 이용약관 동의: 아웃링크 연결
      -->
      <!-- 어드민 관리 -->
      <article
        class="inlifle-banner"
        aria-label="인라이플 배너 영역"
      >
        <!-- 
          2-1. 인라이플 배너 영역
          - 전달받은 이미지(a) + 포인트 값(b) 노출 자동 전시영역
          
          a. 이미지 개수는 맞춤형광고가 있는 경우와 없는 경우 상이
            - 맞춤형광고 있는 경우: 1개 노출 (320x100)
            - 맞춤형광고 없는 경우: 3개 노출 (100x100)
              - 광고 이미지 2개 (각각 전달받는 url로 연결)
              - 쿠팡 로고 이미지 1개 (선택불가)
          
          - 배너 Tap > 아웃링크 연결 (디바이스에 따라 크롬, 사파리 등 외부 브라우저로 연결)
          - c. 문의하기 선택 시 외부 브라우저로 연결
          - 로딩 중 타임아웃 or 로딩지연 or 전달데이터(a and b)없는 경우, 2-1영역 히든 처리
          - 포인트 광고 소진 시 포인트 값(b)은 미전달(오류 아님)
          - 별도 refresh 정책 적용

          *** 인라이플 배너는 2가지 케이스만 있음. 통이미지 형태 배너, 쿠팡 형태 배너 ***
        -->
        <div class="banner-item coupang">
          <a
            role="link"
            aria-label="쿠팡 간편 적립 100포인트"
            class="banner-item__link"
          >
            <div
              class="banner-item__img row-flex"
              aria-hidden="true"
            >
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/img_dummy01.png`"
                alt=""
              />
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/img_dummy02.png`"
                alt=""
              />
            </div>
            <div class="banner-item__actions">
              <div class="logo">
                <img
                  :src="`${$cdnURL}/images/pages/benefits/main/logo_coupang.png`"
                  alt=""
                />
              </div>
              <div
                class="point-badge"
                aria-hidden="true"
              >
                <img
                  :src="`${$cdnURL}/images/pages/benefits/main/icon_point_yellow-18.png`"
                  alt=""
                />
                <span>+100</span>
              </div>
            </div>
          </a>
          <a
            role="button"
            class="banner-item__more"
          >
            <span>문의하기</span>
          </a>
        </div>
        <div class="banner-item inlifle">
          <a
            role="link"
            aria-label="쿠팡 간편 적립 100포인트"
            class="banner-item__link"
          >
            <div
              class="banner-item__img row-flex"
              aria-hidden="true"
            >
              <img
                :src="`${$cdnURL}/images/pages/benefits/main/visual_apptech_bnr0.png`"
                alt=""
              />
            </div>
            <div class="banner-item__actions">
              <div
                class="point-badge"
                aria-hidden="true"
              >
                <img
                  :src="`${$cdnURL}/images/pages/benefits/main/icon_point_yellow-18.png`"
                  alt=""
                />
                <span>+100</span>
              </div>
            </div>
          </a>
          <a
            role="button"
            class="banner-item__more"
          >
            <span>문의하기</span>
          </a>
        </div>

        <!-- 
          2-2. 애드팝콘 배너 영역
          - 0~4개 까지 노출
          - 1개 이상인 경우 점형 인디케이터 하단 노출
          - 전달받은 통이미지(a) + 포인트 값(b) + 타이틀(c) + 서브타이틀(d) 노출
          - 타이틀 최대 1줄 노출, 초과시 ...처리
          - 서브타이틀 최대 2줄 노출, 초과시 ...처리
          - 배너 Tap > 아웃링크 연결 (디바이스에 따라 크롬, 사파리 등 외부 브라우저로 연결)
          - 로딩 중 타임아웃 or 로딩지연 or 전달데이터 없는 경우, 디폴트 이미지 노출
          - 별도 refresh 정책 적용
          - 더보기 버튼 Tap > [오퍼월 > 포인트 충전소 : 참여적립 화면] 으로 이동
        -->
        <div
          class="adpicon-banner"
          aria-label="애드팝콘"
        >
          <Carousel
            rootClass="adpicon-banner__carousel"
            :pagination="slides.length > 1"
            pagination-type="bullets"
            pagination-placement="outside-center"
            :autoplay="false"
            :loop="false"
            :space-between="16"
            :centered-slides="slides.length > 1"
            :navigation="slides.length > 1"
            :allow-touch-move="slides.length > 1"
            :auto-height="true"
          >
            <CarouselItem
              v-for="(slide, i) in slides"
              :key="i"
            >
              <a
                role="link"
                :aria-label="`${slide.title} ${slide.description} ${slide.rewardText}`"
                class="adpicon-banner__card"
              >
                <figure class="adpicon-banner__card-inner">
                  <div class="adpicon-banner__card-visual">
                    <img
                      :src="slide.image"
                      alt=""
                    />
                  </div>
                  <figcaption class="adpicon-banner__content">
                    <strong class="adpicon-banner__title">{{ slide.title }}</strong>
                    <p class="adpicon-banner__description">{{ slide.description }}</p>
                    <div
                      v-if="slide.rewardText"
                      class="adpicon-banner__actions"
                    >
                      <div
                        class="point-badge"
                        :aria-label="slide.rewardText"
                        aria-hidden="true"
                      >
                        <img
                          :src="`${$cdnURL}/images/pages/benefits/main/icon_point_yellow-18.png`"
                          alt=""
                        />
                        <span>{{ slide.rewardText }}</span>
                      </div>
                    </div>
                  </figcaption>
                </figure>
              </a>
            </CarouselItem>
          </Carousel>
          <TextButton
            text="더보기"
            color="secondary"
            size="small"
            :rightIcon="{ iconName: 'Chevron_right' }"
            aria-label="포인트 충전소 참여적립 더보기"
            class="adpicon-banner__more"
          />
        </div>
      </article>
    </section>

    <Divider
      variant="group"
      color="tertiary"
    />
    <!-- 
      3. 포인트 더 받기
      - 목록 Tap > 플레이 앱 Deep Link페이지 이동 (back시 앱테크 화면으로 히스토리백)
      - 회원/로그인 정책 각 서비스별 정책 따름
      - 이미지+텍스트 하드코딩 영역으로, 현업 요청에 따라 변경될 수 있음
        - (변경 시 CSR작업 필요)
      
      3-1. 숏폼보고 포인트 받기
      - 링크: 숏핑 플러스 서비스 안내 화면
      
      3-2. 도장찍고 포인트 받기
      - 링크: 마이데이터 이벤트 단축url 연결
      - URL: https://shcard.io/apptech01
      
      3-3. 라방보고 포인트 받기
      - 링크: 라방플러스 딥링크 연결
      
      3-4. 광고보고 포인트 받기
      - 링크: 포인트팡팡 딥링크 연결
      
      3-5. 하루 3번 포인트 받기
      - 링크: 오늘의줍줍 딥링크 연결
      
      3-6. 올댓에서 포인트 받기
      - 링크: 올댓쇼핑 딥링크 연결
    -->
    <section aria-label="포인트 더 받기">
      <h2 class="apptech-title">포인트 더 받기</h2>
      <ul class="sc-point-more__list">
        <li
          v-for="(item, index) in pointMoreList"
          :key="index"
        >
          <a
            role="link"
            :aria-label="item.label"
            class="point-more__item"
          >
            <ListItem align="centered">
              <template #leftIcon>
                <div class="point-icon">
                  <ScImage
                    :src="item.icon"
                    alt=""
                    aria-hidden="true"
                  />
                </div>
              </template>
              <template #leftMainText>
                <span>{{ item.label }}</span>
              </template>
            </ListItem>
          </a>
        </li>
      </ul>
    </section>
  </div>
</template>
<script setup>
import { AppContextKey } from "@/configs/inject/appContext";
import { ScImage } from "@shc-nss/ui/shc";
import {
  Carousel,
  CarouselItem,
  Divider,
  ListItem,
  LoadingSkeleton,
  TextBadge,
  TextButton,
} from "@shc-nss/ui/solid";
import { inject } from "vue";

const { $cdnURL } = inject(AppContextKey);

// 오늘의 앱테크 게임 목록
const todayGameList = [
  {
    label: "룰렛 돌리기",
    icon: "/images/pages/benefits/main/icon_today01_36.png",
    bgClass: "bg-brand",
    badge: "",
    link: "https://apptech-dev.sh-adtech.com/#/rouletteread",
  },
  {
    label: "가위바위보",
    icon: "/images/pages/benefits/main/icon_today02_36.png",
    bgClass: "bg-cyan",
    badge: "",
    link: "https://apptech-dev.sh-adtech.com/#/rpsrouletteread/2",
  },
  {
    label: "사다리타기",
    icon: "/images/pages/benefits/main/icon_today03_36.png",
    bgClass: "bg-red",
    badge: "",
    link: "https://dev-web.anick.io/shinhan/ladder?userKey=test&clientCode=shinhancard&adid=c855f53c-d6c-407c-9932-af448bf6f792&productCode=LADDER",
  },
  {
    label: "무료 사주",
    icon: "/images/pages/benefits/main/icon_today04_36.png",
    bgClass: "bg-brand",
    badge: "is-hot",
    link: "https://apptech-dev.sh-adtech.com/#/todaytarocard",
  },
  {
    label: "쿠팡 혜택",
    icon: "/images/pages/benefits/main/icon_today05_36.png",
    bgClass: "bg-red",
    badge: "is-new",
    link: "https://pay.shinhancard.com/pay/PAYFM006N/PAYFM006001.shc?afoCd=BO&menuCd=0",
  },
  {
    label: "포인트박스",
    icon: "/images/pages/benefits/main/icon_today06_36.png",
    bgClass: "bg-brand",
    badge: "is-hot",
    link: "https://dev-web.anick.io/shinhan?userKey=test&clientCode=shinhancard&adid=c855f53c-5d6c-407c-9932-af448bf6f792",
  },
];

// 애드팝콘 배너 목록
const slides = [
  {
    title:
      "11번가 X 갤럭시 이벤트11번가 X 갤럭시 이벤트11번가 X 갤럭시 이벤트11번가 X 갤럭시 이벤트",
    description:
      "연말이면 HOT한 갤럭시 인기아이템 총집합 갤럭시 브랜드위크 인기아이템 총집합 갤럭시 브랜드위크 총집합 갤럭시 브랜드위크",
    image: `${$cdnURL}/images/pages/benefits/main/visual_apptech_exad01.png`,
    rewardText: "최대 70만",
    link: "#",
  },
  {
    title: "11번가 X 갤럭시 이벤트",
    description:
      "연말이면 HOT한 갤럭시 인기아이템 총집합 갤럭시 브랜드위크 인기아이템 총집합 갤럭시 브랜드위크",
    image: `${$cdnURL}/images/pages/benefits/main/visual_apptech_exad01.png`,
    rewardText: "최대 70만",
    link: "#",
  },
  {
    title: "11번가 X 갤럭시 이벤트",
    description:
      "연말이면 HOT한 갤럭시 인기아이템 총집합 갤럭시 브랜드위크 인기아이템 총집합 갤럭시 브랜드위크",
    image: `${$cdnURL}/images/pages/benefits/main/visual_apptech_exad01.png`,
    rewardText: "최대 70만",
    link: "#",
  },
  {
    title: "11번가 X 갤럭시 이벤트",
    description:
      "연말이면 HOT한 갤럭시 인기아이템 총집합 갤럭시 브랜드위크 인기아이템 총집합 갤럭시 브랜드위크",
    image: `${$cdnURL}/images/pages/benefits/main/visual_apptech_exad01.png`,
    rewardText: "",
    link: "#",
  },
];

// 포인트 더 받기 목록
const pointMoreList = [
  {
    label: "숏폼보고 포인트 받기",
    icon: "/images/pages/benefits/main/icon_indigo-700.png",
    link: "#", // 숏핑 플러스 서비스 안내 화면
  },
  {
    label: "도장찍고 포인트 받기",
    icon: "/images/pages/benefits/main/icon_red-400.png",
    link: "https://shcard.io/apptech01", // 마이데이터 이벤트 단축url
  },
  {
    label: "라방보고 포인트 받기",
    icon: "/images/pages/benefits/main/icon_purple-600.png",
    link: "#", // 라방플러스 딥링크
  },
  {
    label: "광고보고 포인트 받기",
    icon: "/images/pages/benefits/main/icon_blue-400.png",
    link: "#", // 포인트팡팡 딥링크
  },
  {
    label: "하루 3번 포인트 받기",
    icon: "/images/pages/benefits/main/icon_green-200.png",
    link: "#", // 오늘의줍줍 딥링크
  },
  {
    label: "올댓에서 포인트 받기",
    icon: "/images/pages/benefits/main/icon_brand-300.png",
    link: "#", // 올댓쇼핑 딥링크
  },
];
</script>


```

{% endraw %}
---
