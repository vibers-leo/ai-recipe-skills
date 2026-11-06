# "앱다운" 모바일 웹 가이드

> **문제:** Next.js·Rails 웹은 데스크톱에서 괜찮은데 **모바일에서 투박하다.**
> 원인은 대부분 "데스크톱 레이아웃을 줄인 것"이지 "모바일로 설계한 것"이 아니기 때문이다.
>
> **이 문서의 목표:** 브라우저에서 열었는데 **네이티브 앱처럼 느껴지는** 모바일 웹.
> 수치는 강남언니 앱 22화면 실측(`vibers-app-skill/screen-patterns.md`)을 웹으로 옮긴 것이다.
>
> 적용 대상: 도메인 붙는 모든 Next.js / Rails / 순수 HTML 프로젝트의 **모바일 뷰(≤768px)**

---

## 0. 웹이 "앱답지 않게" 보이는 7가지 신호

작업 시작 전 이것부터 확인한다. 하나라도 해당하면 그게 투박함의 원인이다.

| 신호 | 왜 앱답지 않은가 | 고치는 법 |
|------|-----------------|----------|
| 좌우 패딩이 화면마다 다름 (16/24/12 혼재) | 스크롤할 때 텍스트 시작점이 흔들린다 | **20px 단일값**으로 통일 |
| 본문이 14~15px | 앱은 16~17px가 기본. 작으면 "웹페이지"로 읽힌다 | 본문 **17px** |
| 버튼 높이 40~48px | 앱 버튼은 52~60px. 얇으면 링크처럼 보인다 | 주요 버튼 **56px** |
| 하단에 아무것도 없음 | 앱은 항상 하단에 손이 닿는 무언가가 있다 | 하단 탭바 or 고정 CTA |
| 모달이 화면 중앙에 뜸 | 앱은 **아래에서 올라온다**(바텀시트) | 바텀시트로 전환 |
| 섹션 사이가 구분선으로 나뉨 | 앱은 여백·배경색으로 나눈다 | 구분선 → 여백 40px |
| 그림자 진한 카드가 잔뜩 | 앱은 그림자를 아낀다 | 그림자 제거, 여백으로 분리 |

---

## 1. 레이아웃

### 1-1. 모바일은 "한 열(single column)" — 예외 없음

```css
/* 모바일에서 grid/flex 다단은 전부 1열로 */
@media (max-width: 768px) {
  .grid-2, .grid-3, .grid-4 { grid-template-columns: 1fr; }
}
```

**단 예외 2가지**
- 아이콘 그리드(카테고리 진입) → **4열 유지**
- 상품 카드 → 1열 대신 **가로 스크롤**(아래 1-3)

### 1-2. 최대 폭 고정 — 큰 폰에서 늘어지지 않게

```css
.app-shell {
  max-width: 480px;      /* 앱 프레임 폭 */
  margin: 0 auto;
  min-height: 100dvh;    /* ⚠️ vh 아님 — iOS 주소창 때문에 100vh는 잘린다 */
}
```

> `100vh` 쓰면 iOS Safari에서 하단이 주소창에 잘린다. **`100dvh`** 필수. 미지원 대비 `min-height: 100vh; min-height: 100dvh;` 로 2줄 선언.

### 1-3. 가로 스크롤 카드 — "다음 카드 20% 걸치기" ⭐

**앱다움의 핵심 신호.** 리스트를 세로로 쭉 나열하면 웹, 가로로 살짝 걸치게 하면 앱이다.

```css
.h-scroll {
  display: flex;
  gap: 12px;
  overflow-x: auto;
  padding-inline: 20px;
  scroll-snap-type: x mandatory;   /* 스냅 필수 — 없으면 어중간하게 멈춘다 */
  scrollbar-width: none;           /* 스크롤바 숨김 */
  -webkit-overflow-scrolling: touch;
}
.h-scroll::-webkit-scrollbar { display: none; }

.h-scroll > * {
  flex: 0 0 auto;
  scroll-snap-align: start;
  /* 화면의 73% → 다음 카드가 20% 보인다 */
  width: calc(100vw - 20px - 8px - (100vw * 0.2));
  max-width: 340px;                /* 480px 셸에서 과하게 커지지 않게 */
}
```

