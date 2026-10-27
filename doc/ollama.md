# Ollama 설치 후 VSCode 오프라인 AI 환경 구성

> MacBook Air 16GB 기준  
> 목표: VSCode에서 Vue / React 프로젝트 분석, 코드 생성, 수정 및 Agent 활용

---

## 전체 진행 순서

```text
Mac : curl -fsSL https://ollama.com/install.sh | sh
Win : irm https://ollama.com/install.ps1 | iex

1. Ollama 설치
      ↓
2. Ollama 정상 실행 확인
      ↓
3. 로컬 AI 모델 설치
      ↓
4. AI 모델 실행 테스트
      ↓
5. VSCode Continue 설치
      ↓
6. Continue ↔ Ollama 연결
      ↓
7. VSCode에서 AI Chat 사용
      ↓
8. 프로젝트 코드 분석
      ↓
9. 코드 수정
      ↓
10. Agent를 이용한 파일 생성/수정
      ↓
11. 코드 자동완성 설정
      ↓
12. 인터넷 차단 후 오프라인 테스트
```

---

# 1. Ollama 설치 확인

Ollama 설치가 끝났다면 macOS 터미널 또는 VSCode 터미널을 실행합니다.

```bash
ollama --version
```

정상적으로 설치되어 있으면 Ollama 버전이 표시됩니다.

예:

```text
ollama version 0.x.x
```

---

# 2. Ollama 서버 확인

다음 명령을 실행합니다.

```bash
curl http://localhost:11434
```

정상적으로 실행 중이면 다음과 비슷한 메시지가 표시됩니다.

```text
Ollama is running
```

만약 연결되지 않는다면 다음을 실행합니다.

```bash
ollama serve
```

단, macOS에서 Ollama 앱이 이미 실행 중이면 별도로 `ollama serve`를 실행하지 않아도 됩니다.

---

# 3. 코딩 AI 모델 설치

MacBook Air 16GB에서는 우선 7B급 모델로 테스트합니다.

```bash
ollama pull qwen2.5-coder:7b
```

모델 다운로드가 진행됩니다.

다운로드 완료 후 설치된 모델을 확인합니다.

```bash
ollama list
```

예:

```text
NAME                    SIZE
qwen2.5-coder:7b        약 4~5GB
```

---

# 4. AI 모델 실행 테스트

다음 명령으로 모델을 실행합니다.

```bash
ollama run qwen2.5-coder:7b
```

실행되면 터미널에서 직접 질문할 수 있습니다.

예:

```text
Vue 2.6.10에서 v-for를 사용하는 방법을 알려줘.
```

또는:

```text
Vue 2.6.10 기준으로 트리 메뉴 컴포넌트를 만들어줘.

조건:
- Options API 사용
- 외부 라이브러리 사용 금지
- SCSS 사용
- 클릭 시 하위 메뉴 toggle
```

정상적으로 답변이 나오면 Ollama와 로컬 AI 모델 설치가 완료된 것입니다.

종료:

```text
/bye
```

---

# 5. VSCode에 Continue 설치

VSCode를 실행합니다.

```text
VSCode
  ↓
Extensions
  ↓
Continue 검색
  ↓
Install
```

설치가 완료되면 VSCode 사이드바에 Continue가 나타납니다.

Continue 공식 사이트:

https://www.continue.dev/

---

# 6. Continue와 Ollama 연결

Continue 설정에서 Ollama 로컬 모델을 등록합니다.

예:

```yaml
name: Local Offline AI
version: 0.0.1
schema: v1

models:
  - name: Qwen Coder 7B
    provider: ollama
    model: qwen2.5-coder:7b
    roles:
      - chat
      - edit
```

구조는 다음과 같습니다.

```text
VSCode
   │
   ↓
Continue
   │
   ↓
Ollama
   │
   ↓
qwen2.5-coder:7b
```

AI 처리는 MacBook 내부에서 수행됩니다.

---

# 7. VSCode에서 첫 질문

실제 프로젝트를 VSCode에서 엽니다.

예:

