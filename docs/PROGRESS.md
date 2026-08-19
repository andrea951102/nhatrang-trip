# 작업 로그 (PROGRESS)

세션·기기 간 작업 인계용 로그. 새 작업을 마칠 때마다 **맨 위**에 1건씩 추가한다 (무엇을 · 왜 · 다음 할 일).

---

## 2026-08-19 — `#food` 나트랑 시내 맛집 섹션 신설 + 구글맵 사진 핫링크 방식 확정 + CSV 기반 콘텐츠 관리로 전환

**무엇을**:
- 새 섹션 `#food`(05 · WHERE WE EAT)를 `#stay`와 `#resort` 사이에 추가, `#resort` 번호는 05→06으로 밀림. 탭바에 "맛집" 링크 추가.
- 구글맵 공유링크(`maps.app.goo.gl/...`)에서 사진을 자동 추출해 핫링크하는 방법을 검증함 — 링크를 curl로 열면 내부 `/maps/preview/place` 엔드포인트를 참조하는데, 여기서 `lh3.googleusercontent.com/geougc/...` 형태의 사진 URL을 API 키 없이 뽑아낼 수 있고 실제로 접근도 됨(200 OK). 씨모이 가든(예시 식당)으로 사진 11장 추출해서 카드에 반영, `GALLERIES` 객체에 `food_seamoi` 키로 저장.
- 헤더에 나트랑 로컬 밥값·맥주값 대략치를 담은 `.ai-card` 인사이트 박스 추가(추정치, 방문 후 갱신 예정이라고 명시).
- 식당 정보를 대화창에 링크로 하나씩 전달하던 방식 대신, `docs/data/food-list.csv`(식당명/카테고리/구글맵링크/코멘트/가격대 컬럼) 파일로 모아 관리하기로 결정. 진행 상황 추적용으로 `docs/tasks/food-section.md` 신설.

**왜**: 리조트 사진과 마찬가지로 실제 사진 파일을 저장소에 넣지 않고도(용량 부담 없이) 카드에 사진을 넣고 싶어함. 또한 식당이 최대 10곳 정도라 매번 대화로 링크를 주고받는 것보다 CSV 파일 하나로 모아 관리하는 게 더 안정적 — 나(Claude)는 파일이나 GitHub 변경을 스스로 감지할 수 없으므로, 사용자가 CSV를 갱신한 뒤 매번 명시적으로 "반영해줘"라고 요청하는 흐름으로 합의함.

**다음 할 일**:
1. 사용자가 `docs/data/food-list.csv`에 실제 식당 목록(최대 10곳)을 채워나감 — 채운 뒤 반영 요청 시 CSV 읽고 각 행마다 사진 추출 + 카드 추가.
2. 구글맵 사진 핫링크는 Agoda와 마찬가지로 비공식 소스 의존 리스크가 있음(오히려 더 불안정할 수 있음, 내부 미문서화 API) — 나중에 안정성 원하면 로컬 저장 전환 검토.

---

## 2026-08-19 — 표준 docs 구조 전체 세팅 (PROJECT/ARCHITECTURE/ROADMAP/COOPERATION/tasks)

**무엇을**: `docs/PROJECT.md`, `docs/ARCHITECTURE.md`, `docs/ROADMAP.md`, `docs/COOPERATION.md`, `docs/tasks/README.md` 추가. 사용자 전역 `~/.claude/CLAUDE.md`도 함께 갱신 — "규모가 있으면" 조건부로 문서 구조를 물어보던 규칙을, 규모 판단 없이 항상 기본으로 세팅하는 규칙으로 변경.

**왜**: 사용자가 이전에도 이 규칙(작업 로그 + Codex와 공유하는 COOPERATION 문서)을 전역 CLAUDE.md에 넣어뒀었는데, "규모가 있으면"이라는 조건 때문에 제가 이 프로젝트를 작다고 판단해서 최초 세팅 때 일부만 반영했었음. 사용자가 규모 판단을 직접 하고 싶지 않다고 해서, 앞으로는 모든 프로젝트에서 조건 없이 기본 세팅하도록 전역 규칙을 수정함.

**다음 할 일**: 없음 (문서 스캐폴딩 완료). 실제 작업 TODO는 아래 항목들 참고.

---

## 2026-08-19 — Claude 앱 → CLI 전환 준비, 기존 인수인계 문서 이관

**무엇을**: Claude 데스크톱/웹 앱에서 세션마다 수동으로 인수인계하던 방식(HANDOFF.md를 매번 복붙)에서, 저장소 안에 상시 작업 로그(`docs/PROGRESS.md`)와 프로젝트 전용 [CLAUDE.md](../CLAUDE.md)를 두는 구조로 전환. 기존 HANDOFF.md 내용을 이 로그와 CLAUDE.md로 이관.

**왜**: 세션 옮길 때마다 문맥을 수동으로 옮기는 게 번거로워서, 앞으로는 Claude Code(CLI)로 이 저장소에서 직접 이어 작업하기로 함. 로그가 저장소 안에 있으면 어느 기기·세션에서 열어도 최신 상태를 바로 파악 가능.

**다음 할 일** (기존 HANDOFF.md의 TODO 이관):
1. 리조트/호텔 사진이 Agoda 이미지 CDN(`pix8.agoda.net`, `pix5.agoda.net`) 핫링크 상태 — 다운로드해서 리포에 저장한 게 아니라 아고다 서버에서 바로 불러오는 방식이라, 나중에 URL이 만료·변경되면 깨질 수 있음. 안정성 원하면 사진을 직접 저장해서 `images/` 폴더에 넣고 로컬 경로로 바꾸는 걸 권장. JS의 `GALLERIES` 객체(스크립트 하단)에 호텔별 URL 배열이 있음.
2. 다이아몬드 베이 리조트 6박 가격(₩442,776)을 담은 스크린샷이 중복 업로드된 것으로 보이는 사례가 있었음 — 다른 두 스크린샷 합계에서 역산한 5박 기준 ₩378,760으로 이미 업데이트됨 (현재 index.html이 최신 값, 참고 기록용).
3. Pre-Hotel 조식 포함 여부 미확인 (현재 페이지엔 리조트 4곳만 조식 포함으로 표기됨).

**참고 원본 자료**:
- Notion 브리프: https://app.notion.com/p/Vietnam-Trip-Brief-3be8958aebc48006ac0ac5167fddb86c
- 숙소 링크(agoda 검색 슬러그): Pre-Hotel `t-78-hotel-nha-trang` / 하바나 `havana-nha-trang-hotel` / 두옌 하 `duyen-ha-resort-cam-ranh` / 다이아몬드 베이 `diamond-bay-resort-spa` / 디 엠피리언 `the-empyrean-cam-ranh-beach-resort` / 윈덤 가든 `wyndham-garden-cam-ranh-resort`
