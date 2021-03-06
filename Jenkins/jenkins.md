![젠킨스](https://media.vlpt.us/images/beoms96/post/05b4d550-7403-4fcb-8612-61abab463f05/logo-title-opengraph.png)

# CI/CD 란?

- `CI/CD` 란?
    + `CI`
        * `Continuous Integration`
        * `Code`에 대한 지속적인 통합
        * 여러 개발자들의 코드베이스를 계속해서 통합하는 것
    + `CD`
        * `Continuous Delivery`
        * 사용자에게 제품 및 서비스를 지속적으로 제공
        * 코드베이스가 항상 배포가 가능한 상태를 유지!!
    + `CD`
        * `Continuous Deployment`
        * 코드베이스를 사용자가 사용 가능한 환경에 배포하는 것을 자동화함
    + 각각의 개발자들이 개발을 하는 개발을 하는 개발 환경을 사용자가 사용 가능한 서비스로 전달하는 모든 과정을 지속 가능한 형태로 또 가능하다면 자동으로 해서 개발자와 사용자 사이의 격차를 없애는 것!!
    + 위의 과정에는 코드를 빌드하고, 테스트하고 배포하는 활동이 포함됨!
    
![CI/CD](https://www.redhat.com/cms/managed-files/ci-cd-flow-desktop_1.png)

- `CI 필요성`
    + 각각의 개발자들의 코드를 통합할때 문제가 발생하는 것을 방지
    + 가능한 빠르고, 많이 본인의 코드를 코드베이스에 안착!!
    + 테스트 코드 없는 무서운 코드 버그 더미 코드를 코드베이스에서 제외시킴

- `CD 필요성`
    + `CD`를 통해 배포를 지속적으로 수행!!
    + 개발자는 코드만 작성하면 됨

- `CI/CD의 목적`
    + 외부 사용자 뿐만 아니라 내부 사용자에게도 디버거를 지속적으로 전달할때 사용
        * 내부 사용자는 백엔드, 프론트 엔드 등의 개발자..

- `Jenkins`
    + `Jenkins`는 `CI/CD`를 진행하는 프로그램
    + `CI/CD Pipe Line`
        * 코드 작성
        * 빌드 -> ex Webpack, Tsc, javac
        * 테스트 -> Jest, Junit
        * 배포 -> esc update
        * 각 단계를 갖춰 수행됨
    + 개발자가 수행해야 하는 귀찮은 작업들을 대신 수행해줌!!
    + `Java Runtime` 위에서 동작하는 자동화 서버
    + 빌드, 테스트, 배포 등 모든 것을 자동화 해주는 자동화 서버
    + 다양한 플러그인들을 활용해서 각종 자동화 작업을 처리할 수 있음
    + 일련의 자동화 작업의 순서들의 집합인 `Pipe-Line`을 통해 `CI/CD` 파이프라인을 구축
    + 젠킨스는 단지 서비일 뿐
        * 배포에 필요한 각종 리소스에 접근하기 위해서 여러가지 중요 정보를 저장해야됨

- `Jenkins Plugin`
    + 대표적인 플러그인
        * `Credentials Plugin`
            + 중요한 정보를 저장해 주는 플러그인
        * `Git plugin`
        * `PipeLine`
            + `PipeLine`을 관리하는 플러그인
        * `Docker Plugin and Docker PipeLine`
            * `Docker Agent`를 사용하고 젠킨스에서 도커를 사용하기 위해 쓰는 플러그인
    + 다양한 플러그인이 존재

![Jenkins PIPLine](https://qph.fs.quoracdn.net/main-qimg-928f83effe3f46296ef857b098c1e2a6)

- `Pipe Line`
    + `CI/CD` 파이프라인을 젠킨스에 구현하기 위한 일련의 플러그인들의 집합 또는 구성
        * 여러 플러그인들을 파이프라인에서 용도에 맞게 사용하고 정의함으로써 파이프라인을 통해 서비스가 배포됨
    + `PipeLine DSL(Domain Specific Language`로 작성
    + 구성 요소
        * `Declarative` 문법
        * `Scripted PipleLine` 문법

- `PipeLine Syntax`
    + `Agent Section`
        * 여러 `slave node`를 두고 일을 시킬 수 있는데, 어떤 젠킨스가 일을 하게 할 것인지 지정
        * 젠킨스 노드 관리에서 새로 노드를 띄우거나 혹은 docker 이미지 등을 통해서 처리 가능
    + `Post Section`
        * 스테이지가 끝 난 이후의 결과에 따라서 후속 조치를 취할 수 있음
    + `Stages Section`
        * 어떤 일들을 처리할 건지 일련의 `stage`를 정의함
    + `Steps Section`
        * 한 스테이지 안에서의 단계로 일련의 스텝을 보여줌
    + `Declaratives`
        * 각 스테이지에서 어떤 일을 수행할지 정의
    + `Steps`
        * `Steps` 내부는 여러가지 스탭들로 구성
        * 여러 작업들을 실행가능
        * 플러그인을 깔면 사용할 수 있는 스탭들이 생겨남

- 개발 환경의 종류
    + 개발자가 개발을 하는 `Local` 환경
        * 자신의 `workspace`
    + 개발자들끼리 개발 내용에 대한 통합 테스트를 하는 `Development` 환경 --> `DEV`
    + 개발이 끝나고 `QA` 엔지니어 및 내부 사용자들이 사용해 보기 위한 `QA` 환경 --> `QA`
    + 실제 유저가 사용하는 `Production` 환경 --> `PROD`

- `CI/CD의 기본 동작`
    + 개발 프로세스
        * 개발자가 자신의 `PC`에서 개발을 진행
        * 다른 개발자가 작성한 코드와 차이가 발생하지 않는지 내부 테스트 진행
        * 진행한 내용을 다른 개발자들과 공유하기 위해 `git`과 같은 `SCM`에 올림
        * `DEV`브랜치의 내용을 개발 환경에 배포하기 전에 테스트와 `Lint` 등 코드 포맷팅 진행
        * 배포하기 위한 빌드과정 거침
        * 코드 배포
        * 테스트 진행
        * 위의 모든 과정을 `DEV, QA, PROD` 환경에서 모두 진행하고 각각에 맞는 환경에 배포

- 여러 배포 환경의 관리
    + 인프라를 모듈화하여 어떤것이 변수인지 잘 설정하고, 설계
    + 키 관리 서비스를 사용하는 것을 추천!!
