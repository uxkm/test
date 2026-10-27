# 페이지 기본 예시

Vue 2, Vue 3, React, Next.js에서 페이지 하나를 만드는 최소 구조입니다.

## Vue 2

Options API를 쓰는 단일 파일 컴포넌트입니다. 페이지는 `src/views/Home.vue`에 둡니다.

```vue
<template>
  <main>
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <button @click="count++">클릭 {{ count }}</button>
  </main>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      title: "Vue 2 페이지",
      message: "Options API로 상태를 둡니다.",
      count: 0,
    };
  },
};
</script>
```

목록 페이지는 `v-for`로 항목을 돌고, `v-if`로 상태 문구를 나눕니다. 항목을 누르면 화면을 덮는 레이어 팝업이 열립니다.

```vue
<!-- src/views/List.vue -->
<template>
  <main>
    <h1>목록</h1>

    <p v-if="items.length === 0">등록된 항목이 없습니다.</p>

    <ul v-else>
      <li v-for="(item, index) in items" :key="item.id">
        <button type="button" @click="open(item)">
          {{ index + 1 }}. {{ item.name }}
          <span v-if="item.status === 'done'">완료</span>
          <span v-else-if="item.status === 'hold'">보류</span>
          <span v-else>진행</span>
        </button>
      </li>
    </ul>

    <div v-if="selected" class="layer" @click.self="close">
      <div class="popup" role="dialog" aria-modal="true">
        <h2>{{ selected.name }}</h2>
        <p>{{ selected.desc }}</p>
        <button type="button" @click="close">닫기</button>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
      selected: null,
      items: [
        { id: 1, name: "공지", desc: "첫 번째 항목", status: "done" },
        { id: 2, name: "안내", desc: "두 번째 항목", status: "progress" },
        { id: 3, name: "일정", desc: "세 번째 항목", status: "hold" },
      ],
    };
  },
  methods: {
    open(item) {
      this.selected = item;
    },
    close() {
      this.selected = null;
    },
  },
};
</script>

<style scoped>
.layer {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.45);
}
.popup {
  width: min(420px, calc(100% - 32px));
  padding: 24px;
  background: #fff;
}
</style>
```

`vue-router` 3을 쓰고, `Vue.use`로 등록한 뒤 루트 인스턴스에 `router`를 넘깁니다.

```js
// src/router/index.js
import Vue from "vue";
import VueRouter from "vue-router";
import Home from "../views/Home.vue";
import About from "../views/About.vue";
import List from "../views/List.vue";

Vue.use(VueRouter);

const routes = [
  { path: "/", name: "Home", component: Home },
  { path: "/about", name: "About", component: About },
  { path: "/list", name: "List", component: List },
];

export default new VueRouter({
  mode: "history",
  routes,
});
```

```js
// src/main.js
import Vue from "vue";
import App from "./App.vue";
import router from "./router";

new Vue({
  router,
  render: (h) => h(App),
}).$mount("#app");
```

```vue
<!-- src/App.vue -->
<template>
  <div id="app">
    <nav>
      <router-link to="/">홈</router-link>
      <router-link to="/about">소개</router-link>
      <router-link to="/list">목록</router-link>
    </nav>
    <router-view />
  </div>
</template>
```

## Vue 3

`<script setup>`과 Composition API를 쓰는 페이지입니다. 파일 위치는 `src/views/Home.vue`입니다.

```vue
<script setup>
import { ref } from "vue";

const title = ref("Vue 3 페이지");
const message = ref("Composition API로 상태를 둡니다.");
const count = ref(0);
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <button @click="count++">클릭 {{ count }}</button>
  </main>
</template>
```

목록 페이지입니다. `v-for`에 인덱스를 같이 받고, 상태에 따라 `v-if` 분기를 탑니다. 선택한 항목은 레이어 팝업으로 보여 줍니다.

