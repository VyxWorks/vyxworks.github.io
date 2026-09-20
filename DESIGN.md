---
version: 1.0
name: VyxWorks-Studio
product: vyxworks.com (스튜디오 사이트 + 제품 랜딩 + 법적 고지)
platform: 정적 HTML + 순수 CSS (빌드 도구·프레임워크 없음), GitHub Pages
description: >
  이 레포에는 **두 개의 디자인 시스템**이 있다.
  (A) 셸 시스템 — 법적 고지 16개 페이지. 절제된 뉴트럴, 흰 캔버스(#FFFFFF)
  위 near-black 잉크, 시스템 폰트 한 벌, 장식 없는 1px 헤어라인.
  그림자 없이 테두리와 여백으로 위계를 만든다.
  (B) 스튜디오 시스템 — 홈과 제품 랜딩 3장(`/`, `/carpin/`, `/opaline/`).
  2026-09-20 에 Hallmark studied-DNA 로 갈라져 나왔고, 같은 날 제품 랜딩까지
  확장됐다. Geist 웹폰트, 쿨 틴트 페이퍼, 그라디언트 배경, 떠 있는 내비.
  구조는 전 페이지 공용이고 **액센트만 제품이 정한다.**
  아래 `studio-system` 블록이 정본이다.
  **두 시스템은 의도적으로 다르다.** 섞지 않는다.

source-of-truth:
  tokens: assets/css/base.css   # :root 블록이 정답이다. 이 문서는 그 해설·계약서.
  overrides: assets/css/opaline.css
  note: 값이 어긋나면 CSS 가 정답이다. 문서는 의도, CSS 는 계약.

colors:
  # ── 셸 (전 제품 공용). base.css 의 CSS 변수와 1:1 대응한다.
  #    여기 없는 색은 존재하지 않는 색이다 — 새로 만들지 말고 이 중에서 고른다. ──
  canvas:   { light: "#FFFFFF", dark: "#0C0C0D" }   # --color-bg
  ink:      { light: "#0A0A0A", dark: "#F5F6F7" }   # --color-fg
  muted:    { light: "#6B7280", dark: "#9CA3AF" }   # --color-muted (2·3차 텍스트 공용)
  surface:  { light: "#F7F7F8", dark: "#161618" }   # --color-surface
  hairline: { light: "#E5E7EB", dark: "#232326" }   # --color-border
  # ── 액센트 (제품별) ──
  accent-carpin:   "#04C98A"   # 그린. hover 시 #03B57B
  accent-carpin-fg: "#FFFFFF"
  accent-opaline:  { light: "#0A0A0A", dark: "#F5F6F7" }   # 모노크롬 = 앱 아이콘 톤
  # accent-studio 는 (A) 에서 제거됐다 — 홈은 (B) 시스템으로 이관.
  # 홈 액센트는 studio-home.colors.accent (인디고) 를 본다.

typography:
  font-sans: >
    -apple-system, BlinkMacSystemFont, "SF Pro Display", "Segoe UI", Roboto,
    "Noto Sans", "Noto Sans JP", "Noto Sans SC", sans-serif
  font-mono: '"SF Mono", Menlo, Consolas, monospace'
  hero:      { size: "clamp(36px, 6vw, 56px)", weight: 700, lineHeight: 1.08, letterSpacing: "-0.02em" }
  section-h2: { size: "clamp(28px, 5vw, 36px)", weight: 700, lineHeight: 1.2,  letterSpacing: "-0.015em" }
  card-h3:   { size: "18px", weight: 600, lineHeight: 1.4, letterSpacing: "-0.01em" }
  body:      { size: "16px", weight: 400, lineHeight: 1.7 }   # 본문·법적 고지
  body-home: { size: "16px", weight: 400, lineHeight: 1.5 }   # 홈 (디스플레이 위주 카피)
  body-sm:   { size: "14px", weight: 400, lineHeight: 1.6 }
  caption:   { size: "13px", weight: 400, lineHeight: 1.6 }
  micro:     { size: "12px", weight: 400, lineHeight: 1.5 }

layout:
  container-prose:  "720px"   # base.css --max-width. 법적 고지·본문 위주 페이지
  container-wide:   "880px"   # 홈 랜딩
  container-nav:    "960px"   # 내비/푸터 (본문보다 넓게 — 셸이 콘텐츠를 감싼다)
  gutter:           "24px"    # ≤640px 에서 20px
  nav-height:       "56px"
  spacing-scale:    [4, 8, 12, 14, 16, 20, 24, 40, 48, 80]
  breakpoint-shell: "640px"   # 셸(내비·푸터·거터) 공용. 그 외는 clamp() 로 유체 대응
  breakpoint-grid:  ["720px", "480px"]   # 다열 그리드 재배치 전용 (opaline features)

radius:
  pill: "999px"   # 버튼
  card: "12px"    # 기본 카드
  lg:   "14px"
  xl:   "16px"
  xs:   "4px"     # 코드/뱃지

# ─────────────────────────────────────────────────────────────
# (B) 스튜디오 시스템 — 홈 + 제품 랜딩. 위 (A) 와 공유하는 토큰이 없다.
#     정본: assets/css/studio-tokens.css. 이 블록은 그 해설이다.
# ─────────────────────────────────────────────────────────────
studio-system:
  applies-to: [/index.html, /carpin/index.html, /opaline/index.html]
  source: "Hallmark studied-DNA · https://www.usehallmark.com/examples/tally/"
  stamp: "macrostructure: Marquee Hero · genre: modern-minimal · nav: N5 Floating pill · footer: Ft5 Statement"
  loads:
    공통:   [assets/css/studio-tokens.css, assets/css/shell.css]
    홈:     assets/css/home.css
    제품:   assets/css/product.css
  does-not-load: assets/css/base.css   # 의도적. 셸 시스템과 캐스케이드가 섞이지 않는다.
  # shell.css 가 리셋·컨테이너·N5 내비·버튼·Ft5 푸터를 혼자 소유한다.
  # 내비 CSS 를 페이지마다 복사하면 세 벌이 갈라지므로, 새 페이지는 반드시 shell 을 쓴다.

  colors:   # OKLCH. 라이트 / 다크 쌍. 22개 대비쌍 전부 WCAG AA 통과 검증됨.
    paper:  { light: ["98.4% .005 258", "96.2% .010 258", "93.0% .015 258", "89.0% .020 258"],
              dark:  ["16.0% .018 258", "20.5% .020 258", "25.5% .022 258", "31.0% .024 258"] }
    ink:    { light: ["18.0% .030 258", "35.0% .025 258", "47.0% .020 258", "64.0% .016 258"],
              dark:  ["96.0% .008 258", "85.5% .012 258", "72.0% .016 258", "56.0% .016 258"] }
    accent:       # 홈 기본값. 제품 페이지가 :root 에서 이 토큰만 덮는다.
      { light: "54.0% .220 268", dark: "72.0% .165 268" }   # 인디고
    accent-carpin:
      { light: "50.0% .140 162", dark: "78.0% .150 162" }
      # CarPin 브랜드 그린 #04C98A = oklch(73.9% .162 162) 는 페이퍼 위에서 2.06:1 이라
      # 텍스트를 못 싣는다. 같은 색상각을 50% L 로 내려 AA 를 통과시키고(5.15:1),
      # 진짜 브랜드 그린은 --color-brand 로 남겨 상태 도트에만 쓴다.
    accent-opaline:
      { light: "18.0% .030 258", dark: "96.0% .008 258" }
      # 모노크롬 = 앱 아이콘 톤. 액센트가 잉크와 같으므로 링크와 강조는
      # 반드시 밑줄을 함께 쓴다 — 접근성 요구사항이지 스타일 선택이 아니다.
    companion: { light: "62.0% .150 145", dark: "76.0% .160 145" } # 출시 상태 표시 전용. 장식 금지.
    focus:  { light: "46.0% .220 268", dark: "80.0% .150 268" }

  typography:
    font-display: '"Geist", ui-sans-serif, system-ui, -apple-system, sans-serif'
    font-body:    '"Geist", ui-sans-serif, system-ui, -apple-system, sans-serif'
    font-mono:    '"Geist Mono", ui-monospace, "SF Mono", Menlo, Consolas, monospace'
    loaded-from:  "Google Fonts (Geist 400;500;600 + Geist Mono 400;500)"
    note: >
      Instrument Serif 는 원본에 있지만 **일부러 뺐다** — 원본은 h1 안에서
      이탤릭 강조에 쓰는데, 그게 Hallmark gate 38a(이탤릭 제목 금지) 위반이다.
      강조는 액센트 색으로 준다 (푸터 statement 의 `em` 이 그 예시).

  layout:
    container-max: "1120px"    # 셸 시스템의 720/880/960 과 무관한 별도 값
    tap-min: "44px"
    breakpoints: ["980px (히어로 2열 해제)", "760px (섹션헤드·About 2열 해제)", "640px (거터)", "430px (내비 워드마크·CTA 제거)"]

  section-rhythm:   # 균일 패딩 금지 규칙은 여기서도 유효하다
    products: "80px / 48px"
    about:    "48px / 80px"
    contact:  "80px / 128px"
---

## Overview

VyxWorks 사이트는 **제품 카탈로그**지 브랜드 쇼케이스가 아니다. 사이트 자체는
최대한 조용해야 하고, 시선은 제품 이름과 스크린샷으로 가야 한다.

세 종류의 표면이 있고 규칙이 다르다:

| 표면 | 경로 | 시스템 | 컨테이너 | 폰트 | 액센트 | 다크 |
|---|---|---|---|---|---|---|
| 스튜디오 홈 | `/index.html` | **(B)** | 1120px | Geist | 인디고 | ✅ |
| 제품 랜딩 | `/carpin/`, `/opaline/` | **(B)** | 920px | Geist | 제품별 | ✅ |
| 법적 고지 | `/*/privacy/`, `/*/terms/` | (A) 셸 | 720px | 시스템 | 제품별 | ✅ |

(A) 공용 셸은 `_partials/header.html` · `_partials/footer.html` + `assets/css/base.css`.
(B) 는 `studio-tokens.css` + `shell.css` 를 공통으로 깔고, 홈이 `home.css`,
제품 랜딩이 `product.css` 를 얹는다.

> ⚠️ **전환 솔기가 하나 남아 있다.** 제품 랜딩(B)에서 개인정보처리방침·이용약관(A)
> 으로 넘어가면 폰트와 내비가 바뀐다. 법적 문서는 읽히는 게 전부라 조용한
> 시스템폰트 레이아웃이 오히려 적합하다고 보고 의도적으로 남긴 상태다.
> 없애려면 법적 고지 16개에 `studio-tokens.css` + `shell.css` 를 물리면 된다 —
> 본문 마크업은 손대지 않아도 된다.

> **아래 Colors·Typography·Elevation·Components 절은 전부 (A) 셸 시스템 이야기다.**
> (B) 페이지를 고칠 때는 프론트매터의 `studio-system` 블록과 `studio-tokens.css`
> 를 본다.

---

## Colors

### 원칙

1. **셸은 무채색이다.** 내비·푸터·본문·테두리에 유채색을 쓰지 않는다.
2. **액센트는 페이지당 하나.** 링크·주 버튼·포커스가 같은 색을 공유한다.
3. **액센트는 제품이 정한다.** `base.css` 를 고치지 말고 제품 CSS 에서
   `--color-accent` 만 재정의한다 (`opaline.css` 가 그 예시).
4. **의미색(성공/경고/오류) 없음.** 이 사이트에 폼도 상태도 없다.
   생기면 그때 추가하고, 그 전엔 팔레트를 늘리지 않는다.

### 다크 스킴

라이트는 그림자 없이 **테두리 + 여백**으로, 다크는 **1px 헤어라인**으로 같은
분리감을 만든다. 다크에서 캔버스를 띄우려고 흰색 오버레이를 쓰지 않는다 —
`surface`(#161618) 를 쓴다.

> ⚠️ 현재 `base.css` 다크는 네이비 틴트(`#0B1426`/`#111C2F`/`#1E293B`)이고
> `opaline.css` 가 이를 순수 뉴트럴로 덮어쓴다. 위 토큰 표는 **뉴트럴이 정본**이라는
> 전제로 쓰였다. Known Gaps 3 참조.

---

## Typography

**(A) 셸 시스템 한정.** 법적 고지는 시스템 폰트 한 벌만 쓰고 웹폰트를 로드하지
않는다 — 다국어 법적 문서에서 FOUT 와 요청 한 번을 아끼는 게 서체 개성보다
가치 있고, CJK 폴백(`Noto Sans JP/SC`)이 스택에 들어 있어야 한다.
(B) 페이지는 이 규칙의 **예외**로 Geist 를 로드한다.
Geist 에는 한글이 없어 CarPin 본문은 시스템 한글 폰트로 폴백된다 — 그래서
(B) 에서 모노(`--font-mono`) 자리에는 한글을 넣지 않는다. 폴백 체인에 한글
모노가 없어 서체가 튄다. CJK 폴백(`Noto Sans JP/SC`)이
스택에 포함돼 있으니 다국어 법적 고지에서 임의로 빼지 않는다.

### 위계

- **큰 글자일수록 자간을 좁힌다.** hero `-0.02em` → h2 `-0.015em` → h3 `-0.01em` → 본문 `0`.
  이게 시스템 폰트를 쓰면서도 "기본값" 느낌을 지우는 유일한 장치다.
- **본문 line-height 1.7.** 제목은 1.08~1.4 로 조인다.
- **크기는 clamp() 로 유체.** 제목에 breakpoint 별 `font-size` 재정의를 쓰지 않는다.
- **굵기는 400 / 600 / 700 세 단계.** 500 을 새로 들이지 않는다.
  (`opaline/index.html:41` 에 800 이 하나 남아 있다 — Known Gaps 7.)

---

## Layout & Spacing

- 간격은 4의 배수. `spacing-scale` 밖의 값(예: 30px, 52px)을 새로 만들지 않는다.
- **셸이 콘텐츠보다 넓다**: 내비·푸터 960px > 홈 880px > 본문 720px.
  이 역순 관계가 페이지에 프레임을 만든다. 뒤집지 않는다.
- 섹션 사이 수직 리듬은 80px(푸터 `margin-top` 기준), 섹션 내부는 40~48px.
- **셸 breakpoint 는 640px 하나.** 거터·내비 축소가 여기서 일어난다.
  다열 그리드를 3→2→1 로 접을 때만 720px/480px 를 추가로 쓴다(`opaline/index.html:98-99`).
  그 외 목적으로 새 breakpoint 를 만들기 전에 clamp() 로 풀 수 있는지 먼저 본다.

### 화이트스페이스

애플 마케팅 페이지에서 가져온 유일한 구조 원칙: **요소를 채우지 말고 비워서 나눈다.**
구분선을 긋기 전에 여백을 두 배로 늘려보고, 그래도 안 갈리면 그때 헤어라인을 쓴다.

---

## Elevation & Depth

**(A) 셸 시스템은 그림자를 쓰지 않는다.** 법적 고지에 `box-shadow` 는 존재하지
않으며 그게 의도다. (B) 는 떠 있는 내비와 셸프 카드에 그림자를 쓴다 —
`--shadow-nav` / `--shadow-card` 토큰으로만, 라이트·다크 각각 다른 값으로.

깊이는 세 가지로만 표현한다:

1. `surface` 배경색 차이 (#FFFFFF → #F7F7F8 → #F2F2F4)
2. 1px `hairline` 테두리
3. hover 시 `translateY(-1px ~ -2px)` — 그림자 없는 미세 부양

유일한 예외: 스티키 내비의 `backdrop-filter: saturate(180%) blur(12px)` +
85% 불투명 배경. 이건 깊이가 아니라 **가독성** 장치다.

---

## Components

### 버튼

```
.btn         padding 12px 24px · radius 999px · 15px/600
.btn-primary background var(--color-accent) · color var(--color-accent-fg)
             hover: translateY(-1px) + 액센트 한 단계 어둡게
.btn-ghost   투명 배경 · 1px hairline · hover 시 surface 채움
```

페이지당 primary 버튼은 **하나**. 나머지는 전부 ghost 나 텍스트 링크.

### 링크

본문 링크는 액센트 색 + `border-bottom: 1px solid transparent` → hover 시 색 채움.
**법적 고지 페이지는 예외**로 `text-decoration: underline` + `text-underline-offset: 2px`.
모노크롬 액센트(Opaline)에서는 색만으로 링크를 구분할 수 없기 때문 — 접근성 요구사항이지
스타일 선택이 아니다. 제거하지 않는다.

### 카드 (feature / product)

radius 12~16px · 1px hairline · `surface` 배경 · 패딩 24px.
hover 시 테두리를 액센트 쪽으로 45% 섞고(`color-mix`) 2px 부양.
제목 16~18px/600~700, 본문 14px/1.6 muted.

**아이콘은 제목 위에 쌓지 않고 제목과 같은 줄에 둔다.** 둥근 사각형 + 상단 아이콘 +
제목 + 두 줄 본문 조합은 생성형 UI 의 대표적 지문(icon-tile card)이라 피한다.

### feature 레이아웃 — 균등 3열 금지

`grid-template-columns: repeat(3, 1fr)` 로 같은 폭 카드를 세 개 늘어놓는 배치는
쓰지 않는다. 페이지마다 항목 수에 맞는 다른 리듬을 고른다:

| 페이지 | 항목 | 레이아웃 |
|---|---|---|
| `opaline/` | 6개 | 12컬럼 위 비대칭 스팬 — `7-5 / 5-7 / 6-6` |
| `carpin/` | 3개 | 카드 없이 헤어라인으로 나눈 리스트 (max-width 560px) |

두 페이지가 같은 리듬을 반복하지 않는 것 자체가 요구사항이다.
항목이 3~4개로 적으면 카드를 버리고 타이포 리듬으로 가는 쪽이 대체로 낫다.

### 아이콘

- **이모지를 UI 아이콘으로 쓰지 않는다.** 플랫폼마다 다르게 그려지고, 실제
  앱아이콘과 나란히 놓이면 획 voice 가 어긋난다.
- **제품 아이콘** — 실제 앱아이콘 이미지. `assets/img/<product>-appicon.jpg`,
  200×200 JPEG, 52px 렌더, radius 12px.
- **개념 아이콘** — 인라인 SVG 한 세트로 통일. `viewBox="0 0 24 24"` ·
  `stroke="currentColor"` · `stroke-width="1.5"` · round cap/join · `fill="none"`.
  외부 아이콘 라이브러리를 로드하지 않는다(웹폰트 금지와 같은 이유).
  색은 `--color-muted`, 크기는 20px.

### 내비 · 푸터

`_partials/` 의 마크업이 정본. 페이지에서 재작성하지 말고 포함해서 쓴다.
내비 링크는 `muted` → hover 시 `ink`. 밑줄 없음.

---

## Do's and Don'ts

### Do
- 새 제품 페이지는 `base.css` 로드 + `var(--color-*)` 사용으로 시작한다.
- 제품 브랜드색은 제품 전용 CSS 에서 `--color-accent` 만 덮어쓴다.
- 제목에 음수 자간을 준다.
- 다크 스킴을 라이트와 **동시에** 만든다. 나중에 붙이면 홈처럼 영영 안 붙는다.
- 크기는 `clamp()`, 간격은 4의 배수.
- **페이지 `:root` 에서 스킴 의존 토큰(`--color-bg/fg/muted/border/surface`)을 덮었다면
  다크 블록에서 반드시 되돌린다.** 미디어쿼리 밖 `:root` 는 두 스킴 모두에 걸리므로,
  라이트만 보고 넘어가면 다크에서 어두운 글자가 어두운 배경에 얹힌다.
  라이트·다크를 **둘 다** 렌더해서 확인하기 전에는 끝난 게 아니다.

### Don't
- ❌ `box-shadow` 를 도입하지 않는다. **((A) 한정 — 개정 2026-09-20)**
- ❌ 웹폰트를 로드하지 않는다. **((A) 한정 — 개정 2026-09-20)**
- ❌ 그라디언트를 장식으로 쓰지 않는다. **((A) 한정 — 개정 2026-09-20)**
- ❌ 셸에 유채색을 쓰지 않는다. **((A) 한정 — 개정 2026-09-20)**
- ❌ **(A) 와 (B) 의 토큰을 섞지 않는다.** 홈에서 `--color-fg` 를 찾거나
  제품 페이지에서 `--color-ink-0` 을 찾는 코드는 잘못 쓴 것이다.
- ❌ `base.css` 에 제품 고유의 값을 넣지 않는다 (지금 그린이 들어가 있는 게 실수다).
- ❌ 애플 팔레트(`#0066cc` Action Blue, `#f5f5f7` parchment)나 SF Pro 헤드라인 조합을
  그대로 쓰지 않는다. **App Store 개발자 사이트가 애플 공식 페이지처럼 보이는 건
  브랜드 혼동 리스크다.** 구조(간격 리듬·화이트스페이스·자간)만 참고하고 색은 우리 것을 쓴다.
- ❌ 그리드 재배치 외의 목적으로 breakpoint 를 늘리지 않는다.
- ❌ 균등 3열 카드 그리드(`repeat(3, 1fr)`)를 쓰지 않는다.
- ❌ 전 섹션에 같은 패딩을 주지 않는다. 섹션마다 상·하 여백을 달리해 리듬을 만든다.
- ❌ 직선 따옴표를 본문에 쓰지 않는다 — `’` `“` `”` (코드·CSS 주석은 예외).
- ❌ CSS 주석 안에 `<` 문자를 넣지 않는다. 브라우저는 견디지만
  HTML 을 다루는 스크립트·도구가 가짜 태그로 오인해 탈선한다.
- ❌ 이모지를 아이콘 자리에 쓰지 않는다.
- ❌ 로고 SVG 의 `stroke` 를 `#fff` 같은 고정값으로 두지 않는다 —
  `rect` 가 `currentColor` 라 다크에서 획이 사라진다. `var(--color-bg)` 로 뚫는다.

---

## Responsive

- 셸 breakpoint 640px: gutter 24px → 20px, 내비 링크 gap 24px → 16px / 14px → 13px.
- 그리드 breakpoint 720px / 480px: feature 그리드 3열 → 2열 → 1열. 이 용도로만 쓴다.
- 제목은 breakpoint 가 아니라 `clamp()` 로 줄어든다.
- 터치 타겟 최소 44×44px. `.btn` 은 12px 패딩 + 15px 폰트로 이미 충족하지만,
  아이콘 전용 버튼을 새로 만들면 별도로 확보해야 한다.
- 이미지·SVG 는 전역 `max-width: 100%` + `display: block`.

---

## Known Gaps

이 문서가 기술한 시스템과 현재 코드가 어긋나는 지점. 고칠 때 여기서 지운다.

1. **`index.html` 이 `base.css` 를 로드하지 않는다 — 의도된 상태로 되돌아갔다
   (2026-09-20).** 한때 해결 처리했으나, 홈이 (B) 시스템으로 갈라지면서 셸
   토큰을 전부 덮어쓰는 구조가 됐다. 로드를 유지하면 죽은 CSS 와 캐스케이드
   함정만 남으므로 끊는 쪽이 맞다. 홈은 `studio-tokens.css` 에서 토큰을 받는다.

2. ~~홈에 다크 모드가 없다~~ → **해결.** (B) 재구축 후에도 유지된다.
   원본 Tally DNA 는 라이트 전용이라 다크 팔레트는 258 색상각을 유지한 채
   새로 만들었다. 22개 대비쌍 WCAG AA 검증 완료.

3. **다크 팔레트가 두 벌이다.** `base.css` 는 네이비 틴트(`#0B1426`),
   `index.html`·`opaline.css` 가 뉴트럴(`#0C0C0D`)로 각각 덮어쓴다.
   지금은 페이지마다 같은 override 를 복사하는 중 — base 를 뉴트럴로 바꾸고
   네이비가 필요하면 CarPin 전용 override 로 옮기면 중복이 사라진다.

4. **본문 잉크가 두 값이다.** `base.css` `--color-fg: #1A1A1A` vs 의도값 `#0A0A0A`.
   홈은 페이지 `:root` 에서 `#0A0A0A` 로 덮어쓰는 중(임시).
   `base.css` 를 `#0A0A0A` 로 고치면 홈의 override 를 지울 수 있고
   `opaline/`·`carpin/` 본문도 함께 정렬된다 — 다만 그 두 페이지 렌더가 바뀐다.

5. **`base.css` 가 CarPin 브랜드색을 기본값으로 싣고 있다.**
   `opaline.css` 주석이 이미 자인하는 문제. 공용 base 는 액센트를 뉴트럴로 두고
   CarPin 이 `carpin.css` 에서 그린을 켜는 구조가 맞다.

6. **컨테이너 폭 3종(720/880/960)이 문서화 없이 흩어져 있었다.**
   위 `layout` 블록이 최초 성문화. 새 값을 추가하지 않는다.

7. ~~`font-weight: 800` 이 한 군데 남아 있다~~ → **해결.** 700 으로 정리, 이제 400/600/700 3단계.

9. ~~다크에서 내비 로고의 V 가 사라진다~~ → **해결.**
   `base.css` 에 `.site-nav-brand svg path { stroke: var(--color-bg); }` 추가.
   19개 페이지의 마크업을 건드리지 않고 한 곳에서 고쳤다. 대비 1.08:1 → 18:1.

10. ~~이모지가 아이콘 자리에 쓰인다~~ → **해결.**
    홈 `📔` → Achieve 앱아이콘, opaline/carpin 개념 이모지 9종 → 인라인 SVG 하우스 세트.

11. ~~균등 3열 카드 그리드~~ → **해결.** opaline 비대칭 스팬, carpin 헤어라인 리스트.

12. ~~홈 제품 카드가 "Diary" 로 되어 있다~~ → **해결.**
    `Achieve` + "Todos, events, and habits on one board." 로 정리.

13. ~~직선 따옴표~~ → **해결.** 랜딩 3개 + 법적 고지 13개 파일의 본문을
    곡선 따옴표(`’ “ ”`)로 변환. HTML 속성 구분자와 `style`/`script` 내부는 제외.

14. ~~전 섹션 동일 패딩~~ → **해결.** 홈 `#products` / `#about` / `#contact` 에
    서로 다른 상·하 여백 (데스크톱·모바일 모두).

15. ~~페이지에 Hallmark 스탬프가 없다~~ → **해결.**
    (B) 3장은 `studio-tokens.css` · `shell.css` · `home.css` · `product.css`
    스탬프를, 법적 고지는 `base.css` 스탬프를 상속.
    프로젝트 메모리는 `.hallmark/log.json`.

16. **내비가 AI nav 형태에 근접한다** ((B) 3장 해결, 법적 고지 16개 미해결).
    홈과 제품 랜딩은 N5 Floating pill 로 교체됐다 — 화면에서 떠 있고,
    워드마크·링크·CTA 가 한 알약 안에 들어간다. 430px 이하에서는 워드마크와
    CTA 를 버리고 목적지 3개만 남긴다 (원본 Tally 는 여기서 링크를 통째로 숨겨
    목적지에 갈 방법이 사라지는데, 그건 따라하지 않았다).
    법적 고지 16개는 여전히 `_partials/header.html` 의 sticky 바다.

17. ~~파비콘이 깨져 있다~~ → **해결 (2026-09-20).**
    `index.html` 이 존재하지 않는 `/assets/img/vyxworks-logo.svg` 를 가리켰고,
    루트 `favicon.svg` 는 최초 커밋(`733479b`)부터 0바이트로 트래킹되고 있었다.
    중복 파일을 만들지 않으려고 이미 트래킹 중인 루트 `favicon.svg` 를 실제
    마크로 채우고 홈이 거길 보게 했다. 파비콘은 문서 밖에서 그려져
    `currentColor` 가 없으므로 색을 명시하고, `opaline-logo.svg` 와 같은
    SVG 내부 `prefers-color-scheme` 로 스킴을 뒤집는다. 획은 3 → 3.5 로 굵혔다
    (16px 렌더에서 3/32 는 1.5px 라 뭉갠다). 라이트·다크 16/32/64px 렌더 확인 완료.
    제품 페이지 18개는 각자의 제품 로고를 쓰며 전부 정상 — 의도된 브랜딩이라 건드리지 않았다.
    남은 것: `*/privacy/index.html` · `*/terms/index.html` 4개 언어 리다이렉트 스텁에는
    아이콘 링크가 없다. `meta refresh` 로 즉시 튕기는 페이지라 실익이 없어 그대로 뒀다.

18. ~~제품 랜딩이 홈과 다른 시스템이다~~ → **해결 (2026-09-20).**
    `carpin/`·`opaline/` 을 (B) 로 옮겼다. 구조·타이포·내비·푸터는 홈과 같고
    액센트만 제품이 갖는다. 기능 리듬은 서로 다르게 유지 — CarPin 은 3개 항목
    헤어라인 리스트, Opaline 은 6개 항목 12칼럼 비대칭 스팬(7-5 / 5-7 / 6-6).
    카피·App Store 링크·법적 링크·사업자 정보는 한 글자도 바꾸지 않았다.

19. **`base.css` 가 이제 법적 고지 전용이다** (기록용).
    (B) 로 3장이 빠져나가면서 `base.css` 의 `.btn` · `.btn-primary` ·
    `.btn-ghost` 와 홈 전용 값들은 쓰는 페이지가 없어졌을 가능성이 높다.
    지우기 전에 법적 고지 16개에서 실제 사용 여부를 확인한다.

20. **`base.css` 의 그린 링크가 대비 미달이다** (미해결, 법적 고지 영향).
    `a { color: var(--color-accent) }` 에 CarPin 그린 `#04C98A` 가 들어가 있고,
    흰 배경에서 **2.16:1** 이라 본문 기준(4.5:1)에 한참 못 미친다.
    CarPin 법적 고지가 이 링크 색을 쓴다. (B) 는 같은 문제를 색상각 유지 +
    명도 하향(oklch 50% .14 162, 5.15:1)으로 풀었으니 같은 값을 쓰면 된다.
    Opaline 법적 고지는 `opaline.css` 가 모노크롬 + 밑줄로 덮어서 영향 없다.

8. **홈의 임의 회색이 토큰으로 정규화됐다** (기록용, 조치 불필요).
   토큰 도입 과정에서 헤어라인 `#EFEFEF`→`#E5E7EB`(`--color-border`),
   보조 텍스트 `#555`·`#888`→`#6B7280`(`--color-muted`) 로 흡수됐다.
   전체 픽셀의 1.4% 변화, 최대 채널차 43. 의도된 결과다 —
   이 값들을 되살리려고 토큰을 덮어쓰지 않는다.

---

## Iteration Guide

**(B) 페이지를 고칠 때:** 프론트매터 `studio-system` 블록 →
`assets/css/studio-tokens.css` → `shell.css` → `home.css` 또는 `product.css`
순으로 본다.

**새 제품 랜딩을 만들 때 (B):**

1. `carpin/index.html`(3개 항목·헤어라인 리스트) 또는 `opaline/index.html`
   (6개 항목·비대칭 스팬)에서 항목 수가 가까운 쪽을 복사한다.
2. `studio-tokens.css` + `shell.css` + `product.css` 로드를 유지하고,
   인라인 `<style>` 에서는 `--color-accent` 계열만 덮는다. 구조는 건드리지 않는다.
3. **액센트를 정하기 전에 대비를 계산한다.** 브랜드색이 페이퍼 위에서 4.5:1 에
   못 미치면 CarPin 방식을 쓴다 — 같은 색상각을 어둡게 내려 텍스트용
   `--color-accent` 로 쓰고, 원래 브랜드색은 `--color-brand` 로 도트에만 남긴다.
4. 기능 리듬을 **두 기존 페이지와 다르게** 고른다. 같은 리듬의 반복이 곧 템플릿이다.
5. 라이트·다크 둘 다 렌더해서 확인한다.

아래 절차는 (A) 셸 시스템(법적 고지) 전용이다:
2. `_partials/header.html`·`footer.html` 포함, `base.css` 로드 유지.
3. 제품 액센트가 그린이 아니면 `assets/css/<product>.css` 를 만들어
   `--color-accent` / `--color-accent-fg` 만 재정의하고 base.css **뒤에** 로드한다.
4. 라이트·다크 둘 다 확인한다.
5. 이 문서의 Do's and Don'ts 로 셀프 점검한 뒤 커밋한다.

에이전트에게: 이 사이트의 UI 를 만들거나 고칠 때 이 문서를 먼저 읽는다.
**어느 시스템인지부터 정한다** — `/`, `/carpin/`, `/opaline/` 이면 (B),
법적 고지면 (A) 다.
토큰 값은 (A) 는 `assets/css/base.css`, (B) 는 `assets/css/studio-tokens.css`
가 정답이다 (문서보다 CSS 가 정답).
