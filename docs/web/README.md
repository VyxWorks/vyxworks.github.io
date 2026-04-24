# vyxworks — Product legal pages

vyxworks가 배포하는 앱들의 정적 랜딩·법적 문서(개인정보처리방침·이용약관)를 모아두는 디렉터리. 현재 CarPin(`/carpin/`)이 들어 있으며, 신규 앱은 동일 구조를 복사해 추가한다.

## 구조

```
docs/web/
├── assets/
│   ├── css/
│   │   ├── base.css          # 공통(레이아웃·네비·푸터·타이포·버튼)
│   │   └── legal.css         # 법적 문서 전용(목차·표·인쇄)
│   └── img/
│       └── carpin-logo.svg   # CarPin 로고 + 파비콘
├── _partials/
│   ├── header.html           # 공통 헤더 원본(런타임 include 불가 → 페이지에 복제)
│   └── footer.html           # 공통 푸터 원본
├── carpin/
│   ├── index.html            # 앱 랜딩
│   ├── privacy/
│   │   ├── index.html        # 언어 자동 감지 리다이렉트(기본 ko)
│   │   ├── ko.html · en.html · ja.html · zh-Hans.html
│   └── terms/                # (동일 구조)
└── README.md
```

## 로컬 미리보기

```bash
cd docs/web
python3 -m http.server 8000
# http://localhost:8000/carpin/
```

또는 Node:

```bash
npx serve .
```

## 배포

### 1) 기존 루트 사이트와 통합 배포 (권장)

레포 루트에는 이미 `index.html`이 있다. GitHub Pages가 루트를 서빙하므로 `docs/web/carpin/`을 `carpin/`으로 심볼릭 링크하거나 배포 시 복사한다.

가장 간단한 방법: **루트에서 `ln -s docs/web/carpin carpin && ln -s docs/web/assets assets`** 후 커밋(심볼릭 링크 커밋은 git에서 지원). 또는 GitHub Actions로 복사 스크립트 실행.

### 2) Cloudflare Pages / Netlify

- Build command: *(없음)*
- Publish directory: `docs/web`
- Custom domain: `vyxworks.com`

### 3) GitHub Pages에서 `/docs`를 소스로 지정

Settings → Pages → Source → Branch `main` / folder `/docs`로 변경하면 `docs/web`이 아닌 `docs/`가 루트가 된다. 이 경우 `carpin/`을 `docs/carpin/`으로 이동하거나 `docs/index.html`을 추가로 둔다.

> 현 레포는 루트 `index.html`을 이미 사용 중이라 **(1)** 방식을 추천한다.

## 신규 앱 추가

예시: `Diary` 앱 추가.

1. 디렉터리 복사
   ```bash
   cp -R docs/web/carpin docs/web/diary
   ```
2. `diary/` 하위 모든 HTML에서 다음을 일괄 치환
   - `CarPin` → `Diary`
   - `carpin/` → `diary/`
   - `/carpin/` → `/diary/`
   - `support@carpin.app` → 해당 앱 지원 이메일
3. 앱별 사실(수집 데이터·SDK·결제 구조)을 4개 언어 모두 수정
4. 루트 `index.html`의 Products 카드와 푸터 링크를 갱신
5. `assets/img/`에 새 로고 SVG 추가

## 약관 개정

1. 개정 내용을 확정하고 시행일을 결정
2. 4개 언어 파일 전부 본문 수정
3. 각 파일 `<section #s13>`(시행일·개정 이력) 표에 **버전·시행일·주요 변경**을 한 행 추가
4. `<header class="legal-header">`의 "최종 개정일/Last updated" 날짜 갱신
5. 앱 내 배너 또는 시작 화면 공지로 이용자에게 고지 (최소 7일 전, 중요 변경은 30일 전)
6. 커밋 메시지 예: `docs(legal): carpin privacy v1.1 — add kakao login notice`

## 번역 추가 (예: 스페인어)

1. 어느 언어든 하나(예: `en.html`)를 `es.html`로 복사
2. `<html lang="es">`, `<title>`, `<meta description>`을 스페인어로 변경
3. `legal-lang-switcher` 블록에 `<a href="es.html" lang="es">Español</a>` 추가 — **4개 언어 파일 모두**에 동일하게 추가
4. `<link rel="alternate" hreflang="es" ...>`를 모든 페이지 `<head>`에 추가
5. 본문 번역 (사실 누락·과잉 금지)
6. `privacy/index.html`과 `terms/index.html`의 언어 감지 스크립트에 `es` 분기 추가

## 배포 전 반드시 교체할 플레이스홀더

```bash
grep -r "TODO_REPLACE" docs/web/
```

현재 남아 있는 항목:

| 위치 | 내용 | 교체 시점 |
| --- | --- | --- |
| `carpin/index.html` | App Store URL (`TODO_REPLACE_APP_STORE_URL`) | App Store 심사 통과 후 |

이메일 변경 시:

```bash
# support@carpin.app 전체 변경 예시 (macOS)
grep -rl "support@carpin.app" docs/web/ | xargs sed -i "" "s/support@carpin.app/NEW_EMAIL/g"
```

## 배포 전 법률 검토 안내

본 문서는 vyxworks의 현재 서비스 구조(서버 없음, 로컬 저장, Google Mobile Ads, Apple IAP)에 맞춘 내용이지만, **배포 전 관할 국가의 법률 자문을 받을 것을 권장한다**.

특히:

- **한국 개인정보보호법** — 개인정보보호책임자 지정, 분쟁 조정 안내
- **EU GDPR** — 대리인(EU Representative) 지정 여부, UMP 동의 설계
- **미국 CCPA/CPRA** — Do Not Sell 링크 표시 의무(캘리포니아 거주자 대상 매출 발생 시)
- **일본 개人情報保護法** — 개인관련정보의 제3자 제공 고지
- **중국 个人信息保护法(PIPL)** — 중국 본토 서비스 시 별도 대응 필요(현재 앱은 중국 본토 App Store 미배포 가정)

법적 면책 문구(disclaimer)는 본문에 포함하지 않았다. 실효성이 낮고 오히려 이용자에게 혼란을 준다.

## 제약

- JavaScript가 없어도 모든 콘텐츠 열람 가능. 언어 감지는 편의 기능일 뿐, `/privacy/index.html`은 `<meta refresh>`로 한국어 페이지로 리다이렉트된다.
- 외부 CDN·폰트·분석 스크립트를 포함하지 않는다. 정적 법적 문서가 사용자를 추적하면 자기모순이다.
- 파비콘/로고 외 이미지 없음 (오프라인 배포 가능).

## 라이선스

© 2026 vyxworks. All rights reserved.
