# vyxworks.github.io

VyxWorks 스튜디오 사이트 + 제품 랜딩(Opaline · CarPin) + 법적 고지.
빌드 도구 없는 정적 HTML/CSS, GitHub Pages 배포.

## UI 작업 전 반드시

**`DESIGN.md` 를 먼저 읽는다.** 색·타이포·간격·컴포넌트 규칙과
현재 코드의 이탈 지점(Known Gaps)이 거기 있다.

토큰 실제값은 `assets/css/base.css` 의 `:root` 가 정답이다 —
문서와 CSS 가 어긋나면 CSS 를 따르고 DESIGN.md 를 고친다.

## 구조

- `index.html` — 스튜디오 홈 (⚠️ base.css 미로드, 전부 인라인 하드코딩)
- `opaline/`, `carpin/` — 제품 랜딩 + privacy/terms 다국어(ko·en·ja·zh-Hans)
- `_partials/` — 공용 내비·푸터 마크업
- `assets/css/base.css` — 공용 토큰 + 셸. `opaline.css` 가 액센트만 override