**끝에 여백을 반드시 준다.** 없으면 마지막 카드가 화면에 꽉 안 찬다.
```css
.h-scroll::after { content: ''; flex: 0 0 8px; }
```

### 1-4. 이미지는 비율 고정

```css
.card-img {
  width: 100%;
  aspect-ratio: 4 / 5;    /* 인물·시술·제품 기본 */
  object-fit: cover;
  border-radius: 16px;
  background: var(--surface-alt);   /* 로딩 중 플레이스홀더 */
}
```

> 원본 비율 그대로 두면 카드 높이가 제각각이라 피드가 무너진다. **비율 고정 + `object-fit: cover`**.

---

## 2. 여백 — 안정적으로 보이는 핵심

### 2-1. 좌우 패딩은 **20px 하나로 통일**

```css
:root { --pad: 20px; }

.section, .header, .list-row, .cta-bar, .footer {
  padding-inline: var(--pad);
}
```

**전 화면 동일해야 한다.** 헤더 16 / 본문 20 / 버튼 24 처럼 섞이면 스크롤할 때 왼쪽 정렬선이 흔들리고, 이게 "투박함"의 가장 큰 원인이다.

**검증:** 개발자도구에서 페이지 세로로 훑으며 왼쪽 시작점이 한 줄로 서는지 본다.

### 2-2. 세로 여백 — 4단계만 쓴다

```css
:root {
  --gap-xs: 8px;    /* 같은 덩어리 안 (라벨↔값) */
  --gap-sm: 16px;   /* 관련 요소 사이 (카드↔카드) */
  --gap-md: 24px;   /* 그룹 사이 */
  --gap-lg: 44px;   /* 섹션 사이 */
}
```

값을 5개 이상 쓰기 시작하면 리듬이 깨진다. **애매하면 큰 쪽**을 고른다 — 모바일은 여백이 부족해서 답답한 경우가 압도적으로 많다.

### 2-3. 섹션 구분은 **구분선이 아니라 여백**

```css
/* ❌ 웹 습관 */
.section { border-bottom: 1px solid var(--border); padding-bottom: 24px; }

/* ✅ 앱 방식 */
.section + .section { margin-top: 44px; }
```

구분선이 필요한 곳은 **리스트 행 사이**뿐이다. 섹션은 여백으로 나눈다.

큰 덩어리를 나눌 땐 선 대신 **두꺼운 배경 띠**:
```css
.section-break { height: 8px; background: var(--surface-alt); }
```

### 2-4. 하단 여백 — 잘림 방지

```css
.page {
  /* 하단 고정 요소 높이 + 홈 인디케이터 */
  padding-bottom: calc(64px + env(safe-area-inset-bottom) + 24px);
}
```

> `env(safe-area-inset-bottom)`을 빼먹으면 iPhone 홈 인디케이터에 콘텐츠가 겹친다. 앱답지 않게 보이는 대표적 실수.

---

## 3. 간격 — 요소 사이 띄우기

### 3-1. 터치 타깃 최소 44×44

```css
.icon-btn {
  min-width: 44px;
  min-height: 44px;
  display: grid;
  place-items: center;
}
```

아이콘 자체가 24px여도 **감싸는 영역이 44px**여야 한다. 시각적으로 커 보이는 게 싫으면 배경을 투명하게 두면 된다.

### 3-2. 리스트 행 높이

| 종류 | 높이 |
|------|------|
| 설정·메뉴 행 | **60px** |
| 아이콘 + 제목 + 설명 (2줄) | `padding-block: 16px` (고정 높이 금지) |
| 자산 행 (포인트·쿠폰) | 52px |

### 3-3. 아이콘과 텍스트 사이

```css
.row { display: flex; align-items: center; gap: 14px; }   /* 아이콘↔텍스트 */
.inline { display: inline-flex; align-items: center; gap: 6px; }  /* 텍스트↔뱃지 */
```

---

## 4. 폰트 사용

### 4-1. 웹폰트는 **본문 1종 + 헤드라인 1종**까지

```css
:root {
  --font-head: 'Paperlogy', 'Pretendard', -apple-system, sans-serif;
  --font-body: 'Pretendard', -apple-system, BlinkMacSystemFont, sans-serif;
}
```

3종 이상 쓰면 로딩이 느려지고 톤이 흐려진다.

### 4-2. 폰트 로딩 — 깜빡임 방지

