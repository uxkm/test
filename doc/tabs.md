test1
```vue
<template>
  <div class="tab-wrap">
    <!-- 탭 메뉴 -->
    <div class="tab-menu" ref="tabMenu">
      <!-- 슬라이딩 배경 -->
      <span
        class="tab-indicator"
        :class="{ 'is-ready': indicator.ready }"
        :style="{
          width: indicator.width + 'px',
          transform: `translate3d(${indicator.left}px, 0, 0)`
        }"
        aria-hidden="true"
      ></span>

      <!-- 탭 버튼 -->
      <button
        v-for="(tab, index) in tabs"
        :key="tab.id"
        ref="tabItems"
        type="button"
        class="tab-btn"
        :class="{ 'is-active': activeIndex === index }"
        :aria-pressed="activeIndex === index"
        @click="changeTab(index)"
      >
        {{ tab.label }}
      </button>
    </div>

    <!-- 선택된 콘텐츠만 렌더링 -->
    <div class="tab-content">
      <component
        v-if="activeTab"
        :is="activeTab.component"
        :key="activeTab.id"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'SlidingTabs',

  components: {
    AllContent: () => import('./contents/AllContent.vue'),
    ProgressContent: () => import('./contents/ProgressContent.vue'),
    CompleteContent: () => import('./contents/CompleteContent.vue'),
    ArchiveContent: () => import('./contents/ArchiveContent.vue'),
    SettingContent: () => import('./contents/SettingContent.vue')
  },

  data() {
    return {
      activeIndex: 0,

      indicator: {
        left: 0,
        width: 0,
        ready: false
      },

      tabs: [
        { id: 'all', label: '전체', component: 'AllContent' },
        { id: 'progress', label: '진행 중', component: 'ProgressContent' },
        { id: 'complete', label: '완료', component: 'CompleteContent' },
        { id: 'archive', label: '보관함', component: 'ArchiveContent' },
        { id: 'setting', label: '설정', component: 'SettingContent' }
      ]
    };
  },

  computed: {
    activeTab() {
      return this.tabs[this.activeIndex] || null;
    }
  },

  mounted() {
    this.$nextTick(() => {
      this.updateIndicator();

      requestAnimationFrame(() => {
        requestAnimationFrame(() => {
          this.indicator.ready = true;
        });
      });
    });

    window.addEventListener('resize', this.updateIndicator);

    if (typeof ResizeObserver !== 'undefined') {
      this.resizeObserver = new ResizeObserver(
        this.updateIndicator
      );
      this.observeItems();
    }
  },

  beforeDestroy() {
    window.removeEventListener('resize', this.updateIndicator);

    if (this.resizeObserver) {
      this.resizeObserver.disconnect();
    }
  },

  watch: {
    tabs: {
      deep: true,
      handler() {
        this.$nextTick(() => {
          if (this.activeIndex >= this.tabs.length) {
            this.activeIndex = Math.max(0, this.tabs.length - 1);
          }
          this.updateIndicator();
          this.observeItems();
        });
      }
    }
  },

  methods: {
    changeTab(index) {
      if (this.activeIndex === index) return;

      this.activeIndex = index;
      this.$nextTick(this.updateIndicator);
    },

    updateIndicator() {
      const items = this.$refs.tabItems || [];
      const active = items[this.activeIndex];

      if (!active) {
        this.indicator.width = 0;
        return;
      }

      this.indicator.left = active.offsetLeft;
      this.indicator.width = active.offsetWidth;
    },

    observeItems() {
      if (!this.resizeObserver) return;

      this.resizeObserver.disconnect();

      if (this.$refs.tabMenu) {
        this.resizeObserver.observe(this.$refs.tabMenu);
      }

      const items = this.$refs.tabItems || [];
      items.forEach(item => this.resizeObserver.observe(item));
    }
  }
};
</script>

<style lang="scss" scoped>
.tab-wrap {
  width: 100%;
}

.tab-menu {
  position: relative;
  display: flex;
  padding: 5px;
  border-radius: 15px;
  background: #f1f1f1;
  isolation: isolate;
}

.tab-btn {
  position: relative;
  z-index: 1;
  flex: 1;
  min-width: 0;
  padding: 14px 10px;
  border: 0;
  border-radius: 11px;
  background: transparent;
  color: #666;
  font-size: 14px;
  white-space: nowrap;
  cursor: pointer;
  transition: color 250ms ease;

  &.is-active {
    color: #fff;
    font-weight: 600;
  }

  &:focus-visible {
    outline: 2px solid #333;
    outline-offset: 3px;
  }
}

.tab-indicator {
  position: absolute;
  top: 5px;
  bottom: 5px;
  left: 0;
  z-index: 0;
  border-radius: 11px;
  background: #7357e8;
  pointer-events: none;
  opacity: 0;

  &.is-ready {
    opacity: 1;
    transition:
      transform 650ms cubic-bezier(0.22, 1, 0.36, 1),
      width 650ms cubic-bezier(0.22, 1, 0.36, 1),
      opacity 200ms ease;
  }
}

.tab-content {
  padding: 24px 0;
}

@media (prefers-reduced-motion: reduce) {
  .tab-btn,
  .tab-indicator.is-ready {
    transition: none;
  }
}
</style>
```

