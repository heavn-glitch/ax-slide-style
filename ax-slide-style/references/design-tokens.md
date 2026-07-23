# AX Skillaton 덱 — 디자인·논리 표현 시스템 분석

원본: `AX Skillaton | Codex로 업무 자동화 Skill 만들기` (47 슬라이드)

---

## 1. 디자인 토큰

### 색상 (CSS variables)
| 토큰 | 값 | 용도 |
|---|---|---|
| `--ink` | `#0a0908` | 기본 배경 |
| `--ink-soft` | `#15130f` | 그라데이션 배경 |
| `--ink-rise` | `#1f1c16` | 배경 하이라이트 |
| `--bone` | `#f0ede5` | 제목/주요 텍스트 |
| `--bone-dim` | `#c9c5bc` | 본문 텍스트 |
| `--bone-mute` | `#7a766e` | 눈썹라벨·출처·페이지번호 |
| `--card-bone` | `#e6dfd3` | 라이트 카드 |
| `--ember` | `#eba8ff` | 액센트(핑크/퍼플) |
| `--ember-deep` | `#c873e0` | 액센트 딥 |
| `--cyan-glow` | `#00c2ff` | 보조 글로우 |

### 폰트
- 본문: `"Pretendard Variable", "Pretendard", system-ui, sans-serif`
- 코드: `ui-monospace, SFMono-Regular, Menlo, Consolas, monospace`
- 한글 줄바꿈: `word-break: keep-all; overflow-wrap: normal; line-break: strict`
- `-webkit-font-smoothing: antialiased`

### 타이포 스케일
| 요소 | 크기 | 굵기 | 비고 |
|---|---|---|---|
| h1 (히어로) | `clamp(74px, 8.4vw, 136px)` | 650 | line 1.02 |
| h2 (제목=핵심메시지) | `clamp(56px, 5.8vw, 92px)` | 650 | line 1.08 |
| h3 (소제목) | 35px | 650 | line 1.22 |
| `.lead` (리드문) | 32px | 450 | `--bone-dim`, line 1.52 |
| `.cell p` (본문) | 26px | — | `--bone-dim`, line 1.45 |
| `.meta` (눈썹라벨) | 19px | 700 | 대문자, letter-spacing 0.08em, `--bone-mute` |
| `.code-block` | 27px | — | mono, `--ember` 25% 보더 |
| `.footnote` | 21px | — | `--bone-mute` |
| `.source-line` | 17px | — | 좌하단 절대배치 |
| `.slide-no` | 18px | 700 | 우하단, tabular-nums |

### 레이아웃
- `.slide`: `100vw x min-height 100vh`, padding `34px 56px`, `scroll-snap-align: start`
- `--safe-w: min(100%, 1760px)` — 16:9 프로젝터 프레임(뒷줄 가독성 목표)
- `.slide-inner`: 상단 여백 `clamp(72px, 8vh, 96px)`
- 고정 요소: 좌하단 출처(`.source-line`), 우하단 페이지번호(`.slide-no`)

### 배경 4모드 (다크/라이트 교차 리듬)
| 클래스 | 사용 수 | 스타일 |
|---|---|---|
| `bg-dark` | 18 | `linear-gradient(135deg, ink→ink-soft)` |
| `bg-light` | 16 | `radial(ember 16%) + bone` (텍스트 반전 `--ink`) |
| `bg-soft` | 7 | `radial(ember) + linear(ink-soft→ink)` |
| `bg-hero` | 5 | 이중 radial(ember/ember-deep) + 3-stop linear |

### 핵심 컴포넌트
- `.icon-box` — 48x48, `--ember` 아이콘, 앰버 5% 배경 + 25% 보더 (lucide 아이콘)
- `.cell` — 그리드 카드, min-height 196px, padding 34px
- `.mini-table` — 1px gap 그리드로 만든 비교표
- `.code-block` — 앰버 보더 다크 박스, 프롬프트 원문 노출
- `.callout` — 앰버 틴트 강조 박스 (padding 42px)
- `.timeline-step` — 번호형 단계 카드 (min-height 286px)
- `.grid-3` / `.grid-4` — 개념 분할 그리드
- `.prompt-label` — 대문자·800·앰버, 프롬프트 라벨

---

## 2. 슬라이드 골격 (고정 패턴)

```
<section class="slide bg-* dot-texture">
  <div class="slide-inner">
    <p class="meta">EYEBROW LABEL</p>            ← 영문 카테고리 태그
    <h2>핵심 메시지 <span class="accent">강조</span></h2>  ← 제목=결론
    <div class="grid-3 | mini-table | code-block ...">  ← 본문 템플릿
      ...한 포인트 = 한 문장...
    </div>
  </div>
  <div class="source-line">Source: ...</div>     ← 근거
  <div class="slide-no">13</div>                  ← 페이지번호
</section>
```

---

## 3. 논리·표현 규칙 (스킬화 대상)

1. 1페이지 1메시지 — 한 장에 주장 하나. 본문은 포인트당 한 문장, 문단 금지.
2. 제목 = 키 메시지 — h2가 결론. 펀치라인만 `<span class="accent">`로 앰버 강조.
3. 눈썹라벨 분리 — 상단 영문 카테고리는 위치표식일 뿐, 메시지와 시각적으로 분리.
4. 간지 슬라이드 — 섹션 전환 시 큰 단어 하나(`TINKERING`, `unlearn / open-mind`)로 호흡 조절.
5. 반복 구조 템플릿 6종
   - 3·4분할 개념카드 (아이콘 + 소제목 + 한 문장)
   - 비교표 (`mini-table`)
   - 번호형 단계 (01–05)
   - 프롬프트/코드 블록 (원문 노출)
   - 콜아웃 (`중요` 강조)
   - 타임라인
6. 모든 주장에 출처 — 하단 `Source:` 라인.
7. 전체 흐름 = why → what → how → so-what
   문제(반복 비용) → 정의(Skill이란) → 해부(폴더 구조) → 방법(5단계) → 실증(Live Demo) → 안전 → 확장(제품화)
8. 병렬 구조 — 분할 항목은 문법까지 평행하게 (반복 설명 / 반복 실수 / 반복 맥락).
9. 실증 우선 — 개념 설명 뒤 반드시 실제 프롬프트·실습 산출물로 착지.

---

## 4. 스킬화 시 캡처해야 할 3층
- 비주얼 층: 위 CSS 토큰 + 컴포넌트 라이브러리 (그대로 재사용 가능)
- 골격 층: eyebrow → title(accent) → 템플릿 본문 → source/page 고정 구조
- 논리 층: 1슬라이드 1메시지, 제목=결론, why→what→how→so-what 흐름, 문장 1개 원칙