```css
@font-face {
  font-family: 'Pretendard';
  src: url('/fonts/Pretendard-Regular.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;      /* 필수 — 없으면 로딩 중 텍스트가 안 보인다 */
}
```

```html
<!-- 본문 폰트만 preload. 여러 개 preload하면 오히려 느려진다 -->
<link rel="preload" href="/fonts/Pretendard-Regular.woff2" as="font"
      type="font/woff2" crossorigin>
```

### 4-3. 한글 자간·행간

```css
body {
  font-family: var(--font-body);
  letter-spacing: -0.02em;   /* 한글은 살짝 좁혀야 정돈돼 보인다 */
  word-break: keep-all;      /* ⚠️ 필수 — 단어 중간에서 줄바꿈되는 것 방지 */
  -webkit-font-smoothing: antialiased;
}
```

> `word-break: keep-all` 없으면 "안녕하세" / "요" 처럼 어절 중간이 끊긴다. 한국어 모바일 웹에서 가장 흔한 투박함.

---

## 5. 글자 크기

### 5-1. 모바일 타입 스케일 (이 값을 그대로 쓴다)

```css
@media (max-width: 768px) {
  :root {
    --t-hero:    32px;  /* 히어로 헤드라인 (2줄까지) */
    --t-title:   26px;  /* 화면 제목 */
    --t-section: 22px;  /* 섹션 제목 */
    --t-lead:    19px;  /* 강조 문장·리스트 행 */
    --t-body:    17px;  /* 본문 ← 기본값 */
    --t-sub:     16px;  /* 보조 설명 */
    --t-caption: 14px;  /* 캡션 (최소값) */
  }
}
```

**절대 규칙**
- **본문 17px.** 15px 이하는 즉시 "웹페이지"로 읽힌다
- **14px 미만 금지.** 어떤 요소든
- **`input`·`select`·`textarea`는 16px 이상** — 미만이면 iOS가 포커스 시 화면을 확대한다

```css
input, select, textarea { font-size: 16px; }   /* iOS 자동 줌 방지 */
```

### 5-2. 행간

```css
.body  { font-size: var(--t-body);  line-height: 1.6; }   /* 17 → 27px */
.title { font-size: var(--t-title); line-height: 1.35; }  /* 큰 글씨는 좁게 */
```

한글은 **본문 1.6 / 제목 1.3~1.4**. 1.4 이하 본문은 답답하고, 1.8 이상은 흩어진다.

### 5-3. 굵기는 3단계만

```
400 (본문) / 600 (강조·라벨) / 800 (제목)
```

500·700을 섞으면 위계가 흐려진다.

---

## 6. 색상

### 6-1. 토큰 6개로 끝낸다

```css
:root {
  --bg:           #FFFFFF;   /* 페이지 배경 */
  --surface:      #FFFFFF;   /* 카드 */
  --surface-alt:  #F5F6F8;   /* 구분 띠·빈 상태·칩 배경 */
  --border:       #E8EAED;
  --text:         #1A1A1A;   /* 본문 */
  --text-muted:   #8B95A1;   /* 보조 */
  --accent:       #FF5722;   /* 브랜드 — 프로젝트마다 교체 */
  --accent-soft:  #FFEDE6;   /* 브랜드 연한 틴트 */
}
```

**새 색을 발명하지 않는다.** 회색이 더 필요하면 `--text-muted`의 투명도를 조절한다.

### 6-2. 액센트는 **아껴 쓸수록 앱답다**

| 쓰는 곳 | 안 쓰는 곳 |
|---------|-----------|
| FAB·플로팅 버튼 | 하단 탭바 활성 상태 (→ 검정) |
| 가격·할인율 | 주요 CTA 버튼 (→ 검정) |
| 뱃지·알림 점 | 링크 텍스트 (→ 검정 + 밑줄) |
| 선택된 칩의 틴트 배경 | 제목 |

> **주요 CTA는 검정(`--text`)**이 정답이다. 액센트 컬러 버튼은 브랜드가 바뀌면 대비가 깨지고, 화면에 액센트가 3개 이상 생기면 어디를 눌러야 할지 알 수 없어진다.

### 6-3. 다크모드

```css
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #121212;  --surface: #1C1C1E;  --surface-alt: #2C2C2E;
    --border: #38383A;  --text: #F5F5F7;  --text-muted: #8E8E93;
  }
}
:root[data-theme="dark"] { /* 위와 동일 — 토글이 이기게 */ }
```