```vue
<!-- src/views/List.vue -->
<script setup>
import { ref } from "vue";

const selected = ref(null);
const items = ref([
  { id: 1, name: "공지", desc: "첫 번째 항목", status: "done" },
  { id: 2, name: "안내", desc: "두 번째 항목", status: "progress" },
  { id: 3, name: "일정", desc: "세 번째 항목", status: "hold" },
]);

function open(item) {
  selected.value = item;
}

function close() {
  selected.value = null;
}
</script>

<template>
  <main>
    <h1>목록</h1>

    <p v-if="items.length === 0">등록된 항목이 없습니다.</p>

    <ul v-else>
      <li v-for="(item, index) in items" :key="item.id">
        <button type="button" @click="open(item)">
          {{ index + 1 }}. {{ item.name }}
          <span v-if="item.status === 'done'">완료</span>
          <span v-else-if="item.status === 'hold'">보류</span>
          <span v-else>진행</span>
        </button>
      </li>
    </ul>

    <div v-if="selected" class="layer" @click.self="close">
      <div class="popup" role="dialog" aria-modal="true">
        <h2>{{ selected.name }}</h2>
        <p>{{ selected.desc }}</p>
        <button type="button" @click="close">닫기</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
.layer {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.45);
}
.popup {
  width: min(420px, calc(100% - 32px));
  padding: 24px;
  background: #fff;
}
</style>
```

`vue-router` 4는 `createRouter`로 만들고 `app.use(router)`로 연결합니다. 화면의 `<router-link>`, `<router-view>`는 Vue 2와 같습니다.

```js
// src/router/index.js
import { createRouter, createWebHistory } from "vue-router";
import Home from "../views/Home.vue";
import About from "../views/About.vue";
import List from "../views/List.vue";

const routes = [
  { path: "/", name: "Home", component: Home },
  { path: "/about", name: "About", component: About },
  { path: "/list", name: "List", component: List },
];

export default createRouter({
  history: createWebHistory(),
  routes,
});
```

```js
// src/main.js
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";

createApp(App).use(router).mount("#app");
```

```vue
<!-- src/App.vue -->
<template>
  <nav>
    <router-link to="/">홈</router-link>
    <router-link to="/about">소개</router-link>
    <router-link to="/list">목록</router-link>
  </nav>
  <router-view />
</template>
```

## React

함수 컴포넌트와 `useState`로 만든 페이지입니다. `src/pages/Home.jsx`에 둡니다.

```jsx
import { useState } from "react";

export default function Home() {
  const [count, setCount] = useState(0);

  return (
    <main>
      <h1>React 페이지</h1>
      <p>함수 컴포넌트로 화면을 구성합니다.</p>
      <button onClick={() => setCount(count + 1)}>클릭 {count}</button>
    </main>
  );
}
```

목록 페이지입니다. `map`으로 항목을 돌고, 삼항 연산자와 `&&`로 상태와 팝업을 나눕니다. 항목을 누르면 레이어 팝업이 열립니다.

```jsx
// src/pages/List.jsx
import { useState } from "react";
import "./List.css";

const items = [
  { id: 1, name: "공지", desc: "첫 번째 항목", status: "done" },
  { id: 2, name: "안내", desc: "두 번째 항목", status: "progress" },
  { id: 3, name: "일정", desc: "세 번째 항목", status: "hold" },
];

const statusLabel = {
  done: "완료",
  hold: "보류",
  progress: "진행",
};

export default function List() {
  const [selected, setSelected] = useState(null);

  return (
    <main>
      <h1>목록</h1>

      {items.length === 0 ? (
        <p>등록된 항목이 없습니다.</p>
      ) : (
        <ul>
          {items.map((item, index) => (
            <li key={item.id}>
              <button type="button" onClick={() => setSelected(item)}>
                {index + 1}. {item.name}{" "}
                <span>{statusLabel[item.status] ?? "진행"}</span>
              </button>
            </li>
          ))}
        </ul>
      )}

      {selected && (
        <div className="layer" onClick={() => setSelected(null)}>
          <div
            className="popup"
            role="dialog"
            aria-modal="true"
            onClick={(event) => event.stopPropagation()}
          >
            <h2>{selected.name}</h2>
            <p>{selected.desc}</p>
            <button type="button" onClick={() => setSelected(null)}>
              닫기
            </button>
          </div>
        </div>
      )}
    </main>
  );
}
```

