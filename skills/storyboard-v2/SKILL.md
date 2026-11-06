---
name: storyboard-v2
description: "스토리보드 V2 — '한 컷' 하나를 여러 앵글로 잘게 쪼개 초별 START/END 프레임과 나레이션·효과음(SFX)까지 한 장에 설계하는 정밀 분해 시트 스킬. 컷 하나를 S1~S6 멀티샷으로 분해하고, 샷마다 시작/끝 프레임·카메라무브·연출·대사·인클립 SFX를 채운 다크 네이비 콘티 시트(이미지 생성용 프롬프트)를 출력한다. 배경음악 없음(NO BGM), 나레이션+SFX만. Use this skill whenever the user wants to break ONE cut/scene down shot-by-shot in detail — 컷 분해, 한 컷 디테일하게, 샷 브레이크다운, shot breakdown, start/end frame 콘티, 초별 콘티, 멀티앵글 분해, 스타트엔드 프레임, 디테일 스토리보드, 씬 정밀 콘티. 트리거: '이 컷 쪼개줘 · 앵글별로 · 초 단위로 · START END 프레임 줘 · 디테일하게 짜줘'. ⚠️ 광고/영상 '한 편 전체'를 한눈에 정리하는 건 V2가 아니라 storyboard-v1을 쓴다. 한 컷 정밀 구현 = V2(이 스킬), 전체 흐름 한 장 = V1."
metadata:
  version: "2.2.0"
---

# Storyboard V2 — 단일 컷 정밀 분해 시트 (멀티앵글 / 초별 START·END)

**한 컷**을 여러 앵글로 분해해, 샷마다 **시작/끝 프레임 + 카메라무브 + 연출 + 대사 + SFX**를
한 장에 담는 **다크 네이비 콘티 시트** 프롬프트를 만든다. 장면을 디테일하게 구현(재화)할 때 쓴다.