`--surface-alt`가 다크에서 **배경과 구분되는지** 반드시 확인한다. 구분 띠가 안 보이면 섹션이 뭉개진다.

---

## 7. 하단 내비게이터 ⭐ 앱다움의 최대 신호

**모바일 웹에 하단 탭바가 있으면 그 순간 앱처럼 느껴진다.** 반대로 없으면 아무리 잘 만들어도 웹페이지다.

### 7-1. 구조

```html
<nav class="tabbar">
  <a class="tab is-active" href="/">
    <svg class="tab-ico">…</svg><span>홈</span>
  </a>
  <a class="tab" href="/search">…<span>검색</span></a>
  <a class="tab" href="/saved">…<span>저장</span></a>
  <a class="tab" href="/my">…<span>마이</span></a>
</nav>
```

```css
.tabbar {
  position: fixed;
  bottom: 0; left: 50%; transform: translateX(-50%);
  width: 100%; max-width: 480px;
  display: flex;
  background: var(--bg);
  border-top: 1px solid var(--border);
  padding-top: 10px;
  padding-bottom: calc(10px + env(safe-area-inset-bottom));  /* 홈 인디케이터 */
  z-index: 100;
}
.tab {
  flex: 1;                       /* ⚠️ 균등 분할 — 텍스트 길이 무관 */
  display: flex; flex-direction: column; align-items: center; gap: 5px;
  color: var(--text-muted);
  font-size: 13px; font-weight: 500;
  text-decoration: none;
}
.tab-ico { width: 26px; height: 26px; }
.tab.is-active { color: var(--text); font-weight: 700; }
.tab.is-active .tab-ico { fill: currentColor; }   /* 활성=채움 */
```

### 7-2. 정렬 규칙

- **`flex: 1` 균등 분할.** `justify-content: space-around`는 라벨 길이에 따라 간격이 달라져 삐뚤어 보인다
- **탭 개수 4~5개.** 3개는 허전하고, 6개는 라벨이 잘린다
- **라벨 13px.** 5개 탭에서 "마이페이지"가 안 잘리는 최대 크기
- **활성 표현은 `fill` + 굵기.** 액센트 컬러 금지 — 탭바가 시끄러워진다
- 뱃지는 **점(8px)만**. 숫자 뱃지는 "몇 개"가 중요할 때만

```css
.tab-badge {
  position: absolute; top: -2px; right: -3px;
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--accent);
}
```

### 7-3. 탭바가 부적합할 때 — 고정 CTA 바

정보성 랜딩·상세 페이지처럼 탭이 필요 없으면, 대신 **하단 고정 CTA**를 둔다. 하단이 비어 있으면 안 된다.

```css
.cta-bar {
  position: fixed; bottom: 0; left: 50%; transform: translateX(-50%);
  width: 100%; max-width: 480px;
  padding: 12px 20px calc(12px + env(safe-area-inset-bottom));
  background: var(--bg);
  border-top: 1px solid var(--border);
}
.cta {
  width: 100%; height: 56px; border-radius: 12px;
  background: var(--text); color: var(--bg);
  font-size: 18px; font-weight: 700;
  border: 0;
}
```

> **검정 채움 CTA는 화면당 1개.** 보조 액션은 아웃라인(`border: 1px solid var(--border); background: transparent`)으로.

---

## 8. 모바일식 모달 = 바텀시트

**화면 중앙에 뜨는 모달은 웹의 습관이다.** 앱은 아래에서 올라온다.

### 8-1. CSS만으로 구현

