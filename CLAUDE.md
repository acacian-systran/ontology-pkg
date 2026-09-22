# ontology-pkg

『온톨로지와 지식 그래프 — 의미 모델링에서 운영·GraphRAG까지』(위키독스, 117절)를
책의 리테일 사례 대신 **오픈소스 패키지 생태계** 도메인으로 다시 밟는 학습 프로젝트다.

책 4부 = 4주. 한 주에 한 부. 12장까지 한 번 통과하는 게 목표고, 깊이는 두 번째 사이클에서 올린다.

## 도메인

npm·PyPI 패키지, 버전, 의존, 라이선스, 메인테이너, 취약점.

**규모를 고정한다 — 패키지 200개, 버전 2,000개, 의존 엣지 1만 개 선.**
supernode 를 재현하기엔 충분하고 추론기와 Protégé 가 버티는 크기다.
일정이 밀리면 데이터를 줄이지 주차를 밀지 않는다.

책의 `retail.sql` 에 대응하는 관계형 원천은 직접 만든다. 아래는 출발점이고 1주차 CQ 를 쓴 뒤 확정한다.

| 테이블 | 대응하는 학습 지점 |
| --- | --- |
| `package(name, registry)` | 복합키 → IRI (7.3) |
| `package_version(name, registry, version)` | 복합키 → IRI (7.3) |
| `dependency(from_name, from_version, to_name, version_range, kind)` | M:N + 관계 속성 (7.4, 8.2) |
| `license(spdx_id)` | enum (7.4) |
| `package_maintainer(...)` | M:N (7.4) |
| `advisory(cve_id, severity)` | enum (7.4) |

## 제약

- **LLM API 를 호출하는 코드를 쓰지 않는다.** 전 과정을 로컬 도구로 한다 —
  RDFLib · owlrl · pySHACL · Protégé(HermiT·ELK) · Fuseki 또는 GraphDB Free · Neo4j Community.
  Entity Resolution 은 blocking + 문자열 유사도로 한다.
- **12장 GraphRAG 는 검색 층까지만 실행한다.** 청크 임베딩은 로컬 sentence-transformers 로 돌리고,
  생성 층은 평가 프로토콜만 문서로 남기고 실행하지 않는다. 12.07 LangChain 절은 조회로만 본다.

## AI 역할

판단이 들어가면 사람, 반복과 형식이면 AI. 이 경계를 넘으면 책은 읽었는데 남는 게 없다.

- **온톨로지·SHACL·SPARQL 을 대신 작성하지 않는다.** 사람이 쓴 것에 반례를 든다.
- 막혔다고 하면 답을 주기 전에 어디까지 했는지 먼저 묻는다.
- 책 내용은 `./book '<검색어>'` 로 확인하고 **절 번호를 인용한다.** 기억으로 답하지 않는다.
- 코드는 수집·적재·실행 하네스까지만 쓴다. 모델링 결정은 사람이 한다.
- LLM API 를 호출하는 코드는 쓰지 않는다.

### 사람이 하는 것 — 넘기지 않는다

CQ 작성 · IRI 정책 · ADR · 클래스와 프로퍼티 결정 · OWL 공리 · SHACL 제약 선택 ·
CQ 별 SPARQL 작성 · 복합키 IRI 설계 · 매핑 방식 선택 · reifier 와 LPG 중 선택 ·
시간 패턴 선택 · ER feature 와 임계값 정책 · **ER 평가셋 정답 라벨** · 인덱스 결정 · chunk 모델

### AI 가 하는 것

수집 스크립트 · SQLite 적재 · Docker 환경 · 실행 하네스 · 문법 오류 수정 ·
오류 메시지와 EXPLAIN 해석 · 사람이 정한 규칙의 기계적 확장 · 확인 문제 채점 · 반례 제시

## 세션 루틴

- **시작** — "PROGRESS.md 읽고 오늘 할 일 3개 제안해줘"
- **중간** — 직접 쓴 것을 놓고 "이 공리 반박해봐" 또는 `/grilling`
- **끝** — "오늘 한 것 PROGRESS.md 에 반영하고, 내일 막힐 것 같은 지점 하나 짚어줘"

장 끝의 "실패와 복구, 확인 문제"는 직접 풀고 채점만 받는다.

## 책 조회

`./book '<검색어>'` — `~/projects/ask-wikidocs/bookgrep` 을 부른다. 절 본문만 검색한다.
전체 지도는 `~/projects/ask-wikidocs/references/book-map.md` 에 있다.
**볼트를 수정하지 않는다.** 원문은 개인 참고용 사본이다.

## 구성

```
CLAUDE.md          이 파일
PROGRESS.md        주차별 진행 상태 — 세션 시작 때 먼저 읽는다
book               책 본문 검색 래퍼
cq/catalog.md      CQ 카탈로그 (5.7 에서 SPARQL 과 대조한다)
adr/               결정 기록 (2.3)
data/              packages.db 와 수집 원본
rdf/               seed.ttl · pkg.ttl · shapes.ttl · 변환 산출물
queries/           CQ 별 SPARQL
notes/             막힌 것, 받은 반례, 확인 문제 오답
scripts/           수집·적재·실행 하네스
```