검증 예시: `assets/reference-cut-breakdown.png` (CUT03「최후의 수호대 / The Last Guardian」
90s 특촬 톤, S1~S6 분해 · START/END · 나레이션·SFX · DIRECTOR'S INTENT/TRANSITION).
이 레이아웃·컬럼·톤을 기준선으로 삼는다.

---

## V1 vs V2 — 무엇을 쓰나 (먼저 확인)

| | **V1 (`storyboard-v1`)** | **V2 (이 스킬)** |
|---|---|---|
| 담는 범위 | 광고/영상 **한 편 전체** | **한 컷** 하나 |
| 단위 | 1컷 = 1셀 (①…⑫) | 1컷 = **6샷 분해 (S1~S6)** |
| 프레임 | 컷당 썸네일 1장 | 샷마다 **START + END 2프레임** |
| 오디오 | DIALOGUE 한 줄 | **나레이션·대사 + 인클립 SFX** 정밀 |
| 배경톤 | 밝은 크림 | **다크 네이비 `#0A0A12`** |

→ "이 컷 디테일하게/앵글별로 쪼개줘" = **V2**. "광고 전체 콘티" = **V1**.
워크플로: `master-sheet` → `storyboard-v1`(전체) → **V2(핵심 컷 정밀)** → Seedance 2.0 (start/end 프레임 체이닝).

---

## 핵심 규칙 (STRICT)

1. 출력은 **한 장 가로 콘티 시트 이미지 프롬프트** — `aspect_ratio: "3:2"` (≈2048×1360).
2. 배경 **`#0A0A12`** (다크 네이비-블랙), 선명한 흰색 텍스트, 얇은 흰색 구분선.
3. 텍스트 = **영어 + 한국어만. 일본어 문자 금지.**
4. **멀티샷 앵글 필수**: 모든 샷은 서로 다른 앵글/무브먼트. **기본 6샷(S1~S6)**, 컷 길이 따라 6~8.
   (WIDE / REVERSE DOLLY / ECU / LOW ANGLE / OTS / DUTCH TILT·HERO POSE / HIGH ANGLE /
   LATERAL TRACK / WHIP-PAN / TOP-DOWN / MIRROR·REFLECTION …) — **같은 앵글 반복 금지.**
5. **오디오 정책: 배경음악 없음(NO BGM). 나레이션·대사 + 효과음(SFX)만.** → MUSIC 컬럼 없음.
6. 각 샷 썸네일의 캐릭터·배경·제품 = **마스터 시트와 동일 디자인**으로 일관 유지.

---

## 시트 구조 (CUT03 기준)

**HEADER (상단 1줄):**
`CUTxx (전체영상 내 절대시간 0:26-0:39) 「제목(KOR) / Title(ENG)」 [프로젝트 아트 스타일 · NO BGM]`

**TABLE — 7 COLUMNS (얇은 흰색 구분선):**
- 컬럼 폭 예시: `8% / 22% / 22% / 14% / 16% / 11% / 7%`
- 헤더: `SHOT/TIME | START FRAME | END FRAME | CAMERA/MOVEMENT | ACTION/DIRECTION | 나레이션·대사 | SFX`
- **기본 6행 (S1~S6)** — 각 행:
  - `SHOT/TIME`: `S1` + **컷 내 상대시간** `00:00-00:02` (절대시간 아님)
  - `START FRAME` / `END FRAME`: 시작·끝 프레임을 각각 구체 묘사 (샷의 동작 시작점→끝점)
  - `CAMERA/MOVEMENT`: 그 샷만의 고유 앵글/무브
  - `ACTION/DIRECTION`: 연출·동작 (한국어 간결)
  - `나레이션·대사`: 한국어 (없으면 `—`) — 기본은 대부분 `—`, 결정적 1줄만
  - `SFX`: 인클립 효과음 (한국어, 예 "잔해 부스러기·바람 / 저음 긴장 / 금속 뽑는 챙—")

**FOOTER (하단 2칸):**
- 좌 `DIRECTOR'S INTENT:` 연출 의도(예: 패배→회상→결의→제품 전환) + **오디오 정책 명시(NO BGM — 대사 1줄+SFX만, 나레이션 삭제)**
- 우 `TRANSITION:` 다음 컷으로의 **매치컷/전환 설계** + 전환 썸네일 2컷(예: 캔 햇빛 글린트 → 변신 트리거)

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
You are a film director and storyboard artist. Generate ONE single horizontal SHOT-BREAKDOWN SHEET for a SINGLE CUT, on a dark navy-black background (#0A0A12) with crisp white text and thin white dividers.

[HEADER one line]
CUT[xx] ([절대시간 0:26-0:39]) 「[제목 KOR] / [Title ENG]」 [아트 스타일] · NO BGM

[LOCKED DESIGN — identical in every shot]
Character(s): [외형/의상 — 마스터 시트 기준]
World/props/product: [고정 요소]

[TABLE — 7 columns, 6 rows S1–S6]
columns: SHOT/TIME | START FRAME | END FRAME | CAMERA/MOVEMENT | ACTION/DIRECTION | 나레이션·대사 | SFX
S1  00:00-00:02 | START:[프레임] | END:[프레임] | WIDE         | [연출] | — | [SFX]
S2  00:02-00:05 | START:…        | END:…        | REVERSE DOLLY| [연출] | — | [SFX]
S3  00:05-00:07 | …              | …            | ECU          | [연출] | — | [SFX]
S4  00:07-00:09 | …              | …            | LOW ANGLE    | [연출] | — | [SFX]
S5  00:09-00:11 | …              | …            | OTS          | [연출] | — | [SFX]
S6  00:11-00:13 | …              | …            | DUTCH TILT / HERO POSE | [연출] | 「[결정적 대사 1줄]」 | [SFX]

[FOOTER — 2 boxes]
DIRECTOR'S INTENT: [의도 흐름]. NO BGM — hero line ×1 + SFX only (narration removed).
TRANSITION: [다음 컷 매치컷 설계] (+ 2 small transition thumbnails)

[STYLE RULES]
- One flat sheet, dark navy #0A0A12, white text, thin white grid. Each shot = a DIFFERENT angle/move, no repeats.
- Same character/world design in every thumbnail (master-sheet consistency).
- Per-shot times are RELATIVE to the cut (00:00–). Audio = narration/dialogue + in-clip SFX, NO music column.
- English + Korean only. NO Japanese, NO hex codes crammed in, NO watermark.
```

---

## 사용법
입력 = (1) 컷 내용/비트, (2) 캐릭터·배경 마스터 시트(또는 디자인 설명), (3) 아트 스타일.
컷이 여러 개면 **컷별 시트 1장씩**. 한 시퀀스를 쪼갤 땐 **컷당 기본 6개의 서로 다른 앵글 샷**.
Seedance 2.0로 넘길 때 각 샷의 START→END를 start_image/end_image 체이닝 소스로 그대로 활용.
