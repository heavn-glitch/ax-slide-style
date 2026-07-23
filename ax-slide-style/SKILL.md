---
name: ax-slide-style
description: Use this skill when the user wants to create an HTML slide deck (presentation, 발표자료, 슬라이드) in the "AX Skillaton" editorial keynote style — a dark, Pretendard-based, full-screen scroll deck with an ember/pink accent, eyebrow-label → title-as-message structure, and one message per slide. Trigger when the user asks to build slides, a deck, or a presentation and wants this specific look, or references this style/template. Do not use for .pptx output, for spreadsheets, or for plain documents.
---

# AX Slide Style — HTML 키노트 생성기

이 스킬은 "AX Skillaton" 덱의 디자인과 논리 표현 방식을 그대로 재현하는 **단일 파일 HTML 슬라이드**를 만든다. 스크롤 스냅 방식의 풀스크린 슬라이드이며, 다크 테마 + Pretendard + 앰버(핑크) 액센트를 쓴다.

## 언제 켜지나
- "이 스타일로 발표자료/슬라이드/덱 만들어줘", "AX Skillaton 스타일 슬라이드"
- 다크 테마 편집형 키노트 HTML을 원할 때

## 언제 안 켜지나
- PowerPoint(.pptx), 스프레드시트, 일반 문서가 산출물일 때
- 라이트/코퍼레이트 톤 등 다른 비주얼을 원할 때

## 입력
- 발표 주제와 목적, 대상 청중
- 각 섹션의 핵심 메시지(장별 결론 한 줄씩)
- (선택) 실제 프롬프트·표·비교 항목·출처

## 출력
- 단일 `deck.html` 1개. 핵심 CSS는 인라인하고 Pretendard·lucide는 CDN에서 불러온다.
- 완전한 오프라인 산출물이 필요하면 CDN 의존성을 로컬 폰트와 인라인 SVG로 바꾼다.

## Workflow
1. **논리부터 잡는다.** 발표를 why → what → how → so-what 흐름으로 배열하고, 각 슬라이드의 **결론 한 문장**을 먼저 확정한다. (references/logic-rules.md)
2. **장별 템플릿을 고른다.** 내용 유형에 맞춰 grid / mini-table / timeline / code-block / callout / divider 중 하나를 매핑한다. (references/components.md)
3. **골격을 채운다.** 각 슬라이드는 `meta`(눈썹라벨) → `h2`(제목=메시지, 펀치라인만 `.accent`) → 본문 템플릿 → `source-line`/`slide-no` 순. 본문 포인트는 **한 문장**, 병렬 구조로.
4. **배경 리듬을 넣는다.** bg-dark 기본, 도입·간지는 bg-hero, 전환은 bg-soft/bg-light. 논리 전환에 맞춰 배경을 바꾼다.
5. **빌드.** CSS가 이미 인라인된 `assets/deck-template.html`을 복사해 예시 슬라이드를 실제 내용으로 교체한다. `assets/base.css`를 다시 삽입하지 않는다. 끝의 `lucide.createIcons()`는 유지한다.
6. **검수.** 브라우저로 렌더해 (a) 한 장에 메시지 하나인지, (b) 제목만 읽어도 논지가 서는지, (c) 출처·페이지번호가 있는지, (d) 1280×720에서 잘림·겹침이 없는지 확인한다. PDF가 필요하면 인쇄 미리보기에서 한 장당 한 페이지인지 확인한다.

## 디자인 토큰 (요약; 전체는 references/design-tokens.md)
- 색: `--ink #0a0908`(배경) · `--bone #f0ede5`(제목) · `--bone-dim #c9c5bc`(본문) · `--bone-mute #7a766e`(라벨/출처) · `--ember #eba8ff`(액센트)
- 폰트: Pretendard Variable, 코드 ui-monospace, `word-break:keep-all`
- 스케일: h2 제목 `clamp(56–92px)`/650, 본문 26px, 눈썹라벨 19px·대문자·자간 0.08em
- 프레임: 슬라이드 100vw×100vh, `--safe-w 1760px`, 좌하단 출처·우하단 번호

## 핵심 논리 규칙 (전체는 references/logic-rules.md)
1. 1페이지 1메시지 2. 제목 = 결론 3. 펀치라인만 액센트(장당 1회)
4. 눈썹라벨은 위치표식(메시지 아님) 5. 본문 한 문장·병렬 6. 모든 인용에 Source
7. 흐름 why→what→how→so-what, 섹션 사이 간지 슬라이드

## Stop Conditions
- 장별 핵심 메시지가 정해지지 않았으면 추측하지 말고 사용자에게 확인한다.
- 실제 수치·인용의 출처가 없으면 지어내지 말고 "확인 필요"로 표시한다.
- 다른 비주얼 톤을 원하면 이 스킬을 쓰지 않는다.

## Files
- `assets/base.css` — 재현용 핵심 스타일 시스템
- `assets/deck-template.html` — 6가지 슬라이드 유형 예시가 든 자립형 템플릿
- `references/design-tokens.md` — 색·폰트·스케일·컴포넌트 상세
- `references/logic-rules.md` — 논리 전개·표현 규칙, 콘텐츠→템플릿 매핑
- `references/components.md` — 컴포넌트별 HTML 스니펫
