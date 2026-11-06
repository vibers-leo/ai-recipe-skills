---
name: storyboard-v1
description: "스토리보드 V1 — 광고/영상 '한 편 전체'를 단일 가로형 콘티 시트 한 장으로 정리하는 스킬. 15초 광고의 흐름을 ①~⑫ 컷 그리드로 한눈에 잡고, 컷마다 썸네일+ACTION+CAMERA+DIALOGUE를 달아 전체 그림·내러티브 아크·캐릭터/제품 일관성을 한 장으로 lock한다. Use this skill whenever the user wants the WHOLE ad/film laid out at a glance as one board — 광고 콘티, 전체 콘티, 한 장 콘티, 15초 콘티, 12컷 콘티, 광고 흐름 정리, 스토리보드 한눈에, overview board, full-spot storyboard, one-sheet board, ad continuity sheet. 트리거: '광고 전체 스토리보드/콘티로 빼줘 · 한 장에 정리 · 흐름 보게 · 몇 컷으로 짜줘'. ⚠️ 한 컷을 여러 앵글로 초별 START/END까지 잘게 쪼개는 디테일 분해는 V1이 아니라 storyboard-v2를 쓴다. 광고 한 편의 큰 그림 = V1(이 스킬), 한 컷 정밀 구현 = V2."
metadata:
  version: "1.1.0"
---

# Storyboard V1 — 광고 한 편 전체 콘티 시트 (한 장 / 한눈에)

영상/광고 **한 편 전체의 흐름**을 **단일 가로형 콘티 시트 이미지 한 장**으로 정리하는
ChatGPT/Codex 이미지 생성 프롬프트를 만든다. "광고 전체 그림을 한눈에" + "캐릭터·배경·제품 디테일
일관성 유지"가 존재 이유다.

검증 예시: `assets/reference-ad-sheet.png` (옥수수수염차「들결」15초 / 12컷 A안 — 외갓집·선형).
이 레이아웃·텍스트 밀도·톤을 기준선으로 삼는다.

---

## V1 vs V2 — 무엇을 쓰나 (먼저 확인)

| | **V1 (이 스킬)** | **V2 (`storyboard-v2`)** |
|---|---|---|
| 담는 범위 | 광고/영상 **한 편 전체** | **한 컷** 하나 |
| 단위 | 1컷 = 1셀 (①②③…⑫) | 1컷 = 6샷으로 분해 (S1~S6) |
| 목적 | 전체 흐름·아크·일관성 한눈에 | 한 컷을 초별로 정밀 구현 |
| 프레임 | 컷당 썸네일 1장 | 샷마다 START/END 2프레임 |
| 배경톤 | **밝은 크림/아이보리** 에디토리얼 | 다크 네이비 `#0A0A12` |
| 오디오 | DIALOGUE 한 줄 표기 | 나레이션·대사 + SFX 정밀 |

→ "광고 한 편 콘티 짜줘" = **V1**. "이 컷 디테일하게 쪼개줘" = **V2**.
워크플로 순서: `master-sheet` → **V1 전체 콘티** → 핵심 컷만 **V2 분해** → Seedance/영상.

---

## 핵심 규칙 (STRICT)

1. 출력은 **한 장짜리 가로 콘티 시트 이미지 프롬프트** — `aspect_ratio: "3:2"` (≈2048×1360).
2. 배경 = **밝은 크림/아이보리** (예 `#F4F1EA`), 얇은 회색 셀 구분선. (V2의 다크 톤과 정반대)
3. 텍스트 = **영어 + 한국어만. 일본어 문자 금지.**
4. **상단 타이틀바 1줄** + **N컷 그리드** (셀마다 원형 번호 ①②③…).
5. 각 셀 = **상단 포토(또는 프로젝트 아트스타일) 썸네일** + 하단 **3줄 메타**:
   - `ACTION:` 한국어 동작/연출
   - `CAMERA:` 영어 카메라 용어 (wide low-angle / medium tracking / tight close-up / macro dewy / OTS / two-shot / hero / fixed product close-up …)
   - `DIALOGUE:` 한국어 대사「…」 또는 `(없음)`
6. **마지막 컷 = 제품 + 슬로건 키비주얼** (제품 히어로샷에 슬로건 오버레이).
7. **캐릭터·배경·제품 = 전 컷 동일 디자인** (마스터 시트 기준). ← V1의 핵심 가치.
8. **오디오 정책: 배경음악 없음(NO BGM)** — 디렉터 노트에 명시. 셀에는 DIALOGUE만.

---

## 컷 수 로직 (러닝타임 → 그리드)

| 러닝타임 | 기본 컷 수 | 그리드 | 컷당 평균 |
|---|---|---|---|
| 6~8초 | 6컷 | 2×3 | ~1.2s |
| 10~12초 | 9컷 | 3×3 | ~1.2s |
| **15초** | **12컷** | **3×4** | **~1.25s** ← 기본 |
| 20~30초 | 16컷 | 4×4 | ~1.5s |

- 컷이 더 필요하면 셀을 늘리되 **셀당 텍스트 3줄 한도**는 유지(과밀=글자 깨짐).
- 내러티브는 **선형(линейный) 아크**로: 설정 → 갈등/고조 → 제품 → 해소 → 슬로건.
  (들결 예: 도착 → 더위·탈진 → 할머니 호출 → 제품 리빌 → 음용 → 시원함 → 함께 마심 → 히어로 → 슬로건)

