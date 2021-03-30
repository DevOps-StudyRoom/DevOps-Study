# Fluentd

<img src="https://www.fluentd.org/images/fluentd-architecture.png" width= 480px height=320px>




공식 사이트 : https://www.fluentd.org/

Github : https://github.com/fluent/fluentd

Fluentd의 내부 구조 : https://bcho.tistory.com/1115

Fluentd 란? : https://skasha.tistory.com/99



* Fluentd란 무엇인가?

  * Fluentd는 데이터를 수집할 때 사용하는 오픈소스이다.
  * 많은 데이터 소스와 시스템에서 수집된 로그를 하나의 로깅 레이어로 통합시키는 데 목적을 두고 있다.
  * 로그를 수집하기도 하지만, 다양한 데이터 소스로부터 데이터를 받아오는 역할도 한다.
  * Fluentd를 사용하면 데이터 수집과 소비를 통합해 데이터를 더 잘 사용하고 이해할 수 있다. (공식 사이트)
  * 데이터를 가능한 한 JSON 형식으로 구조화하려고 한다.
  * 이를 통해 여러 소스와 대상에 걸쳐 로그 데이터의 모든 측면을 통합할 수 있다.
  * 로그를 수집하는 기능만 있기 때문에, ElasticSearch, Kibana같은 로그 분석 및 시각화 엔진과 함께 사용한다.


+ Fluentd를 사용하는 이유
  + C와 Ruby의 조합으로 작성되어 시스템 자원을 거의 필요로 하지 않는다.
  + 더 적은 메모리를 필요로 하는 환경에서는 Fluentd-bit 이라는 경량화 버전과 함께 사용할 수 있다.
  + 메모리 및 파일 기반 버퍼링을 지원하여 노드 간 데이터 손실을 방지한다.
  + 강력한 Fail-Over 를 지원하며 이를 위한 high availability를 설정할 수 있다.
  + 직관적인 문법을 사용해 이해하고 사용하기 쉬우며, Fluentd의 다운로드, 플러그인 다운로드와 배포 역시 편하다.


* 기본적인 흐름
  * Fluentd는 C와 Ruby가 기반이기 때문에 매우 가볍고 빠르다.
  * 기본적으로 원하는 기능들을 플러그인 방식으로 설정 파일에 추가함으로써 사용한다.'
  * 전반적으로 Input -> Filter -> Buffer -> Output의 흐름으로 동작한다.


* 입력 플러그인
  * 입력 플러그인(Input) 외부 소스에서 이벤트 로그를 검색하고 가져온다.
  * 입력 플러그인은 데이터에서 event를 생성한다. 이벤트의 구조는 Tag, Time, Record로 구성된다.
    + Tag는 이벤트의 구분값이다. Tag로 source를 구분해서 처리한다.
    + Time은 이벤트의 생성 시간이다.
    + Record는 JSON 형태로 되어있는 이벤트의 내용이다.
  * 주기적으로 데이터 소스를 가져오도록 할 수도 있다.

* Filter 플러그인
  * Fluentd 이벤트 스트림을 수정한다.
    + 특정 필드에 대한 필터링 조건을 적용한다.
    + 새로운 필드를 추가한다.
    + 필드를 삭제하거나 값을 숨긴다.

* Output 플러그인
  * 출력 플러그인은 이벤트를 내보낸다.
  * <match> 섹션에 정의한다.
  * ElasticSearch 로 이벤트 레코드를 전송할 때는 output_elasticsearch를 사용한다.

* Buffer 플러그인
  * Output 플러그인에서 사용된다.
  * chunk 집합을 담고 있으며, 각 chunk는 이벤트 묶음이 저장된 하나의 Blob 파일이다.
  * chunk 가 가득차면, 다음 목적지로 전달이 된다.
