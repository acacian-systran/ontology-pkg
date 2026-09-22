# rdf/

## seed.ttl — 손으로 쓰는 시드 (1주차)

책 3장의 산출물이다. **직접 타이핑한다.** 문법을 아는 것과 그래프로 읽히는 건 다른 일이고,
이 30여 줄이 4주 내내 읽기 속도를 결정한다.

트리플 개수가 아니라 문법 요소로 쪼갠다. 한 단계가 10~15분이다.
각 단계 끝에 RDFLib 로 파싱해서 term 을 확인한다 ([3.4]).

| 단계 | 추가 | 새로 쓰는 문법 | 책 |
| --- | ---: | --- | --- |
| S1 | 6 | `@prefix`, IRI, `rdf:type`, 문자열 리터럴 | [3.1]~[3.2] |
| S2 | +6 | `;` 로 주어 반복 줄이기, `,` 로 목적어 묶기 | [3.2] |
| S3 | +8 | 데이터타입 리터럴 (`xsd:date`, `xsd:integer`), 언어태그 | [3.2]~[3.3] |
| S4 | +6 | blank node | [3.2] |
| S5 | +8 | `rdfs:subClassOf`, `rdfs:domain`, `rdfs:range` | [3.6]~[3.7] |

S1 은 이 정도다. 패키지 하나, 버전 하나, 둘의 관계 하나.

```turtle
@prefix ex: <https://example.org/pkg/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

ex:lodash a ex:Package .
ex:lodash ex:name "lodash" .
ex:lodash ex:registry "npm" .
ex:lodash-4.17.21 a ex:PackageVersion .
ex:lodash-4.17.21 ex:versionString "4.17.21" .
ex:lodash ex:hasVersion ex:lodash-4.17.21 .
```

IRI 는 `adr/0001` 에서 정한 정책을 따른다. 위 `ex:` 는 자리표시자다.

S4 의 blank node 는 의존 관계의 버전 범위를 담는 데 쓴다.
3주차 [8.3] reifier 가 이 자리를 다시 건드린다.

**각 단계 끝에 일부러 한 번 깨뜨린다.** 점 빼먹기, prefix 미선언, IRI 에 공백.
[3.9] 가 "실패와 복구"고, 오류 메시지를 미리 봐두면 2주차부터 디버깅이 빨라진다.

## 이후 파일

| 파일 | 주차 | 내용 |
| --- | --- | --- |
| `seed.ttl` | 1 | 손으로 쓴 시드 |
| `pkg.ttl` | 2 | OWL 온톨로지 (TBox) |
| `shapes.ttl` | 2 | SHACL |
| `mapping.r2rml.ttl` | 3 | 관계형 → RDF 매핑 |
| `packages.ttl` | 3 | 전량 변환 결과 (ABox) |

<!-- 절 링크 — references/book.md 에서 나온다 -->
[3.1]: https://wikidocs.net/389920 "3.1 RDF는 파일 형식이 아니라 데이터 모델입니다"
[3.2]: https://wikidocs.net/389921 "3.2 Turtle 문법을 그래프 관점에서 읽기"
[3.3]: https://wikidocs.net/389922 "3.3 도구 - RDF·Turtle 문법 레퍼런스"
[3.4]: https://wikidocs.net/389923 "3.4 RDFLib로 파싱하고 term을 확인하기"
[3.6]: https://wikidocs.net/389925 "3.6 ABox·TBox와 RDFS로 어휘·계층 표현하기"
[3.7]: https://wikidocs.net/389926 "3.7 domain·range의 한계와 RDFS 함의"
[3.9]: https://wikidocs.net/389928 "3.9 실패와 복구, 확인 문제"
[8.3]: https://wikidocs.net/389966 "8.3 RDF 1.2의 triple term과 reifier"
