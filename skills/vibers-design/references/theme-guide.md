---
name: vibers-design-engine
description: Vibers(계발자들) 생태계 전용 디자인 엔진. Supanova Design Engine을 포크해 한국 서비스 특성에 맞게 재설계. 9개 테마(MODERN_BW, DARK_ORANGE, LIGHT_GREEN, WARM_CREAM, BOLD_DARK, SOFT_LIGHT, MEDIA_GRAY, CORP_BLUE, BEAUTY_PINK) + BTL_AGENCY(다크오렌지)/BTL_MARKETING(다크그린) 서브테마, Paperlogy+Pretendard 탑재, 라이트/다크 혼합, HTML·TSX 모두 지원. 실전 스켈레톤: github.com/vibers-leo/btl-skeleton
based-on: Supanova Design Engine
---

# Vibers Design Engine — Theme Guide

## 1. 테마 선택 (ACTIVE THEME)

### 선택형 헤더 테마

- `HEADER_THEME: ROUNDED_HEADER` — “둥근 헤더 / 팬이지 기존 헤더 / 캡슐 헤더” 요청 시 [rounded-header.md](rounded-header.md)를 읽는다. 전체 색상 테마와 독립적으로 조합하며 다른 프로젝트에 자동 적용하지 않는다.

작업 시작 전 반드시 테마를 지정한다. **사용자가 테마를 명시하지 않으면 `MODERN_BW`가 기본값**이다.

```
ACTIVE_THEME: MODERN_BW   ← 기본값
OUTPUT_FORMAT: html | tsx   (기본: html)
LANDING_PURPOSE: conversion | brand | portfolio | saas
```

**AI Instruction:** 사용자가 테마를 언급하면 즉시 전환. 예) "와요 스타일로" → WARM_CREAM, "러너스커넥트 스타일로" → BOLD_DARK, "다크하게" → DARK_ORANGE. 테마 외 모든 수파노바 기본 규칙(레이아웃 다양성, 안티-슬롭, 완전 출력)은 그대로 유지.

**테마 빠른 매핑:**
- "기본 / 범용" → MODERN_BW
- "행사 / 에너지 / 축제" → DARK_ORANGE
- "비더라인 스타일 / 행사 에이전시 다크" → DARK_ORANGE (BTL_AGENCY 서브테마)
- "전문직 / 세무 / B2B" → LIGHT_GREEN
- "웨딩 / 감성 / 초대장" → WARM_CREAM
- "스포츠 / 러닝 / 도전" → BOLD_DARK
- "SaaS / AI / 테크 / 구독" → SOFT_LIGHT
- "뉴스 / 미디어 / 콘텐츠 / 정보" → MEDIA_GRAY
- "공기업 / 제조업 / KOSDAQ / KOSPI / 기업 브랜드 / B2B 산업재" → CORP_BLUE
- "뷰티 / 미용 / 네일 / 헤어 / 스파 / 예약앱 / 여성 타깃 커머스" → BEAUTY_PINK

---

## 2. 테마 정의

### ⬛ MODERN_BW (기본값)
> 범용 고급 미니멀. 에이전시, 포트폴리오, 브랜드 소개.

```
배경: #ffffff
표면: #f5f5f5
테두리: #e5e5e5
텍스트 주: #0a0a0a
텍스트 부: #525252 (neutral-600)
텍스트 약: #a3a3a3 (neutral-400)
액센트: #0a0a0a (강조/아이콘/링크 전용, 버튼과 동일 OK)
액센트 연: #f5f5f5
버튼 주: #0a0a0a (Primary CTA 배경)
버튼 hover: #262626 (neutral-800)
버튼 텍스트: #ffffff
반전 배경: #0a0a0a (다크 섹션)
반전 텍스트: #ffffff
```

**폰트:**
- 헤드라인: `Paperlogy` (CDN: `https://cdn.jsdelivr.net/gh/Freesentation/paperlogy@main/Paperlogy.css`)
- 본문: `Pretendard` (CDN: `https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.min.css`)
- 영문 보조: `Geist` (Google Fonts: `family=Geist:wght@400;500;600;700`)
- 스택: `'Paperlogy', 'Pretendard', 'Geist', -apple-system, sans-serif`

