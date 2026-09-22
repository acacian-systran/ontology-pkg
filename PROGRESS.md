# 진행 상태

**현재 — 1주차 시작 전**
마지막 갱신: (없음)

책 — <https://wikidocs.net/book/20789> · 절 번호는 모두 원문으로 링크된다 (`references/book.md`).

세션을 시작할 때 이 파일을 먼저 읽는다. 끝낼 때 여기에 반영한다.
막힌 것과 받은 반례는 `notes/` 에 쌓고 여기에는 한 줄로만 적는다.

---

## 1주차 — [1부]. 문제를 의미 모델로 바꾸기

책 1~3장 (17절). [`3.3`][3.3] [`3.5`][3.5] [`3.8`][3.8] 은 도구 레퍼런스라 통독하지 않고 실습 중 찾아본다.
2장이 이 주의 중심이다. 여기가 부실하면 3주차 7장에서 되돌아온다.

**읽기**
- [ ] [1장]. 지식그래프와 온톨로지의 전체 지도 ([1.1]~[1.4])
- [ ] [2장]. 요구사항·CQ와 설계 방법론 ([2.1]~[2.4])
- [ ] [3장]. RDF·Turtle·RDFS로 사실과 어휘 표현하기 ([3.1]~[3.9])

**산출물**
- [ ] `cq/catalog.md` — CQ 20개
- [ ] `adr/0001` IRI 정책
- [ ] `adr/0002` 레지스트리 범위
- [ ] `adr/0003` 버전 표현 방식
- [ ] `data/packages.db` — 관계형 원천
- [ ] `rdf/seed.ttl` — 손으로 쓴 시드 (S1~S5, `rdf/README.md` 참고)

**시드 단계**
- [ ] S1 기본 트리플 (6)
- [ ] S2 `;` `,` 축약 (+6)
- [ ] S3 데이터타입·언어태그 (+8)
- [ ] S4 blank node (+6)
- [ ] S5 RDFS 어휘 (+8)

**확인 문제** — [ ] [1.4]  [ ] [2.4]  [ ] [3.9]

---

## 2주차 — [2부]. 의미를 추론하고 품질을 검증하기

책 4~6장 (23절). 레퍼런스 절 [`4.3`][4.3] [`4.6`][4.6] [`5.2`][5.2] [`6.2`][6.2] [`6.6`][6.6].
데이터는 1주차 시드 Turtle 을 쓴다. 대량 데이터는 3주차에 들어온다.

**읽기**
- [ ] [4장]. OWL 2 모델링과 추론 ([4.1]~[4.7])
- [ ] [5장]. SPARQL과 CQ 검증 ([5.1]~[5.8])
- [ ] [6장]. SHACL과 품질 게이트 ([6.1]~[6.8])

**산출물**
- [ ] `rdf/pkg.ttl` — OWL 온톨로지
- [ ] `queries/` — CQ 20개에 대응하는 SPARQL
- [ ] `cq/catalog.md` 에 쿼리 대조 채우기 ([5.7])
- [ ] `rdf/shapes.ttl` — SHACL
- [ ] `notes/shacl-report.md` — 정상·실패 양쪽 검증 보고서 ([6.4], [6.5])

**모델링 결정** — 직접 하고 반례를 요구한다
- [ ] 클래스 계층
- [ ] `dependsOn` 전이성 ([4.2])
- [ ] disjoint — copyleft ↔ permissive ([4.5])
- [ ] Restriction ([4.2])
- [ ] 정의된 클래스 ([4.4])
- [ ] hasKey ([4.5])

공리를 욕심내면 추론기가 느려지고 원인 추적에 며칠 간다. 라이선스 호환성 하나만 제대로 한다.

**확인 문제** — [ ] [4.7]  [ ] [5.8]  [ ] [6.8]

---

## 3주차 — [3부]. 데이터를 옮기고 저장소에 서비스하기

책 7~9장 (21절). 레퍼런스 절 [`9.03`][9.03] [`9.04`][9.04] [`9.06`][9.06] [`9.08`][9.08].
**네 주 중 제일 막히는 주다.** [7.3] 복합키 IRI 가 `패키지@버전` 과 정면으로 부딪힌다.