```css
.sheet-dim {
  position: fixed; inset: 0;
  background: rgba(0,0,0,0.45);
  opacity: 0; pointer-events: none;
  transition: opacity .25s ease;
  z-index: 200;
}
.sheet-dim.is-open { opacity: 1; pointer-events: auto; }

.sheet {
  position: fixed; bottom: 0; left: 50%;
  width: 100%; max-width: 480px;
  transform: translateX(-50%) translateY(100%);   /* 아래 숨김 */
  background: var(--bg);
  border-radius: 20px 20px 0 0;                    /* 상단만 라운드 */
  padding-bottom: env(safe-area-inset-bottom);
  max-height: 85dvh;                               /* 전체를 덮지 않는다 */
  overflow-y: auto;
  transition: transform .3s cubic-bezier(.32,.72,0,1);   /* iOS 시트 곡선 */
  z-index: 201;
}
.sheet.is-open { transform: translateX(-50%) translateY(0); }

/* 핸들바 — "아래로 끌어 닫기"를 알리는 유일한 신호 */
.sheet-handle {
  width: 48px; height: 5px; border-radius: 3px;
  background: var(--border);
  margin: 12px auto 0;
}
.sheet-head {
  display: flex; align-items: center;
  padding: 0 20px; height: 68px;
}
.sheet-title { flex: 1; font-size: 24px; font-weight: 800; }
```

### 8-2. 필수 규칙

- **상단만 라운드 20px.** 4면 라운드는 중앙 모달의 습관
- **`max-height: 85dvh`** — 전체를 덮으면 "새 페이지"지 시트가 아니다
- **핸들바 필수** (48×5)
- **열릴 때 배경 스크롤 잠금**
  ```js
  document.body.style.overflow = 'hidden';   // 열 때
  document.body.style.overflow = '';         // 닫을 때
  ```
- **딤 클릭 = 닫기** + `Esc` 키도 지원
- 애니메이션 곡선 `cubic-bezier(.32,.72,0,1)` — iOS 시트와 같은 감속

### 8-3. 시트 안의 확인 버튼

시트 하단에 CTA를 고정한다. 스크롤 끝까지 내려야 버튼이 나오면 안 된다.

```css
.sheet-cta {
  position: sticky; bottom: 0;
  padding: 12px 20px;
  background: var(--bg);
}
```

### 8-4. 언제 시트가 아니라 전체 화면인가

| 상황 | 형태 |
|------|------|
| 선택·필터·간단 입력 | 바텀시트 |
| 항목 20개 이상 목록 | 바텀시트 + 상단 검색 |
| 다단계 폼·이미지 편집 | **전체 화면**(라우트 이동) |
| 삭제 확인 등 단순 확인 | 바텀시트 (중앙 alert 금지) |

---

## 9. 햄버거 버튼

### 9-1. 먼저 — **하단 탭바가 있으면 햄버거는 없애는 게 낫다**

메뉴 진입점이 둘이면 사용자는 어디에 뭐가 있는지 학습하지 못한다.

| 상황 | 권장 |
|------|------|
| 하단 탭바 있음 | 햄버거 **제거**. 나머지는 "마이" 탭 안으로 |
| 탭바 없는 정보성 사이트 | 햄버거 유지 (아래 규격) |
| 메뉴 항목 4개 이하 | 햄버거 대신 상단에 그냥 노출 |

### 9-2. 유지할 때의 규격

```css
.hamburger {
  width: 44px; height: 44px;          /* 터치 타깃 */
  display: grid; place-items: center;
  background: none; border: 0;
}
.hamburger span {
  display: block;
  width: 22px; height: 2px;           /* 2px — 3px는 둔해 보인다 */
  background: var(--text);
  border-radius: 2px;
  transition: transform .25s, opacity .2s;
}
.hamburger span + span { margin-top: 6px; }   /* 줄 간격 6px */

/* 열림 → X 로 변형 */
.hamburger.is-open span:nth-child(1) { transform: translateY(8px) rotate(45deg); }
.hamburger.is-open span:nth-child(2) { opacity: 0; }
.hamburger.is-open span:nth-child(3) { transform: translateY(-8px) rotate(-45deg); }
```

### 9-3. 메뉴는 **오른쪽에서 슬라이드** (드로어)

위에서 툭 떨어지는 드롭다운은 웹의 습관이다.

```css
.drawer {
  position: fixed; top: 0; right: 0;
  width: 82%; max-width: 340px; height: 100dvh;
  background: var(--bg);
  transform: translateX(100%);
  transition: transform .3s cubic-bezier(.32,.72,0,1);
  padding-top: env(safe-area-inset-top);
  z-index: 201;
}
.drawer.is-open { transform: translateX(0); }

.drawer-item {
  display: flex; align-items: center;
  height: 60px; padding-inline: 20px;
  font-size: 19px; color: var(--text);
  text-decoration: none;
}
```

