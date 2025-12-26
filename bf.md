
{% raw %}
```js

<route lang="yaml">
meta:
  id: SBT001A01
  title: 혜택
  menu: "혜택 > 혜택"
  layout: MainLayout
  category: 혜택
  publish: 김대민
  publishVersion: 0.8
  status: 작업중
  appClassList: "app_benefits"
  mainClassList: "benefits_main"
</route>
<template>
  <!-- 스켈레톤 로딩이 로딩이 완료된 모듈부터 콘텐츠 제공  -->
  <div class="sc-contents__body bf-main">
    <!-- S: 혜택 대시보드 호출 -->
    <SBT001A01Dashboard />
    <!-- E: 혜택 대시보드 호출 -->

    <!-- S: 추천 혜택 호출 -->
    <SBT001A01RecommendBenefit />
    <!-- E: 추천 혜택 호출 -->

    <!-- S: 배너 호출 -->
    <SBT001A01Banner />
    <!-- E: 배너 호출 -->

    <!-- S: 퀴즈팡팡 호출 -->
    <SBT001A01QuizPangpang />
    <!-- E: 퀴즈팡팡 호출 -->

    <!-- S: 포인트팡팡 호출 -->
    <SBT001A01PointPangpang />
    <!-- E: 포인트팡팡 호출 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 카테고리 호출 -->
    <SBT001A01Category />
    <!-- E: 카테고리 호출 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 앱테크 호출 -->
    <SBT001A01Apptech />
    <!-- E: 앱테크 호출 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 이벤트 호출 -->
    <SBT001A01Event />
    <!-- E: 이벤트 호출 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 프로모션 배너 호출 -->
    <SBT001A01Promotion />
    <!-- E: 프로모션 배너 호출 -->

    <Divider color="tertiary" variant="group" />

    <!-- S: 할인·쿠폰 호출 -->
    <SBT001A01Discount />
    <!-- E: 할인·쿠폰 호출 -->

    <!-- S: 혜택 서비스 호출 -->
    <SBT001A01Service />
    <!-- E: 혜택 서비스 호출 -->
  </div>
</template>

<script setup>
import { Divider } from "@shc-nss/ui/solid";
// 1. 혜택 대시보드
import SBT001A01Dashboard from "./section/SBT001A01-dashboard.vue";
// 2. 추천 혜택
import SBT001A01RecommendBenefit from "./section/SBT001A01-recommend-benefit.vue";
// 3. 배너
import SBT001A01Banner from "./section/SBT001A01-banner.vue";
// 4. 퀴즈팡팡
import SBT001A01QuizPangpang from "./section/SBT001A01-quiz-pangpang.vue";
// 5. 포인트팡팡
import SBT001A01PointPangpang from "./section/SBT001A01-point-pangpang.vue";
// 6. 카테고리
import SBT001A01Category from "./section/SBT001A01-category.vue";
// 7. 앱테크
import SBT001A01Apptech from "./section/SBT001A01-apptech.vue";
// 8. 이벤트
import SBT001A01Event from "./section/SBT001A01-event.vue";
// 9. 프로모션 배너
import SBT001A01Promotion from "./section/SBT001A01-promotion.vue";
// 10. 할인·쿠폰
import SBT001A01Discount from "./section/SBT001A01-discount.vue";
// 11. 혜택 서비스
import SBT001A01Service from "./section/SBT001A01-service.vue";
</script>


```
{% endraw %}
---
