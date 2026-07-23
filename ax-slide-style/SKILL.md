---
name: ax-slide-style
description: Create HTML or PowerPoint (.pptx) slide decks in the "AX Skillaton" editorial keynote style: dark Pretendard typography, ember/pink accents, eyebrow label → title-as-message structure, and one message per slide. Use when the user asks for a presentation, 발표자료, 슬라이드, deck, HTML deck, PPT, or PowerPoint in this specific style. Honor an explicit HTML/PPTX choice; when the format is ambiguous, ask which output they want before building.
---

# AX Slide Style

AX Skillaton의 디자인과 논리 표현을 유지하면서 사용자가 선택한 형식으로 발표자료를 만든다.

## 출력 형식 결정

1. 사용자가 `HTML`, `.html`, 웹 공유를 명시하면 **HTML**로 만든다.
2. 사용자가 `PPT`, `PowerPoint`, `.pptx`, 편집 가능한 파일을 명시하면 **PPTX**로 만든다.
3. 형식이 불명확하면 제작 전에 “HTML과 PPTX 중 어떤 형식이 필요한가요?”라고 한 번만 묻는다.
4. 두 형식을 모두 요청하면 먼저 공통 슬라이드 아웃라인을 확정하고 HTML과 PPTX를 각각 만든다.

## 공통 입력

- 발표 주제·목적·대상 청중
- 각 슬라이드의 결론 한 문장
- 선택 사항: 실제 프롬프트, 표, 비교 항목, 수치, 인용, 출처

## 공통 논리 Workflow

1. 발표를 `why → what → how → so-what`으로 배열한다.
2. 각 슬라이드의 결론 한 문장을 먼저 확정한다.
3. 내용 유형을 hero / divider / grid / table / timeline / code / callout 중 하나에 매핑한다.
4. `eyebrow → title(결론) → 본문 → source/page` 골격을 유지한다.
5. 본문 포인트를 한 문장으로 쓰고 병렬 구조를 맞춘다.
6. 외부 사실·수치·인용에 `Source:`를 붙인다.
7. 제목에서 펀치라인 한 곳만 앰버로 강조한다.

상세 논리와 컴포넌트는 `references/logic-rules.md`, `references/components.md`를 읽는다.

## HTML 경로

1. `assets/deck-template.html`을 복사한다.
2. 예시 슬라이드를 실제 내용으로 교체한다.
3. 이미 인라인된 CSS를 유지하고 `assets/base.css`를 다시 삽입하지 않는다.
4. 끝의 `lucide.createIcons()`를 유지한다.
5. 단일 `deck.html`로 저장한다.
6. 브라우저에서 1280×720 기준 잘림·겹침·줄바꿈과 스크롤 스냅을 확인한다.
7. PDF가 필요하면 인쇄 미리보기에서 슬라이드당 한 페이지인지 확인한다.

Pretendard와 lucide는 CDN을 사용한다. 완전한 오프라인 산출물이 필요하면 로컬 폰트와 인라인 SVG로 교체한다.

## PPTX 경로

1. 현재 환경의 `Presentations` 스킬을 함께 사용하고 해당 지침을 끝까지 따른다.
2. 구현은 `Presentations` 스킬이 지정한 `@oai/artifact-tool` JavaScript 경로를 사용한다.
3. 이 스킬의 비주얼 방향을 명시적 사용자 스타일로 취급하고 다른 기본 템플릿과 섞지 않는다.
4. `references/pptx-style.md`의 16:9 레이아웃, 색, 타이포, 아키타입 규격을 적용한다.
5. 편집 가능한 도형·텍스트·표를 유지하고 최종 파일을 `deck.pptx`로 저장한다.
6. `Presentations` 스킬의 렌더링·오버플로 검사를 실행하고 모든 슬라이드를 이미지로 확인한다.
7. Pretendard가 없을 때의 대체 폰트 렌더링을 확인하되, 텍스트가 잘리면 문장을 줄이거나 레이아웃을 바꾼다.

`pptxgenjs`나 별도 PPTX 생성 라이브러리를 추가하지 않는다.

## 배경 리듬

- 기본 본문: dark
- 도입·섹션 간지: hero
- 전환·강조: soft 또는 light
- 기계적인 교차 대신 논리 전환에 맞춰 배경을 바꾼다.

## 공통 QA

- 한 슬라이드에 메시지가 하나인가?
- 제목만 읽어도 전체 논지가 이어지는가?
- 본문이 포인트당 한 문장인가?
- 강조가 슬라이드당 한 곳인가?
- 수치·인용에 출처가 있는가?
- 페이지 번호와 출처가 잘리지 않는가?
- 제목·본문·표에 겹침이나 의도하지 않은 줄바꿈이 없는가?

## Stop Conditions

- 출력 형식이 불명확하면 제작 전에 확인한다.
- 슬라이드별 핵심 메시지가 없으면 임의로 확정하지 말고 확인한다.
- 실제 수치·인용의 출처가 없으면 지어내지 말고 `확인 필요`로 표시한다.
- 사용자가 다른 비주얼 톤을 원하면 이 스킬을 적용하지 않는다.

## Files

- `assets/base.css` — HTML 핵심 스타일
- `assets/deck-template.html` — HTML 슬라이드 템플릿
- `references/design-tokens.md` — HTML 색·폰트·스케일
- `references/logic-rules.md` — 공통 논리 전개 규칙
- `references/components.md` — HTML 컴포넌트 스니펫
- `references/pptx-style.md` — PPTX 스타일·레이아웃·아키타입 규격
