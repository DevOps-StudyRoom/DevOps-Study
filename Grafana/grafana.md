# Grafana

---

그라파나 (Graphana) 공식 웹 사이트

- https://grafana.com/

그라이파나 라이브 데모 사이트

- https://play.grafana.org/d/000000012/grafana-play-home?orgId=1

* Graphana 란 ?

  - 그라파나(Grafana)는 그라파나 랩(Grafana Labs)에서 오픈소스로 개발하고 있는 메트릭/로그 시각화 대시보드 애플리케이션
  - 모든 metrics 를 위한 분석 플랫폼
  - 처음에는 그라파이트 (Graphite) , 인플럭스DB (InfluxDB), 오픈TSDB (openTSDB) 등을 지원하는 오픈소스 대시보드 도구로 개발 됨
  - AWS 클라우드와치 (AWS CloudeWarch), 애저 모니터 (Azure Monitor) 와 같은 클라우드 데이터 소스를 비롯해 로키(Loki) 나 엘라스틱서치(Elastic Search) 등을 기반으로 로그 데이터를 지원 하는 등 최근에는 더 많은 데이터 소스 지원
  - 이 외에도 스플렁크(Splunk), 뉴 렐릭(New Relic), 오라클(Oracle) 등의 외부서비스와의 통합도 지원해줌

* Graphana 는 언제 이용하는가?

  - Grahpana 는 데이터 소스로부터 차트, 그래프, 알람 등을 웹 환경에서 제공해주는 interactive visualization web applicationd 임. 주로 InfluxDB, Prometheus, Grapite 같은 시계열 데이터베이스와 함께 사용함

* Graphana 개발환경 구성

  - 3단계 솔루션으로 분류
  - 백엔드 , 프론트엔드 , 인터페이스로 MVC 모델과 유사
  - 백엔드는 go, python, SQLite 로 구성됨 (설정에 따라 MySQL 사용가능)
  - 프론트엔드는 anguler.js , javascript 로 구성됨
  - 인터페이스로는 html, javscript, css 로 구성됨
  - 프론트엔드와 인터페이스를 나눈 이유는 그라파나는 플러그인 형식으로 기능을 추가/ 제거 할 수 있는데, 그중 프론트엔드에서 모듈화 된 함수들을 통해 데이터를 지정하거나 사용할 수 있고, 인터페이스는 액션 기능들만 담당하도록 구성되어있기 때문

* Graphana vs Datadag

  - 데이터독의 경우 데이터를 직접 저장하고 있는 것과 달리 그라파나는 외부 데이터 소스를 정의하고, 해당 데이터 소스에 쿼리를 통해서 데이터를 동적으로 가지고 와서 시각화를 지원
  - AWS 서비스가 데이터독에서 크론을 이용해 일정 주기로 데이터를 이용할 경우, 대시보드를 조회하는 동안의 시차가 발생함

* Graphana vs Kibana

  - ELK stack 의 Kibana 와 비교됨
  - 그라파나는 시스템 관점인 CPU 메모리, 디스크 IO 및 사용율과 같은 메트릭스 지표를 시각화하는데 특화되어 있음.
  - 반면 키바나는 엘라스틱 위에서 실행되며 주로 로그메세지 분석에 이용됨.