test2
```vue
<template>
  <div class="tab-wrap">
    <!-- 탭 메뉴 -->
    <div class="tab-menu" ref="tabMenu">
      <!-- 슬라이딩 배경 인디케이터 -->
      <span
        class="tab-indicator"
        :class="{ 'is-ready': indicator.ready }"
        :style="{
          width: indicator.width + 'px',
          transform: `translate3d(${indicator.left}px, 0, 0)`
        }"
        aria-hidden="true"
      ></span>

      <!-- 메뉴 -->
      <button
        v-for="(tab, index) in tabs"
        :key="tab.id"
        ref="tabItems"
        type="button"
        class="tab-btn"
        :class="{ 'is-active': activeIndex === index }"
        :aria-pressed="activeIndex === index"
        @click="changeTab(index)"
      >
        {{ tab.label }}
      </button>
    </div>

    <!-- 각 콘텐츠에 v-if 직접 적용 -->
    <div class="tab-content">
      <AllContent v-if="activeTab === 'all'" />

      <ProgressContent v-if="activeTab === 'progress'" />

      <CompleteContent v-if="activeTab === 'complete'" />

      <ArchiveContent v-if="activeTab === 'archive'" />

      <SettingContent v-if="activeTab === 'setting'" />
    </div>
  </div>
</template>

<script>
import AllContent from './contents/AllContent.vue'
import ProgressContent from './contents/ProgressContent.vue'
import CompleteContent from './contents/CompleteContent.vue'
import ArchiveContent from './contents/ArchiveContent.vue'
import SettingContent from './contents/SettingContent.vue'

export default {
  name: 'SlidingTabs',

  components: {
    AllContent,
    ProgressContent,
    CompleteContent,
    ArchiveContent,
    SettingContent
  },

  data() {
    return {
      activeIndex: 0,

      tabs: [
        { id: 'all', label: '전체' },
        { id: 'progress', label: '진행 중' },
        { id: 'complete', label: '완료' },
        { id: 'archive', label: '보관함' },
        { id: 'setting', label: '설정' }
      ],

      indicator: {
        left: 0,
        width: 0,
        ready: false
      }
    }
  },

  computed: {
    activeTab() {
      return this.tabs[this.activeIndex]
        ? this.tabs[this.activeIndex].id
        : null
    }
  },

  mounted() {
    this.$nextTick(() => {
      this.updateIndicator()

      requestAnimationFrame(() => {
        requestAnimationFrame(() => {
          this.indicator.ready = true
        })
      })
    })

    window.addEventListener('resize', this.updateIndicator)

    if (typeof ResizeObserver !== 'undefined') {
      this.resizeObserver = new ResizeObserver(
        this.updateIndicator
      )

      this.observeItems()
    }
  },

  beforeDestroy() {
    window.removeEventListener('resize', this.updateIndicator)

    if (this.resizeObserver) {
      this.resizeObserver.disconnect()
    }
  },

  watch: {
    tabs: {
      deep: true,
      handler() {
        this.$nextTick(() => {
          if (this.activeIndex >= this.tabs.length) {
            this.activeIndex = Math.max(
              0,
              this.tabs.length - 1
            )
          }

          this.updateIndicator()
          this.observeItems()
        })
      }
    }
  },

  methods: {
    changeTab(index) {
      if (this.activeIndex === index) return

      this.activeIndex = index

      this.$nextTick(this.updateIndicator)
    },

    updateIndicator() {
      const items = this.$refs.tabItems || []
      const active = items[this.activeIndex]

      if (!active) {
        this.indicator.width = 0
        return
      }

      this.indicator.left = active.offsetLeft
      this.indicator.width = active.offsetWidth
    },

    observeItems() {
      if (!this.resizeObserver) return

      this.resizeObserver.disconnect()

      if (this.$refs.tabMenu) {
        this.resizeObserver.observe(this.$refs.tabMenu)
      }

      const items = this.$refs.tabItems || []

      items.forEach(item => {
        this.resizeObserver.observe(item)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.tab-wrap {
  width: 100%;
}

.tab-menu {
  position: relative;
  display: flex;
  padding: 5px;
  border-radius: 15px;
  background: #f1f1f1;
  isolation: isolate;
}

.tab-btn {
  position: relative;
  z-index: 1;
  flex: 1;
  min-width: 0;
  padding: 14px 10px;
  border: 0;
  border-radius: 11px;
  background: transparent;
  color: #666;
  font-size: 14px;
  white-space: nowrap;
  cursor: pointer;
  transition: color 250ms ease;

  &.is-active {
    color: #fff;
    font-weight: 600;
  }

  &:focus-visible {
    outline: 2px solid #333;
    outline-offset: 3px;
  }
}

.tab-indicator {
  position: absolute;
  top: 5px;
  bottom: 5px;
  left: 0;
  z-index: 0;
  border-radius: 11px;
  background: #7357e8;
  pointer-events: none;
  opacity: 0;

  &.is-ready {
    opacity: 1;

    transition:
      transform 650ms cubic-bezier(0.22, 1, 0.36, 1),
      width 650ms cubic-bezier(0.22, 1, 0.36, 1),
      opacity 200ms ease;
  }
}

.tab-content {
  padding: 24px 0;
}

@media (prefers-reduced-motion: reduce) {
  .tab-btn,
  .tab-indicator.is-ready {
    transition: none;
  }
}
</style>
```