```css
/* List.css */
.layer {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.45);
}
.popup {
  width: min(420px, calc(100% - 32px));
  padding: 24px;
  background: #fff;
}
```

`react-router-dom`의 `BrowserRouter`로 앱을 감싸고, `Routes` 안에서 `element`로 페이지를 연결합니다.

```jsx
// src/main.jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>
);
```

```jsx
// src/App.jsx
import { Link, Route, Routes } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import List from "./pages/List";

export default function App() {
  return (
    <>
      <nav>
        <Link to="/">홈</Link>
        <Link to="/about">소개</Link>
        <Link to="/list">목록</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/list" element={<List />} />
      </Routes>
    </>
  );
}
```

## Next.js

App Router 기준의 기본 페이지입니다. 클릭처럼 브라우저 상태가 필요하면 파일 맨 위에 `"use client"`를 붙입니다.

```tsx
"use client";

import { useState } from "react";

export default function Page() {
  const [count, setCount] = useState(0);

  return (
    <main>
      <h1>Next.js 페이지</h1>
      <p>app/page.tsx가 루트 경로입니다.</p>
      <button onClick={() => setCount(count + 1)}>클릭 {count}</button>
    </main>
  );
}
```

목록 페이지입니다. `app/list/page.tsx`가 `/list`가 됩니다. `map`과 조건식으로 목록을 그리고, 항목을 누르면 레이어 팝업이 열립니다.

```tsx
// app/list/page.tsx
"use client";

import { useState } from "react";

const items = [
  { id: 1, name: "공지", desc: "첫 번째 항목", status: "done" },
  { id: 2, name: "안내", desc: "두 번째 항목", status: "progress" },
  { id: 3, name: "일정", desc: "세 번째 항목", status: "hold" },
];

const statusLabel: Record<string, string> = {
  done: "완료",
  hold: "보류",
  progress: "진행",
};

export default function ListPage() {
  const [selected, setSelected] = useState<(typeof items)[number] | null>(
    null
  );

  return (
    <main>
      <h1>목록</h1>

      {items.length === 0 ? (
        <p>등록된 항목이 없습니다.</p>
      ) : (
        <ul>
          {items.map((item, index) => (
            <li key={item.id}>
              <button type="button" onClick={() => setSelected(item)}>
                {index + 1}. {item.name}{" "}
                <span>{statusLabel[item.status] ?? "진행"}</span>
              </button>
            </li>
          ))}
        </ul>
      )}

      {selected && (
        <div className="layer" onClick={() => setSelected(null)}>
          <div
            className="popup"
            role="dialog"
            aria-modal="true"
            onClick={(event) => event.stopPropagation()}
          >
            <h2>{selected.name}</h2>
            <p>{selected.desc}</p>
            <button type="button" onClick={() => setSelected(null)}>
              닫기
            </button>
          </div>
        </div>
      )}

      <style jsx>{`
        .layer {
          position: fixed;
          inset: 0;
          display: flex;
          align-items: center;
          justify-content: center;
          background: rgba(0, 0, 0, 0.45);
        }
        .popup {
          width: min(420px, calc(100% - 32px));
          padding: 24px;
          background: #fff;
        }
      `}</style>
    </main>
  );
}
```

Next.js는 파일 경로가 주소입니다. `app/page.tsx`는 `/`, `app/about/page.tsx`는 `/about`, `app/list/page.tsx`는 `/list`입니다. 이동은 `next/link`의 `Link`를 쓰고, 공통 메뉴는 `app/layout.tsx`에 둡니다.

```tsx
// app/layout.tsx
import Link from "next/link";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="ko">
      <body>
        <nav>
          <Link href="/">홈</Link>
          <Link href="/about">소개</Link>
          <Link href="/list">목록</Link>
        </nav>
        {children}
      </body>
    </html>
  );
}
```

```tsx
// app/about/page.tsx
export default function AboutPage() {
  return (
    <main>
      <h1>소개</h1>
    </main>
  );
}
```
