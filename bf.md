
{% raw %}
```js

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
