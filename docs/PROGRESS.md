# 작업 로그 (PROGRESS)

세션·기기 간 작업 인계용 로그. 새 작업을 마칠 때마다 **맨 위**에 1건씩 추가한다 (무엇을 · 왜 · 다음 할 일).

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
