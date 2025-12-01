# test
```scss
// 251201
  @each $placement, $config in $placements {
    &[data-placement="#{$placement}"] {
      #{map-get($config, "container-position")}: calc(100% + 8px);
      #{map-get($config, "container-align")}: 50%;
      transform: #{map-get($config, "container-transform")};
      &::after {
        #{map-get($config, "arrow-position")}: -8px;
        #{map-get($config, "arrow-align")}: 50%;
        transform: #{map-get($config, "arrow-transform")};
        #{map-get($config, "arrow-border")}: 8px solid var(--bg-dark);
      }
    }
  }
```
