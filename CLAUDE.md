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
- 섹션 순서: 히어로(#top) → `#about`(나트랑은?) → `#budget`(항공) → `#itinerary`(일정) → `#stay`(숙소 — T-78 Pre-Hotel 1박 + 시내 하바나 4박 + 깜란 엠피리언 4박 카드 + 숙박비 총합) → `#food`(맛집) → `#activity`(Activity, placeholder)
- 숙박 확정: T-78 Pre-Hotel 12.18–19(1박, 새벽 도착 직후 반박) → 하바나 나트랑 호텔 12.19–23(4박) → 디 엠피리언 깜란 12.23–27(4박, 마지막 1박은 12.26 밤 출국편 때문에 추가 구매). 리조트는 엠피리언으로 확정 — 예전 `#resort` 비교 섹션은 삭제됨.
- 숙박비(모두 2인 1실 기준): T-78 1박 ₩21,773 / 하바나 4박 ₩262,024(1박 ₩65,506) / 엠피리언 4박 ₩267,368(1박 ₩66,842) / 1인당 총합 ₩275,583 (2인 총액 ₩551,165). 카드마다 "2인 총액"·"2인·1박"·"1인당"·"1인당·1박" 4개 항목 표기.
- 가격 단위 관례: 사용자가 숙박비 숫자 하나만 줄 때는 **항상 2인·1박 기준** — 1인당은 항상 ÷2로 계산할 것(이 프로젝트에서 반복 실수 있었음).
- 주요 컴포넌트: 스플릿플랩 항공 보드(히어로), 타임라인 아코디언(일정), 숙소 카드 + 포토 갤러리 라이트박스
- 스크립트 하단 `GALLERIES` 객체(약 1300번째 줄 부근)에 숙소별 사진 URL 배열이 있음(현재 `prehotel`, `havana`, `empyrean`, `food_seamoi`)

## 알려진 이슈 / TODO
자세한 배경과 최신 업데이트는 [docs/PROGRESS.md](docs/PROGRESS.md) 참고. 요약:
1. 숙소 사진이 Agoda/trip.com CDN(`pix8.agoda.net`, `pix5.agoda.net`, `ak-d.tripcdn.com`)에서 핫링크 중 — URL 만료/변경 시 깨질 수 있음. 안정성 원하면 이미지를 다운받아 `images/`에 넣고 로컬 경로로 교체.
2. `#activity` 섹션은 placeholder — 실제 액티비티 콘텐츠 미작성.
3. 미사용 `.resort-*` CSS 규칙이 남아 있음(`.opinion` 계열과 같은 블록이라 보존 중).

## 검증
- 별도 빌드 도구 없음(순수 HTML/CSS/JS) — 수정 후엔 브라우저로 직접 열거나 로컬 서버 띄워서 확인.
- 자동화된 lint/test 스크립트 없으므로 "테스트 통과"라고 말하지 말 것 — 육안 확인 여부를 그대로 말할 것.
