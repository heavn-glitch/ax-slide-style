# AX Slide Style

AX Skillaton의 디자인 토큰과 논리 표현 규칙으로 단일 HTML 발표자료를 만드는 Codex Skill입니다.

## 주요 원칙

- 한 슬라이드에 한 메시지만 배치
- 제목을 주제가 아닌 결론으로 작성
- `why → what → how → so-what` 흐름으로 구성
- 개념 카드, 비교표, 단계, 프롬프트, 콜아웃, 간지 템플릿 제공
- 외부 사실과 인용에는 `Source:` 표기

## 설치

Codex에서 `$skill-installer`에게 이 저장소의 `ax-slide-style` 폴더를 설치하도록 요청합니다.

```text
$skill-installer로 https://github.com/heavn-glitch/ax-slide-style/tree/main/ax-slide-style 을 설치해줘.
```

또는 `ax-slide-style` 폴더를 직접 복사합니다.

- 개인용: `$HOME/.agents/skills/ax-slide-style`
- 프로젝트용: `<project>/.agents/skills/ax-slide-style`

Skill이 보이지 않으면 Codex를 다시 시작합니다.

## 사용 예시

```text
$ax-slide-style을 사용해 이 기획안을 12장 HTML 발표자료로 만들어줘.
대상은 비개발자이고 발표 시간은 20분이야.
```

## 산출물

기본 산출물은 CSS가 인라인된 단일 `deck.html`입니다. Pretendard와 lucide는 CDN을 사용하므로 완전한 오프라인 실행이 필요하면 로컬 폰트와 인라인 SVG로 교체해야 합니다.