```text
project/
├── package.json
├── src/
│   ├── main.js
│   ├── App.vue
│   ├── components/
│   ├── views/
│   └── assets/
│
└── webpack.config.js
```

Continue를 실행하고 다음과 같이 요청합니다.

```text
현재 프로젝트를 분석해줘.

package.json을 확인해서 다음 내용을 알려줘.

- Vue 버전
- Webpack 버전
- Node 환경
- SCSS 구성
- Router 구성
- 프로젝트 디렉터리 구조

아직 파일은 수정하지 마.
```

처음에는 바로 자동수정을 요청하기보다 AI가 현재 프로젝트 환경을 제대로 파악하는지 확인하는 것이 좋습니다.

---

# 8. Vue 2 프로젝트 분석 예제

레거시 Vue 2 프로젝트라면 환경을 명확하게 지정합니다.

예:

```text
현재 프로젝트 환경:

- Vue 2.6.10
- Webpack 3.6.0
- Options API
- SCSS 사용

금지사항:

- Vue 3 문법 사용 금지
- Composition API 사용 금지
- Vite 변경 금지
- package.json 변경 금지
- Webpack 설정 변경 금지
- 신규 라이브러리 설치 금지

현재 프로젝트 구조를 분석해줘.
```

이렇게 조건을 명확하게 지정하면 최신 Vue 문법으로 잘못 변경하는 것을 줄일 수 있습니다.

---

# 9. 기존 코드 수정

예를 들어 다음 파일이 있다고 가정합니다.

```text
src/components/TreeMenu.vue
```

Continue에서 다음과 같이 요청합니다.

```text
TreeMenu.vue를 분석해서 수정해줘.

조건:

- Vue 2.6.10 유지
- 기존 class명 유지
- 기존 HTML 구조 최대한 유지
- 메뉴 클릭 시 하위 메뉴 toggle
- 현재 메뉴에 active 적용
- 기존 SCSS 최대한 유지
- 외부 라이브러리 사용 금지
```

AI가 코드를 분석하고 수정안을 생성합니다.

일반적인 작업 흐름:

```text
TreeMenu.vue
      ↓
AI 분석
      ↓
변경 코드 생성
      ↓
Diff 확인
      ↓
Accept
      ↓
실제 파일 수정
```

따라서 AI 답변을 복사해서 직접 붙여넣지 않고 코드를 수정하는 방식으로 사용할 수 있습니다.

---

# 10. 새로운 Vue 페이지 생성

예:

```text
새로운 사용자 목록 페이지를 만들어줘.

환경:
- Vue 2.6.10
- Options API
- SCSS

생성:

src/views/UserList.vue

기능:

- 사용자 목록 표시
- v-for 사용
- 검색 input
- 사용자 선택
- JSON 데이터 사용

조건:

- 기존 프로젝트 구조 유지
- 기존 class 네이밍 규칙 유지
- 신규 라이브러리 설치 금지
```

AI가 새로운 Vue 파일을 생성하는 작업을 수행할 수 있습니다.

---

# 11. React 페이지 생성

React 프로젝트에서도 사용할 수 있습니다.

예:

```text
src/pages/UserList.jsx를 생성해줘.

조건:

- React 함수형 컴포넌트
- Hooks 사용
- SCSS 사용
- 사용자 목록 map 출력
- 검색 기능
- 사용자 선택 기능
- 기존 프로젝트 구조 유지
- 기존 class 네이밍 규칙 유지
```

---

# 12. 여러 파일 수정

Agent 기능을 사용하면 하나의 기능을 구현하면서 여러 파일을 수정할 수 있습니다.

예:

```text
사용자 관리 페이지를 추가해줘.

필요한 작업:

1. UserList.vue 생성
2. UserItem.vue 생성
3. Router에 /users 추가
4. 필요한 SCSS 생성
5. 기존 Layout 사용

조건:

- Vue 2.6.10
- 기존 프로젝트 구조 유지
- package.json 변경 금지
- 신규 라이브러리 설치 금지
```

예상되는 변경:

```text
src/
├── views/
│   └── UserList.vue
│
├── components/
│   └── UserItem.vue
│
├── router/
│   └── index.js
│
└── assets/
    └── scss/
        └── _user.scss
```

