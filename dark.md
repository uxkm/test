
{% raw %}
```js


svg {
  path[fill="white"],
  ellipse[fill="white"] {
    fill: var(--bg-canvas_white);

    // card/bank icon 예외
    .card-display & {
      fill: #fff;
    }
    .error &,
    .fail &,
    .intitle &,
    .sc-feedback__notice &,
    .sc-feedback__fail &,
    .sc-feedback__info & {
      fill: #fff;
    }
  }
  &.fixed-color path[fill="white"] {
    fill: #fff;
  }

  path[stroke="white"] {
    .success &,
    .success2 & {
      stroke: var(--bg-canvas_white);
    }
  }
  path[fill="#101828"],
  ellipse[fill="#101828"] {
    fill: var(--text-primary);
  }
  rect[stroke="#101828"],
  path[stroke="#101828"] {
    stroke: var(--text-primary);
  }
  path[fill="#143898"] {
    fill: var(--text-brand);
  }
  path[fill="#344054"] {
    fill: var(--fg-steady);
  }
  path[fill="#0E2A95"] {
    fill: var(--brand-900);
    [data-theme="dark"] & {
      fill: var(--text-blue);
      .coupon-cards:disabled,
      .coupon-cards[disabled] {
        fill: var(--text-disabled-same);
      }
    }
    [data-theme="dark"] .coupon-cards:disabled &,
    [data-theme="dark"] .coupon-cards[disabled] & {
      fill: var(--text-disabled-same);
    }
    html:not([data-theme="dark"]) & {
      @media (prefers-color-scheme: dark) {
        fill: var(--text-blue);
        .coupon-cards:disabled,
        .coupon-cards[disabled] {
          fill: var(--text-disabled-same);
        }
      }
    }
    html:not([data-theme="dark"]) .coupon-cards:disabled &,
    html:not([data-theme="dark"]) .coupon-cards[disabled] & {
      @media (prefers-color-scheme: dark) {
        fill: var(--text-disabled-same);
      }
    }
  }
  path[fill="#005DF9"] {
    fill: var(--text-brand);
  }
  path[fill-rule="evenodd"][fill="#005DF9"] {
    fill: var(--fg-brand-same);
    .coupon-cards:disabled &,
    .coupon-cards[disabled] & {
      fill: var(--gray-400);
    }
  }
  circle[fill="#101828"] {
    [data-theme="dark"] [iconname="icon-line-car"] & {
      fill: #fff;
    }
    html:not([data-theme="dark"]) & {
      @media (prefers-color-scheme: dark) {
        [iconname="icon-line-car"] & {
          fill: #fff;
        }
      }
    }
  }
  path[fill="#000"] {
    [data-theme="dark"] .call & {
      fill: #fff;
    }
    [data-theme="dark"] .convenience & {
      fill: #fff;
    }
    html:not([data-theme="dark"]) & {
      @media (prefers-color-scheme: dark) {
        .call & {
          fill: #fff;
        }
        .convenience & {
          fill: #fff;
        }
      }
    }
  }
  &.isError {
    path[fill="#D0D5DD"] {
      [data-theme="dark"] & {
        fill: var(--fg-disabled);
      }
      html:not([data-theme="dark"]) & {
        @media (prefers-color-scheme: dark) {
          fill: var(--fg-disabled);
        }
      }
    }
  }
}





/// benefits


    .text-price {
      display: flex;
      align-items: center;
      justify-content: flex-start;
      gap: var(--spacing-sm);
      path[fill="#143898"] {
        fill: var(--brand-900);
        [data-theme="dark"] & {
          fill: var(--text-ondark_brand-same);
        }
        html:not([data-theme="dark"]) & {
          @media (prefers-color-scheme: dark) {
            fill: var(--text-ondark_brand-same);
          }
        }
      }
    }
    // .welcome-lounge .custum-card__group .text-price path 다크 fill 명시(캐스케이드 우선)
    @at-root {
      [data-theme="dark"] .welcome-lounge .custum-card__group .text-price path[fill="#143898"] {
        fill: var(--text-ondark_brand-same);
      }
      @media (prefers-color-scheme: dark) {
        html:not([data-theme="dark"]) .welcome-lounge .custum-card__group .text-price path[fill="#143898"] {
          fill: var(--text-ondark_brand-same);
        }
      }
    }



```
{% endraw %}
---