**읽기**
- [ ] [7장]. 관계형 데이터에서 RDF로 ([7.1]~[7.5])
- [ ] [8장]. RDF·LPG와 RDF 1.2 ([8.1]~[8.5])
- [ ] [9장]. Triple Store와 n10s 운영 ([9.01]~[9.11])

**산출물**
- [ ] `rdf/mapping.r2rml.ttl`
- [ ] `rdf/packages.ttl` — 전량 변환 결과
- [ ] 스토어 적재 (Fuseki 또는 GraphDB Free)
- [ ] named graph 구성 ([9.02])
- [ ] `notes/lpg-projection.md` — 투영 규칙과 정보 손실 기록 ([8.4])
- [ ] round-trip 검증 ([9.10])

**모델링 결정**
- [ ] 복합키 IRI 설계 ([7.3]) — 1주차 `adr/0001` 과 맞는지 확인
- [ ] M:N·enum 매핑 방식 ([7.4])
- [ ] Direct Mapping vs R2RML 선택과 근거 ([7.2], [7.4])
- [ ] 의존 관계 메타데이터 — RDF 1.2 reifier vs LPG 관계 속성 ([8.3], [8.4])

**확인 문제** — [ ] [7.5]  [ ] [8.5]  [ ] [9.11]

---

## 4주차 — [4부]. 운영하고 다음 시스템에 넘기기

책 10~12장 (27절). 레퍼런스 절 [`10.02`][10.02] [`10.04`][10.04] [`10.09`][10.09] [`12.07`][12.07].
절 수는 제일 많지만 10장 Cypher 기초는 SQL 을 알면 빠르게 지나간다.

**읽기**
- [ ] [10장]. Neo4j·Cypher와 ETL·ELT ([10.01]~[10.10])
- [ ] [11장]. 시간·버전 관리와 Entity Resolution ([11.1]~[11.7])
- [ ] [12장]. 운영 최적화와 GraphRAG 인계 ([12.01]~[12.10])

**산출물**
- [ ] Neo4j 적재 (n10s 또는 ETL)
- [ ] 버전 이력 모델 ([11.2])
- [ ] `scripts/er/` — blocking + 점수 ([11.4], [11.5])
- [ ] `notes/er-eval.md` — Precision·Recall·F1
- [ ] `notes/perf.md` — supernode 와 인덱스 개선 기록 ([12.01]~[12.03])
- [ ] `notes/handoff.md` — 인계 계약과 두 층 평가 ([12.08])
- [ ] 재현성 매니페스트 ([12.05])

**모델링 결정**
- [ ] 시간 패턴 세 층 중 선택 ([11.2])
- [ ] ER feature 설계 ([11.5])
- [ ] 임계값 세 구간 정책 ([11.6])
- [ ] ER 평가셋 정답 라벨 — **직접 단다.** AI 가 달면 F1 이 AI 의견과의 일치도가 된다
- [ ] 인덱스 결정 ([12.01])
- [ ] chunk 모델 ([12.06])

**GraphRAG 범위** — 검색 층만 실행한다
- [ ] 청크 모델 설계와 그래프 노드 연결 ([12.06])
- [ ] 로컬 임베딩으로 검색 층 지표 측정 (Recall@k, MRR)
- [ ] 생성 층은 평가 프로토콜만 문서화, 실행하지 않음

**확인 문제** — [ ] [10.10]  [ ] [11.7]  [ ] [12.10]

---

## 부록 — 필요할 때

- [ ] [A-1] 실행 환경과 안전한 코드 실행 (1주차 시작 전)
- [ ] [A-2] 도구별 오류 카탈로그 (막혔을 때)
- [ ] [B-1]~[B-4] 리테일 사례 전체 — 내 도메인 산출물과 대조용
- [ ] [C] 용어집 · [D] 기술 선택

