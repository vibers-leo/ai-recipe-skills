---
name: vibers-full-output
description: Vibers 디자인 엔진 완전 출력 강제 규칙. HTML 단독 파일, Next.js TSX, Ruby on Rails ERB 모두 지원. 절대 중단하거나 축약하지 않는다.
---

# Vibers Full-Output Enforcement

## 절대 금지 패턴

**코드 내:**
- `<!-- ... -->`
- `<!-- rest of sections -->`
- `<!-- TODO -->`
- `// ...`
- `{/* 나머지 섹션 */}`

**말로 때우기:**
- "필요시 추가 가능합니다"
- "나머지는 동일한 패턴으로"
- "간략히 보여드리면"
- "히어로만 먼저 보여드릴게요"

## 완성 기준

### HTML 출력
필수 포함: `<!DOCTYPE html>` + 헤더 + 히어로 + 신뢰지표 + 기능/패키지 + 혜택 + 프로세스 + CTA + 푸터 + 스크롤JS

### TSX 출력
필수 포함:
- `"use client"` 선언
- 모든 섹션 컴포넌트 (인라인 or 분리)
- `<style>` 태그 커스텀 CSS
- `useState` / `useEffect` 훅
- 완전한 return JSX (닫는 태그까지)
- 폰트 로드 안내 주석

### ERB 출력 (Ruby on Rails)
필수 포함:
- `application.html.erb` 레이아웃에 폰트 CDN `<link>` 추가 안내
- Tailwind CSS: `app/assets/stylesheets/application.css` 또는 CDN
- 커스텀 CSS: `app/assets/stylesheets/{페이지명}.css` 또는 `<style>` 태그 인라인
- JS: `app/javascript/controllers/{페이지명}_controller.js` (Stimulus) 또는 인라인 `<script>`
- 파셜 분리: `_hero.html.erb`, `_pricing.html.erb` 등 섹션별 파셜 권장
- 이미지: `asset_path` 또는 picsum placeholder
- 구조: `<% %>` ERB 태그로 Rails 데이터 바인딩

```erb
<%# app/views/pages/landing.html.erb %>
<div class="테마-wrapper">
  <%= render 'pages/hero' %>
  <%= render 'pages/trust_bar' %>
  <%= render 'pages/packages' %>
  <%= render 'pages/process' %>
  <%= render 'pages/contact_form' %>
</div>

<style>
  /* 테마 CSS */
</style>

<script>
  // IntersectionObserver 스크롤 리빌
</script>
```

## 중단 시 처리

토큰 한계 도달 시:
```
[PAUSED — {N}/{전체} 섹션 완료. "계속"을 입력하면 {다음 섹션}부터 이어서 출력합니다]
```
재시작 시: `<head>` 재출력 없이 다음 `<section>` 또는 JSX 블록부터 바로 시작.

## TSX 파일 구조 표준

```tsx
"use client";

import { useState, useEffect, useRef } from "react";

// 데이터 상수
const DATA = [...];

export default function PageName() {
  // 상태
  const [form, setForm] = useState({...});

  // 스크롤 리빌
  useEffect(() => {
    const observer = new IntersectionObserver(...);
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
    return () => observer.disconnect();
  }, []);

  return (
    <>
      <style>{`/* 테마 CSS */`}</style>
      <div className="...">
        {/* 헤더 */}
        {/* 히어로 */}
        {/* 신뢰지표 */}
        {/* 패키지 */}
        {/* 생태계 혜택 */}
        {/* 프로세스 */}
        {/* 문의 폼 */}
        {/* 푸터 */}
      </div>
    </>
  );
}
```