---

## 이미지 생성 — ChatGPT / Codex 내장 방식 우선

- 사용자 요청 명칭: ChatGPT Image 2.5. 실제 도구/UI가 모델 버전을 표시할 때만 해당 버전을 기록한다. 모델 선택 인자가 없으면 임의 model 값을 만들거나 2.5 사용을 단정하지 않는다.
- 기본 경로는 Codex `image_gen` 내장 도구. 현재 imagegen 스킬을 읽고 실제 노출된 스키마만 사용한다. API 키를 요구하거나 Higgsfield로 자동 전환하지 않는다.
- 사용자가 브라우저 방식 또는 두 방식 비교를 요청하면 제공된 ChatGPT 대화에서 브라우저 제어로 생성한다. 기존 생성 중 작업은 중단하지 않고 완료 후 요청한다. 생성 완료를 확인하고 다운로드한 원본을 프로젝트에 보존한다.
- 먼저 기존 자산을 컷에 배치하고 필요한 이미지에 한해 생성한다. 사용자가 HTML/오디오 동기화 콘티를 요청하면 한 장 시트 대신 또는 함께 로컬 HTML 검수 보드를 만들 수 있다. 대사·한글 메타는 HTML로 정확하게 조판한다.
- 시트의 기본 비율은 3:2. 개별 세로 광고 자산은 9:16 등 실제 영상 비율을 프롬프트에 지정한다. 내장 도구가 받지 않는 quality/resolution/medias 파라미터를 보내지 않는다.
- 참조 이미지는 먼저 확인하고 지원되는 referenced_image_paths 또는 최근 이미지 참조로 전달한다. 캐릭터·제품·공간의 유지 조건을 명시한다.
- 실존 인물의 콜라보, 실제 이벤트, 매출, 앱 화면 등의 증빙은 생성 이미지로 대체하지 않는다. 콘셉트 이미지와 실제 자료를 구분한다.
- 생성 원본, 프롬프트, 생성 경로(내장/브라우저), 사용 컷을 프로젝트에 기록한다. 사용자가 지정한 기존 이미지를 새 생성물보다 우선 반영한다.
- Higgsfield 영상 생성은 스토리보드 검수 후 사용자가 승인한 범위에서 진행한다. 내장/ChatGPT 사용량의 정확한 차감 수치는 확인되지 않으면 단정하지 않는다.

---

## 프롬프트 템플릿 (복붙용, 빈칸만 채움)

```
You are a commercial director and storyboard artist. Generate ONE single horizontal AD STORYBOARD SHEET (콘티) that lays out an entire spot at a glance, on a light cream/ivory editorial background with thin grey cell borders.

[SPOT]
Title bar (top, one line): [브랜드/제품]「[제품명]」광고 콘티 — [러닝타임] / [N]컷 ([안 이름]: [컨셉])
Art style: [photoreal cinematic | 프로젝트 아트스타일], warm natural light, consistent grade across every cell
Total cuts: [N]  →  grid [행]×[열], circled numbers ①②③… in top-left of each cell

[LOCKED DESIGN — identical in every cell]
Character(s): [이름/외형/의상 — 마스터 시트 기준 고정]
Product: [제품 실루엣/라벨/색 — 고정]
World/location: [배경 톤]

[CELLS — each = thumbnail on top + 3 metadata lines below]
①  ACTION: [동작]      CAMERA: [영문 카메라]   DIALOGUE: 「[대사]」 / (없음)
②  ACTION: …           CAMERA: …               DIALOGUE: …
③ … ④ … ⑤ … ⑥ … ⑦ … ⑧ … ⑨ … ⑩ … ⑪ …
⑫  ACTION: 제품 + 슬로건 키비주얼   CAMERA: fixed product close-up   DIALOGUE: 화면자막「[슬로건]」
    → final cell: product hero shot with slogan overlay "[슬로건]"

[STYLE RULES]
- One flat planning sheet, light cream background, thin grey gridlines, circled cut numbers.
- Each cell thumbnail = a different shot/angle, but SAME character/product/world design throughout.
- Printed text = title bar + per-cell ACTION/CAMERA/DIALOGUE labels only. Korean action & dialogue, English camera terms. NO Japanese, NO hex codes, NO watermark, NO real brand logos.
- Audio policy NO BGM (note in sheet if a director's line is shown).
- Photoreal commercial look (unless an art style is specified).
```

---

## 산출 후

1. 결과 위젯 확인(자동 폴링 — 재폴링 금지).
2. 전체 아크/일관성 OK면 → **핵심 컷만 골라 `storyboard-v2`로 정밀 분해** 후 Seedance로.
3. 수정은 해당 셀만 좁혀서 재생성(전체 재생성 지양).

## 안티-페일 체크리스트 (핸드오프 전 묵시 점검)
```
✓ 한 장 가로 3:2, 밝은 크림 배경, 회색 셀 구분선?
✓ 상단 타이틀바 1줄 + 원형 번호 ①②③…?
✓ 셀당 텍스트 = ACTION(KOR)/CAMERA(ENG)/DIALOGUE(KOR) 3줄만? 과밀 없음?
✓ 캐릭터/제품/배경 디자인이 전 컷 동일?
✓ 마지막 컷 = 제품+슬로건 키비주얼?
✓ 일본어 0, 워터마크 0, 실제 브랜드 로고 0, NO BGM 정책 반영?
```
하나라도 실패면 수정 후 산출.
