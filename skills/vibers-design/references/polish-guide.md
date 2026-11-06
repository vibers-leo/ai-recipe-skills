---
name: polish-guide
description: 사이트 기본 유려함 규격. 카테고리·브랜드 무관하게 모든 웹 프로젝트에 적용하는 최소 품질선 — 유체 타이포·섹션 리듬·스크롤 진입·그레이 스케일·이미지 최적화·함정 7종. corp-enterprise-patterns 에서 범용 요소만 추출.
source: corp-enterprise-patterns.md(HD 역분석) 범용 추출 + mireng 32페이지 실측
updated: 2026-08-14
---

# Polish Guide — 사이트 기본 유려함

> **"대기업 사이트는 왜 유려해 보이나"를 브랜드에서 떼어낸 것.**
> 화려한 모션이 아니라 **타이포 스케일 · 여백 리듬 · 진입 모션 · 이미지 위생** 네 가지다.
> 카테고리(랜딩·쇼핑몰·블로그·어드민) 무관하게 **전부 적용**한다.
>
> 여기 있는 건 전부 **브랜드 색과 무관**하다. 테마는 `theme-guide.md`, 모바일은 `app-feel-guide.md`.

---

## 0. 이 4가지가 "싸구려 티"를 만든다

작업 전 진단부터. 하나라도 해당하면 그게 원인이다.

