# ARCHITECTURE

## 개요
정적 사이트 1개 파일(`index.html`) — 별도 빌드 과정 없음. 배포는 GitHub Pages가 `main` 브랜치 root를 그대로 서빙.

## 구조 (index.html 내부)
- `<style>`: `:root` CSS 변수로 컬러 토큰 정의(`--ink`, `--paper`, `--coral`, `--gold`, `--teal`, `--sky` 등), 이후 컴포넌트별 클래스
- `<body>`: 섹션 순서 — 히어로(#top) → `#about` → `#budget` → `#itinerary` → `#stay` → `#resort` → footer → lightbox 모달
- `<script>` (IIFE, 바닐라 JS): 스크롤 진행바, 탭 active 상태(IntersectionObserver), reveal 애니메이션, 예산 미터, 타임라인 SVG 라인 드로잉, 날짜 아코디언, 스플릿플랩 항공 보드 애니메이션, 날씨/지역 토글, 리조트 가격 정렬, 포토 갤러리 라이트박스(`GALLERIES` 객체)

## 외부 의존성
- Google Fonts CDN (Jua, Gowun Dodum, Fraunces, JetBrains Mono) — 유일한 외부 리소스
- 숙소/리조트 사진: Agoda 이미지 CDN(`pix8.agoda.net`, `pix5.agoda.net`) 핫링크 — 저장소에 이미지 파일 없음

## 배포 파이프라인
로컬에서 `index.html` 수정 → `git add . && git commit && git push origin main` → GitHub Pages가 자동 재배포 → https://andrea951102.github.io/nhatrang-trip/ 반영. CI/빌드 스텝 없음.
