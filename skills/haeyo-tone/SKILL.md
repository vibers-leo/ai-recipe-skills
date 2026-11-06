---
name: haeyo-tone
description: Convert Korean UI/UX copy into Toss-style 해요체 (polite informal Korean) optimized for conversion (CTA) and customer satisfaction (CS). Use this skill whenever the user wants to rewrite, improve, or audit Korean copy in web/app products — including buttons, error messages, empty states, onboarding text, notifications, form labels, tooltips, marketing copy, or any user-facing text. Trigger especially when the user mentions "해요체", "토스 톤", "말투 바꿔", "문구 다듬어", "사용자 친화적", "CTA 강화", "에러 메시지 개선", "UX 라이팅", or references any Korean UX copy that feels cold, formal, negative, or passive. Also trigger when scanning a codebase for UX copy audit, or when producing new Korean copy from scratch for services built for Korean users.
---

# 해요톤 (Toss-style Korean UX Writing)

토스가 공식 가이드로 공개한 8가지 라이팅 원칙과 해요체를 기반으로, 단순 문자 치환을 넘어 **전환(CTA) + 고객만족(CS)** 관점까지 고려해 한국어 UX 카피를 재작성하는 스킬.

## 언제 쓰는 스킬인가

이 스킬은 "말투만 부드럽게 바꾸는" 것이 아니다. 한국어 제품에서 사용자가 마주치는 문구는 **행동을 유도**하거나 **불편을 줄이거나** **신뢰를 쌓는** 기능을 해야 한다. 단순히 "합니다 → 해요"로 바꾸면 토스 톤이 아니라 그냥 존댓말이다.

이 스킬을 쓰는 상황:
- 기존 제품의 버튼/메시지/안내문을 다듬고 싶을 때
- 새 기능의 UX 카피를 처음 쓸 때
- 에러/실패/제한 메시지가 딱딱하거나 차가워서 CS 문의가 들어올 때
- 전환율이 낮은 CTA를 개선하고 싶을 때
- 코드베이스 전체를 스캔해서 UX 카피 감사(audit)를 하고 싶을 때

## 작업 순서

**1. 맥락을 먼저 파악한다.**
같은 단어라도 버튼인지, 토스트인지, 에러인지, 빈 상태 화면인지에 따라 최적의 문구가 완전히 달라진다. 문구를 받으면 무조건 먼저 "이거 어디서 나오는 문구야?"를 파악한다. 파일에서 읽을 때는 JSX/HTML 구조를 보고 (`<Button>`, `<Toast>`, `<Error>` 등), 사용자가 텍스트만 줬다면 맥락을 물어본다.

**2. 8가지 원칙 체크리스트로 진단한다.**
`references/principles.md`에 토스 8원칙 전문이 있다. 매번 다 읽을 필요는 없고, 문구를 볼 때 아래 5가지를 빠르게 체크:

- 해요체인가? (합니다, 하세요, 하십시오 → 해요)
- 능동형인가? (등록되었습니다 → 등록했어요)
- 긍정형인가? (할 수 없습니다 → ~하면 할 수 있어요)
- 잡초가 없는가? (빼도 의미 안 변하는 단어 제거)
- 이 문구가 "누구에게" "무엇을 하게" 하려는 건가?

마지막 질문이 핵심이다. 목적이 명확하지 않으면 톤 변환이 피상적이 된다.

**3. 맥락별 패턴으로 재작성한다.**
맥락에 따라 다른 reference 파일을 읽는다:
- 버튼·CTA → `references/cta-patterns.md`
- 에러·실패·제한 메시지 → `references/cs-patterns.md`
- 빈 상태·온보딩·튜토리얼 → `references/empty-onboarding.md`

각 파일에는 "이런 상황에는 이런 구조로" 라는 패턴 + Before/After 예시가 들어있다. 패턴을 외우려 하지 말고, 그때그때 해당하는 파일을 읽어서 참고한다.

**4. 왜 바꿨는지 짧게 설명한다.**
사용자에게 결과만 던지지 말고, "원본은 수동형이라 책임 소재가 불명확해서 능동형으로 바꿨어요" 정도로 **변경 이유를 1줄로** 알려준다. 그래야 사용자도 기준을 학습하고, 다음엔 직접 쓸 수 있게 된다.

## 3단계 고도화 레벨

사용자가 원하는 깊이에 따라 작업 레벨을 맞춘다.