| 증상 | 원인 | 고치는 곳 |
|------|------|----------|
| 데스크톱에서 글씨가 작고 답답 | 폰트가 px 고정 → 큰 화면에서 안 커짐 | §1 유체 타이포 |
| 섹션이 다닥다닥 붙어 정신없음 | 섹션 간격 40~60px | §2 섹션 리듬 (**160px**) |
| 스크롤해도 아무 일 없어 밋밋 | 진입 모션 없음 | §3 스크롤 진입 |
| 회색이 제각각(#888 #999 #aaa 혼재) | 그레이 스케일 미정의 | §4 그레이 9단 |

---

## 1. 유체 타이포그래피 — 가장 효과가 큰 한 방

**px 고정을 버리고 `clamp()`로 간다.** 1920px 모니터에서 본문이 16px이면 그 순간 아마추어다.

```css
:root {
  --t-display: clamp(2.5rem,  5vw,   4rem);      /* 40 → 64  히어로 */
  --t-hero:    clamp(2rem,    3.5vw, 3.5rem);    /* 32 → 56 */
  --t-title1:  clamp(1.75rem, 2.5vw, 2.75rem);   /* 28 → 44  섹션 제목 */
  --t-title2:  clamp(1.5rem,  2vw,   2.25rem);   /* 24 → 36 */
  --t-title3:  clamp(1.25rem, 1.7vw, 2rem);      /* 20 → 32 */
  --t-head:    clamp(1.125rem,1.5vw, 1.75rem);   /* 18 → 28 */
  --t-body1:   clamp(1rem,    1.2vw, 1.5rem);    /* 16 → 24  리드문 */
  --t-body2:   clamp(0.9375rem,1.1vw,1.25rem);   /* 15 → 20  본문 */
  --t-desc:    clamp(0.875rem, 0.9vw, 1rem);     /* 14 → 16  캡션(하한) */
}
```

**규칙**
- `clamp(최소, 뷰포트비율, 최대)` — 최소값이 **모바일**, 최대값이 **와이드 데스크톱**
- **최소값 14px 미만 금지.** `--t-desc`가 하한선
- 행간: 큰 글씨일수록 좁게 — display/title `1.2~1.35`, 본문 `1.6~1.7`
- 한글은 `letter-spacing: -0.02em` + **`word-break: keep-all`** (없으면 어절 중간에서 끊긴다)

---

## 2. 섹션 리듬 — 여백이 곧 급이다

**아마추어 사이트의 공통점: 섹션 간격이 좁다.** 대기업 사이트가 여유로워 보이는 건 폰트가 아니라 **여백**이다.

```css
.inner { max-width: 1220px; margin: 0 auto; padding: 0 40px; }

/* 섹션 간격 — 이 수치가 핵심 */
.sec + .sec   { margin-top: 160px; }   /* 같은 주제 안의 블록 */
.area + .area { margin-top: 240px; }   /* 큰 주제 전환 */

@media (max-width: 1024px) {
  .inner { padding: 0 24px; }
  .sec + .sec, .area + .area { margin-top: 120px; }
}
@media (max-width: 600px) {
  .inner { padding: 0 20px; }          /* 모바일은 20 — app-feel-guide 와 통일 */
  .sec + .sec, .area + .area { margin-top: 96px; }
}
```

**규칙**
- 컨테이너 **1220px**가 기본. 푸터·풀블리드만 예외
- 섹션 구분은 **여백으로.** 구분선(`border-top`)을 섹션마다 넣지 않는다
- 큰 덩어리를 나눌 땐 선 대신 **배경색 전환**(흰 → `--gray-50`)
- 제목과 본문 사이 `24~32px`, 본문과 다음 요소 사이 `48px`

---

## 3. 스크롤 진입 모션 — GSAP 없이

라이브러리 없이 **CSS + IntersectionObserver**로 끝난다. 무게 0.

```css
.reveal {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity .8s ease, transform .8s ease;
}
.reveal.is-in { opacity: 1; transform: none; }

/* 자식 순차 등장 — 이게 '유려함'의 정체다 */
.reveal-stagger > *:nth-child(2) { transition-delay: .12s; }
.reveal-stagger > *:nth-child(3) { transition-delay: .24s; }
.reveal-stagger > *:nth-child(4) { transition-delay: .36s; }
.reveal-stagger > *:nth-child(5) { transition-delay: .48s; }

/* 그리드는 컬럼 단위로 */
.reveal-3col .reveal:nth-child(3n-1) { transition-delay: .12s; }
.reveal-3col .reveal:nth-child(3n)   { transition-delay: .24s; }

/* 모바일은 딜레이 제거 — 세로로 길어 기다림이 지루해진다 */
@media (max-width: 600px) {
  .reveal-3col .reveal, .reveal-stagger > * { transition-delay: 0s !important; }
}
/* 접근성 — 반드시 넣는다 */
@media (prefers-reduced-motion: reduce) {
  .reveal { opacity: 1; transform: none; transition: none; }
}
```

```ts
// hooks/useReveal.ts
import { useEffect } from 'react'

export function useReveal(selector = '.reveal') {
  useEffect(() => {
    const els = document.querySelectorAll(selector)
    const io = new IntersectionObserver(
      entries => entries.forEach(e => {
        if (!e.isIntersecting) return
        e.target.classList.add('is-in')
        io.unobserve(e.target)          // 한 번만 — 되돌아오면 재생 안 함
      }),
      { threshold: 0.15 }
    )
    els.forEach(el => io.observe(el))
    return () => io.disconnect()
  }, [selector])
}
```

**규칙**
- `threshold: 0.15` — 요소가 15% 보이면 시작. 너무 높으면 늦게 뜬다
- **`unobserve` 필수** — 스크롤 올릴 때마다 재생되면 싸구려로 보인다
- 딜레이 **0.12s 간격**. 0.3s 넘어가면 느려터져 보인다
- `prefers-reduced-motion` 없으면 접근성 위반

---

## 4. 그레이 스케일 9단

`#888` `#999` `#aaa`를 그때그때 쓰면 화면이 지저분해진다. **9단으로 고정.**

```css
:root {
  --gray-900: #1A1A1A;  /* 제목 */
  --gray-800: #4D4D4D;  /* 본문 */
  --gray-700: #666666;  /* 보조 텍스트 */
  --gray-500: #999999;  /* 비활성·플레이스홀더 */
  --gray-400: #CCCCCC;  /* 아이콘 비활성 */
  --gray-300: #D9D9D9;  /* 보더 (진한) */
  --gray-200: #E5E5E5;  /* 보더 (기본) */
  --gray-100: #F0F0F0;  /* 구분 띠 */
  --gray-50:  #F5F5F5;  /* 섹션 배경 */
}
```

브랜드 색은 `--brand-primary` / `--brand-secondary` 두 개면 충분하다.
**이 둘만 바꿔서 전체 톤이 전환되게** 설계한다.

---

## 5. 반응형 3구간

| 구간 | px | 처리 |
|------|-----|------|
| 데스크톱 | ≥1025 | 3열, 모션 풀 적용 |
| 태블릿 | 601~1024 | 2열, 헤더 축소 |
| 모바일 | ≤600 | 1열, 딜레이 0, 패딩 20 |

> Tailwind `sm:640` 은 쓰지 않는다. **`lg:1024` 가 태블릿/데스크톱 경계**다.

---

## 6. 이미지 위생

| 규칙 | 이유 |
|------|------|
| `next/image` 필수 | 원시 `<img>` 는 홈 하나에서 **5.6MB → 1.3MB (-76%)** 차이가 났다 |
| 히어로 첫 장만 `priority` | 나머지는 `loading="lazy"` |
| `fill` 쓰면 부모에 `position: relative` | 없으면 이미지가 사라진다 |
| 고정 크기는 `fill` 대신 `width`/`height` | 썸네일·아이콘류 |
| `aspect-ratio` + `object-fit: cover` | 카드 높이가 들쭉날쭉해지는 것 방지 |

---

## 7. 실전 함정 7종 — 실사이트 32페이지에서 실제로 터진 것

### 7-1. `<a>` 중첩 → 전 페이지 하이드레이션 실패 (가장 치명적)

로고 컴포넌트가 이미 `<Link href="/">` 인데 헤더가 또 `<Link>`로 감싸면 **잘못된 HTML**이 되어
React가 서버 HTML을 통째로 버린다. **페이지 전체가 다시 그려진다.**

> **프로덕션에서는 `Minified React error #418` 로만 뜬다 — 원인을 알 수 없다.**
> `npm run dev` 로 띄워야 `In HTML, <a> cannot be a descendant of <a>` 가 보인다.
> 하이드레이션 에러를 만나면 **가장 먼저 링크 중첩부터 의심할 것.**

### 7-2. `justify-content: center` + `overflow-x: auto` → 첫 항목 접근 불가

탭·칩이 화면보다 넓을 때 `center` 를 주면 **왼쪽으로 넘친 첫 항목에 영영 못 간다.**

```css
/* ❌ */ .tabs { display:flex; justify-content:center; overflow-x:auto; }
/* ✅ */ .tabs { display:flex; justify-content:flex-start; overflow-x:auto; }
/*    항목이 적을 때만 가운데: */
@media (min-width:1025px){ .tabs:not(.is-overflow){ justify-content:center; } }
```

### 7-3. grid 자식 `min-width: auto` → 모바일 가로 넘침

2컬럼 grid는 모바일에서 1컬럼이 되지만, **자식이 내용물 크기만큼 늘어난다.** 실측 +301px.

```tsx
<div className="grid gap-10 [&>*]:min-w-0 lg:grid-cols-2">
```

### 7-4. 원시 `<img>` → 모바일 이미지만 5.6MB
§6 참조.

### 7-5. 가로 스크롤 측정은 `scrollWidth` 로 하지 마라

`body { overflow-x: hidden }` 이면 `scrollWidth` 가 커도 **사용자에겐 스크롤이 없다.** 오탐이 난다.

```js
// 실제 스크롤 가능 여부로 판정
const before = scrollX; scrollTo(500, 0)
const 진짜넘침 = scrollX > before; scrollTo(0, 0)
```

### 7-6. 최소 폰트 14px

eyebrow(13px)·breadcrumb(12px)·`<small>`(기본 0.8em = 11.2px)이 자주 미달한다.
**예외:** 아이콘 글리프(▲▼✕), OG 캔버스(1200×630) — 텍스트가 아니다.

### 7-7. 콘텐츠 진위 — 데이터가 뒷받침하지 않는 표기

디자인과 무관하지만 **납품 전 반드시 확인.** 실제로 나왔던 것들:
- 타사 창고 사진을 자사 생산시설로 표기
- 회의 스톡 사진에 제품명 `alt` 를 붙임
- `verified:false` 인 인증(ISO·방산 등)을 8곳에서 노출

> **"코드가 주장하는 것" vs "데이터가 뒷받침하는 것"** 을 대조한다.

---

## 8. 체크리스트

**유려함 4종**
- [ ] 폰트가 `clamp()` 유체 스케일인가 (px 고정 아님)
- [ ] 섹션 간격이 **160px**(모바일 96px) 이상인가
- [ ] 스크롤 진입 모션 + 순차 딜레이(0.12s)가 있는가
- [ ] 그레이가 9단 토큰으로 통일됐는가

**위생**
- [ ] `prefers-reduced-motion` 처리했는가
- [ ] IntersectionObserver 에 `unobserve` 넣었는가
- [ ] 모든 이미지가 `next/image` 인가
- [ ] `word-break: keep-all` 넣었는가
- [ ] 14px 미만 폰트가 없는가

**함정**
- [ ] 링크 중첩(`<a>` in `<a>`)이 없는가 — **dev 서버에서 확인**
- [ ] 가로 스크롤 컨테이너에 `justify-content: center` 를 쓰지 않았는가
- [ ] grid 자식에 `min-w-0` 을 줬는가
- [ ] 375px에서 실제 가로 스크롤이 없는가 (`scrollWidth` 말고 실측)
- [ ] 사진·인증·수치가 데이터로 뒷받침되는가