- 폭 **82%** — 100%면 "새 페이지", 60%면 답답하다. 뒤가 살짝 보여야 "덮개"로 읽힌다
- 딤 처리 + 딤 클릭 시 닫기
- 드로어 열릴 때 `body` 스크롤 잠금

---

## 10. 푸터 표시

### 10-1. 모바일 푸터의 원칙

데스크톱 푸터(4~5열 링크 그리드)를 그대로 줄이면 **가장 투박해 보이는 구간**이 된다.

| 데스크톱 | 모바일 |
|----------|--------|
| 4~5열 링크 그리드 | **접힌 아코디언** 또는 핵심 링크만 |
| 로고 + 소개문 | 로고만 (소개문 삭제) |
| SNS 아이콘 나열 | 유지 (44px 터치 타깃) |
| 사업자정보 전체 노출 | **아코디언으로 접기** |

### 10-2. 구조

```html
<footer class="footer">
  <img class="footer-logo" src="/logo.svg" alt="브랜드">

  <nav class="footer-links">
    <a href="/terms">이용약관</a>
    <span aria-hidden="true">·</span>
    <a href="/privacy"><strong>개인정보처리방침</strong></a>
    <span aria-hidden="true">·</span>
    <a href="/contact">문의하기</a>
  </nav>

  <details class="footer-biz">
    <summary>사업자정보</summary>
    <div class="footer-biz-body">
      <p>주식회사 …</p>
      <p>대표: … | 사업자등록번호: …</p>
      <p>주소: …</p>
    </div>
  </details>

  <p class="footer-copy">© 2026 Brand. All rights reserved.</p>
</footer>
```

```css
.footer {
  background: var(--surface-alt);
  padding: 40px 20px calc(40px + env(safe-area-inset-bottom));
  /* 하단 탭바가 있으면 그만큼 더 */
  margin-bottom: 0;
}
.footer-logo { height: 24px; opacity: .5; }

.footer-links {
  display: flex; flex-wrap: wrap; align-items: center;
  gap: 10px; margin-top: 24px;
}
.footer-links a {
  font-size: 16px; color: var(--text-muted); text-decoration: none;
  padding-block: 6px;              /* 터치 여유 */
}
/* 개인정보처리방침은 법적으로 강조 표시 */
.footer-links strong { color: var(--text); font-weight: 700; }

.footer-biz { margin-top: 24px; }
.footer-biz summary {
  font-size: 16px; color: var(--text-muted);
  cursor: pointer; padding-block: 10px;
  list-style: none;
}
.footer-biz summary::after { content: ' ⌄'; }
.footer-biz[open] summary::after { content: ' ⌃'; }
.footer-biz-body p {
  font-size: 14px; color: var(--text-muted);
  line-height: 1.7; margin: 4px 0;
}

.footer-copy {
  font-size: 14px; color: var(--text-muted);
  margin-top: 24px;
}
```

### 10-3. 필수 체크

- [ ] **개인정보처리방침 링크가 굵게** 표시되는가 (법적 요건)
- [ ] 하단 탭바가 있으면 **푸터가 탭바에 가리지 않는가** (`padding-bottom` 확보)
- [ ] 사업자정보가 접혀 있는가 (펼쳐두면 페이지 끝이 지저분해진다)
- [ ] 링크 터치 영역이 44px 확보되는가

---

## 11. 앱다움을 완성하는 마무리 5가지

### 11-1. 탭 하이라이트·확대 제거

```css
* { -webkit-tap-highlight-color: transparent; }
body { touch-action: manipulation; }   /* 더블탭 확대 방지 */
```

> 링크를 누를 때 파란 사각형이 번쩍이면 그 순간 "웹"임이 드러난다.

### 11-2. 텍스트 선택 막기 (UI 요소만)

```css
.tabbar, .header, .btn, .chip { user-select: none; }
```

본문·가격은 **선택 가능하게 둔다**(복사 needs).

### 11-3. 스크롤 관성 + 오버스크롤 차단

```css
body { overscroll-behavior-y: none; }   /* 당겨서 새로고침·바운스 억제 */
.scroll-area { -webkit-overflow-scrolling: touch; }
```

### 11-4. 눌림 피드백

```css
.btn, .card, .list-row { transition: transform .12s ease, opacity .12s ease; }
.btn:active, .card:active, .list-row:active { transform: scale(.97); opacity: .9; }
```