<!-- 절 링크 — references/book.md 에서 나온다 -->
[1부]: https://wikidocs.net/389908 "1부. 문제를 의미 모델로 바꾸기"
[1장]: https://wikidocs.net/389909 "1장. 지식그래프와 온톨로지의 전체 지도"
[2부]: https://wikidocs.net/389929 "2부. 의미를 추론하고 품질을 검증하기"
[2장]: https://wikidocs.net/389914 "2장. 요구사항·CQ와 설계 방법론"
[3부]: https://wikidocs.net/389956 "3부. 데이터를 옮기고 저장소에 서비스하기"
[3장]: https://wikidocs.net/389919 "3장. RDF·Turtle·RDFS로 사실과 어휘 표현하기"
[4부]: https://wikidocs.net/389981 "4부. 운영하고 다음 시스템에 넘기기"
[4장]: https://wikidocs.net/389930 "4장. OWL 2 모델링과 추론"
[5장]: https://wikidocs.net/389938 "5장. SPARQL과 CQ 검증"
[6장]: https://wikidocs.net/389947 "6장. SHACL과 품질 게이트"
[7장]: https://wikidocs.net/389957 "7장. 관계형 데이터에서 RDF로"
[8장]: https://wikidocs.net/389963 "8장. RDF·LPG와 RDF 1.2"
[9장]: https://wikidocs.net/389969 "9장. Triple Store와 n10s 운영"
[10장]: https://wikidocs.net/389982 "10장. Neo4j·Cypher와 ETL·ELT"
[11장]: https://wikidocs.net/389993 "11장. 시간·버전 관리와 Entity Resolution"
[12장]: https://wikidocs.net/390001 "12장. 운영 최적화와 GraphRAG 인계"
[1.1]: https://wikidocs.net/389910 "1.1 데이터가 있는데도 답하기 어려운 이유"
[1.4]: https://wikidocs.net/389913 "1.4 함께 풀어 보기와 확인 문제"
[2.1]: https://wikidocs.net/389915 "2.1 모델보다 질문을 먼저 만드는 이유"
[2.4]: https://wikidocs.net/389918 "2.4 실패와 복구, 확인 문제"
[3.1]: https://wikidocs.net/389920 "3.1 RDF는 파일 형식이 아니라 데이터 모델입니다"
[3.3]: https://wikidocs.net/389922 "3.3 도구 - RDF·Turtle 문법 레퍼런스"
[3.5]: https://wikidocs.net/389924 "3.5 도구 - RDFLib 실전 레퍼런스"
[3.8]: https://wikidocs.net/389927 "3.8 도구 - owlrl 추론 레퍼런스"
[3.9]: https://wikidocs.net/389928 "3.9 실패와 복구, 확인 문제"
[4.1]: https://wikidocs.net/389931 "4.1 OWL이 필요한 이유와 OWL 2 프로파일"
[4.2]: https://wikidocs.net/389932 "4.2 프로퍼티 특성과 Restriction"
[4.3]: https://wikidocs.net/389933 "4.3 도구 - OWL 2 레퍼런스"
[4.4]: https://wikidocs.net/389934 "4.4 OWA·no-UNA와 정의된 클래스"
[4.5]: https://wikidocs.net/389935 "4.5 조합·배타성·hasKey와 Reasoner"
[4.6]: https://wikidocs.net/389936 "4.6 도구 - Protégé로 공리 검토하기"
[4.7]: https://wikidocs.net/389937 "4.7 실패와 복구, 확인 문제"
[5.1]: https://wikidocs.net/389939 "5.1 SPARQL은 solution mapping을 만듭니다"
[5.2]: https://wikidocs.net/389940 "5.2 도구 - SPARQL 1.1 레퍼런스"
[5.7]: https://wikidocs.net/389945 "5.7 CQ 카탈로그와 SPARQL 쿼리 대조"
[5.8]: https://wikidocs.net/389946 "5.8 실패와 복구, 확인 문제"
[6.1]: https://wikidocs.net/389948 "6.1 SHACL은 무엇을 검사하나요"
[6.2]: https://wikidocs.net/389949 "6.2 도구 - SHACL 레퍼런스"
[6.4]: https://wikidocs.net/389951 "6.4 검증 보고서를 읽는 법"
[6.5]: https://wikidocs.net/389952 "6.5 pySHACL로 정상·실패를 함께 확인하기"
[6.6]: https://wikidocs.net/389953 "6.6 도구 - pySHACL 실전 레퍼런스"
[6.8]: https://wikidocs.net/389955 "6.8 실패와 복구, 확인 문제"
[7.1]: https://wikidocs.net/389958 "7.1 패러다임 차이와 고정 SQLite 원천"
[7.2]: https://wikidocs.net/389959 "7.2 Direct Mapping과 R2RML"
[7.3]: https://wikidocs.net/389960 "7.3 복합키를 IRI로 만들기"
[7.4]: https://wikidocs.net/389961 "7.4 M -N, enum, 매핑 방식 선택"
[7.5]: https://wikidocs.net/389962 "7.5 실패와 복구, 확인 문제"
[8.1]: https://wikidocs.net/389964 "8.1 RDF와 LPG의 설계 중심"
[8.3]: https://wikidocs.net/389966 "8.3 RDF 1.2의 triple term과 reifier"
[8.4]: https://wikidocs.net/389967 "8.4 투영 규칙, 정보 손실, n10s 선택"
[8.5]: https://wikidocs.net/389968 "8.5 실패와 복구, 확인 문제"
[9.01]: https://wikidocs.net/389970 "9.01 Triple Store가 더 제공하는 것과 인덱싱"
[9.02]: https://wikidocs.net/389971 "9.02 RDF Dataset과 named graph"
[9.03]: https://wikidocs.net/389972 "9.03 도구 - Docker로 스토어 운영하기"
[9.04]: https://wikidocs.net/389973 "9.04 도구 - Fuseki·GraphDB 제품 레퍼런스"
[9.06]: https://wikidocs.net/389975 "9.06 도구 - neosemantics(n10s) 레퍼런스"
[9.08]: https://wikidocs.net/389977 "9.08 도구 - SPARQLWrapper로 원격 엔드포인트 다루기"
[9.10]: https://wikidocs.net/389979 "9.10 n10s 계약, namespace, round-trip, 증거"
[9.11]: https://wikidocs.net/389980 "9.11 실패와 복구, 확인 문제"
[10.01]: https://wikidocs.net/389983 "10.01 LPG 모델과 Cypher 버전 기준"
[10.02]: https://wikidocs.net/389984 "10.02 도구 - Neo4j 서버·드라이버 레퍼런스"
[10.04]: https://wikidocs.net/389986 "10.04 도구 - Cypher 레퍼런스"
[10.09]: https://wikidocs.net/389991 "10.09 도구 - APOC 레퍼런스"
[10.10]: https://wikidocs.net/389992 "10.10 실패와 복구, 확인 문제"
[11.1]: https://wikidocs.net/389994 "11.1 현재값만 저장하면 잃는 질문"
[11.2]: https://wikidocs.net/389995 "11.2 RDF 시간 패턴과 버전 관리 세 층"
[11.4]: https://wikidocs.net/389997 "11.4 Entity Resolution과 blocking"
[11.5]: https://wikidocs.net/389998 "11.5 Feature·점수와 Precision·Recall·F1"
[11.6]: https://wikidocs.net/389999 "11.6 세 구간 정책, 병합, Undo receipt"
[11.7]: https://wikidocs.net/390000 "11.7 실패와 복구, 확인 문제"
[12.01]: https://wikidocs.net/390002 "12.01 성능이 무너지는 두 지점과 인덱스"
[12.03]: https://wikidocs.net/390004 "12.03 Cartesian product와 Supernode"
[12.05]: https://wikidocs.net/390006 "12.05 재현성 매니페스트"
[12.06]: https://wikidocs.net/390007 "12.06 GraphRAG가 더하는 것과 chunk 모델"
[12.07]: https://wikidocs.net/390008 "12.07 도구 - LangChain 그래프 연동 레퍼런스"
[12.08]: https://wikidocs.net/390009 "12.08 인계 계약과 두 층 평가"
[12.10]: https://wikidocs.net/390011 "12.10 실패와 복구, 확인 문제, 마치며"
[A-1]: https://wikidocs.net/390013 "부록 A-1. 실행 환경과 안전한 코드 실행"
[A-2]: https://wikidocs.net/390014 "부록 A-2. 도구별 오류 카탈로그와 자가진단"
[B-1]: https://wikidocs.net/390015 "부록 B-1. 부록 사용법과 관계형 원천"
[B-4]: https://wikidocs.net/390018 "부록 B-4. Neo4j 파생 뷰, GraphRAG handoff, 오프라인 검증"
[C]: https://wikidocs.net/390019 "부록 C. 용어집과 개념 색인"
[D]: https://wikidocs.net/390020 "부록 D. 기술 선택과 참고문헌"