**특성:**
- 라이트 배경, 그레인 텍스처 없음
- 타이포그래피 중심 — 색상보다 크기·굵기·간격으로 위계 표현
- 카드 그림자: `0 1px 4px rgba(0,0,0,0.08)`, 테두리 `#e5e5e5`
- 히어로 반드시 비대칭 2단 (텍스트 좌 / 비주얼 우)
- 인버트 섹션 1개 허용 (다크 배경 #0a0a0a, 흰 텍스트) — CTA 또는 신뢰지표에 사용
- 애니메이션: 부드럽고 절제됨 (transition 0.4s ease)

---

### 🟠 DARK_ORANGE
> 에너제틱한 행사·에이전시. 마당, 축제, B2B 서비스.

```
배경: #09090b (zinc-950)
표면: rgba(255,255,255,0.03)
테두리: rgba(255,255,255,0.08)
텍스트 주: #ffffff
텍스트 부: #a1a1aa (zinc-400)
텍스트 약: #52525b (zinc-600)
액센트: #f97316 (orange-500, 강조/아이콘/링크)
액센트 글로우: rgba(249,115,22,0.2)
버튼 주: #f97316 (다크 테마 — 액센트 OK)
버튼 hover: #ea580c (orange-600)
버튼 테두리: 1px solid rgba(255,255,255,0.1) (inset 분리감)
버튼 텍스트: #0a0a0a
```

**폰트:**
- 헤드라인: `Paperlogy` (CDN: `https://cdn.jsdelivr.net/gh/Freesentation/paperlogy@main/Paperlogy.css`)
- 본문: `Pretendard` (CDN: `https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.min.css`)
- 스택: `'Paperlogy', 'Pretendard', -apple-system, sans-serif`

**특성:**
- 글래스모피즘 카드 (backdrop-blur + inset shadow)
- 그레인 텍스처 오버레이 (noise SVG fixed)
- 오렌지 글로우 효과 (box-shadow orange glow)
- 히어로 반드시 비대칭 2단 (텍스트 좌 / 비주얼 우)

#### 🔥 DARK_ORANGE 실전 서브테마: BTL_AGENCY (2026-08-03 검증)
> BeTheLine (betheline.co.kr) 행사 에이전시 홈페이지에서 실전 검증된 변형. 글래스모피즘 없이 솔리드 다크, 오렌지 포인트.

**컬러 오버라이드 (기본 DARK_ORANGE와 차이):**
```
배경: #0A0A0A (zinc-950보다 살짝 더 검정)
표면: #111111 (섹션 교차 배경)
교차 배경: #0D0D0D (비교 테이블 등)
액센트: #E05A1A (orange보다 어둡고 깊은 오렌지 — 기본 #f97316 대신)
텍스트 부: rgba(255,255,255,0.4)
텍스트 약: rgba(255,255,255,0.2)
테두리: rgba(255,255,255,0.05)
버튼 주: #E05A1A
버튼 hover: #c04d16
버튼 텍스트: #ffffff (기본과 반대 — 어두운 오렌지이므로 흰 텍스트)
```

**레이아웃 패턴 (섹션 순서):**
```
SiteHeader (fixed, blur)
  ↓
SiteHero (fullscreen video, AnimatePresence 슬라이딩 텍스트 8개, 4s 간격)
  ↓
SiteStats (4열 카운터 그리드, gap-px, 오렌지 suffix)
  ↓
SiteWhy (문제/해결 아코디언 5행, 자세히보기/닫기 토글)
  ↓
SiteCompare (비교 테이블, 스태거 애니메이션 delay: 0.3 + i*0.28)
  ↓
SitePortfolio (카드 그리드, 호버 오버레이)
  ↓
SiteServices (6열 스태프 그리드, 코드태그 + 제목 + 설명)
  ↓
SiteDirector (2열: 사진 좌 / 경력 우, 스태거 bullet)
  ↓
SiteContact (2열: 정보 좌 / 폼 우, 태그형 선택 버튼)
  ↓
SiteFooter (미니멀)
```

**타이포그래피 규칙:**
```
섹션 eyebrow: text-[#E05A1A] text-xs tracking-[0.4em] uppercase
섹션 헤딩: text-4xl md:text-5xl font-black text-white
섹션 헤딩 2줄: 흰색 라인 + 오렌지 라인 조합 가능
본문: text-white/40 text-sm leading-relaxed
레이블: text-white/30 text-xs tracking-widest uppercase
```

**컴포넌트 애니메이션 규칙:**
```tsx
// 기본 섹션 진입
const ref = useRef(null)
const inView = useInView(ref, { once: true, margin: '-100px' })

// 헤딩
initial={{ opacity: 0, y: 20 }}
animate={inView ? { opacity: 1, y: 0 } : {}}
transition={{ duration: 0.6 }}

// 그리드 아이템 스태거
transition={{ duration: 0.5, delay: i * 0.04 }}

// 비교 테이블 행 (BTL 시그니처 — 한줄씩 등장)
initial={{ opacity: 0, y: 18 }}
animate={inView ? { opacity: 1, y: 0 } : {}}
transition={{ duration: 0.45, delay: 0.3 + i * 0.28 }}
```

**카운터 애니메이션 (easeOutCubic):**
```tsx
const eased = 1 - Math.pow(1 - progress, 3)
setCount(Math.floor(eased * target))
// grouped: false → 연도형 숫자 (2025) 콤마 없이
// sub: '년' → 숫자 오른쪽 작은 글씨 단위 (suffix는 오렌지 큰 글씨)
```

**참조 레포 (스켈레톤):**
```
수강생 프로젝트의 디자인 레퍼런스
```
- 10개 섹션 컴포넌트 완성본
- `lib/siteConfig.ts` 하나만 수정하면 새 클라이언트 적용 가능
- Tailwind v4 + framer-motion + Next.js 15

**사용 트리거:**
- "비더라인 스타일로" → BTL_AGENCY 서브테마
- "행사 에이전시" + "다크" → BTL_AGENCY 우선 제안
- "btl-skeleton 참고해서" → 레포 clone 후 siteConfig 수정

---

#### 🔀 [선택] 인트로 2분할 패턴: SiteSplitIntro
> 서비스가 2개(에이전시 + 마케팅 등)인 사이트에서 루트(/)를 선택 화면으로 쓸 때. 단일 서비스면 사용 안 해도 됨.

**핵심 동작:**
```
커서 올린 쪽: 블랙 오버레이 0.78 + scale(1.04) + translateY(-6px) + CTA 골드
반대쪽:       블랙 오버레이 0.42 (상대적으로 밝아짐 → 선택 대조)
기본:          블랙 오버레이 0.62
```

**overlayOpacity 패턴 (핵심 로직):**
```tsx
function overlayOpacity(side: "left" | "right", hovered: "left" | "right" | null) {
  if (hovered === side) return 0.78  // 선택 → 블랙 처리
  if (hovered) return 0.42            // 반대쪽 → 밝게
  return 0.62                         // 기본
}
```

**레이아웃 규칙:**
```
데스크탑: flex-row (좌/우 50:50)  — 중앙에 로고 absolute
모바일:   flex-col (상/하 50vh씩) — 상단에 로고 absolute
왼쪽 텍스트: text-left, pl-16 lg:pl-24, pr-28 lg:pr-36
오른쪽 텍스트: text-right, pr-16 lg:pr-24, pl-28 lg:pl-36
사진 슬라이드: 좌 4000ms / 우 3500ms (속도 다르게 → 시각 리듬)
인디케이터: 현재 슬라이드 = 20px pill, 나머지 = 6px dot, 골드 accent
```

**siteConfig 설정 (SPLIT_INTRO):**
```ts
export const SPLIT_INTRO = {
  logo: "/images/logo.png",   // null이면 로고 없음
  accent: "#c9a84c",          // 골드 — 인디케이터 + CTA 호버색
  left:  { href, eyebrow, title, keywords: string[], cta, photos: string[] },
  right: { href, eyebrow, title, keywords: string[], cta, photos: string[] },
}
// keywords 배열의 각 항목은 " ㆍ " 구분자로 태그 파싱됨
```

**컴포넌트:** `SiteSplitIntro.tsx` (btl-skeleton 포함)

---

#### 🌿 DARK_ORANGE 연관 서브테마: BTL_MARKETING (2026-08-04 검증)
> BeTheLine 온라인 마케팅 페이지(/marketing)에서 실전 검증된 변형. 자영업자 타겟 마케팅 대행 서비스에 최적화.

**컬러 팔레트 (그린 계열 — BTL_AGENCY와 독립적):**
```
배경 다크: #1C2B1A (딥 포레스트 그린)
배경 라이트: #F5F1E8 (웜 크림)
배경 크림 alt: #EDE8DC (더 진한 크림, 문의 섹션)
액센트: #3A6830 (다크 그린)
포인트 라이트: #8BAF7A (미디움 그린, 다크 배경 텍스트)
포인트 연: #A8C89A (연 그린, 히어로 강조)
텍스트 다크: #1C2B1A
텍스트 뮤트: #7A7060 (웜 그레이)
```

**레이아웃 패턴 (섹션 순서):**
```
MktHeader (fixed, blur)
  ↓
MktHero (사진 슬라이드쇼 배경, 3초 슬라이딩 메시지, 딥그린 오버레이)
  ↓
MktPainPoints (딥그린 #1C2B1A 배경, 2×2 카드 그리드)
  ↓
MktApproach (크림 배경, 기존방식 vs 우리방식 2열 비교)
  ↓
MktServices (딥그린 배경, 서비스 그리드)
  ↓
MktCases (크림 배경, 케이스 스터디)
  ↓
MktTestimonials (딥그린 배경, 후기 슬라이드)
  ↓
MktProcess (크림 배경, 수평 타임라인 데스크탑 / 세로 스텝 모바일)
  ↓
MktPromises (딥그린 배경, 약속 목록)
  ↓
MktContact (크림 alt #EDE8DC 배경, 2열: 정보 좌 / 폼 우)
```

**핵심 UI 규칙:**
```
eyebrow: text-[#8BAF7A] text-xs tracking-[0.4em] uppercase
히어로 강조색: text-[#A8C89A]
버튼 primary: bg-[#3A6830] hover:bg-[#2D5225]
카드 (다크 배경): bg-white/5 border border-white/10 rounded-xl
카드 (라이트 배경): bg-[#1C2B1A]/5 border border-[#1C2B1A]/10 rounded-xl
태그 선택 버튼: border-[#3A6830] text-[#3A6830] bg-[#3A6830]/10 (선택됨)
입력 필드: bg-[#1C2B1A]/5 border border-[#1C2B1A]/20 focus:border-[#3A6830]
```

**사진 슬라이드쇼 히어로 패턴:**
```tsx
// 사진 교체: 4000ms 간격
// 메시지 교체: 3500ms 간격, fade out 500ms
const [visible, setVisible] = useState(true)
useEffect(() => {
  setVisible(false)
  setTimeout(() => { setMsgIdx(...); setVisible(true) }, 500)
}, [...])
// 메시지 구조: { top: string, bottom: string }
// top → 흰색, bottom → text-[#A8C89A]
```

**참조 레포 (marketing/ 폴더):**
```
수강생 프로젝트의 디자인 레퍼런스 (components/marketing/)
```

**사용 트리거:**
- "자영업자 마케팅" + "다크그린" → BTL_MARKETING 서브테마
- "온라인 마케팅 대행" 홈페이지 → BTL_MARKETING 우선 제안
- "비더라인 마케팅 스타일" → BTL_MARKETING 서브테마

---

### 🟢 LIGHT_GREEN
> 신뢰·전문성. 디어스, 세무, 법률, 금융, B2B 전문직.

```
배경: #ffffff
표면: #f8f9fa
테두리: #e8eaed
텍스트 주: #191f28
텍스트 부: #4e5968
텍스트 약: #8b95a1
액센트: #00a859 (Vibers Green — 배지/아이콘/링크/강조 전용)
액센트 연: #e8f9f1
액센트 테두리: #c8ecd8
버튼 주: #191f28 (블랙 계열 — 액센트와 분리)
버튼 hover: #0a0a0a
버튼 텍스트: #ffffff
```

**폰트:**
- 헤드라인: `Paperlogy`
- 본문: `Pretendard`
- 보조 영문: `Geist` (Google Fonts)
- 스택: `'Paperlogy', 'Pretendard', 'Geist', sans-serif`

**특성:**
- 라이트 모드, 흰 배경
- 카드 그림자: `0 2px 12px rgba(0,0,0,0.06)`
- 취소선 + 할인 배지 활용 (가격 강조)
- 토스(Toss) 스타일 인용: 명확한 계층, 여백 중심
- 히어로: 좌정렬 텍스트 + 우측 목업/스크린샷 이미지

---

### 🍂 WARM_CREAM
> 감성·따뜻함. 와요, 웨딩, 초대장, 감성 브랜드.

```
배경: #faf8f5
표면: #ffffff
테두리: #e8e0d8
텍스트 주: #2c2018
텍스트 부: #6b5c4e
텍스트 약: #a89080
액센트: #c9853a (warm amber — 강조/아이콘/링크 전용)
액센트 연: #fef3e2
버튼 주: #2c2018 (다크 브라운 — 액센트와 분리)
버튼 hover: #1a100a
버튼 텍스트: #faf8f5
```

**폰트:**
- 헤드라인: `Noto Serif KR` (Google Fonts: `https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@400;700;900&display=swap`)
- 본문: `Pretendard`
- 영문 보조: `Cormorant Garamond` (Google Fonts, 웨딩/감성 느낌)
- 스택: `'Noto Serif KR', 'Cormorant Garamond', 'Pretendard', serif`

**특성:**
- 세리프 헤드라인으로 고급스러움 강조
- 배경 크림/아이보리 계열, 순백 회피
- 이미지 placeholder: 따뜻한 톤 (picsum seed 'wedding', 'flowers', 'nature')
- 애니메이션 부드럽고 느리게 (transition 0.6s ease)
- 히어로: 풀블리드 이미지 오버레이 텍스트 or 중앙정렬 감성 카피

---

### ⚡ BOLD_DARK
> 강렬·역동. 러너스커넥트, 스포츠, 피트니스, 챌린지.

```
배경: #0a0a0a
표면: #111111
테두리: rgba(255,255,255,0.1)
텍스트 주: #ffffff
텍스트 부: #888888
텍스트 약: #555555
액센트: #e8ff2a (electric yellow-green, 강조/아이콘/링크)
액센트 글로우: rgba(232,255,42,0.25)
버튼 주: #e8ff2a (다크 테마 — 액센트 OK)
버튼 hover: #d4eb1a
버튼 텍스트: #0a0a0a (검정 텍스트로 대비 극대화)
```

**폰트:**
- 헤드라인: `Gmarket Sans` (CDN: `https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansMedium.woff`)
- 본문: `Pretendard`
- 숫자/수치: `Paperlogy` (기록, 거리, 속도 강조)
- 스택: `'Gmarket Sans', 'Paperlogy', 'Pretendard', sans-serif`

**특성:**
- 헤드라인 uppercase + 강한 letter-spacing
- 굵은 구분선, 강렬한 대비
- 숫자 통계 크게 (**72px+**) — km, 시간, 참가자 수 (이전 64px → +8px)
- 액션 CTA 크고 bold: "지금 참가하기", "오늘 달리기 시작"
- 히어로: 다이나믹 풀블리드 (러닝 이미지 + 오버레이 카피)
- 절대 가운데 정렬 히어로 금지 — 좌정렬 또는 대각선 레이아웃

---

### 💜 SOFT_LIGHT
> 미니멀·테크. 팬이지, SaaS, AI 서비스, 구독 플랫폼.

```
배경: #fafafa
표면: #ffffff
테두리: #eeeeee
텍스트 주: #111111
텍스트 부: #666666
텍스트 약: #999999
액센트: #5b6af0 (indigo — 링크/아이콘/배지 전용)
액센트 연: #eef0fe
버튼 주: #111111 (블랙 — 액센트와 분리)
버튼 hover: #5b6af0 (hover 시에만 인디고로 전환)
버튼 텍스트: #ffffff
```

**폰트:**
- 헤드라인: `Paperlogy` + `IBM Plex Sans KR` (Google Fonts)
- 본문: `IBM Plex Sans KR` (CDN: Google Fonts `family=IBM+Plex+Sans+KR:wght@400;500;600;700`)
- 영문 코드/수치: `JetBrains Mono` (monospace 느낌)
- 스택: `'Paperlogy', 'IBM Plex Sans KR', 'JetBrains Mono', sans-serif`

**특성:**
- 극도로 깨끗한 레이아웃, 여백 풍부
- 베이지/그레이 분리선 (색상 배경 섹션 금지)
- 기능 소개: 3컬럼 아이콘 그리드 or Bento 그리드
- 가격표: 명확한 체크리스트, 토글 없이 심플하게
- 히어로: 좌정렬 헤드라인 + 오른쪽 UI 목업 스크린샷

---

### 📰 MEDIA_GRAY
> 한국형 뉴스·미디어. 언론사, 콘텐츠 플랫폼, 정보 서비스.

```
배경: #f7f7f7
표면: #ffffff
테두리: #d8d8d8
텍스트 주: #1a1a1a
텍스트 부: #444444
텍스트 약: #888888
액센트: #c41e3a (뉴스 레드 — 속보/강조/배지 전용, 버튼 금지)
액센트 연: #fdf0f2
버튼 주: #1a1a1a (블랙 — 레드는 속보 전용)
버튼 hover: #000000
버튼 텍스트: #ffffff
```

**폰트:**
- 헤드라인: `Pretendard` (굵기 800~900, 뉴스 타이포그래피)
- 본문: `Pretendard`
- 스택: `'Pretendard', -apple-system, sans-serif`

**특성:**
- Paperlogy 미사용 — Pretendard 단독으로 위계 표현
- 각진 레이아웃 (border-radius 최소화, 4px)
- 정보 밀도 높게 — 여백보다 콘텐츠 우선
- 레드 액센트는 강조·속보·CTA에만 절제해서 사용
- 구분선 적극 활용 (`border-bottom: 2px solid #1a1a1a`)
- 히어로: 비대칭 2단 (큰 헤드라인 좌 / 카드형 뉴스 목록 우)

---

### 🏭 CORP_BLUE
> 기업 신뢰·산업재. KOSDAQ·KOSPI 상장사, 제조업, 엔지니어링, B2B 하드웨어. CS베어링(씨에스베어링) 실제 케이스에서 추출.

```
배경: #ffffff
표면: #f7f7f7
테두리: #dddddd
텍스트 주: #111111
텍스트 부: #444444
텍스트 약: #797979
액센트: #0168ad (기업 블루 — 버튼·링크·아이콘·강조 통합)
액센트 연: #e8f4fc
액센트 보조: #ff8400 (오렌지 — 내비 hover·서브 CTA)
버튼 주: #0168ad (이 테마 한정 예외 — 블루가 브랜드=버튼)
버튼 hover: #014f8a
버튼 텍스트: #ffffff
다크 섹션: #1a2b3c
```

**폰트:**
- 헤드라인: `Pretendard` (굵기 700~800 — 기업형 신뢰감, Paperlogy 배제)
- 본문: `Pretendard`
- 영문 보조: `Roboto` (Google Fonts `family=Roboto:wght@300;400;500;700`)
- 스택: `'Pretendard', 'Roboto', 'Malgun Gothic', sans-serif`

**테마 빠른 매핑 추가:**
- "공기업 / 제조업 / KOSDAQ / KOSPI / 기업 브랜드 / B2B 산업재" → CORP_BLUE
- "뷰티 / 미용 / 네일 / 헤어 / 스파 / 예약앱 / 여성 타깃 커머스" → BEAUTY_PINK

**특성:**
- **블루 버튼 예외**: 이 테마에서만 버튼 배경 = 액센트 = `#0168ad` 허용 (기업 브랜드 일관성)
- **히어로**: Full-Bleed Media Hero 전용 — 풀스크린 배경 이미지(공장·제품·현장) + 흰 텍스트 오버레이 + 하단 그라디언트
- 히어로 슬라이더 패턴 권장 (슬라이드 3장, 5~7초 자동 전환, 하단 도트 인디케이터)
- **서브페이지 탭 사이드바**: 좌측 고정 세로 탭 (파란 배경 `#0168ad`, 흰 텍스트, active 탭에 흰 배경·파란 글자)
- **블루 좌측 강조 카드** (`border-left: 6px solid #0168ad`, 배경 `#f7f7f7`)
- **오렌지 hover 전환**: 내비게이션 드롭다운 배경 `#ff8400`
- **게시판/테이블**: 헤더 `border-top: 2px solid #111`, 행 구분선 `1px solid #ddd`
- **IR·공시 전용 섹션**: 첨부파일 다운로드 버튼, 날짜 포맷, 공식 문서 레이아웃
- **기업 푸터**: 상호·대표·사업자번호·주소·전화·팩스 전부 노출 (법적 요구사항)
- **언어 토글**: KOR / ENG 2개 언어 전환 버튼 패턴 (상단 우측 고정)
- AOS 스크롤 애니메이션 (`fade-up`, `fade-right`) — 단, 지연 0.2s 이내로 절제
- 카드 그림자: `0 2px 8px rgba(0,0,0,0.08)`, border-radius `4px` (기업체 = 각진 느낌)

**섹션 패턴 (CORP_BLUE 전용):**
```
메인: Hero Slider → 사업 개요 카드 3종 → 제품/기술 소개 → 회사 주요 지표(설립·자본·직원) → 뉴스룸(공지 최신 3건) → 채용 띠 → 푸터
서브: 상단 서브 비주얼(1/3 높이) → 좌측 탭 사이드바 + 우측 콘텐츠 2단 구조
```

**비고 (실제 케이스 수치):**
- 블루 `#0168ad`: 전체 UI의 약 15% 차지 (버튼+탭+강조 통합이라 10% 룰 예외 허용)
- 오렌지 `#ff8400`: hover·서브CTA에만 — 5% 이내 유지
- 이 테마의 '안티-제네릭' 포인트: 좌측 탭 사이드바 + 블루 border 강조 카드의 조합이 한국 기업 사이트의 레거시 언어를 모던하게 재해석

---

### 💗 BEAUTY_PINK
> K-뷰티·예약 서비스. 미용실·네일·피부관리·스파, 여성 타깃 커머스.
> beaupick(뷰픽) 실제 케이스에서 추출. **웹이지만 앱처럼 보여야 하는** 서비스에 쓴다.

```
배경: #ffffff
표면: #fff9fb
표면 강조: #fff5f9
테두리: #eee7eb
구분선: #f2ecef
텍스트 주: #211a20
텍스트 부: #70666b
텍스트 약: #9b9096
액센트: #e8006b (진한 핑크 — 버튼·탭·강조 통합)
액센트 눌림: #cf005f
액센트 연: #fff0f6
액센트 그라디언트: linear-gradient(135deg, #F90070 0%, #E8006B 100%)
별점: #ffa800
성공: #18a66a
카드 배경: #ffffff
```

**폰트:**
- 헤드라인: `Paperlogy` (굵기 800 — 화사하고 단단한 인상)
- 본문: `Pretendard`
- 스택: `'Paperlogy', 'Pretendard', -apple-system, sans-serif`

**테마 빠른 매핑 추가:**
- "뷰티 / 미용 / 네일 / 헤어 / 스파 / 예약앱 / 여성 타깃 커머스" → BEAUTY_PINK

**특성:**
- **핑크 버튼 예외**: 이 테마에서만 버튼 배경 = 액센트 허용. 단 **주요 CTA는 그라디언트**로,
  보조는 `#fff0f6` 배경 + `#e8006b` 글자로 눌러 위계를 만든다. 그라디언트를 남발하면 위계가 사라진다
- 카드 곡률 `16~18px` — CORP_BLUE(4px)와 정반대. 부드러움이 이 업종의 언어다
- **테두리 대신 그림자**: `0 2px 12px rgba(53,26,39,0.07), 0 1px 3px rgba(53,26,39,0.04)`.
  테두리를 많이 쓰면 웹처럼 보이고, 이 서비스는 앱처럼 보여야 한다
- CTA 그림자: `0 6px 20px rgba(232,0,107,0.38)` — 핑크 계열 그림자가 브랜드를 강화한다

**카테고리 파스텔 (뷰티 업종 타일):**
```
헤어 #ffe7ee · 네일 #fce5f3 · 피부 #ebecff · 마사지 #e4f7f1
눈썹 #fff1e5 · 속눈썹 #f9e6f5 · 반영구 #fff0e7 · 스파 #f5e9f7
```
파스텔 배경 위에 진한 동계열 아이콘. **이모지 금지** — 기기·OS마다 모양이 달라지고
아마추어해 보인다. 실제로 파트너 대시보드의 이모지를 아이콘으로 바꾼 것만으로
"잘 만든 서비스" 인상이 크게 달라졌다.

**앱처럼 보이게 하는 장치 (이 테마의 핵심):**
- 하단 탭바: frosted glass (`rgba(255,255,255,0.96)` + `backdrop-filter: blur(20px) saturate(180%)`)
- 선택 탭 **상단에 3px 핑크 pill** — 색만 바꾸면 어느 탭인지 눈에 안 들어온다
- 상단 헤더도 같은 frosted glass. 상세 페이지는 스크롤 320px 이상에서 슬라이드인
- 터치 피드백: `:active { transform: scale(0.96); opacity: 0.85 }`, transition 0.12s
- 전역 스크롤바 숨김 + `overscroll-behavior: none`

**섹션 패턴 (BEAUTY_PINK 전용):**
```
홈: frosted 헤더 → 검색바 → 배너 슬라이드 → 카테고리 그리드(6열 파스텔 타일)
    → 랭킹 TOP3 → 신규 오픈 가로 스크롤 → 하단 탭바
상세: 풀블리드 히어로 갤러리 → 정보 카드 → 시술 메뉴 → 리뷰 → 하단 고정 예약 CTA
```

**빠지기 쉬운 함정:**
- PWA·웹뷰라면 `viewport-fit=cover`를 반드시 넣을 것. 없으면 `env(safe-area-inset-*)`가
  **전부 0**이 되어 노치·홈인디케이터 대응이 통째로 무효가 된다. 실제로 겪은 버그다
- 하단 고정 CTA와 탭바 높이를 따로 계산하면 겹친다. 탭바 높이를 한 곳에서 정의해 공유할 것
- `#fff0f6` 같은 연한 배경 위에 흰 글씨는 읽히지 않는다. 대비를 반드시 확인

**리텐션·전환 패턴 (강남언니 벤치마킹 — 2026-08-12, 레퍼런스: `design-refs/gangnam-unni-app/`):**
> 뷰티·예약·커머스 앱형 서비스라면 화면 디자인만큼 **여정 설계**가 인상을 좌우한다.
> 아래 8패턴은 강남언니(unni 재팬) 22화면에서 추출, beaupick에 실적용 검증.

1. **온보딩 = 개인화 시그널 퍼널**: 가입 직후 관심 부위(최대 2)→관심 지역 순 2~3스텝.
   철칙 — ①매 스텝 "왜 묻는지" 한 줄("알맞는 이벤트를 추천해드려요") ②건너뛰기 상시 허용
   ③상단 진행바 ④"n/2 선택됨" 카운터 ⑤비활성 CTA는 회색이 아니라 **연한 브랜드색**
   (`--accent-light` 배경 + `--accent` 글자) — 죽은 버튼이 아니라 "곧 눌릴 버튼"으로 보인다
2. **웰컴 포인트 + 만료 압박**: 가입 즉시 지급(예: 2,500P) + 30일 만료.
   포인트 페이지 최상단에 잔액 대형 → 바로 아래 "만료 예정 -n P" 행. 만료가 전환을 만든다
3. **포인트 내역 표준**: 필터 칩(전체/적립/사용/만료) + **월별 그룹 헤더** + 행마다
   "~까지 사용 가능" 기한 표기. 적립은 `+n P`를 액센트색으로
4. **혜택 허브**: 적립 방법을 아이콘 카드 리스트 한 페이지에 집약(리뷰 nP·친구초대 nP·예약 적립)
   + 하단에 진행 중 이벤트 미리보기. 포인트를 "행동 유도 시스템"으로 운영하는 관제탑
5. **홈 퀵액션 칩**: 검색바~히어로 사이에 알약 칩 2줄 가로 스크롤 — 핵심 여정(AI 추천·상담·
   예약 내역)과 커머셜 필터(가격대·부위)를 1탭 진입. 아이콘+짧은 라벨, surface 배경+보더
6. **커뮤니티 = before/after UGC**: 사진 캐러셀이 피드의 중심. 목적별 탭(자유수다/시술 질문/
   발품후기) + 추천순·최신순 정렬. 글쓰기 FAB는 최상단에서 "+ 글쓰기" 알약 확장 →
   스크롤하면 원형 축소

   **📐 피드 카드 정밀 스펙** (강남언니 실측, 리뷰·커뮤니티 공통 —
   완성 예시: `design-refs/gangnam-unni-app/feed-card-spec.png`,
   구현체: beaupick `components/feed/FeedMediaCarousel.tsx`)
   | 요소 | 값 |
   |------|-----|
   | 카드 | 카드 나열이 아니라 **피드** — 흰 배경 full-bleed, 좌우 패딩 16px, 카드 사이 1px `#F2ECEF` divider (그림자·보더 카드 금지) |
   | 아바타 | 44px, **라운드 사각 14px**(원형 아님), 이미지 없으면 파스텔 배경 + 이니셜 |
   | 닉네임 / 메타 | 16px semibold `#211A20` / 14px `#9B9096`, "18시간 전 · 후기"처럼 시간·말머리를 `·`로 연결 |
   | 본문 | **16px · 행간 1.55 · `#211A20`** — 5줄 클램프 후 "더보기"(밑줄 `#70666B`). 본문을 13px로 줄이면 UGC가 부수 정보처럼 보인다 |
   | **사진(핵심)** | 폭 **73%** · **3:4 세로** · 라운드 16px · **갭 8px** · `scroll-snap-type: x mandatory` → **다음 장이 20% 걸침(peek)**. 컨테이너 패딩만큼 음수 마진으로 빼내 우측을 화면 밖으로 흘린다. **사진 1장이면 100% 꽉 채움** |
   | 액션 | 아이콘 22px + 숫자 15px `#211A20`, gap 20px. 좋아요·댓글은 좌측 묶음, 조회수 등 보조는 `margin-left:auto`로 우측 |

   > 사진을 화면폭 100%로 채우거나 72px 썸네일로 줄이면 **"더 있다"는 신호가 사라진다.**
   > 73% + peek이 스크롤 힌트 없이 다음 장의 존재를 알려주는 장치다.
7. **기획전 매거진형**: 풀스크린 히어로 + "Contents 01~04" 목차 + 섹션별 시술 가격 리스트
   카드 + 블랙 CTA. 시즌 캠페인을 광고가 아니라 콘텐츠로 포장한다
8. **크로스보더 UX** (외국인 타깃일 때): 국가 선택 드롭다운·국가번호 시트·"내 한국 방문 일정".
   푸터에 중개 플랫폼 면책 고지("통신판매 당사자가 아니므로...") 상시

---

## 2-1. ✨ 기본 유려함 — 테마보다 먼저 (MANDATORY)

**테마(색)를 고르기 전에 `polish-guide.md` 를 먼저 적용한다.**
색을 아무리 잘 골라도 아래 4가지가 없으면 "싸구려 티"가 난다. 카테고리 무관 전 프로젝트 공통.

| # | 규칙 | 없으면 |
|---|------|--------|
| 1 | **유체 타이포 `clamp()`** | 1920px 모니터에서 본문 16px — 그 순간 아마추어 |
| 2 | **섹션 간격 160px**(모바일 96) | 다닥다닥 붙어 정신없음. 여유로움 = 여백이지 폰트가 아니다 |
| 3 | **스크롤 진입 + 순차 딜레이 0.12s** | 스크롤해도 아무 일 없어 밋밋. GSAP 불필요 |
| 4 | **그레이 9단 토큰** | `#888 #999 #aaa` 혼용으로 화면이 지저분 |

추가로 **실사이트 32페이지에서 실제로 터진 함정 7종**이 들어 있다 —
`<a>` 중첩 하이드레이션 실패(프로덕션에선 `error #418`로만 뜬다), grid 자식 `min-w-0`,
가로스크롤을 `scrollWidth`로 재면 오탐 등.

→ **전문: `polish-guide.md`**

---

## 3. 공통 디자인 규칙 (모든 테마 적용)

### 폰트 규칙
- **Paperlogy 탑재**: 모든 테마에서 Paperlogy를 헤드라인 또는 숫자 강조에 사용. CDN 주소 고정.
  ```
  @import url('https://cdn.jsdelivr.net/gh/Freesentation/paperlogy@main/Paperlogy.css');
  ```
- **Pretendard 기본 본문**: 모든 테마 본문 텍스트는 Pretendard. WARM_CREAM만 예외(Noto Serif KR).
- **금지 폰트**: Inter, Noto Sans KR(Pretendard로 대체), Roboto, Arial, Open Sans

### 레이아웃 다양성 규칙 (수파노바 계승)
- DESIGN_VARIANCE 기본값: **8** (비대칭 강제)
- 히어로 중앙정렬은 WARM_CREAM 테마만 허용
- 나머지 4개 테마: 반드시 비대칭 2단 or 풀블리드
- 인접 섹션은 반드시 다른 레이아웃 패턴 사용

### 한국어 타이포그래피
- `word-break: keep-all` 모든 한국어 텍스트에 필수
- 헤드라인: `letter-spacing: -0.04em`, `line-height: 1.15~1.25`
- **본문 기본: 17~18px** (이전 14~15px → 가독성 향상. 한국어는 영문보다 디센더가 짧아 더 큰 사이즈 필요)
- 본문 line-height: 1.7~1.8, max-width: 65ch
- 금지 표현: "혁신적인", "획기적인", "차세대", "스마트한"

### 본문 타이포그래피 스케일 (CRITICAL — 2026-06-23 상향 조정)
2026-06-23 사용자 피드백 반영: 폰트가 너무 작다는 지적 → 전 단계 **+2~4px 상향**.

| 역할 | 이전 | **현재 (필수)** | Tailwind |
|------|------|-------------|----------|
| 캡션 / 메타 | 12px | **14px** | `text-sm` |
| 본문 보조 | 14px | **16px** | `text-base` |
| 본문 기본 | 15~16px | **17~18px** | `text-lg` |
| 본문 강조 | 16~17px | **19~20px** | `text-xl` |
| 서브헤딩 | 18~20px | **22~24px** | `text-2xl` |
| 섹션 제목 | 24~28px | **28~32px** | `text-3xl` |
| 페이지 제목 | 32~40px | **36~44px** | `text-4xl` |
| 히어로 보조 헤드 | 40~48px | **48~56px** | `text-5xl` |

**금지**: `text-xs (12px)`, `text-sm (14px) 본문 사용` — 캡션/배지에만 허용

### 히어로 헤드라인 상한 규칙 (CRITICAL — 상향 조정)
- 데스크톱 최대: `clamp(3rem, 5.5vw, 5rem)` (48px ~ 80px) ← 이전 40~72px
- 모바일 최대: `clamp(2.5rem, 8.5vw, 3.5rem)` (40px ~ 56px) ← 이전 32~48px
- **`text-8xl`, `text-9xl` 사용 금지**
- `text-7xl` 사용 시 조건: 히어로에 한 줄 헤드라인만 있고, 주변 여백이 폰트 크기의 1.5배 이상 확보된 경우에만
- 한국어는 영문보다 **1단계 작게** 적용 (한글이 영문보다 시각적으로 더 크게 느껴짐)
- BOLD_DARK 테마의 숫자 통계(**72px+**)는 예외 적용 가능 ← 이전 64px+

### 컬러 비율 규칙 60-30-10 (CRITICAL)
- **60%**: 배경색 + 표면색 (중성)
- **30%**: 텍스트 + 뉴트럴 그레이
- **10%**: 액센트 + 버튼 (포인트 컬러 총합이 **화면 비율 10% 이내**)
- 액센트 컬러가 히어로 1섹션에 **3회 이상 등장하면 과함** → 2회 이하로 조정
- 액센트와 버튼 배경이 동시에 같은 색으로 5회 이상 반복되면 규칙 위반으로 간주

### 이미지 플레이스홀더
- picsum: `https://picsum.photos/seed/{테마관련키워드}/{w}/{h}`
- 아바타: `https://i.pravatar.cc/150?u={한국이름}`
- Unsplash URL 절대 금지

### CTA 버튼 규칙

**배경색 분리 원칙 (CRITICAL)**:
- Primary CTA 버튼 배경은 반드시 테마의 `버튼 주` 토큰 사용
- **포인트 컬러(액센트)와 버튼 배경이 동일하면 안 됨** — 다크 테마(DARK_ORANGE, BOLD_DARK)만 예외 허용
- 라이트 테마(MODERN_BW, LIGHT_GREEN, WARM_CREAM, SOFT_LIGHT, MEDIA_GRAY):
  → Primary 버튼 배경은 **블랙/다크 계열** (`버튼 주` 토큰)
  → 액센트 컬러는 **텍스트 강조·배지·아이콘·링크**에만 사용
  → 액센트를 버튼 배경으로 쓰면 시각 위계 붕괴
- Secondary CTA: 테두리만 있는 ghost 버튼 (`border + bg-transparent + text-버튼주`)
- Tertiary CTA: 텍스트 링크 (밑줄 hover)
- 한 화면에 Primary 버튼은 **최대 2개**까지

**인터랙션**:
- hover: `transform: scale(1.03)` + 배경을 `버튼 hover` 토큰으로 전환
- active: `transform: scale(0.97)`
- 최소 크기: `padding: 16px 32px`, **`font-size: 17px`** (이전 15px → +2px)
- focus 상태 반드시 포함 (접근성, `outline: 2px solid` + offset)

### 아이콘
- Iconify Solar 세트 전용
- CDN: `https://code.iconify.design/iconify-icon/2.3.0/iconify-icon.min.js`
- 이모지 절대 사용 금지

---

## 4. OUTPUT FORMAT 분기

### HTML 출력 (기본)
- Tailwind CSS CDN
- 모든 스타일 인라인
- `<script>` 태그로 IntersectionObserver 스크롤 리빌
- 파일 하나로 브라우저에서 바로 실행

### TSX 출력 (Next.js)
- `"use client"` 상단 선언
- Tailwind 클래스 사용 (CDN 없이)
- 폰트: globals.css에 `@import` 추가 안내 포함
- `useState`, `useEffect` 활용
- 인라인 `<style>` 태그로 커스텀 CSS 추가 허용
- 컴포넌트명: 파일명 기반 PascalCase

---

## 5. Vibers 생태계 표준 섹션

다음 섹션들은 Vibers 서비스 랜딩에 공통으로 사용되는 패턴이다. 요청 시 즉시 적용.

### 생태계 혜택 섹션 (ECOSYSTEM BENEFITS)
와요·가보자고·러너스커넥트·팬이지 등 연동 혜택을 보여줄 때:
- 다크 배경 섹션 (테마와 무관하게 #0d0d0d 또는 #191f28)
- 4개 서비스 카드 그리드 (2×2)
- 각 카드: 서비스명 + 한 줄 혜택 설명

### 가격 패키지 (PRICING)
- 3단계 기본 (BASIC / STANDARD / PREMIUM)
- 중간이 추천 플랜 (featured border)
- 가격 숫자: Paperlogy **56px+** (이전 52px → +4px)
- 아래 면책 문구: "VAT 별도 · 커스텀 협의 가능"

### 프로세스 (PROCESS)
- 4단계: 상담 → 기획 → 제작 → 오픈
- 가로 스텝 바 (데스크탑) / 세로 타임라인 (모바일)
- 단계 번호: 01/02/03/04 형식

### 신뢰 지표 (TRUST BAR)
- 숫자 + 레이블 3~4개
- 유기적 숫자 사용: `47,200+` not `50,000+`
- 배경: 테마 표면색 or 약한 대비 섹션

---

## 6. 섹션 라이브러리 (Section Library)

제네릭 레이아웃 금지. 아래 패턴에서 골라 사용.

### 히어로
- **Split Hero** — 60/40 텍스트:비주얼. 텍스트 좌, 스크린샷·목업 우. 배경 그라디언트 블리드
- **Full-Bleed Media Hero** — 풀스크린 이미지/영상 + 오버레이 텍스트. 하단 다크 그라디언트. CTA 하단 플로팅
- **Minimal Statement Hero** — 초대형 타이포(text-7xl+) + 극도의 여백. 한 줄 가치 제안. CTA 필 플로팅
- **Interactive Hero** — 타이프라이터 효과로 유즈케이스 순환

### 기능 섹션
- **Bento Grid** — 비대칭 그리드 (2fr 1fr 1fr). 카드 높이 다양. 아이콘+제목+설명
- **Zig-Zag Alternating** — 이미지좌/텍스트우 → 텍스트좌/이미지우 교차. 3컬럼 동일카드 절대 금지
- **Icon Strip** — 가로 스크롤 기능 아이콘 + hover 리빌
- **Comparison Table** — Before vs After 또는 Us vs Them

### 소셜 프루프
- **Logo Cloud** — 클라이언트 로고 자동 마퀴. 그레이스케일 → 컬러 on hover
- **Testimonial Masonry** — 카드 높이 불규칙. 실제 한국인 이름·직책·아바타
- **Metrics Bar** — 숫자 카운팅 애니메이션. `47,200+ 페이지 생성`, `4.87/5.0 만족도`
- **Case Study Cards** — 전후 스크린샷 + 오버레이 설명

### CTA 섹션
- **Full-Bleed CTA** — 다크 배경, 대형 텍스트, 글로우 액센트 버튼, 하단 신뢰 배지
- **Sticky Bottom CTA** — 히어로 스크롤 후 나타나는 고정 하단 바
- **Inline CTA** — 콘텐츠 흐름 안에 삽입, 주변 섹션과 다른 스타일

### 푸터
- **Minimal Footer** — 로고 + 필수 링크 + 저작권. 4컬럼 링크팜 금지
- **Rich Footer** — 회사 설명 + 주요 네비 + SNS 아이콘 + 뉴스레터

---

## 7. 크리에이티브 프로액티비티 (Anti-Generic)

기본값으로 아래 패턴을 적극 적용:

- **Liquid Glass** — `backdrop-blur-xl` + `border border-white/10` + `shadow-[inset_0_1px_0_rgba(255,255,255,0.1)]` + `bg-white/5`
- **Magnetic CTA** — hover 시 `transition: all 0.4s cubic-bezier(0.16,1,0.3,1)` + 방향 화살표 아이콘 shift
- **Staggered Reveal** — `animation-delay: calc(var(--index) * 100ms)` 계단식 등장
- **Floating Elements** — `@keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-10px)} }` 무한루프
- **Gradient Mesh BG** — `radial-gradient` 다중 레이어로 blob형 앰비언트 배경

---

## 8. 퍼포먼스 가드레일

- 그레인/노이즈 필터: `position:fixed; inset:0; pointer-events:none` 요소에만. 스크롤 컨테이너 금지
- 애니메이션: `transform`과 `opacity`만. `top`, `left`, `width`, `height` 절대 금지
- 이미지: fold 아래는 `loading="lazy"` + `decoding="async"`
- 외부 CDN: 최대 5개 (Tailwind + Paperlogy + Pretendard + Iconify + Motion One)
- 뷰포트: `h-screen` 금지 → 반드시 `min-h-[100dvh]` (iOS Safari 레이아웃 점프 방지)
- z-index: sticky nav(`z-40`), overlay(`z-50`), noise texture(`z-[60]`)만

---

## 9. AI Tells — 절대 금지 패턴

### 시각/CSS
- 네온/외부 글로우 금지 → 내부 border 또는 tinted shadow 사용
- 순수 블랙(`#000000`) 금지 → `#0a0a0a`, Zinc-950, Slate-950 사용
- 과포화 액센트 금지
- 그라디언트 텍스트 페이지당 1개 최대

### 레이아웃
- 3컬럼 동일 카드 줄 금지 → Bento, Zig-Zag, 비대칭 사용
- 인접 섹션 동일 레이아웃 금지
- 엣지-투-엣지 콘텐츠 금지 → `max-w-7xl mx-auto` 컨테이너 필수

### 콘텐츠
- `김철수`, `홍길동` 금지 → `하윤서`, `박도현`, `이서진` 등 실제스러운 이름
- 라운드 숫자 금지 → `47,200+` not `50,000+`
- Lorem ipsum 금지 → 모든 플레이스홀더 한국어로

---

## 10. 개편 모드 (Redesign Mode)

기존 페이지 작업 시 반드시 모드를 명시하거나 사용자 발언에서 판단:

| 모드 | 트리거 예시 | 범위 |
|------|-----------|------|
| `FULL` | "전면 개편", "다시 만들어줘" | 레이아웃·색상·폰트 전부 교체 |
| `LAYOUT_KEEP` | "레이아웃 유지하고 개편", "색만 바꿔줘" | 레이아웃 그대로, 색상·폰트만 테마 적용 |
| `FIX_ONLY` | "시각적 오류만", "깨진 곳만 고쳐줘" | 간격·반응형·깨진 요소만 수정 |

---

## 11. Pre-flight 체크리스트

출력 전 반드시 확인:
- [ ] 테마 팔레트 색상만 사용했는가
- [ ] Paperlogy 헤드라인 탑재됐는가
- [ ] 금지 폰트(Inter, Noto Sans KR, Roboto) 없는가
- [ ] 한국어 텍스트에 `word-break: keep-all` 있는가
- [ ] `h-screen` 없고 `min-h-[100dvh]` 사용했는가
- [ ] 인접 섹션이 다른 레이아웃 패턴인가
- [ ] 이모지 없고 Iconify Solar 아이콘 사용했는가
- [ ] picsum 이미지 사용, Unsplash URL 없는가
- [ ] CTA 버튼 hover/active/focus 상태 있는가
- [ ] 모바일 탭 타겟 최소 48px인가
- [ ] 템플릿처럼 보이지 않고 프리미엄하게 느껴지는가
- [ ] **Primary 버튼 배경색이 액센트 컬러와 분리되어 있는가** (라이트 테마 필수)
- [ ] **히어로 헤드라인이 `clamp(3rem, 5.5vw, 5rem)` 상한을 지키는가 (48~80px)**
- [ ] **본문이 17px 이상인가** (text-lg 이상. text-sm/text-xs는 캡션만)
- [ ] **버튼 font-size가 17px 이상인가**
- [ ] **액센트 컬러가 화면 비율 10% 이내인가** (60-30-10 규칙)
- [ ] `text-8xl`, `text-9xl` 클래스를 사용하지 않았는가

---

## 12. 그레인 텍스처 코드 (DARK_ORANGE, BOLD_DARK 필수)

```css
.grain::before {
  content: '';
  position: fixed; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 999; opacity: 0.35;
}
```

## 7. 스크롤 리빌 JS (모든 테마 공통)

```javascript
const observer = new IntersectionObserver(
  entries => entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('in-view'); }),
  { threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
);
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

```css
.reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.65s cubic-bezier(0.4,0,0.2,1), transform 0.65s cubic-bezier(0.4,0,0.2,1); }
.reveal.in-view { opacity: 1; transform: translateY(0); }
.reveal-d1 { transition-delay: 0.1s; }
.reveal-d2 { transition-delay: 0.2s; }
.reveal-d3 { transition-delay: 0.3s; }
```
