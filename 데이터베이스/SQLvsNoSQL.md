# NoSQL(Non SQL, Not only SQL)

![NoSQL – Scaling for Success | Code Geekz](https://codegeekz.com/wp-content/uploads/NoSQL.png)

- 유연한 데이터 모델을 갖춘 고성능 비관계형 데이터베이스

### 특징

- 유연성 - 유연한 스키마를 제공하여 개발 시 요구사항 변화에 유연하게 대처 가능
- 확장성 - 수평적으로 확장하여 여러 개의 데이터 베이스 서버를 클러스터로 묶어 더 많은 데이터 처리
- 고성능 - 데이터 볼륨이나 트래픽이 증가할 때 관계형 데이터베이스보다 성능이 뛰어남

- 트랜잭션의 ACID(원자성, 일관성, 독립성, 지속성) 미보장



### 유형

- Key Value
  - 해시 테이블을 사용하여 저장
  - 수정 시 전체 데이터를 덮어써서 수행
  - DynamoDB


![키/값 저장소의 데이터 예](https://docs.microsoft.com/ko-kr/azure/architecture/guide/technology-choices/images/key-value.png)

- Document
  - 키 값 데이터베이스를 확장하여 문서 전체를 컬렉션으로 구성
  - MongoDB


![예제 문서 데이터 저장소](https://docs.microsoft.com/ko-kr/azure/architecture/data-guide/big-data/images/document.png)

- Graph
  - Node, Edge 기반 모델을 바탕으로 상호 연결된 데이터를 표현
  - Neo4j


![그래프 데이터 저장소의 데이터 예](https://docs.microsoft.com/ko-kr/azure/architecture/guide/technology-choices/images/graph.png)

- Wide Columnar Store
  - 데이터를 행과 열로 구성
  - Cassandra, HBase


![열 패밀리 데이터의 예](https://docs.microsoft.com/ko-kr/azure/architecture/guide/technology-choices/images/column-family.png)



# SQL vs NoSQL



|             | SQL DB(RDB)                                                  | NoSQL DB                                                     |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 데이터 모델 | 행, 열로 구성된 테이블<br>관계로 그룹화                      | 키값, 문서, 열 형식, 그래프...                               |
| 확장        | 서버 부하를 증가 -> 수직적 확장                              | 서버 분할 -> 수평적 확장                                     |
| 적합한 환경 | - 요구사항이 뚜렷한 관계형 데이터<br />- 복잡한 쿼리. 다중 행 트랜잭션이 필요한 앱 | - 대규모 데이터, 비관게형 데이터, 확정되지 않은 데이터, 빠르게 변화하는 데이터<br />- 일관성 보다 성능과 가용성이 중요한 앱 |
| ACID 속성   | - Atomicity - 실행됨 or 실행되지 않음<br />- Consistency - 데이터가 항상 스키마 준수<br />- Isolation - 트랜잭션들이 서로 영향을 주지 않음<br />- Durability - 트랜잭션 완료시, 영구 반영 | ACID 속성을 완화하여 성능 향상                               |

![Difference between scaling horizontally and vertically for databases -  Stack Overflow](https://i.stack.imgur.com/On3tO.png)

### 참고자료

- SQL과 NoSQL(MongoDB)의 질의어 비교

  https://docs.mongodb.com/manual/reference/sql-comparison/

- NoSQL DB의 수평적 확장 관련 용어: 샤딩(sharding)

​		https://www.mongodb.com/features/database-sharding-explained

### References

https://aws.amazon.com/ko/nosql/

https://www.samsungsds.com/kr/insights/1232564_4627.html

https://azure.microsoft.com/ko-kr/overview/nosql-database/

https://www.oracle.com/kr/database/nosql/what-is-nosql/

https://docs.microsoft.com/ko-kr/azure/architecture/data-guide/big-data/non-relational-data

https://www.youtube.com/watch?v=Q_9cFgzZr8Q&ab_channel=%EB%85%B8%EB%A7%88%EB%93%9C%EC%BD%94%EB%8D%94NomadCoders