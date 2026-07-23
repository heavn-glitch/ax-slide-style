# 컴포넌트 레퍼런스

모든 슬라이드는 아래 골격을 따른다.

```html
<section class="slide bg-소프트 dot-texture">
  <div class="slide-inner">
    <p class="meta">EYEBROW</p>
    <h2>핵심 메시지 <span class="accent">강조</span></h2>
    <!-- 본문 템플릿 하나 -->
  </div>
  <div class="source-line">Source: …</div>   <!-- 필요 시 -->
  <div class="slide-no">N</div>
</section>
```

## 개념 카드 (grid-3 / grid-4)
```html
<div class="grid-3">
  <div class="cell">
    <span class="icon-box"><i data-lucide="repeat"></i></span>
    <h3>소제목</h3>
    <p>한 문장.</p>
  </div>
  ...
</div>
```
아이콘은 lucide 이름(`repeat`, `alert-triangle`, `layers`, `shield-check`, `send` 등).

## 비교표 (mini-table)
```html
<div class="mini-table row-3">
  <div class="head">구분</div><div class="head">A</div><div class="head">B</div>
  <div class="head">기준</div><div>값</div><div>값</div>
</div>
```
열 개수에 맞춰 `row-3` 또는 `row-4`. 첫 열/헤더 행에 `.head`.

## 단계 (timeline)
```html
<div class="timeline">
  <div class="timeline-step"><p class="meta">01</p><div><h3>제목</h3><p>한 문장.</p></div></div>
  ... (5개)
</div>
```

## 프롬프트/코드
```html
<div class="code-block"><span class="prompt-label">Prompt · 설명</span>여기에 프롬프트 원문…</div>
```
`.compact`를 붙이면 긴 원문용 작은 폰트.

## 강조 콜아웃
```html
<div class="callout"><p><strong>중요:</strong> 한 문장 결론.</p></div>
```

## 간지 (divider)
```html
<section class="slide bg-hero dot-texture">
  <div class="center-stage"><div>
    <p class="meta">라벨</p>
    <p class="quote">단어 <span class="accent">하나</span></p>
  </div></div>
  <div class="slide-no">N</div>
</section>
```
