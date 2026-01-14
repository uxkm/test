# test

{% raw %}
```scss

@use "sass:math";

@keyframes slideFade {
  0% {
    transform: translateY(100%);
    opacity: 0;
  }

  #{math.percentage(math.div($fade-time, $total-duration))} {
    transform: translateY(0);
    opacity: 1;
  }

  #{math.percentage(math.div($fade-time + $stay-time, $total-duration))} {
    transform: translateY(0);
    opacity: 1;
  }

  100% {
    transform: translateY(-100%);
    opacity: 0;
  }
}


```
{% endraw %}

---