---

# 13. Continue 작업 방식

Continue에서는 용도에 따라 작업 방식이 달라집니다.

## Chat

일반적인 코딩 질문과 코드 설명에 사용합니다.

```text
Vue 2에서 ref가 어떻게 동작하는지 설명해줘.
```

---

## Plan

프로젝트를 분석하고 수정 방향을 확인할 때 사용합니다.

```text
현재 프로젝트를 분석하고
TreeMenu를 수정하려면 어떤 파일을 변경해야 하는지 알려줘.

아직 파일은 수정하지 마.
```

---

## Agent

실제 프로젝트 파일을 생성하거나 수정하는 작업에 사용합니다.

```text
TreeMenu 기능을 수정해줘.

필요하면 관련 Vue와 SCSS 파일도 수정해.
```

Agent의 목적은 다음과 같습니다.

```text
Agent
 │
 ├─ 프로젝트 파일 검색
 │
 ├─ 파일 읽기
 │
 ├─ 코드 분석
 │
 ├─ 기존 파일 수정
 │
 ├─ 새로운 파일 생성
 │
 └─ 필요한 명령 실행
```

---

# 14. 자동수정

AI가 실제 프로젝트 파일을 수정하도록 할 수 있습니다.

예:

```text
현재 Header.vue를 수정해줘.

요구사항:

- 기존 HTML 구조 유지
- 기존 class 유지
- 모바일 메뉴 기능 추가
- Vue 2 문법 사용
- 기존 SCSS 유지
```

작업 흐름:

```text
요구사항 입력
      ↓
AI 프로젝트 분석
      ↓
관련 파일 확인
      ↓
수정안 생성
      ↓
Diff 표시
      ↓
사용자 확인
      ↓
Accept
      ↓
파일 수정
```

처음에는 자동으로 모든 변경을 허용하기보다 Diff를 확인하고 적용하는 것을 권장합니다.

---

# 15. 코드 자동완성 모델 설치

Chat / Edit 모델과 자동완성 모델을 분리해서 사용할 수도 있습니다.

자동완성용 모델:

```bash
ollama pull qwen2.5-coder:1.5b
```

설치 확인:

```bash
ollama list
```

예:

```text
qwen2.5-coder:7b
qwen2.5-coder:1.5b
```

---

# 16. Continue 자동완성 설정

예:

```yaml
models:
  - name: Qwen Coder 7B
    provider: ollama
    model: qwen2.5-coder:7b
    roles:
      - chat
      - edit

  - name: Qwen Autocomplete
    provider: ollama
    model: qwen2.5-coder:1.5b
    roles:
      - autocomplete
```

역할:

```text
Qwen2.5-Coder 7B
      │
      ├─ Chat
      ├─ 코드 분석
      └─ 코드 수정


Qwen2.5-Coder 1.5B
      │
      └─ 코드 자동완성
```

---

# 17. 자동완성 사용

예를 들어 다음 코드까지 작성합니다.

```javascript
methods: {
  toggleMenu(index) {
```

AI가 다음에 들어갈 코드를 예측하여 제안합니다.

적절한 코드라면 `Tab`을 눌러 적용합니다.

---

# 18. 오프라인 테스트

모든 설치가 완료되었다면 Wi-Fi를 끕니다.

그리고 VSCode를 실행합니다.

구조:

```text
인터넷
  X

MacBook Air
   │
   ├─ VSCode
   │    │
   │    └─ Continue
   │          │
   │          ↓
   │       Ollama
   │          │
   │          ↓
   │     Local AI Model
   │
   └─ 프로젝트 파일
```

Continue에서 다음과 같이 질문합니다.

```text
현재 App.vue를 분석해줘.
```

정상적으로 답변이 나오면 오프라인 AI 환경이 구축된 것입니다.

---

# 19. 오프라인에서 가능한 작업

