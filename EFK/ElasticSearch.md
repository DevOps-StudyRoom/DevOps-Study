Apache Lucene
- https://lucene.apache.org/core/index.html

ElasticSearch ?
- What is ElasticSearch? https://www.elastic.co/guide/en/elasticsearch/reference/current/elasticsearch-intro.html
- Data in: documents and indices? https://www.elastic.co/guide/en/elasticsearch/reference/current/documents-indices.html
- Information out: search and analyze? https://www.elastic.co/guide/en/elasticsearch/reference/current/search-analyze.html
- Scalability and resilience: clusters, nodes, and shards? https://www.elastic.co/guide/en/elasticsearch/reference/current/scalability.html

우아한 형제들 ElasticSearch 튜닝기
- https://woowabros.github.io/woowabros/2021/03/02/search-system.html

## 1. EFK(Elasticsearch + Fluentd + Kibana)란 무엇인가?
EFK란 Elasticsearch + Fluentd + Kibana의 조합을 일컫는다. 보통 Log처럼 지속적으로 누적되는 데이터를 실시간으로 분석할 때 많이 사용한다. 흔히들 알고 있는 ELK Stack은 ElasticSearch, Logstash, Kibana의 조합인데, Logstash 대신 Fluentd를 사용할 경우 EFK Stack이라고 부르기도 한다.
모니터링 시스템 구축 시 로그 수집기를 Logstash를 사용할지 Fluentd를 사용할지는 선택사항이지만, 필자가 EFK Stack 구축으로 글을 쓰는 이유는 Fluentd는 쿠버네티스와 같은 CNCF(Cloud Native Computing Foundation) Stack이라 요즘 마이크로서비스 모니터링 시스템 구축 시 많이 사용되기 때문이다.
EFK Stack에서 Elasticsearch, Fluentd, Kibana는 다음과 같은 역할을 수행한다.
1) Fluentd : 데이터(로그)를 수집해서 Elasticsearch로 전달
2) Elasticsearch : Fluentd로부터 받은 데이터를 검색 및 집계하여 필요한 정보 획득
3) Kibana : Elasticsearch의 빠른 검색능력을 통해 데이터 시각화 및 모니터링

### 1-1. Fluentd란?
Fluentd란 오픈소스 데이터(로그) 수집기이다. 보통 로그를 수집하는데 사용하지만, 다양한 데이터 소스(HTTP, TCP)로부터 데이터를 받아올 수 있다. Fluentd로 전달된 데이터는 tag, time, record(JSON) 로 구성된 이벤트로 처리되며, 원하는 형태로 가공되어 다양한 목적지(ElasticSearch, S3 등)로 전달될 수 있으며 Fail-Over를 위한 HA(High Availability) 구성도 가능하다. 
Fluentd는 C와 Ruby로 개발되었으며, 더 적은 메모리를 사용하는 경량버전인 Fluent-Bit와 함께 사용할 수 있다(하지만 Fluent-Bit의 경우 HA 구성이 되지 않는다). 

### 1-2. Elasticsearch란?
Elasticsearch는 아파치 루씬 기반의 확장성이 좋은 JAVA 오픈소스 분산 검색엔진이다. 많은 양의 데이터를 보관하고 실시간으로 저장, 검색, 분석할 수 있게 해준다.
Elasticsearch는 다음과 같은 특징을 가지고 있다.
1) 테이블과 스키마 대신에 문서 형식(JSON)으로 저장한다.
2) 쿼리 속도가 매우 빠르며 확장성이 뛰어나다
3) 에러에 대한 높은 탄성을 가지고 있으며 데이터 타입에 유연하다
4) 빅데이터를 처리할 때 매우 유리하다.

### 1-3. Kibana란?
Kibana는 Elasticsearch에서 색인된 데이터를 검색하고 시각화하는 오픈소스 도구이다. Elasticsearch의 데이터(로그)를 차트와 그래프 등을 활용하여 대쉬보드 형태로 시각화 할 수 있다. 

---

# ElasticSearch 가이드북
https://esbook.kimjmin.net/


- 클러스터 구성
- https://esbook.kimjmin.net/03-cluster/3.1-cluster-settings
- 인덱스와 샤드
- https://esbook.kimjmin.net/03-cluster/3.2-index-and-shards
- 마스터 노드와 데이터노드
- https://esbook.kimjmin.net/03-cluster/3.3-master-and-data-nodes

ElasticSearch의 검색, 빠른 이유
- 역인덱스
- https://esbook.kimjmin.net/06-text-analysis/6.1-indexing-data
- 텍스트분석
- https://esbook.kimjmin.net/06-text-analysis/6.2-text-analysis
