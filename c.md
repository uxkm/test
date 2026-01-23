# scss

{% raw %}
```js


<!doctype html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>SC Loader Preview</title>
    <style>
      body {
        margin: 0;
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        background: #ffffff;
      }

      .sc-loader {
        width: 40px;
        height: 40px;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 6px; /* 점 사이 간격 */
        background: transparent; /* 투명배경 */
      }

      .sc-loader__dot {
        width: 8px;
        height: 8px;
        border-radius: 50%;
        transform: translateY(0);
        animation: scDot 1.33s ease-in-out infinite;
      }

      /* 점 3개 색상 */
      .sc-loader__dot:nth-child(1) {
        background: #ff4d4f;
        animation-delay: 0s;
      }
      .sc-loader__dot:nth-child(2) {
        background: #2f54eb;
        animation-delay: 0.26s;
      }
      .sc-loader__dot:nth-child(3) {
        background: #52c41a;
        animation-delay: 0.52s;
      }

      /* 순서대로 “튀는” 모션 */
      @keyframes scDot {
        0%,
        40%,
        100% {
          transform: translateY(2px) scale(0.92);
        }
        20% {
          transform: translateY(-6px) scale(1.05);
        }
      }

      /* 접근성: 모션 줄이기 */
      @media (prefers-reduced-motion: reduce) {
        .sc-loader__dot {
          animation: none;
        }
      }
    </style>
  </head>
  <body>
    <div class="sc-loader" role="status" aria-label="로딩 중">
      <span class="sc-loader__dot"></span>
      <span class="sc-loader__dot"></span>
      <span class="sc-loader__dot"></span>
    </div>
  </body>
</html>

```
{% endraw %}
