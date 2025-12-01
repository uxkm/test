# test
```scss
// 251201

// custom popover style
.sc-popover__custom {
  display: inline-block;
  position: absolute;
  z-index: 1;
  width: max-content;
  max-width: 260px;
  height: auto;
  padding: var(--spacing-md) var(--spacing-lg);
  border-radius: var(--radius-xs);
  background-color: var(--bg-dark);
  &-content {
    display: block;
    @include font-set("body-s", 500);
    font-weight: 500;
    color: var(--text-ondark_primary);
    span {
      white-space: nowrap;
    }
  }
  // 화살표 공통 스타일
  &::after {
    content: "";
    position: absolute;
    width: 0;
    height: 0;
    border-top: 8px solid transparent;
    border-right: 8px solid transparent;
    border-bottom: 8px solid transparent;
    border-left: 8px solid transparent;
  }
  // placement별 위치 및 화살표 설정
  $placements: (
    "bottom-center": (
      "container-position": "bottom",
      "container-align": "left",
      "container-transform": "translateX(-50%)",
      "arrow-position": "top",
      "arrow-align": "left",
      "arrow-transform": "translateX(-50%)",
      "arrow-border": "border-top",
    ),
    "top-center": (
      "container-position": "top",
      "container-align": "left",
      "container-transform": "translateX(-50%)",
      "arrow-position": "bottom",
      "arrow-align": "left",
      "arrow-transform": "translateX(-50%)",
      "arrow-border": "border-bottom",
    ),
    "right-center": (
      "container-position": "right",
      "container-align": "top",
      "container-transform": "translateY(-50%)",
      "arrow-position": "left",
      "arrow-align": "top",
      "arrow-transform": "translateY(-50%)",
      "arrow-border": "border-left",
    ),
    "left-center": (
      "container-position": "left",
      "container-align": "top",
      "container-transform": "translateY(-50%)",
      "arrow-position": "right",
      "arrow-align": "top",
      "arrow-transform": "translateY(-50%)",
      "arrow-border": "border-right",
    ),
  );

  @each $placement, $config in $placements {
    &[data-placement="#{$placement}"] {
      #{map-get($config, "container-position")}: calc(100% + 8px);
      #{map-get($config, "container-align")}: 50%;
      transform: #{map-get($config, "container-transform")};
      &::after {
        #{map-get($config, "arrow-position")}: 100%;
        #{map-get($config, "arrow-align")}: 50%;
        transform: #{map-get($config, "arrow-transform")};
        #{map-get($config, "arrow-border")}: 8px solid var(--bg-dark);
      }
    }
  }
}
// 개별 방향 offset (data-placement 기반으로 적용)
// .sc-popover__custom 요소에 data-placement와 함께 data-offset-* 속성 사용
$directions: (
  "top": "top",
  "bottom": "bottom",
  "left": "left",
  "right": "right",
);

@each $direction, $css-prop in $directions {
  // .sc-popover__custom에 data-placement와 함께 offset 적용
  .sc-popover__custom[data-placement][data-offset-#{$direction}]:not(
      [data-offset-#{$direction}-property]
    ) {
    // CSS 변수에 attr() 사용 (단위 포함)
    --offset-#{$direction}: attr(data-offset-#{$direction} px);

    // 해당 방향에 offset 적용
    #{$css-prop}: var(--offset-#{$direction}) !important;
  }
}

// Popover 닫히는 효과 class hide-close가 있는 요소에 적용
// .sc-popover__custom에 data-placement 기반 애니메이션 적용
.sc-popover__custom.hide-close {
  // top-center: 위로 사라지는 애니메이션 (아래에 위치한 popover가 위로 사라짐)
  &[data-placement^="top-"] {
    animation: tooltip-fade-up 0.5s forwards;
    -webkit-animation-delay: 3s;
    animation-delay: 3s;
  }

  // bottom-center: 아래로 사라지는 애니메이션 (위에 위치한 popover가 아래로 사라짐)
  &[data-placement^="bottom-"] {
    animation: tooltip-fade-down 0.5s forwards;
    -webkit-animation-delay: 3s;
    animation-delay: 3s;
  }
}

// Popover 닫히는 애니메이션 키프레임
// tooltip-fade-down: 아래로 사라지는 효과 (위에 위치한 popover가 아래로 이동하며 사라짐)
// 기존 transform을 유지하면서 Y만 추가하기 위해 애니메이션에서 전체 transform 포함
@-webkit-keyframes tooltip-fade-down {
  from {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  to {
    opacity: 0;
    transform: translateX(-50%) translateY(10px);
  }
}

@keyframes tooltip-fade-down {
  from {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  to {
    opacity: 0;
    transform: translateX(-50%) translateY(10px);
  }
}

// tooltip-fade-up: 위로 사라지는 효과 (아래에 위치한 popover가 위로 이동하며 사라짐)
// 기존 transform을 유지하면서 Y만 추가하기 위해 애니메이션에서 전체 transform 포함
@-webkit-keyframes tooltip-fade-up {
  from {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  to {
    opacity: 0;
    transform: translateX(-50%) translateY(-10px);
  }
}

@keyframes tooltip-fade-up {
  from {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
  to {
    opacity: 0;
    transform: translateX(-50%) translateY(-10px);
  }
}
```
