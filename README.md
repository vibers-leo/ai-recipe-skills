# AI 레시피 수강생용 스킬

교재 9편에서 쓰는 개인 스킬과 공식 플러그인 안내를 모았어요. 처음이라면 02편의 첫 요청으로 광고 콘티를 만들어 보세요.

## 시작하기

1. 초대받은 GitHub 계정으로 접속한 뒤 **Code → Download ZIP**을 눌러 압축을 풀어요.
2. 원하는 스킬 폴더 하나를 참조 이미지와 함께 통째로 복사해요. 실습 프로젝트 기준으로 Codex는 `.agents/skills/`, Claude Code는 `.claude/skills/` 아래에 놓아요. 예를 들어 Codex에서 콘티를 연습할 때는 `.agents/skills/storyboard-v1/SKILL.md`가 보여야 해요.
3. 그 프로젝트에서 새 대화를 열고 아래 첫 요청을 입력해요. 설치 없이 맛보려면 해당 폴더의 SKILL.md와 필요한 참조 자료를 대화에 첨부하고 같은 요청을 넣어도 돼요.

## 편별 바로가기

| 교재 | 스킬 또는 공식 플러그인 | 첫 요청 |
|---|---|---|
| 01. AI 인플루언서 만들기 | [master-sheet-v2](skills/master-sheet-v2/) | master-sheet-v2로 하루의 기준 시트를 설계해 줘. 첨부 이미지를 기준으로 정면, 3/4, 측면, 전신에 같은 눈·머리·셔츠가 유지되게 해 줘. 먼저 이미지 생성용 요청문과 패널 배치만 보여 줘. |
| 02. AI로 숏폼 광고 만들기 | [storyboard-v1](skills/storyboard-v1/) → [storyboard-v2](skills/storyboard-v2/) | storyboard-v1으로 15초 카페 광고 한 편의 콘티를 설계해 줘. 각 컷의 화면·동작·대사를 표시해 줘. 내가 고른 컷은 이어서 storyboard-v2로 시작과 끝 프레임, 카메라 움직임을 나눠 줘. 이번에는 설계 요청문까지만 작성해 줘. |
| 03. AI로 마케팅 자동화하기 | [ops-content-calendar](skills/ops-content-calendar/) | ops-content-calendar를 참고해 다음 7일의 카페 홍보 초안을 만들어 줘. 인스타그램과 스레드의 문구를 나누고, 각 행에 날짜·채널·소재·문구·검토 상태를 넣어 줘. 결과는 대화 안의 표로만 보여 줘. |
| 04. AI로 마케팅 홈페이지 만들기 | [vibers-design](skills/vibers-design/) → [Sites](plugins/) | vibers-design의 LIGHT_GREEN을 참고해 50+AI 소개 화면과 커뮤니티 홈의 글자·버튼·간격 기준을 정해 줘. 이어 Sites 대화에 붙여 넣을 제작 요청문도 써 줘. 소개에서 커뮤니티로 이동하는 버튼과 모바일 하단 메뉴를 포함해 줘. |
| 05. AI로 외주용역 홈페이지 만들기 | [final-state-coding](skills/final-state-coding/) | final-state-coding으로 이 외주 홈페이지의 완료 조건을 정리해 줘. 방문자가 문의를 남기고 담당자가 확인하는 장면을 중심으로 화면·저장·인계 항목마다 확인 방법과 증거를 하나씩 붙여 줘. 합의 전 기능은 별도로 적어 줘. |
| 06. AI로 다양한 서비스 MCP 연결하기 | [plugin-management](plugins/) | plugin-management로 브랜드 자료를 조회할 수 있는 연결 후보를 확인해 줘. 현재 사용 가능한 도구, 필요한 권한, 읽기 작업 하나를 표로 보여 줘. 이번에는 조회와 설명까지만 해 줘. |
| 07. AI로 제안서 만들고 수정하기 | [rfp-analyzer](skills/rfp-analyzer/) → [proposal-writer](skills/proposal-writer/) | rfp-analyzer로 첨부한 교육사업 제안요청서의 필수 제출물과 평가 항목을 정리해 줘. proposal-writer로 그 표에 맞는 목차와 페이지별 핵심 문장을 써 줘. 실적 근거가 없는 칸은 자료 요청으로 남겨 줘. |
| 08. MCP와 API 연결하기 — Higgsfield 실습 | [Higgsfield](plugins/) | higgsfield 스킬로 hero-shot 프리셋의 용도와 필요한 입력을 찾아 줘. 지금은 목록과 안내만 확인하고, 내 제품 사진을 어느 단계에 넣을지 알려 줘. |
| 09. 50+AI로 생활 질문 만들고 경험 나누기 | [haeyo-tone](skills/haeyo-tone/) | haeyo-tone으로 이 버튼과 안내를 다듬어 줘. 버튼 원문은 “저장”, 안내 원문은 “완료”야. 체험판은 같은 브라우저에서만 초안을 다시 열 수 있어. 처음 쓰는 사람에게 저장 위치와 다음 행동이 보이게 각각 한 문장으로 써 줘. |

주간 콘텐츠 캘린더는 교재 과제로 새로 구성한 수강생용 버전이에요. 공식 플러그인의 설치와 계정 연결은 [플러그인 안내](plugins/)에서 확인하세요.