**Level 1 — 톤 전환만 (Quick)**
단순히 말투를 해요체로. 구조/의도는 건드리지 않음. 대량 카피를 빠르게 정리할 때.

**Level 2 — CTA/CS 강화 (Standard, 기본값)**
맥락을 파악해서 버튼이면 행동 동사 + 가치, 에러면 공감 + 해결책 구조로 재작성. 이게 이 스킬의 핵심이고 기본값이다.

**Level 3 — A/B 변형 생성 (Deep)**
하나의 문구에 대해 2~3가지 변형을 제안. 사용자가 전환율 테스트를 돌릴 수 있게. "더 강하게", "더 친근하게" 같은 요청에 대응.

사용자가 지정 안 하면 **Level 2**로 진행한다.

## Before/After 빠른 감 잡기

```
원본: "파일 업로드에 실패하였습니다."
Level 1: "파일 업로드에 실패했어요."  ← 톤만 변환, 여전히 차가움
Level 2: "파일을 올리지 못했어요. 잠시 후 다시 시도해볼게요." ← 공감 + 해결책
Level 3: [
  "파일을 올리지 못했어요. 잠시 후 다시 시도해볼게요.",
  "앗, 파일 올리는 중에 문제가 생겼어요. 한 번 더 해볼까요?",
  "지금은 파일을 올릴 수 없어요. 네트워크를 확인해주세요."
]
```

Level 2가 왜 나은가: 원본은 "실패"라는 부정 단어 + 책임 회피(수동형) + 해결책 부재. 사용자는 이 문구를 보면 "내가 뭘 잘못했나?" 싶어서 이탈하거나 CS에 문의한다. Level 2는 "올리지 못했어요"(능동, 시스템이 책임을 짐) + "다시 시도해볼게요"(해결 경로 제시)로 CS 문의를 원천 차단한다.

## 하지 말아야 할 것

- **이모지 남발**: 토스는 이모지를 거의 안 쓴다. 쓰더라도 한 문구에 1개 이하. "✨ 지금 만들어볼게요 🎉" 같은 건 토스 톤이 아니라 카카오/네이버 톤이다. 사용자가 명시적으로 요청하지 않는 한 이모지는 넣지 않는다.
- **과한 존중 표현**: "~해드릴게요", "~해주시겠어요?" 남발. 친근함을 넘어서 과공손이 되면 거리감이 생긴다.
- **길이 늘리기**: 친근하게 만든다고 문장이 길어지면 안 된다. 토스 원칙 중 "잡초 제거"가 가장 강력한 규칙이다. 원본보다 길어졌으면 다시 줄인다.
- **맥락 없는 일괄 치환**: 같은 "삭제하기"라도 실행 버튼일 때와 설명 텍스트일 때 문구가 달라야 한다. 파일 전체를 받아서 sed로 치환하듯 처리하면 안 된다.

## 코드베이스 스캔 모드

사용자가 "이 프로젝트 전체 문구 점검해줘" 같은 요청을 하면:

1. `.tsx`, `.jsx`, `.vue`, `.svelte`, `i18n.json`, `locale/*.json` 같은 파일들을 Grep으로 찾는다.
2. 한글이 들어있는 문자열 리터럴만 추출한다.
3. 각 문구를 3가지 카테고리로 분류: **버튼/CTA**, **메시지/알림**, **설명/라벨**.
4. 표 형태로 정리해서 사용자에게 보여준다: `파일 경로 | 원본 | 제안 | 이유`
5. 한 번에 다 바꾸려 하지 말고, 사용자가 승인한 것만 적용한다.

## 테스트 방법

새로운 변환 규칙을 만들었거나 애매한 문구를 다룰 때는 사용자에게 직접 물어본다. 특히:
- 브랜드 보이스가 진지한 프로젝트(B2B, 금융, 의료)인가, 캐주얼한 프로젝트(SNS, 커머스)인가?
- 타겟 연령대는?
- 이 문구의 핵심 목적은 행동 유도인가, 안심시키는 것인가, 정보 전달인가?

이 3가지만 알면 톤이 확실하게 결정된다.

## 참고 자료

- [앱인토스 UX 라이팅 공식 가이드](https://developers-apps-in-toss.toss.im/design/ux-writing.html)
- [토스의 8가지 라이팅 원칙](https://toss.tech/article/8-writing-principles-of-toss)
- [토스 에러 메시지 시스템 글](https://toss.tech/article/introducing-toss-error-message-system)

references/ 폴더에 위 자료들의 핵심 내용이 압축되어 있다.
