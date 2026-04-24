# vyxworks — Product legal pages (guide)

vyxworks가 배포하는 앱들의 정적 랜딩·법적 문서(개인정보처리방침·이용약관) 관리 가이드. 현재 CarPin(`/carpin/`)이 들어 있으며, 신규 앱은 동일 구조를 복사해 추가한다.

## 구조 (레포 루트 기준)

```
/
├── index.html            # vyxworks 회사 메인 (별도 관리)
├── favicon.svg           # 회사 파비콘
├── CNAME                 # vyxworks.com
├── assets/
│   ├── css/
│   │   ├── base.css      # 공통(레이아웃·네비·푸터·타이포·버튼)
│   │   └── legal.css     # 법적 문서 전용(목차·표·인쇄)
│   └── img/
│       └── carpin-logo.svg
├── _partials/
│   ├── header.html       # 공통 헤더 원본(런타임 include 불가 → 페이지에 복제)
│   ├── footer.html       # 공통 푸터 원본
│   └── README.md         # (이 문서)
└── carpin/
    ├── index.html        # 앱 랜딩 → vyxworks.com/carpin/
    ├── privacy/
    │   ├── index.html    # 언어 자동 감지 리다이렉트(기본 ko)
    │   ├── ko.html · en.html · ja.html · zh-Hans.html
    └── terms/            # (동일 구조)
```

## 배포

**GitHub Pages user/org site** (`vyxworks/vyxworks.github.io`, CNAME `vyxworks.com`).
레포 루트를 그대로 서빙하므로 **추가 설정 불필요** — push 후 1~2분이면 반영된다.

라이브 URL:
- `https://vyxworks.com/carpin/` — 랜딩
- `https://vyxworks.com/carpin/privacy/` — 개인정보처리방침(언어 자동 감지)
- `https://vyxworks.com/carpin/terms/` — 이용약관(언어 자동 감지)
- `https://vyxworks.com/carpin/privacy/ko.html` 등 — 언어 고정

## 로컬 미리보기

```bash
python3 -m http.server 8000
# http://localhost:8000/carpin/
```

## 신규 앱 추가

예시: `Diary` 앱 추가.

1. `cp -R carpin diary`
2. `diary/` 하위 HTML에서 일괄 치환
   - `CarPin` → `Diary`
   - `carpin/` → `diary/`, `/carpin/` → `/diary/`
   - `support@carpin.app` → 해당 앱 지원 이메일
3. 앱별 사실(수집 데이터·SDK·결제 구조) 4개 언어 모두 수정
4. 루트 `index.html`의 Products 카드·푸터 링크 갱신
5. `assets/img/`에 새 로고 SVG 추가

## 약관 개정

1. 개정 내용과 시행일 확정
2. 4개 언어 파일 본문 수정
3. `<section #s13>` 표에 **버전·시행일·주요 변경** 한 행 추가
4. `<header class="legal-header">`의 "최종 개정일/Last updated" 갱신
5. 앱 내 배너로 이용자 고지 (최소 7일 전, 중요 변경은 30일 전)

## 번역 추가 (예: 스페인어)

1. 어느 언어든 하나를 `es.html`로 복사
2. `<html lang="es">`, `<title>`, `<meta description>` 변경
3. `legal-lang-switcher` 블록에 `<a href="es.html">Español</a>` — **4개 언어 파일 모두** 추가
4. `<link rel="alternate" hreflang="es" ...>` 모든 페이지 `<head>`에 추가
5. 본문 번역 (사실 누락·과잉 금지)
6. `privacy/index.html`·`terms/index.html`의 언어 감지 스크립트에 `es` 분기 추가

## 배포 전 교체 필요

```bash
grep -rn "TODO_REPLACE" carpin/ _partials/
```

| 위치 | 내용 | 교체 시점 |
| --- | --- | --- |
| `carpin/index.html` | App Store URL (`TODO_REPLACE_APP_STORE_URL`) | App Store 심사 통과 후 |

이메일 일괄 변경:

```bash
grep -rl "support@carpin.app" carpin/ | xargs sed -i "" "s/support@carpin.app/NEW_EMAIL/g"
```

## 법률 검토

본 문서는 vyxworks의 현재 서비스 구조(서버 없음·로컬 저장·AdMob·Apple IAP)에 맞춘 내용이지만, **배포 전 관할 국가의 법률 자문을 권장**한다.

- 한국 PIPA — 개인정보보호책임자 지정, 분쟁 조정 안내
- EU GDPR — EU 대리인(Representative) 지정 여부, UMP 동의 설계
- 미국 CCPA/CPRA — Do Not Sell 링크 표시 의무(캘리포니아 매출 발생 시)
- 일본 個人情報保護法 — 개인관련정보의 제3자 제공 고지
- 중국 PIPL — 중국 본토 배포 시 별도 대응(현재 중국 본토 미배포 가정)

법적 면책 문구는 본문에 포함하지 않았다(실효성 낮음·이용자 혼란).

## 제약

- JavaScript 없이도 전 콘텐츠 열람 가능. 언어 감지는 편의 기능이며, `/privacy/index.html`은 `<meta refresh>`로 한국어로 폴백.
- 외부 CDN·폰트·분석 스크립트 없음. 법적 문서가 사용자를 추적하면 자기모순.
- 파비콘/로고 외 이미지 없음 (오프라인 배포 가능).

© 2026 vyxworks.
