# 나트랑 트립 브리프 — 프로젝트 가이드

> 이 파일은 이 저장소 전용. 전역 `~/.claude/CLAUDE.md` 규칙 위에 얹혀서 세부를 보충한다.

## 프로젝트 개요
- **무엇**: 베트남 나트랑 여행(2026.12.18~12.26) 계획을 지인들에게 공유하는 인터랙티브 웹페이지
- **형태**: 단일 `index.html` 파일 (CSS/JS 전부 인라인, 외부 의존은 Google Fonts CDN뿐)
- **배포**: GitHub Pages — `main` 브랜치 root를 그대로 서빙
- **Repo**: `andrea951102/nhatrang-trip` (public)
- **라이브 URL**: https://andrea951102.github.io/nhatrang-trip/

## 작업 방식 (중요 — 예전 방식에서 전환됨)
- 예전엔 Claude 앱(데스크톱/웹)에서 만든 산출물을 GitHub 웹 UI "Upload files"로 수동 커밋했음.
- **이제부터는 이 저장소에서 Claude Code(CLI)로 직접 작업** → `git add . && git commit -m "..." && git push`. `main`에 푸시하면 Pages가 자동 재배포됨. 웹 UI 업로드는 더 이상 안 씀.
- 문서 구조: [docs/PROJECT.md](docs/PROJECT.md)(목적/이해관계자) · [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)(구조) · [docs/ROADMAP.md](docs/ROADMAP.md)(확정/미정/다음 단계) · [docs/PROGRESS.md](docs/PROGRESS.md)(작업 로그) · [docs/COOPERATION.md](docs/COOPERATION.md)(Codex 등 다른 에이전트와 공유하는 진행 방식) · `docs/tasks/`(작업이 커지면 단위별로 분리).
- 작업 로그는 [docs/PROGRESS.md](docs/PROGRESS.md) — 세션/기기 넘나들며 이어 작업하므로, 의미 있는 작업을 마칠 때마다 맨 위에 1건씩 기록할 것.

## 코드 구조 (index.html 안에서)
- `:root` CSS 변수로 컬러 토큰 정의: `--ink`, `--paper`, `--coral`, `--gold`, `--teal`, `--sky` 등
- 폰트: 제목 `Jua`, 본문 `Gowun Dodum`, 영문 악센트("Nha Trang" 이탤릭) `Fraunces`, 숫자/데이터 `JetBrains Mono`
- 섹션 순서: 히어로(#top) → `#about`(나트랑은?) → `#budget`(항공) → `#itinerary`(일정) → `#stay`(숙소) → `#resort`(리조트)
- 주요 컴포넌트: 스플릿플랩 항공 보드(히어로), 타임라인 아코디언(일정), 리조트 카드 + 정렬/토글, 포토 갤러리 라이트박스(모든 숙소 카드)
- 스크립트 하단 `GALLERIES` 객체(약 1300번째 줄 부근)에 호텔/리조트별 사진 URL 배열이 있음

## 알려진 이슈 / TODO
자세한 배경과 최신 업데이트는 [docs/PROGRESS.md](docs/PROGRESS.md) 참고. 요약:
1. 숙소 사진이 Agoda CDN(`pix8.agoda.net`, `pix5.agoda.net`)에서 핫링크 중 — URL 만료/변경 시 깨질 수 있음. 안정성 원하면 이미지를 다운받아 `images/`에 넣고 로컬 경로로 교체.
2. Pre-Hotel 조식 포함 여부 미확인.

## 검증
- 별도 빌드 도구 없음(순수 HTML/CSS/JS) — 수정 후엔 브라우저로 직접 열거나 로컬 서버 띄워서 확인.
- 자동화된 lint/test 스크립트 없으므로 "테스트 통과"라고 말하지 말 것 — 육안 확인 여부를 그대로 말할 것.
