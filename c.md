# scss

{% raw %}
```js
<!-- 임시: 해지하기 버튼 -->
<button @click="onShowToast">해지하기</button>


import { AppContextKey } from "@/configs/inject/appContext";
import useToastStore from "@/stores/common/toast";
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
const { toast } = useToastStore();

// 토스트 표시 함수
const onShowToast = () => {
  toast.info("서비스 이용동의를 해지했습니다.", {
    position: "bottom",
    color: "dark",
    autoCloseDuration: 3000,
  });
};
```
{% endraw %}

---

{% raw %}
```js
<route lang="yaml">
meta:
  id: SBT068A01_pu1
  title: 앱테크
  menu: 혜택 > 앱테크 메인화면 > 서비스 이용 동의 해지 (PU)
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
    home: true
  appClassList: "sc-bf__apptech"
  mainClassList: "bf-apptech__submain"
</route>
<template>
  <ModalPopup
    title=""
    v-model="isOpen"
  >
    <p>
      <strong class="modal-tit">서비스 이용 동의를 해지하시겠어요?</strong>
      해지 시 매일 랜덤포인트 서비스를 이용하실 수 없어요. 해지 후 다시 동의할 수 있어요.
    </p>
    <template #footer>
      <BoxButton
        @click="isOpen = false"
        text="취소"
        size="medium"
        color="secondary"
      />
      <BoxButton
        @click="isOpen = false"
        text="해지하기"
        size="medium"
      />
    </template>
  </ModalPopup>
</template>

<script setup>
import { ModalPopup, BoxButton } from "@shc-nss/ui/solid";
// import { ScIcon } from "@shc-nss/ui/shc";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });
</script>

```
{% endraw %}

---

{% raw %}
```js
<route lang="yaml">
meta:
  id: SBT068A01_pu1
  title: 앱테크
  menu: 혜택 > 앱테크 메인화면 > 서비스 이용 동의 해지 (PU)
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
  <ModalPopup
    title=""
    v-model="isOpen"
  >
    <p>
      <strong class="modal-tit">서비스 이용 동의를 해지하시겠어요?</strong>
      해지 시 매일 랜덤포인트 서비스를 이용하실 수 없어요. 해지 후 다시 동의할 수 있어요.
    </p>
    <template #footer>
      <BoxButton
        @click="isOpen = false"
        text="취소"
        size="medium"
        color="secondary"
      />
      <BoxButton
        @click="isOpen = false"
        text="해지하기"
        size="medium"
      />
    </template>
  </ModalPopup>
</template>

<script setup>
import { ModalPopup, BoxButton } from "@shc-nss/ui/solid";
// import { ScIcon } from "@shc-nss/ui/shc";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });
</script>
```
{% endraw %}

---

{% raw %}
```js
<route lang="yaml">
meta:
  id: SBT068A01_pu2
  title: 앱테크
  menu: 혜택 > 앱테크 메인화면 > 알림 끄기 안내 (PU)
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
    home: true
  appClassList: "sc-bf__apptech"
  mainClassList: "bf-apptech__submain"
</route>
<template>
  <ModalPopup
    title=""
    v-model="isOpen"
  >
    <p>
      <strong class="modal-tit">알림을 끌까요?</strong>
      알림을 켜두면 적립 받으실 포인트를 실시간으로 알려드려요. 알림을 꺼도 포인트는 다음날 적립돼요.
    </p>
    <template #footer>
      <BoxButton
        @click="isOpen = false"
        text="닫기"
        size="medium"
        color="secondary"
      />
      <BoxButton
        @click="isOpen = false"
        text="알림끄기"
        size="medium"
      />
    </template>
  </ModalPopup>
</template>

<script setup>
import { ModalPopup, BoxButton } from "@shc-nss/ui/solid";
// import { ScIcon } from "@shc-nss/ui/shc";

// 팝업 상태 관리
const isOpen = defineModel({ default: true });
</script>
```
{% endraw %}
