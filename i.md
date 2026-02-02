# index.vue

{% raw %}
```js


<route lang="yaml">
meta:
  id: publish-index
  title: 퍼블리싱 진행 현황
  menu: 가이드 > 목차
  layout: SubLayout
  category: 가이드
  publish: 김대민
  publishVersion: 0.8
  # 네비게이션 상세 옵션
  header:
    fixed: true
    close: false
  mainClassList: "pt-none"
</route>
<template>
  <!-- 로딩 인디케이터 -->
  <div v-if="isLoading" class="loading-container">
    <LoadingSpinner
      size="large"
      text="데이터를 불러오는 중..."
      alignment="center"
    />
  </div>

  <!-- 메인 콘텐츠 -->
  <div v-else class="main-content">
    <div class="deviceinfo px-2xl">
      <ul class="device-list">
        <li v-if="deviceInfo.deviceType">
          <strong>디바이스 타입:</strong>
          <span>{{ deviceInfo.deviceType }}</span>
        </li>
        <li v-if="deviceInfo.browser">
          <strong>브라우저 + 버전:</strong>
          <span>{{ deviceInfo.browser }}</span>
        </li>
        <li v-if="deviceInfo.os">
          <strong>OS + 버전:</strong>
          <span>{{ deviceInfo.os }}</span>
        </li>
        <li v-if="deviceInfo.screenSize">
          <strong>논리적 화면 크기 (Screen):</strong>
          <span>{{ deviceInfo.screenSize }}</span>
        </li>
        <li v-if="deviceInfo.dpr">
          <strong>DPR (Device Pixel Ratio):</strong>
          <span>{{ deviceInfo.dpr }}</span>
        </li>
        <li v-if="deviceInfo.physicalSize">
          <strong>물리적 해상도 (Physical):</strong>
          <span>{{ deviceInfo.physicalSize }}</span>
        </li>
        <li v-if="deviceInfo.hasTouch">
          <strong>터치 지원 여부:</strong>
          <span>{{ deviceInfo.hasTouch }}</span>
        </li>
      </ul>
    </div>
    <div class="worker-index__page">
      <ul
        class="worker-counts"
        aria-label="작업자별 페이지 총개수"
        style="display: none"
      >
        <li v-for="grp in workerGroups" :key="grp.name">
          <span class="name">{{ grp.title }}</span>
          <span class="count">{{ grp.items.length }}</span>
        </li>
      </ul>
      <div class="divider">
        <small>
          <span>Pay: {{ payCount }}</span> | <span>MYD: {{ mydCount }}</span> |
          <span>PPC: {{ ppcCount }}</span> |
          <span>팝업: {{ totalPopupCount }}</span>
        </small>
        <small
          v-if="totalPopupCount === 0"
          style="color: red; display: block; margin-top: 4px"
        >
          (디버깅) 팝업이 0개입니다. 콘솔을 확인해주세요.
        </small>
      </div>
      <div ref="searchSection" class="section worker-search">
        <div class="search-container">
          <div
            class="search-input-wrapper"
            :class="{ 'animation-complete': animationComplete }"
            @animationend="onAnimationEnd"
          >
            <input
              :value="searchQuery"
              type="text"
              class="search-input"
              placeholder="검색어를 입력하세요..."
              aria-label="페이지 검색"
              @input="onSearchInput"
              @focus="onFocus"
              @blur="onBlur"
            />
            <button
              v-if="searchQuery"
              class="clear-btn"
              @click="searchQuery = ''"
              aria-label="검색어 지우기"
              type="button"
            >
              ✕
            </button>
          </div>
          <div class="filter-buttons" role="group" aria-label="검색 필터">
            <button
              v-for="filter in searchFilters"
              :key="filter.value"
              :class="['filter-btn', { active: searchFilter === filter.value }]"
              @click="searchFilter = filter.value"
              :aria-pressed="searchFilter === filter.value"
            >
              {{ filter.label }}
            </button>
          </div>
        </div>

        <div
          v-if="searchQuery || searchFilter === 'agree'"
          class="search-results"
        >
          <small class="search-result-count">
            검색 결과: <strong>{{ searchResultCount }}</strong
            >개
          </small>
        </div>
      </div>

      <div v-if="shouldShowResults" class="worker-search__results">
        <section>
          <h2>
            카테고리
            <small class="count">{{ workTotalCount }}</small>
          </h2>
          <ul class="accordion-list accordion-list--primary">
            <li
              v-for="grp in filteredWorkGroups"
              :key="grp.name"
              class="accordion-item"
              :class="{ 'is-open': openPrimaryItems.includes(grp.name) }"
            >
              <div class="accordion-header" @click="togglePrimary(grp.name)">
                <span class="accordion-title"
                  >{{ grp.title }} ({{ getPageCount(grp.name) }},
                  {{ getPopupCount(grp.name) }})</span
                >
                <Icon class="accordion-icon" name="Chevron_down" />
              </div>
              <div
                v-if="openPrimaryItems.includes(grp.name)"
                class="accordion-content"
              >
                <!-- Guide는 2뎁스 없이 바로 링크 리스트 -->
                <ul v-if="grp.items" class="link-list">
                  <li v-for="item in grp.items" :key="item.path">
                    <a
                      class="link-item"
                      :href="item.path"
                      target="_blank"
                      rel="noopener"
                      role="link"
                    >
                      <span>
                        {{ item.label }}
                        <template v-if="item.worker"
                          ><br />( {{ item.worker }} )</template
                        >
                      </span>
                      <span class="body-s text-secondary">{{
                        prettyPath(item.path)
                      }}</span>
                    </a>
                  </li>
                </ul>

                <!-- 나머지는 2뎁스 아코디언 구조 -->
                <ul
                  v-else-if="grp.subGroups"
                  class="accordion-list accordion-list--secondary"
                >
                  <li
                    v-for="subGrp in grp.subGroups"
                    :key="subGrp.name"
                    class="accordion-item"
                    :class="{
                      'is-open': openSecondaryItems.includes(subGrp.name),
                    }"
                  >
                    <div
                      class="accordion-header"
                      @click="toggleSecondary(subGrp.name)"
                    >
                      <span class="accordion-title"
                        >{{ subGrp.title }} ({{ getSubGroupPageCount(subGrp) }},
                        {{ getSubGroupPopupCount(subGrp) }})</span
                      >
                      <Icon class="accordion-icon" name="Chevron_down" />
                    </div>
                    <div
                      v-if="openSecondaryItems.includes(subGrp.name)"
                      class="accordion-content"
                    >
                      <ul class="link-list">
                        <li v-for="item in subGrp.items" :key="item.path">
                          <a
                            class="link-item"
                            :href="item.path"
                            target="_blank"
                            rel="noopener"
                            role="link"
                          >
                            <div class="link-content">
                              <span>
                                {{ item.label }}
                                <template v-if="item.worker"
                                  ><br />( {{ item.worker }} )</template
                                >
                              </span>
                              <span class="body-s text-secondary">{{
                                prettyPath(item.path)
                              }}</span>
                            </div>
                            <div
                              class="meta-menu"
                              v-if="getMetaMenu(item.path)"
                            >
                              {{ getMetaMenu(item.path) }}
                            </div>
                          </a>
                        </li>
                      </ul>
                    </div>
                  </li>
                </ul>
              </div>
            </li>
          </ul>
        </section>

        <!-- 작업 상태별 섹션 -->
        <section hidden>
          <h2>
            작업 상태
            <small class="count">{{ workTotalCount }}</small>
          </h2>
          <ul class="accordion-list accordion-list--primary">
            <li
              v-for="grp in filteredStatusGroups"
              :key="grp.name"
              class="accordion-item"
              :class="{ 'is-open': openStatusItems.includes(grp.name) }"
            >
              <div class="accordion-header" @click="toggleStatus(grp.name)">
                <span class="accordion-title"
                  >{{ grp.title }} ({{ grp.pageCount }},
                  {{ grp.popupCount }})</span
                >
                <Icon class="accordion-icon" name="Chevron_down" />
              </div>
              <div
                v-if="openStatusItems.includes(grp.name)"
                class="accordion-content"
              >
                <!-- 카테고리별 2뎁스 아코디언 구조 -->
                <ul
                  class="accordion-list accordion-list--secondary accordion-list--status-category"
                >
                  <li
                    v-for="categoryGrp in grp.categories"
                    :key="categoryGrp.name"
                    class="accordion-item"
                    :class="{
                      'is-open': openStatusCategoryItems.includes(
                        `${grp.name}-${categoryGrp.name}`,
                      ),
                    }"
                  >
                    <div
                      class="accordion-header"
                      @click="
                        toggleStatusCategory(`${grp.name}-${categoryGrp.name}`)
                      "
                    >
                      <span class="accordion-title"
                        >{{ categoryGrp.title }} ({{ categoryGrp.pageCount }},
                        {{ categoryGrp.popupCount }})</span
                      >
                      <Icon class="accordion-icon" name="Chevron_down" />
                    </div>
                    <div
                      v-if="
                        openStatusCategoryItems.includes(
                          `${grp.name}-${categoryGrp.name}`,
                        )
                      "
                      class="accordion-content"
                    >
                      <!-- 3뎁스 아코디언 구조 (auth, pay, benefits 등) -->
                      <ul class="accordion-list accordion-list--secondary">
                        <li
                          v-for="subGrp in categoryGrp.subGroups"
                          :key="subGrp.name"
                          class="accordion-item"
                          :class="{
                            'is-open': openStatusSubGroupItems.includes(
                              `${grp.name}-${categoryGrp.name}-${subGrp.name}`,
                            ),
                          }"
                        >
                          <div
                            class="accordion-header"
                            @click="
                              toggleStatusSubGroup(
                                `${grp.name}-${categoryGrp.name}-${subGrp.name}`,
                              )
                            "
                          >
                            <span class="accordion-title"
                              >{{ subGrp.title }} ({{ subGrp.pageCount }},
                              {{ subGrp.popupCount }})</span
                            >
                            <Icon class="accordion-icon" name="Chevron_down" />
                          </div>
                          <div
                            v-if="
                              openStatusSubGroupItems.includes(
                                `${grp.name}-${categoryGrp.name}-${subGrp.name}`,
                              )
                            "
                            class="accordion-content"
                          >
                            <ul class="link-list">
                              <li v-for="item in subGrp.items" :key="item.path">
                                <a
                                  class="link-item"
                                  :href="item.path"
                                  target="_blank"
                                  rel="noopener"
                                  role="link"
                                >
                                  <div class="link-content">
                                    <span>
                                      {{ item.label }}
                                      <template v-if="item.worker"
                                        ><br />( {{ item.worker }} )</template
                                      >
                                    </span>
                                    <span class="body-s text-secondary">{{
                                      prettyPath(item.path)
                                    }}</span>
                                  </div>
                                  <div
                                    class="meta-menu"
                                    v-if="getMetaMenu(item.path)"
                                  >
                                    {{ getMetaMenu(item.path) }}
                                  </div>
                                </a>
                              </li>
                            </ul>
                          </div>
                        </li>
                      </ul>
                    </div>
                  </li>
                </ul>
              </div>
            </li>
          </ul>
        </section>

        <!-- 담당자별 페이지 섹션: _new 하위(모듈 제외) 폴더별 아코디언 -->
        <section hidden>
          <h2>
            담당자
            <small class="count">{{ workerTotalCount }}</small>
          </h2>
          <ul class="accordion-list accordion-list--primary">
            <li
              v-for="grp in filteredWorkerGroups"
              :key="grp.name"
              class="accordion-item"
              :class="{ 'is-open': openWorkerItems.includes(grp.name) }"
            >
              <div class="accordion-header" @click="toggleWorker(grp.name)">
                <span class="accordion-title"
                  >{{ grp.title }} ({{ grp.items.length }})</span
                >
                <Icon class="accordion-icon" name="Chevron_down" />
              </div>
              <div
                v-if="openWorkerItems.includes(grp.name)"
                class="accordion-content"
              >
                <ul class="link-list">
                  <li v-for="item in grp.items" :key="item.path">
                    <a
                      class="link-item"
                      :href="item.path"
                      target="_blank"
                      rel="noopener"
                      role="link"
                    >
                      <span>
                        {{ item.label }}
                        <br />[ {{ folderLabel(item.path) }} ]
                      </span>
                      <span class="body-s text-secondary">{{
                        prettyPath(item.path)
                      }}</span>
                    </a>
                  </li>
                </ul>
              </div>
            </li>
          </ul>
        </section>
      </div>

      <div v-else-if="shouldShowNoResults" class="worker-search__no-results">
        검색 결과가 없습니다.
      </div>
    </div>
  </div>
</template>

<script setup>
import { Icon, LoadingSpinner } from "@shc-nss/ui/solid";
import { computed, nextTick, onBeforeUnmount, onMounted, ref } from "vue";
// 동적 페이지 목록(HMR 대응) – 파일 생성/삭제 시 자동 반영
import generatedPages from "virtual:generated-pages";

// 로딩 상태
const isLoading = ref(true);

// 검색 섹션 ref
const searchSection = ref(null);

// Header 높이 계산
const headerHeight = ref(0);

// 스크롤 상태 관리
const lastScrollY = ref(0);
const isHeaderVisible = ref(true);

// 이벤트 리스너 참조 저장 (cleanup용)
let scrollHandler = null;
let resizeHandlerForHeader = null;
let resizeHandlerForSection = null;

// 디바이스 정보
const deviceInfo = computed(() => {
  const ua = navigator.userAgent;

  // 디바이스 타입
  const isMobile = /Mobile|Android|iPhone|iPod/.test(ua);
  const isTablet = /iPad|Android(?!.*Mobile)/.test(ua);
  let deviceType = "Desktop";
  if (isMobile) deviceType = "Mobile";
  if (isTablet) deviceType = "Tablet";

  // 브라우저
  let browser = "Unknown";
  let browserVersion = "";
  if (ua.includes("Chrome") && !ua.includes("Edg")) {
    browser = "Chrome";
    const match = ua.match(/Chrome\/([\d.]+)/);
    if (match) browserVersion = match[1];
  } else if (ua.includes("Safari") && !ua.includes("Chrome")) {
    browser = "Safari";
    const match = ua.match(/Version\/([\d.]+)/);
    if (match) browserVersion = match[1];
  } else if (ua.includes("Firefox")) {
    browser = "Firefox";
    const match = ua.match(/Firefox\/([\d.]+)/);
    if (match) browserVersion = match[1];
  } else if (ua.includes("Edg")) {
    browser = "Edge";
    const match = ua.match(/Edg\/([\d.]+)/);
    if (match) browserVersion = match[1];
  }
  const browserInfo = browserVersion ? `${browser} ${browserVersion}` : browser;

  // OS
  let os = "Unknown";
  let osVersion = "";
  let deviceModel = "";

  if (ua.includes("Android")) {
    os = "Android";
    const versionMatch = ua.match(/Android ([\d.]+)/);
    if (versionMatch) osVersion = versionMatch[1];
    const modelMatch = ua.match(/;\s*([^;)]+)\s+Build/);
    if (modelMatch) deviceModel = modelMatch[1].trim();
  } else if (ua.includes("iPhone")) {
    os = "iOS";
    deviceModel = "iPhone";
    const versionMatch = ua.match(/OS ([\d_]+)/);
    if (versionMatch) osVersion = versionMatch[1].replace(/_/g, ".");
  } else if (ua.includes("iPad")) {
    os = "iPadOS";
    deviceModel = "iPad";
    const versionMatch = ua.match(/OS ([\d_]+)/);
    if (versionMatch) osVersion = versionMatch[1].replace(/_/g, ".");
  } else if (ua.includes("Mac")) {
    os = "macOS";
    const versionMatch = ua.match(/Mac OS X ([\d._]+)/);
    if (versionMatch) osVersion = versionMatch[1].replace(/_/g, ".");
  } else if (ua.includes("Win")) {
    os = "Windows";
    if (ua.includes("Windows NT 10.0")) osVersion = "10/11";
  }

  let osInfo = os;
  if (osVersion) osInfo += ` ${osVersion}`;
  if (deviceModel) osInfo += ` (${deviceModel})`;

  // 화면 크기
  const logicalSize = `${window.innerWidth}×${window.innerHeight}`;
  const pixelRatio = window.devicePixelRatio || 1;
  const physicalSize = `${Math.round(window.innerWidth * pixelRatio)}×${Math.round(window.innerHeight * pixelRatio)}`;

  // 터치 지원
  const hasTouch = "ontouchstart" in window || navigator.maxTouchPoints > 0;

  return {
    deviceType,
    browser: browserInfo,
    os: osInfo,
    screenSize: logicalSize,
    dpr: pixelRatio.toFixed(2),
    physicalSize: pixelRatio > 1 ? physicalSize : null,
    hasTouch: hasTouch ? "Touch (터치 가능)" : null,
  };
});

// 파일 내용에서 sc-agree 클래스 포함 여부를 확인하기 위한 인덱스
// import.meta.glob을 사용하여 파일 내용을 읽음 (빌드 타임에 인덱싱)
const fileContentCache = import.meta.glob("@/publish/**/*.vue", {
  as: "raw",
  eager: true,
});

// 경로를 정규화하여 매칭 (간소화)
function normalizePath(path) {
  return path
    .replace(/^\/publish\//, "")
    .replace(/\.vue$/, "")
    .toLowerCase();
}

// 정규화된 파일 캐시 (간소화된 초기화)
const normalizedFileCache = new Map();
Object.entries(fileContentCache).forEach(([key, content]) => {
  if (typeof content === "string") {
    const keyPath = key
      .replace(/^.*\/publish\//, "")
      .replace(/\.vue$/, "")
      .toLowerCase();
    normalizedFileCache.set(keyPath, content);
  }
});

// 파일 내용에서 약관 관련 클래스 포함 여부 확인 (동기)
function hasScAgreeClass(path) {
  // _guide 폴더는 약관 필터에서 제외
  if (path.includes("/_guide/") || path.startsWith("/publish/_guide/")) {
    return false;
  }

  const normalizedPath = normalizePath(path);
  const content = normalizedFileCache.get(normalizedPath);

  if (!content) return false;

  // 약관 관련 클래스 확인 (간소화)
  return (
    content.includes("sc-agree") ||
    content.includes("terms-popup") ||
    /\bterms-/.test(content) ||
    /-agree\b/.test(content)
  );
}

// 검색 상태 관리
const searchQuery = ref("");
const debouncedSearchQuery = ref(""); // debounced 검색어
const searchFilter = ref("all"); // 'all', 'name', 'page', 'path', 'agree'
const animationComplete = ref(false);

// 검색 필터 옵션
const searchFilters = [
  { label: "전체", value: "all" },
  { label: "이름", value: "name" },
  { label: "타이틀", value: "page" },
  { label: "경로", value: "path" },
  { label: "약관", value: "agree" },
];

// Debounce 타이머
let searchDebounceTimer = null;

// 아코디언 상태 관리
const openPrimaryItems = ref([]);
const openSecondaryItems = ref([]);
const openWorkerItems = ref([]);
const openStatusItems = ref([]);
const openStatusCategoryItems = ref([]);
const openStatusSubGroupItems = ref([]);

// 검색 상태에 따른 아코디언 자동 펼침 관리
const isSearching = computed(() => searchQuery.value.length > 0);

// 토글 함수들
function togglePrimary(name) {
  const index = openPrimaryItems.value.indexOf(name);
  if (index > -1) {
    openPrimaryItems.value.splice(index, 1);
  } else {
    openPrimaryItems.value.push(name);
  }
}

function toggleStatus(name) {
  const index = openStatusItems.value.indexOf(name);
  if (index > -1) {
    openStatusItems.value.splice(index, 1);
  } else {
    openStatusItems.value.push(name);
  }
}

function toggleStatusCategory(name) {
  const index = openStatusCategoryItems.value.indexOf(name);
  if (index > -1) {
    openStatusCategoryItems.value.splice(index, 1);
  } else {
    openStatusCategoryItems.value.push(name);
  }
}

function toggleStatusSubGroup(name) {
  const index = openStatusSubGroupItems.value.indexOf(name);
  if (index > -1) {
    openStatusSubGroupItems.value.splice(index, 1);
  } else {
    openStatusSubGroupItems.value.push(name);
  }
}

function toggleSecondary(name) {
  const index = openSecondaryItems.value.indexOf(name);
  if (index > -1) {
    openSecondaryItems.value.splice(index, 1);
  } else {
    openSecondaryItems.value.push(name);
  }
}

function toggleWorker(name) {
  const index = openWorkerItems.value.indexOf(name);
  if (index > -1) {
    openWorkerItems.value.splice(index, 1);
  } else {
    openWorkerItems.value.push(name);
  }
}

// 라우트 중 publish 경로만 추출
/** @typedef {{ path: string, label: string, worker?: string }} LinkItem */

const publishRoutes = computed(() =>
  generatedPages.filter(
    (r) => r.path?.startsWith("/publish/") && !!r.component,
  ),
);

// 파일명 → 라벨 변환 보조: 메타 타이틀 우선, 없으면 파일명 마지막 슬러그
/**
 * 파일 경로를 사람이 읽기 쉬운 라벨로 변환
 * @param {string} path
 * @returns {string}
 */
function toLabel(path) {
  const metaTitle = generatedPages.find((r) => r.path === path)?.meta?.title;
  if (metaTitle) return metaTitle;
  const seg = path.split("/").pop() || path;
  return seg.replace(/\.(vue|md)$/, "");
}

/* 작업자 이름(meta.publish)은 별도 표시 줄로 렌더링 */

/**
 * 표시용 경로: /publish 접두어 제거
 * @param {string} path
 * @returns {string}
 */
function prettyPath(path) {
  return path.replace(/^\/publish\//, "/");
}

// 작업 페이지: /publish/<folder>/... (_guide, myd, pay, ppc만 포함, _module 제외)
/** @typedef {{ name: string, title: string, items: LinkItem[] }} SubGroup */
/** @typedef {{ name: string, title: string, subGroups?: SubGroup[], items?: LinkItem[], totalCount: number }} Group */
/** @type {import('vue').ComputedRef<Group[]>} */
const workGroups = computed(() => {
  /** @type {Record<string, Record<string, LinkItem[]>>} */
  const groups = {};
  const allowedFolders = ["_guide", "myd", "pay", "ppc"];

  publishRoutes.value
    .filter((r) => {
      if (!r.path.startsWith("/publish/")) return false;
      // /publish/_module/은 제외 (moduleList에서 별도 관리)
      if (r.path.startsWith("/publish/_module/")) return false;

      const parts = r.path.replace("/publish/", "").split("/");
      const folder = parts[0];
      // 허용된 폴더만 포함
      return allowedFolders.includes(folder);
    })
    .forEach((r) => {
      const parts = r.path.replace("/publish/", "").split("/");
      const folder1 = parts[0] || "기타"; // 1뎁스 (pay, myd, ppc 등)
      const folder2 = parts[1] || "기타"; // 2뎁스 (auth, pay, benefits 등)

      groups[folder1] ||= {};
      groups[folder1][folder2] ||= [];

      const meta = generatedPages.find((mr) => mr.path === r.path)?.meta || {};
      groups[folder1][folder2].push({
        path: r.path,
        label: toLabel(r.path),
        worker: /** @type {any} */ (meta).publish,
      });
    });

  return Object.entries(groups)
    .sort(([a], [b]) => a.localeCompare(b))
    .map(([name, subFolders]) => {
      // _guide는 2뎁스 없이 바로 items로
      if (name === "_guide") {
        const allItems = Object.values(subFolders).flat();
        return {
          name,
          title: folderLabelMap[name] ?? name,
          items: allItems.sort((a, b) => a.label.localeCompare(b.label)),
          totalCount: allItems.length,
        };
      }

      // 나머지는 2뎁스 구조
      const subGroups = Object.entries(subFolders)
        .sort(([a], [b]) => a.localeCompare(b))
        .map(([subName, items]) => ({
          name: subName,
          title: folderLabelMap[subName] ?? subName,
          items: items.sort((a, b) => a.label.localeCompare(b.label)),
        }));

      const totalCount = subGroups.reduce(
        (acc, sg) => acc + sg.items.length,
        0,
      );

      return {
        name,
        title: folderLabelMap[name] ?? name,
        subGroups,
        totalCount,
      };
    });
});

// 담당자별 작업 페이지: /publish/<folder>/... (_guide, myd, pay, ppc만 포함, _module 제외) 를 담당자(meta.publish) 기준으로 그룹화
/** @typedef {{ name: string, title: string, items: LinkItem[] }} WorkerGroup */
/** @type {import('vue').ComputedRef<WorkerGroup[]>} */
const workerGroups = computed(() => {
  /** @type {Record<string, LinkItem[]>} */
  const groups = {};
  const allowedFolders = ["_guide", "myd", "pay", "ppc"];

  publishRoutes.value
    .filter((r) => {
      if (!r.path.startsWith("/publish/")) return false;
      // /publish/_module/은 제외 (moduleList에서 별도 관리)
      if (r.path.startsWith("/publish/_module/")) return false;

      const parts = r.path.replace("/publish/", "").split("/");
      const folder = parts[0];
      // 허용된 폴더만 포함
      return allowedFolders.includes(folder);
    })
    .forEach((r) => {
      const meta = generatedPages.find((mr) => mr.path === r.path)?.meta || {};
      const worker = /** @type {any} */ (meta).publish || "미정";
      groups[worker] ||= [];
      groups[worker].push({ path: r.path, label: toLabel(r.path), worker });
    });

  return Object.entries(groups)
    .sort(([a], [b]) => a.localeCompare(b))
    .map(([name, items]) => ({
      name,
      title: `${name}`,
      items: items.sort((a, b) => a.label.localeCompare(b.label)),
    }));
});

// 작업 상태별 그룹화: status 값에 따라 그룹화하고 카테고리별로 2뎁스, 3뎁스 구조 생성
// 작업중과 작업진행은 "작업진행"으로 통합
// _guide는 제외
/** @typedef {{ name: string, title: string, items: LinkItem[], pageCount: number, popupCount: number }} SubGroup */
/** @typedef {{ name: string, title: string, subGroups: SubGroup[], totalCount: number, pageCount: number, popupCount: number }} CategoryGroup */
/** @typedef {{ name: string, title: string, categories: CategoryGroup[], totalCount: number, pageCount: number, popupCount: number }} StatusGroup */
/** @type {import('vue').ComputedRef<StatusGroup[]>} */
const statusGroups = computed(() => {
  /** @type {Record<string, Record<string, Record<string, LinkItem[]>>>} */
  const statusCategorySubGroups = {};
  const allowedFolders = ["myd", "pay", "ppc"]; // _guide 제외

  publishRoutes.value
    .filter((r) => {
      if (!r.path.startsWith("/publish/")) return false;
      // /publish/_module/은 제외 (moduleList에서 별도 관리)
      if (r.path.startsWith("/publish/_module/")) return false;

      const parts = r.path.replace("/publish/", "").split("/");
      const folder = parts[0];
      // 허용된 폴더만 포함 (_guide 제외)
      return allowedFolders.includes(folder);
    })
    .forEach((r) => {
      const meta = generatedPages.find((mr) => mr.path === r.path)?.meta || {};

      // status가 없거나 "작업중"이면 "작업진행"으로 간주
      let status = /** @type {any} */ (meta).status || "작업진행";
      if (status === "작업중") {
        status = "작업진행";
      }

      // 카테고리 추출 (1뎁스 폴더)
      const parts = r.path.replace("/publish/", "").split("/");
      const folder1 = parts[0] || "기타"; // 1뎁스 (pay, myd, ppc 등)
      const folder2 = parts[1] || "기타"; // 2뎁스 (auth, pay, benefits 등)

      statusCategorySubGroups[status] ||= {};
      statusCategorySubGroups[status][folder1] ||= {};
      statusCategorySubGroups[status][folder1][folder2] ||= [];

      statusCategorySubGroups[status][folder1][folder2].push({
        path: r.path,
        label: toLabel(r.path),
        worker: /** @type {any} */ (meta).publish,
      });
    });

  // 상태별 정렬 순서 정의 (작업완료 > 작업진행 > 기타)
  const statusOrder = { 작업완료: 1, 작업진행: 2 };

  return Object.entries(statusCategorySubGroups)
    .sort(([a], [b]) => {
      const orderA = statusOrder[a] || 999;
      const orderB = statusOrder[b] || 999;
      if (orderA !== orderB) return orderA - orderB;
      return a.localeCompare(b);
    })
    .map(([statusName, categories]) => {
      // 카테고리별로 정리 (모두 3뎁스 구조)
      const categoryGroups = Object.entries(categories)
        .sort(([a], [b]) => a.localeCompare(b))
        .map(([categoryName, subFolders]) => {
          // 모든 카테고리는 3뎁스 구조 (subGroups)
          const subGroups = Object.entries(subFolders)
            .sort(([a], [b]) => a.localeCompare(b))
            .map(([subName, items]) => {
              const sortedItems = items.sort((a, b) =>
                a.label.localeCompare(b.label),
              );

              // 팝업 개수 계산
              const popupCount = sortedItems.filter((item) => {
                const page = generatedPages.find((r) => r.path === item.path);
                const metaId = page?.meta?.id || "";
                return isPopup(metaId);
              }).length;

              const pageCount = sortedItems.length - popupCount;

              return {
                name: subName,
                title: folderLabelMap[subName] ?? subName,
                items: sortedItems,
                pageCount,
                popupCount,
              };
            });

          const totalCount = subGroups.reduce(
            (acc, sg) => acc + sg.items.length,
            0,
          );
          const pageCount = subGroups.reduce(
            (acc, sg) => acc + sg.pageCount,
            0,
          );
          const popupCount = subGroups.reduce(
            (acc, sg) => acc + sg.popupCount,
            0,
          );

          return {
            name: categoryName,
            title: folderLabelMap[categoryName] ?? categoryName,
            subGroups,
            totalCount,
            pageCount,
            popupCount,
          };
        });

      const totalCount = categoryGroups.reduce(
        (acc, cg) => acc + cg.totalCount,
        0,
      );
      const pageCount = categoryGroups.reduce(
        (acc, cg) => acc + cg.pageCount,
        0,
      );
      const popupCount = categoryGroups.reduce(
        (acc, cg) => acc + cg.popupCount,
        0,
      );

      return {
        name: statusName,
        title: statusName,
        categories: categoryGroups,
        totalCount,
        pageCount,
        popupCount,
      };
    });
});

// 총 개수 계산
/** @type {import('vue').ComputedRef<number>} */
const workTotalCount = computed(() =>
  workGroups.value.reduce((acc, g) => acc + g.totalCount, 0),
);
/** @type {import('vue').ComputedRef<number>} */
const workerTotalCount = computed(() =>
  workerGroups.value.reduce((acc, g) => acc + g.items.length, 0),
);

// 팝업 여부 확인 함수 (언더스코어가 있지만 sp_로 시작하지 않는 경우)
function isPopup(metaId) {
  if (!metaId || !metaId.includes("_")) return false;
  // sp_로 시작하는 경우는 팝업이 아님
  return !metaId.toLowerCase().startsWith("sp_");
}

// 각 폴더별 팝업 개수 계산
const payPopupCount = computed(() => {
  return publishRoutes.value.filter((r) => {
    if (!r.path.startsWith("/publish/pay/")) return false;
    const metaId = r.meta?.id || "";
    return isPopup(metaId);
  }).length;
});

const mydPopupCount = computed(() => {
  return publishRoutes.value.filter((r) => {
    if (!r.path.startsWith("/publish/myd/")) return false;
    const metaId = r.meta?.id || "";
    return isPopup(metaId);
  }).length;
});

const ppcPopupCount = computed(() => {
  return publishRoutes.value.filter((r) => {
    if (!r.path.startsWith("/publish/ppc/")) return false;
    const metaId = r.meta?.id || "";
    return isPopup(metaId);
  }).length;
});

// 폴더별 개수 계산 (팝업 제외)
/** @type {import('vue').ComputedRef<number>} */
const payCount = computed(() => {
  const payGroup = workGroups.value.find((g) => g.name === "pay");
  const totalCount = payGroup ? payGroup.totalCount : 0;
  return totalCount - payPopupCount.value;
});
/** @type {import('vue').ComputedRef<number>} */
const mydCount = computed(() => {
  const mydGroup = workGroups.value.find((g) => g.name === "myd");
  const totalCount = mydGroup ? mydGroup.totalCount : 0;
  return totalCount - mydPopupCount.value;
});
/** @type {import('vue').ComputedRef<number>} */
const ppcCount = computed(() => {
  const ppcGroup = workGroups.value.find((g) => g.name === "ppc");
  const totalCount = ppcGroup ? ppcGroup.totalCount : 0;
  return totalCount - ppcPopupCount.value;
});

// 전체 팝업 개수 계산 (pay + myd + ppc의 팝업 합계)
/** @type {import('vue').ComputedRef<number>} */
const totalPopupCount = computed(() => {
  return payPopupCount.value + mydPopupCount.value + ppcPopupCount.value;
});

// 그룹별 페이지 개수 반환 (팝업 제외)
function getPageCount(groupName) {
  if (groupName === "pay") return payCount.value;
  if (groupName === "myd") return mydCount.value;
  if (groupName === "ppc") return ppcCount.value;

  // 다른 그룹들은 전체 개수 반환
  const group = workGroups.value.find((g) => g.name === groupName);
  return group ? group.totalCount : 0;
}

// 그룹별 팝업 개수 반환
function getPopupCount(groupName) {
  if (groupName === "pay") return payPopupCount.value;
  if (groupName === "myd") return mydPopupCount.value;
  if (groupName === "ppc") return ppcPopupCount.value;

  // 다른 그룹들은 팝업 개수 계산
  return publishRoutes.value.filter((r) => {
    if (!r.path.startsWith("/publish/")) return false;
    const folder = r.path.split("/")[2] || "";
    if (folder !== groupName) return false;
    const metaId = r.meta?.id || "";
    return isPopup(metaId);
  }).length;
}

// 하위 그룹의 팝업 개수 반환
function getSubGroupPopupCount(subGroup) {
  const paths = subGroup.items.map((item) => item.path);
  return publishRoutes.value.filter((r) => {
    if (!paths.includes(r.path)) return false;
    const metaId = r.meta?.id || "";
    return isPopup(metaId);
  }).length;
}

// 하위 그룹의 페이지 개수 반환 (팝업 제외)
function getSubGroupPageCount(subGroup) {
  const totalCount = subGroup.items.length;
  const popupCount = getSubGroupPopupCount(subGroup);
  return totalCount - popupCount;
}

// 검색 함수
/**
 * 아이템이 검색 조건과 일치하는지 확인
 * @param {LinkItem} item
 * @param {string} query
 * @param {string} filter
 * @returns {boolean}
 */
function matchesSearch(item, query, filter) {
  // 검색어 정규화 (공백 제거)
  const normalizedQuery = query?.trim() || "";
  const lowerQuery = normalizedQuery.toLowerCase();

  // 검색어가 없고 약관 필터가 아닌 경우 모든 항목 반환
  if (!normalizedQuery && filter !== "agree") return true;

  switch (filter) {
    case "name":
      // 이름 필터: 검색어가 있으면 이름으로만 검색
      if (normalizedQuery) {
        return item.worker?.toLowerCase().includes(lowerQuery) ?? false;
      }
      return true;
    case "page":
      // 타이틀 필터: 검색어가 있으면 타이틀로만 검색
      if (normalizedQuery) {
        return item.label.toLowerCase().includes(lowerQuery);
      }
      return true;
    case "path":
      // 경로 필터: 검색어가 있으면 경로로만 검색
      if (normalizedQuery) {
        return item.path.toLowerCase().includes(lowerQuery);
      }
      return true;
    case "agree":
      // 약관 필터: sc-agree 클래스가 포함된 파일인지 확인
      const hasAgreeClass = hasScAgreeClass(item.path);

      // 검색어가 있으면 약관 필터와 검색어 조건을 모두 만족해야 함
      if (normalizedQuery) {
        return (
          hasAgreeClass &&
          (item.label.toLowerCase().includes(lowerQuery) ||
            item.path.toLowerCase().includes(lowerQuery) ||
            (item.worker?.toLowerCase().includes(lowerQuery) ?? false))
        );
      }

      // 검색어가 없으면 약관 필터만 확인
      return hasAgreeClass;
    case "all":
    default:
      // 전체 필터: 검색어가 있으면 이름, 타이틀, 경로 모두에서 검색
      if (normalizedQuery) {
        return (
          item.label.toLowerCase().includes(lowerQuery) ||
          item.path.toLowerCase().includes(lowerQuery) ||
          (item.worker?.toLowerCase().includes(lowerQuery) ?? false)
        );
      }
      return true;
  }
}

// 필터링된 workGroups
/** @type {import('vue').ComputedRef<Group[]>} */
const filteredWorkGroups = computed(() => {
  // 검색어가 있거나 약관 필터가 선택되었을 때만 필터링 수행
  if (!debouncedSearchQuery.value && searchFilter.value !== "agree")
    return workGroups.value;

  return workGroups.value
    .map((grp) => {
      if (grp.items) {
        // Guide: 2뎁스 없이 바로 items
        const filteredItems = grp.items.filter((item) =>
          matchesSearch(item, debouncedSearchQuery.value, searchFilter.value),
        );
        return {
          ...grp,
          items: filteredItems,
          totalCount: filteredItems.length,
        };
      } else if (grp.subGroups) {
        // 2뎁스 구조
        const filteredSubGroups = grp.subGroups
          .map((subGrp) => ({
            ...subGrp,
            items: subGrp.items.filter((item) =>
              matchesSearch(
                item,
                debouncedSearchQuery.value,
                searchFilter.value,
              ),
            ),
          }))
          .filter((subGrp) => subGrp.items.length > 0);

        const totalCount = filteredSubGroups.reduce(
          (acc, sg) => acc + sg.items.length,
          0,
        );

        return {
          ...grp,
          subGroups: filteredSubGroups,
          totalCount,
        };
      }
      return grp;
    })
    .filter((grp) => grp.totalCount > 0);
});

// 필터링된 workerGroups
/** @type {import('vue').ComputedRef<WorkerGroup[]>} */
const filteredWorkerGroups = computed(() => {
  // 검색어가 있거나 약관 필터가 선택되었을 때만 필터링 수행
  if (!debouncedSearchQuery.value && searchFilter.value !== "agree")
    return workerGroups.value;

  return workerGroups.value
    .map((grp) => ({
      ...grp,
      items: grp.items.filter((item) =>
        matchesSearch(item, debouncedSearchQuery.value, searchFilter.value),
      ),
    }))
    .filter((grp) => grp.items.length > 0);
});

// 필터링된 statusGroups
/** @type {import('vue').ComputedRef<StatusGroup[]>} */
const filteredStatusGroups = computed(() => {
  // 검색어가 있거나 약관 필터가 선택되었을 때만 필터링 수행
  if (!debouncedSearchQuery.value && searchFilter.value !== "agree")
    return statusGroups.value;

  return statusGroups.value
    .map((grp) => {
      // 각 카테고리의 아이템 필터링 (모두 3뎁스 구조)
      const filteredCategories = grp.categories
        .map((categoryGrp) => {
          // 3뎁스 구조
          const filteredSubGroups = categoryGrp.subGroups
            .map((subGrp) => {
              const filteredItems = subGrp.items.filter((item) =>
                matchesSearch(
                  item,
                  debouncedSearchQuery.value,
                  searchFilter.value,
                ),
              );

              // 팝업 개수 계산
              const popupCount = filteredItems.filter((item) => {
                const page = generatedPages.find((r) => r.path === item.path);
                const metaId = page?.meta?.id || "";
                return isPopup(metaId);
              }).length;

              const pageCount = filteredItems.length - popupCount;

              return {
                ...subGrp,
                items: filteredItems,
                pageCount,
                popupCount,
              };
            })
            .filter((subGrp) => subGrp.items.length > 0);

          const totalCount = filteredSubGroups.reduce(
            (acc, sg) => acc + sg.items.length,
            0,
          );
          const pageCount = filteredSubGroups.reduce(
            (acc, sg) => acc + sg.pageCount,
            0,
          );
          const popupCount = filteredSubGroups.reduce(
            (acc, sg) => acc + sg.popupCount,
            0,
          );

          return {
            ...categoryGrp,
            subGroups: filteredSubGroups,
            totalCount,
            pageCount,
            popupCount,
          };
        })
        .filter((categoryGrp) => categoryGrp.totalCount > 0);

      const totalCount = filteredCategories.reduce(
        (acc, cg) => acc + cg.totalCount,
        0,
      );
      const pageCount = filteredCategories.reduce(
        (acc, cg) => acc + cg.pageCount,
        0,
      );
      const popupCount = filteredCategories.reduce(
        (acc, cg) => acc + cg.popupCount,
        0,
      );

      return {
        ...grp,
        categories: filteredCategories,
        totalCount,
        pageCount,
        popupCount,
      };
    })
    .filter((grp) => grp.totalCount > 0);
});

// 검색 결과 총 개수
/** @type {import('vue').ComputedRef<number>} */
const searchResultCount = computed(() => {
  // 약관 필터가 선택되었을 때는 검색어가 없어도 결과 개수 계산
  if (!debouncedSearchQuery.value && searchFilter.value !== "agree") return 0;
  return (
    (filteredWorkGroups.value.reduce((acc, g) => acc + g.totalCount, 0) +
      filteredWorkerGroups.value.reduce((acc, g) => acc + g.items.length, 0)) /
    2
  ); // 두 섹션에 중복으로 표시되므로 나누기 2
});

// 검색 결과 표시 여부
const shouldShowResults = computed(() => {
  return (
    (!debouncedSearchQuery.value && searchFilter.value !== "agree") ||
    searchResultCount.value > 0
  );
});

// 검색 결과 없음 표시 여부
const shouldShowNoResults = computed(() => {
  return (
    (debouncedSearchQuery.value || searchFilter.value === "agree") &&
    searchResultCount.value === 0
  );
});

// 폴더명 → 표시 라벨 매핑 (작업/담당자 섹션 공유)
const folderLabelMap = {
  _module: "Module",
  _guide: "Guide",
  myd: "MYD",
  pay: "Pay",
  ppc: "PPC",
  account: "account(자산)",
  auth: "auth(Sign in/up)",
  benefits: "benefits(혜택)",
  discover: "discover(디스커버)",
  menu: "menu(전체메뉴)",
  my: "my(마이)",
  payplus: "payplus(페이플러스)",
};

/**
 * 경로에서 1-depth 폴더 라벨 반환
 * @param {string} path
 */
function folderLabel(path) {
  const after = path.replace("/publish/", "");
  const folder = after.split("/")[0] || "기타";
  return folderLabelMap[folder] ?? folder;
}

/**
 * 경로에서 메타정보의 menu 값 반환
 * @param {string} path
 * @returns {string}
 */
function getMetaMenu(path) {
  const page = generatedPages.find((r) => r.path === path);
  return page?.meta?.menu || "";
}

// 애니메이션 이벤트 핸들러
function onFocus() {
  animationComplete.value = false;

  // 검색 입력 필드 클릭 시 검색 영역을 상단으로 스크롤
  if (searchSection.value) {
    searchSection.value.scrollIntoView({
      behavior: "smooth",
      block: "start",
    });
  }
}

function onBlur() {
  animationComplete.value = false;
}

function onAnimationEnd(event) {
  if (event.animationName === "borderDraw") {
    animationComplete.value = true;
  }
}

// 검색 입력 핸들러 (실시간 검색을 위해)
function onSearchInput(event) {
  searchQuery.value = event.target.value;

  // Debounce: 300ms 후에 실제 검색 실행
  if (searchDebounceTimer) clearTimeout(searchDebounceTimer);

  searchDebounceTimer = setTimeout(() => {
    debouncedSearchQuery.value = searchQuery.value;
    // 검색어 입력 시 아코디언을 자동으로 펼치지 않도록 유지
    // 검색 중 1뎁스만 자동 펼침: _guide는 접힘 유지, 2뎁스는 닫힘
    if (debouncedSearchQuery.value.length > 0) {
      openPrimaryItems.value = workGroups.value
        .filter((grp) => grp.name !== "_guide")
        .map((grp) => grp.name);
      openSecondaryItems.value = [];
    }
  }, 300);
}

// 섹션 H2 높이 측정하여 CSS 변수(--sec-h2-h) 주입
onMounted(async () => {
  try {
    await nextTick();

    // 데이터 로딩 시뮬레이션 (파일 캐시가 준비될 때까지 대기)
    await new Promise((resolve) => setTimeout(resolve, 100));

    // Header 높이 계산
    const calculateHeaderHeight = () => {
      // 여러 가능한 header 선택자 시도
      const headerSelectors = [
        ".sc-header",
        ".sv-navigation",
        ".pms-page__header",
        "header",
        '[class*="header"]',
        '[class*="Header"]',
      ];

      let headerElement = null;
      for (const selector of headerSelectors) {
        headerElement = document.querySelector(selector);
        if (headerElement) break;
      }

      if (headerElement) {
        const height = Math.ceil(headerElement.getBoundingClientRect().height);
        headerHeight.value = height;
        document.documentElement.style.setProperty(
          "--calculated-header-height",
          `${height}px`,
        );
      } else {
        // header를 찾지 못한 경우 CSS 변수 또는 기본값 사용
        const cssHeight = getComputedStyle(document.documentElement)
          .getPropertyValue("--sc-header-height")
          .trim();
        const defaultHeight = cssHeight ? parseInt(cssHeight) : 60;
        headerHeight.value = defaultHeight;
        document.documentElement.style.setProperty(
          "--calculated-header-height",
          `${defaultHeight}px`,
        );
      }
    };

    calculateHeaderHeight();
    resizeHandlerForHeader = calculateHeaderHeight;
    window.addEventListener("resize", calculateHeaderHeight);

    // 스크롤 이벤트로 header 표시/숨김 제어
    const handleScroll = () => {
      const currentScrollY = window.scrollY;
      const scrollThreshold = 50; // 스크롤 임계값

      if (currentScrollY > scrollThreshold) {
        // 아래로 스크롤 (header 숨김)
        if (currentScrollY > lastScrollY.value && isHeaderVisible.value) {
          isHeaderVisible.value = false;
          const headerSelectors = [
            ".sc-header",
            ".sv-navigation",
            ".pms-page__header",
            "header",
            '[class*="header"]',
            '[class*="Header"]',
          ];

          let headerElement = null;
          for (const selector of headerSelectors) {
            headerElement = document.querySelector(selector);
            if (headerElement) break;
          }

          if (headerElement) {
            headerElement.style.transform = `translateY(-${headerHeight.value}px)`;
            headerElement.style.transition = "transform 0.3s ease-in-out";
          }
        }
        // 위로 스크롤 (header 표시)
        else if (currentScrollY < lastScrollY.value && !isHeaderVisible.value) {
          isHeaderVisible.value = true;
          const headerSelectors = [
            ".sc-header",
            ".sv-navigation",
            ".pms-page__header",
            "header",
            '[class*="header"]',
            '[class*="Header"]',
          ];

          let headerElement = null;
          for (const selector of headerSelectors) {
            headerElement = document.querySelector(selector);
            if (headerElement) break;
          }

          if (headerElement) {
            headerElement.style.transform = "translateY(0)";
            headerElement.style.transition = "transform 0.3s ease-in-out";
          }
        }
      } else {
        // 최상단 근처에서는 항상 header 표시
        if (!isHeaderVisible.value) {
          isHeaderVisible.value = true;
          const headerSelectors = [
            ".sc-header",
            ".sv-navigation",
            ".pms-page__header",
            "header",
            '[class*="header"]',
            '[class*="Header"]',
          ];

          let headerElement = null;
          for (const selector of headerSelectors) {
            headerElement = document.querySelector(selector);
            if (headerElement) break;
          }

          if (headerElement) {
            headerElement.style.transform = "translateY(0)";
            headerElement.style.transition = "transform 0.3s ease-in-out";
          }
        }
      }

      lastScrollY.value = currentScrollY;
    };

    scrollHandler = handleScroll;
    window.addEventListener("scroll", handleScroll, { passive: true });

    const root = document.getElementById("main") || document.body;
    const sections = Array.from(root.querySelectorAll("section"));
    const applySectionH2Heights = () => {
      sections.forEach((sec) => {
        const h2 = sec.querySelector("h2");
        const h = h2 ? Math.ceil(h2.getBoundingClientRect().height) : 0;
        sec && sec.style && sec.style.setProperty("--sec-h2-h", `${h}px`);
      });
    };
    applySectionH2Heights();
    resizeHandlerForSection = applySectionH2Heights;
    window.addEventListener("resize", applySectionH2Heights);

    // 초기 로딩 성능 개선: 필요 시에만 아코디언 펼침
    // statusGroups.value.forEach((grp) => {
    //   if (!openStatusItems.value.includes(grp.name)) {
    //     openStatusItems.value.push(grp.name);
    //   }
    // });
  } finally {
    // 로딩 완료
    isLoading.value = false;
  }
});

// cleanup: 컴포넌트 제거 시 이벤트 리스너 정리
onBeforeUnmount(() => {
  if (scrollHandler) {
    window.removeEventListener("scroll", scrollHandler);
  }
  if (resizeHandlerForHeader) {
    window.removeEventListener("resize", resizeHandlerForHeader);
  }
  if (resizeHandlerForSection) {
    window.removeEventListener("resize", resizeHandlerForSection);
  }

  // Header transform 초기화
  const headerSelectors = [
    ".sc-header",
    ".sv-navigation",
    ".pms-page__header",
    "header",
    '[class*="header"]',
    '[class*="Header"]',
  ];

  let headerElement = null;
  for (const selector of headerSelectors) {
    headerElement = document.querySelector(selector);
    if (headerElement) break;
  }

  if (headerElement) {
    headerElement.style.transform = "";
    headerElement.style.transition = "";
  }
});
</script>

<style lang="scss" scoped>
@use "sass:math";
@use "sass:map";
@use "sass:meta";
@use "@assets/styles/shared" as *; // tokens + mixins

* {
  box-sizing: border-box;
}

body {
  max-width: 100%;
  overflow-x: hidden;
}

/* 메인 콘텐츠 */
.main-content {
  position: relative;
  min-height: 100vh;
}

/* 로딩 인디케이터 */
.loading-container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(2px);
  z-index: 9999;
}

/* 디바이스 정보 */
.deviceinfo {
  margin-bottom: var(--spacing-xl);
  padding: var(--spacing-lg);
  background: var(--bg-graylight);
  border-radius: 8px;
  border-left: 4px solid var(--primary-base);

  > strong {
    display: block;
    margin-bottom: var(--spacing-sm);
    font-size: 16px;
    font-weight: 700;
    color: var(--text-primary);
  }

  .device-list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xs);

    li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: var(--spacing-xs) 0;
      font-size: 14px;
      line-height: 1.6;
      color: var(--text-primary);

      strong {
        flex-shrink: 0;
        font-weight: 600;
        color: var(--text-secondary);
        margin-right: var(--spacing-md);
      }

      span {
        flex: 1;
        text-align: right;
        color: var(--text-primary);
        font-weight: 500;
      }

      &:not(:last-child) {
        border-bottom: 1px solid var(--border-subtle);
        padding-bottom: var(--spacing-sm);
        margin-bottom: var(--spacing-xs);
      }
    }
  }
}

.worker-index__page {
  /* 상단 제목 + 작업자 카운트 영역 */
  .publish-header {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    position: relative;
    width: 100%;
    max-width: 100%;
    padding-inline: 0;
    overflow: hidden;
    h1 {
      width: 100%;
      font-size: clamp(1.5rem, 5vw, 2rem);
    }
    small {
      margin-inline: auto;
      color: var(--text-secondary);
      @include font-set(body-m, 500);
    }
  }
  .divider {
    display: flex;
    justify-content: space-around;
    max-width: 100%;
    overflow: hidden;
    padding: 0 var(--spacing-md);
    small {
      display: inline-flex;
      gap: 4px;
      margin-inline: auto;
      color: var(--text-secondary);
      @include font-set(body-m, 500);
      white-space: nowrap;
    }
  }
  .worker-counts {
    display: flex;
    flex-wrap: wrap;
    gap: var(--spacing-lg);
    flex-wrap: wrap;
    list-style: none;
    margin: 0;
    padding: 0;
    max-width: 100%;
    overflow: hidden;
  }
  .worker-counts .name {
    color: var(--text-secondary);
    margin-right: var(--spacing-xs);
  }
  .worker-counts .count {
    display: inline-block;
    min-width: 20px;
    padding: 2px 8px;
    border-radius: 999px;
    background: var(--bg-graylight);
    color: var(--text-secondary);
    text-align: center;
  }

  section {
    margin-top: var(--spacing-2xl);
  }
  /* 섹션 제목 간격: 좌우 20px, 하단 16px */
  section > h2 {
    position: sticky;
    top: var(--sc-header-height, 60px);
    padding-inline: var(--spacing-2xl);
    margin-bottom: var(--spacing-xl);
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    background-color: var(--bg-canvas-white);
    z-index: 5;
  }
  section > h2 .count {
    color: var(--text-secondary);
  }

  /* 아코디언 리스트 */
  .accordion-list {
    list-style: none;
    margin: 0;
    padding: 0;

    &.accordion-list--primary {
      > .accordion-item {
        margin-bottom: var(--spacing-md);
        background: var(--bg-canvas-white);
        border-radius: 8px;
        overflow: hidden;

        > .accordion-header {
          background: var(--bg-graylight);
          padding: 16px 20px;
          font-weight: 600;
          font-size: 16px;
          cursor: pointer;
          user-select: none;
          display: flex;
          align-items: center;
          justify-content: space-between;
          position: sticky;
          top: calc(var(--sc-header-height, 60px) + var(--sec-h2-h, 48px));
          z-index: 3;

          .accordion-title {
            flex: 1;
          }

          .accordion-icon {
            transition: transform 0.2s ease;
            width: 20px;
            height: 20px;
            color: var(--text-secondary);
          }
        }

        &.is-open > .accordion-header {
          position: relative;
          top: auto;

          .accordion-icon {
            transform: rotate(-180deg);
          }
        }

        > .accordion-content {
          padding: 0;

          // Guide 폴더는 2뎁스 없이 바로 링크 리스트
          > .link-list {
            padding: 0;
          }
        }
      }
    }

    &.accordion-list--secondary {
      padding: 0;
      margin: 0;

      > .accordion-item {
        margin-bottom: var(--spacing-sm);

        > .accordion-header {
          background: var(--bg-canvas-white);
          padding: 12px 20px;
          font-weight: 500;
          font-size: 14px;
          cursor: pointer;
          user-select: none;
          display: flex;
          align-items: center;
          justify-content: space-between;
          border-bottom: 1px solid var(--border-subtle);

          .accordion-title {
            flex: 1;
          }

          .accordion-icon {
            transition: transform 0.2s ease;
            width: 16px;
            height: 16px;
            color: var(--text-secondary);
          }
        }

        &.is-open > .accordion-header .accordion-icon {
          transform: rotate(-180deg);
        }

        > .accordion-content {
          padding: 0;
        }
      }
    }

    // 작업 상태 섹션의 2뎁스 (Guide, MYD, Pay, PPC)
    &.accordion-list--status-category {
      > .accordion-item {
        > .accordion-header {
          font-weight: 700;
        }
      }
    }
  }

  ul.link-list {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .link-item {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 100%;
    max-width: 100%;
    padding: 12px 20px;
    color: var(--text-primary);
    font-size: 14px;
    text-decoration: none;
    gap: 4px;

    .link-content {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      gap: 8px;
    }

    span {
      overflow: hidden;
      text-overflow: ellipsis;
      font-size: 14px;
    }

    &:hover {
      color: var(--primary-base);
    }
  }

  .text-secondary {
    color: var(--text-secondary);
  }

  .meta-menu {
    font-size: 12px;
    color: var(--text-secondary);
  }

  /* 검색 영역 */
  .worker-search {
    // 검색 스타일 변수
    $search-border-color: #d0d0d0;
    $search-focus-color: #0066ff;
    $search-border-width: 2px;
    $search-border-radius: 0px;
    $search-animation-border-width: 2px;
    $search-transition-duration: 0.3s;
    $search-animation-duration: 0.3s;

    position: sticky;
    top: 0;
    margin-top: 0;
    margin-bottom: var(--spacing-xl);
    background-color: var(--bg-canvas_white);
    z-index: 100;
    padding: var(--spacing-md) 0;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    border-bottom: 1px solid var(--border-subtle);

    .search-container {
      display: flex;
      flex-direction: column;
      gap: var(--spacing-md);

      .search-input-wrapper {
        position: relative;
        width: 100%;
        padding: $search-border-width;
        border-radius: $search-border-radius;
        border: $search-border-width solid $search-border-color;
        background: var(--bg-canvas-white);
        transition: border-color $search-transition-duration ease;
        overflow: visible;

        // 시계방향 border 애니메이션
        &::before {
          position: absolute;
          top: -1px;
          left: -1px;
          right: -1px;
          bottom: -1px;
          border-radius: calc(#{$search-border-radius} - 2px);
          background:
            linear-gradient(to right, $search-focus-color 100%, transparent 0)
              top left / 0 $search-animation-border-width no-repeat,
            linear-gradient(to bottom, $search-focus-color 100%, transparent 0)
              top right / $search-animation-border-width 0 no-repeat,
            linear-gradient(to left, $search-focus-color 100%, transparent 0)
              bottom right / 0 $search-animation-border-width no-repeat,
            linear-gradient(to top, $search-focus-color 100%, transparent 0)
              bottom left / $search-animation-border-width 0 no-repeat;
          content: "";
          pointer-events: none;
          opacity: 0;
          transition: opacity $search-transition-duration;
        }
        &:focus-within {
          &::before {
            opacity: 1;
            animation: borderDraw $search-animation-duration ease-out forwards;
          }

          // 애니메이션 완료 후 파란색 border로 변경
          &.animation-complete {
            border-color: $search-focus-color;

            &::before {
              opacity: 0;
            }
          }

          // 애니메이션 진행 중에는 회색 border 유지
          &:not(.animation-complete) {
            border-color: $search-border-color;
          }
        }

        .search-input {
          width: 100%;
          padding: 12px 40px 12px 16px;
          font-size: 16px;
          border: none;
          border-radius: 0px;
          background: transparent;
          color: var(--text-primary);
          position: relative;
          z-index: 1;

          &:focus {
            outline: none;
          }

          &::placeholder {
            color: var(--text-secondary);
          }
        }

        .clear-btn {
          $clear-btn-size: 28px;
          $clear-btn-transition: 0.2s;

          position: absolute;
          right: 10px;
          top: 50%;
          transform: translateY(-50%);
          width: $clear-btn-size;
          height: $clear-btn-size;
          border: none;
          border-radius: 50%;
          background: var(--text-secondary);
          color: white;
          font-size: 18px;
          cursor: pointer;
          display: flex;
          align-items: center;
          justify-content: center;
          transition: background $clear-btn-transition ease;
          padding: 0;
          line-height: 1;
          z-index: 2;

          &:hover {
            background: $search-focus-color;
          }

          &:focus {
            outline: 2px solid $search-focus-color;
            outline-offset: 2px;
          }
        }
      }
      .filter-buttons {
        padding-right: 16px;
        padding-left: 16px;
      }

      @keyframes borderDraw {
        0% {
          background-size:
            0 $search-animation-border-width,
            $search-animation-border-width 0,
            0 $search-animation-border-width,
            $search-animation-border-width 0;
          opacity: 1;
        }
        25% {
          background-size:
            100% $search-animation-border-width,
            $search-animation-border-width 0,
            0 $search-animation-border-width,
            $search-animation-border-width 0;
          opacity: 1;
        }
        50% {
          background-size:
            100% $search-animation-border-width,
            $search-animation-border-width 100%,
            0 $search-animation-border-width,
            $search-animation-border-width 0;
          opacity: 1;
        }
        75% {
          background-size:
            100% $search-animation-border-width,
            $search-animation-border-width 100%,
            100% $search-animation-border-width,
            $search-animation-border-width 0;
          opacity: 1;
        }
        95% {
          background-size:
            100% $search-animation-border-width,
            $search-animation-border-width 100%,
            100% $search-animation-border-width,
            $search-animation-border-width 100%;
          opacity: 1;
        }
        100% {
          background-size:
            100% $search-animation-border-width,
            $search-animation-border-width 100%,
            100% $search-animation-border-width,
            $search-animation-border-width 100%;
          opacity: 1;
        }
      }

      .filter-buttons {
        $filter-btn-transition: 0.2s;

        display: flex;
        gap: var(--spacing-sm);
        flex-wrap: wrap;

        .filter-btn {
          padding: 8px 16px;
          font-size: 14px;
          font-weight: 500;
          border: 2px solid var(--border-subtle);
          border-radius: 20px;
          background: var(--bg-canvas-white);
          color: var(--text-secondary);
          cursor: pointer;
          transition: all $filter-btn-transition ease;
          user-select: none;

          &:hover {
            border-color: var(--primary-base);
            color: var(--primary-base);
          }

          &.active {
            border-color: $search-focus-color;
            background: $search-focus-color;
            color: #ffffff;
          }
        }
      }
    }

    .search-results {
      margin-top: var(--spacing-sm);
      padding: 8px 16px;
      background: var(--bg-graylight);
      border-radius: 8px;

      .search-result-count {
        color: var(--text-secondary);
        @include font-set(body-m, 500);

        strong {
          color: $search-focus-color;
          font-weight: 700;
        }
      }

      .search-help {
        display: block;
        margin-top: 4px;
        color: var(--text-secondary);
        @include font-set(body-s, 400);
        font-style: italic;
      }
    }
  }

  .worker-search__no-results {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: var(--spacing-3xl) var(--spacing-xl);
    margin-top: var(--spacing-2xl);
    color: var(--text-secondary);
    font-size: 16px;
    font-style: italic;
    text-align: center;
  }
}
</style>




```
{% endraw %}