> `:hover`는 모바일에서 동작하지 않는다. **`:active`로 즉각 반응**을 준다. 이게 있으면 "눌린다"는 감각이 생긴다.

### 11-5. PWA 메타 (홈 화면 추가 시 앱처럼)

```html
<meta name="viewport"
      content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#FFFFFF">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<link rel="apple-touch-icon" href="/icon-180.png">
<link rel="manifest" href="/manifest.json">
```

> **`viewport-fit=cover` 필수** — 이게 없으면 `env(safe-area-inset-*)`가 전부 0이 되어 노치·홈인디케이터 대응이 무효가 된다.

---

## 12. 수치 요약 (복붙용)

| 항목 | 값 |
|------|-----|
| 좌우 패딩 | **20px** (전 화면 통일) |
| 셸 최대 폭 | 480px |
| 화면 높이 | `100dvh` (vh 아님) |
| 여백 4단계 | 8 / 16 / 24 / 44 |
| 섹션 구분 띠 | height 8px, surface-alt |
| 본문 | **17px / line-height 1.6** |
| 화면 제목 | 26px / 800 / lh 1.35 |
| 섹션 제목 | 22px / 800 |
| 리스트 행 텍스트 | 19px |
| 캡션 (최소) | 14px |
| input | **16px 이상** (iOS 줌 방지) |
| 주요 CTA | height **56px** / radius 12 / 검정 |
| 리스트 행 높이 | 60px |
| 터치 타깃 | 44×44 최소 |
| 카드 라운드 | 16px |
| 가로 스크롤 카드 폭 | `calc(100vw - 28px - 20vw)` |
| 이미지 비율 | `aspect-ratio: 4/5` + `object-fit: cover` |
| 탭바 아이콘 / 라벨 | 26px / 13px |
| 탭 개수 | 4~5개, `flex: 1` |
| 바텀시트 | 상단만 radius 20 / `max-height: 85dvh` |
| 시트 핸들바 | 48×5 / radius 3 |
| 햄버거 라인 | 22×2, 간격 6 |
| 드로어 폭 | 82% / max 340px |
| 애니메이션 곡선 | `cubic-bezier(.32,.72,0,1)` |
| 눌림 피드백 | `:active { transform: scale(.97) }` |

---

## 13. 체크리스트 — 모바일 뷰 완료 판정

**레이아웃·여백**
- [ ] 좌우 패딩이 전부 20px인가 (세로로 훑어 왼쪽 선이 한 줄로 서는가)
- [ ] `100vh` 대신 `100dvh`를 썼는가
- [ ] 하단 여백에 `env(safe-area-inset-bottom)`이 들어갔는가
- [ ] 섹션 구분을 구분선이 아니라 여백(44px)으로 했는가
- [ ] 375px에서 가로 스크롤이 안 생기는가

**글자**
- [ ] 본문이 17px인가
- [ ] 14px 미만이 하나도 없는가
- [ ] `input`이 16px 이상인가
- [ ] `word-break: keep-all`을 적용했는가
- [ ] 굵기가 400/600/800 3단계인가

**색상**
- [ ] 액센트 컬러가 화면에 3개 이하인가
- [ ] 주요 CTA가 검정인가 (액센트 아님)
- [ ] 다크모드에서 `surface-alt`가 배경과 구분되는가

**앱다움 핵심**
- [ ] **하단에 탭바 또는 고정 CTA가 있는가**
- [ ] 탭이 `flex: 1` 균등 분할인가
- [ ] **모달이 바텀시트인가** (중앙 모달 아님)
- [ ] 시트에 핸들바가 있고 `max-height: 85dvh`인가
- [ ] 가로 스크롤 카드가 다음 장을 20% 보여주는가
- [ ] `scroll-snap-type`이 걸려 있는가
- [ ] `:active` 눌림 피드백이 있는가
- [ ] `-webkit-tap-highlight-color: transparent`를 넣었는가
- [ ] `viewport-fit=cover`가 있는가

**푸터·메뉴**
- [ ] 푸터 사업자정보가 접혀 있는가
- [ ] 개인정보처리방침이 굵게 표시되는가
- [ ] 하단 탭바가 있는데 햄버거를 중복으로 두지 않았는가
- [ ] 드로어가 오른쪽에서 슬라이드되는가 (드롭다운 아님)
