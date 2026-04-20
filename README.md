# VyxWorks Corporate Website

`vyxworks.com` 에서 운영되는 빅스웍스 공식 사이트. Apple Developer Program 조직 계정 심사용으로 처음 만들어졌으며, 이후 회사 공식 사이트로 운영.

## 구조

순수 정적 HTML. 빌드 도구·프레임워크 없음. `index.html` 하나가 전부.

## 로컬 미리보기

```bash
open index.html
# 또는
python3 -m http.server 8000
# → http://localhost:8000
```

## 배포 (GitHub Pages)

1. `vyxworks` GitHub Organization 생성
2. 레포 생성: `vyxworks/vyxworks.github.io`
3. 이 디렉토리를 push:

```bash
git remote add origin git@github.com:vyxworks/vyxworks.github.io.git
git push -u origin main
```

4. 레포 Settings → Pages → Source: `main` branch / root → Save
5. 같은 화면에서 Custom domain: `vyxworks.com` 입력 → Save
6. DNS 전파 후 "Enforce HTTPS" 체크

## 가비아 DNS 설정

가비아 → 도메인 관리 → DNS 정보 → 레코드 수정:

**A 레코드 4개 (호스트: `@`)**
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**CNAME 레코드 1개**
```
호스트: www
값: vyxworks.github.io
```

전파 시간: 30분 ~ 수시간.

## 라이선스

© 2026 VyxWorks. All rights reserved.