| 작업 | 가능 여부 |
|---|---|
| AI Chat | 가능 |
| HTML 작성 | 가능 |
| CSS 작성 | 가능 |
| SCSS 작성 | 가능 |
| JavaScript 작성 | 가능 |
| Vue 2 코드 작성 | 가능 |
| Vue 3 코드 작성 | 가능 |
| React 코드 작성 | 가능 |
| 오류 분석 | 가능 |
| 현재 파일 분석 | 가능 |
| 코드 수정 | 가능 |
| 파일 생성 | 가능 |
| 여러 파일 수정 | 가능 |
| 코드 자동완성 | 가능 |
| Agent 작업 | 가능 |
| 인터넷 검색 | 불가능 |
| 새로운 npm 패키지 다운로드 | 인터넷 필요 |
| 최신 문서 검색 | 인터넷 필요 |

---

# 20. 오프라인 환경의 주의점

AI가 다음 파일을 작성하는 것은 가능합니다.

```text
package.json
vite.config.js
webpack.config.js
.vue
.jsx
.js
.scss
.css
.html
```

하지만 인터넷이 완전히 차단되어 있고 필요한 npm 패키지가 로컬에 없다면:

```bash
npm install
```

을 실행해도 새로운 패키지를 다운로드할 수 없습니다.

즉 다음 두 가지는 구분해야 합니다.

```text
AI가 코드 작성
      ↓
오프라인 가능


npm 패키지 다운로드
      ↓
인터넷 필요
```

폐쇄망에서 새로운 프로젝트까지 생성하려면 필요한 npm 패키지와 캐시를 미리 준비해야 합니다.

---

# 21. MacBook Air 16GB 권장 구성

기본 구성:

```text
MacBook Air 16GB
       │
       ├─ VSCode
       │
       ├─ Continue
       │
       └─ Ollama
            │
            ├─ Qwen2.5-Coder 7B
            │     ├─ Chat
            │     ├─ 코드 분석
            │     └─ 코드 수정
            │
            └─ Qwen2.5-Coder 1.5B
                  └─ 자동완성
```

---

# 22. 실제 구축 순서 요약

현재 Ollama 설치까지 완료했다면 다음 순서로 진행합니다.

### STEP 1

Ollama 확인:

```bash
ollama --version
```

### STEP 2

코딩 모델 다운로드:

```bash
ollama pull qwen2.5-coder:7b
```

### STEP 3

설치 확인:

```bash
ollama list
```

### STEP 4

모델 실행:

```bash
ollama run qwen2.5-coder:7b
```

### STEP 5

코딩 질문 테스트:

```text
Vue 2.6.10에서 v-for를 사용하는 예제를 만들어줘.
```

### STEP 6

VSCode에 Continue 설치

```text
Extensions
→ Continue
→ Install
```

### STEP 7

Continue와 Ollama 연결

```text
VSCode
 ↓
Continue
 ↓
Ollama
 ↓
Qwen Coder
```

### STEP 8

실제 프로젝트 분석:

```text
현재 프로젝트의 package.json과
프로젝트 구조를 분석해줘.

아직 파일은 수정하지 마.
```

### STEP 9

코드 수정:

```text
현재 Vue 파일을 분석해서 수정해줘.

기존 class명과 프로젝트 구조는 유지해.
```

### STEP 10

Agent 테스트:

```text
새로운 페이지를 생성하고
필요한 Router와 SCSS까지 수정해줘.

변경하기 전에 수정 대상 파일을 확인해줘.
```

---

# 최종 목표

모든 설정이 완료되면 다음과 같은 작업 환경을 만들 수 있습니다.

```text
VSCode에서 프로젝트 열기
          ↓
AI에게 요구사항 입력
          ↓
프로젝트 파일 분석
          ↓
Vue / React 코드 생성
          ↓
기존 코드 자동수정
          ↓
새로운 파일 생성
          ↓
여러 파일 수정
          ↓
Diff 확인
          ↓
Accept
          ↓
실제 프로젝트 반영
```

인터넷이 없는 환경에서도 로컬 Ollama 모델을 이용하여 Vue / React / JavaScript / HTML / CSS / SCSS 프로젝트의 코딩 질문, 분석 및 수정 작업을 수행할 수 있습니다.