test3
탭 개수에 따라 인디케이터 width / left를 `%` + `calc`로 유동 계산 (px 측정 불필요)
```vue
<template>
  <div class="tab-wrap">
    <!-- 탭 메뉴 -->
    <div
      class="tab-menu"
      :style="{ '--tab-count': tabs.length || 1 }"
    >
      <!-- 슬라이딩 배경: 탭 개수 기준으로 유동 계산 -->
      <span
        class="tab-indicator"
        :class="{ 'is-ready': indicatorReady }"
        :style="indicatorStyle"
        aria-hidden="true"
      ></span>

      <!-- 탭 버튼 -->
      <button
        v-for="(tab, index) in tabs"
        :key="tab.id"
        type="button"
        class="tab-btn"
        :class="{ 'is-active': activeIndex === index }"
        :aria-pressed="activeIndex === index"
        @click="changeTab(index)"
      >
        {{ tab.label }}
      </button>
    </div>

    <!-- 각 콘텐츠에 v-if 직접 적용 -->
    <div class="tab-content">
      <AllContent v-if="activeTab === 'all'" />

      <ProgressContent v-if="activeTab === 'progress'" />

      <CompleteContent v-if="activeTab === 'complete'" />

      <ArchiveContent v-if="activeTab === 'archive'" />

      <SettingContent v-if="activeTab === 'setting'" />
    </div>
  </div>
</template>

<script>
import AllContent from './contents/AllContent.vue'
import ProgressContent from './contents/ProgressContent.vue'
import CompleteContent from './contents/CompleteContent.vue'
import ArchiveContent from './contents/ArchiveContent.vue'
import SettingContent from './contents/SettingContent.vue'

export default {
  name: 'SlidingTabs',

  components: {
    AllContent,
    ProgressContent,
    CompleteContent,
    ArchiveContent,
    SettingContent
  },

  data() {
    return {
      activeIndex: 0,
      indicatorReady: false,
      // 탭을 추가/삭제해도 개수에 맞춰 자동 계산됨
      tabs: [
        { id: 'all', label: '전체' },
        { id: 'progress', label: '진행 중' },
        { id: 'complete', label: '완료' },
        { id: 'archive', label: '보관함' },
        { id: 'setting', label: '설정' }
      ]
    };
  },

  computed: {
    activeTab() {
      return this.tabs[this.activeIndex]
        ? this.tabs[this.activeIndex].id
        : null;
    },

    // 탭 개수 N → width = (100% - padding*2) / N
    // left = padding + width * activeIndex
    indicatorStyle() {
      const count = this.tabs.length || 1;
      const pad = 5; // .tab-menu padding 과 동일

      return {
        width: `calc((100% - ${pad * 2}px) / ${count})`,
        transform: `translate3d(calc(${pad}px + ((100% - ${pad * 2}px) / ${count}) * ${this.activeIndex}), 0, 0)`
      };
    }
  },

  mounted() {
    this.$nextTick(() => {
      requestAnimationFrame(() => {
        requestAnimationFrame(() => {
          this.indicatorReady = true;
        });
      });
    });
  },

  watch: {
    tabs: {
      deep: true,
      handler() {
        if (this.activeIndex >= this.tabs.length) {
          this.activeIndex = Math.max(0, this.tabs.length - 1);
        }
      }
    }
  },

  methods: {
    changeTab(index) {
      if (this.activeIndex === index) return;
      this.activeIndex = index;
    }
  }
};
</script>

<style lang="scss" scoped>
.tab-wrap {
  width: 100%;
}

.tab-menu {
  --tab-count: 1;
  position: relative;
  display: flex;
  padding: 5px;
  border-radius: 15px;
  background: #f1f1f1;
  isolation: isolate;
}

.tab-btn {
  position: relative;
  z-index: 1;
  flex: 1;
  min-width: 0;
  padding: 14px 10px;
  border: 0;
  border-radius: 11px;
  background: transparent;
  color: #666;
  font-size: 14px;
  white-space: nowrap;
  cursor: pointer;
  transition: color 250ms ease;

  &.is-active {
    color: #fff;
    font-weight: 600;
  }

  &:focus-visible {
    outline: 2px solid #333;
    outline-offset: 3px;
  }
}

.tab-indicator {
  position: absolute;
  top: 5px;
  bottom: 5px;
  left: 0;
  z-index: 0;
  border-radius: 11px;
  background: #7357e8;
  pointer-events: none;
  opacity: 0;

  &.is-ready {
    opacity: 1;
    transition:
      transform 650ms cubic-bezier(0.22, 1, 0.36, 1),
      width 650ms cubic-bezier(0.22, 1, 0.36, 1),
      opacity 200ms ease;
  }
}

.tab-content {
  padding: 24px 0;
}

@media (prefers-reduced-motion: reduce) {
  .tab-btn,
  .tab-indicator.is-ready {
    transition: none;
  }
}
</style>
```
