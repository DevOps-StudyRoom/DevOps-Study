# DevOPs
> 신뢰성과 보안성 기반으로 빠른 개발과 테스팅을 진행하며 최종적으로 배포를 진행하는 일련의 과정을 순환하는 체계

![사진](https://dinfree.com/lecture/backend/img/jw_1.2_1.png)

### `Devops` 란?
    + 애플리케이션과 서비스를 빠른 속도로 제공할 수 있도록 조직의 역량을 향상시키는 문화 철학, 방식 및 도구의 조합
    + 기존의 소프트웨어 개발 및 인프라 관리 프로세스를 사용하는 조직보다 제품을 더 빠르게 혁신하고 개선
    + 개발과 운영의 합성어로 개발과 운영 간의 상호 작용을 원활하게 하기 위한 개발 방법론
    + 개발자와 비 개발자 사이의 대화, 협동, 통합을 강조하고 담당 업무와 직급 간 상호 이해를 추구

### `Devops` 특징
    + `Cross Functional Team`
    + `Widely Shared Metrics`
    + `Automating repetitive tasks`
    + `Post Mortems`
    + `Regular Release`

### `DevOps ToolChain`
![Devops](http://www.datanet.co.kr/news/photo/201907/135675_61340_711.jpg)
    
- 계획
- 코딩
- 구축
- 테스트
- 배포
- 운영
- 모니터링

### `DevOps`의 주된 요소
- 품질
    + 테스트 자동화
       - 서비스 통합/시스템 테스트
       - 단위 테스트 `xUnit`, `UI` 테스
    + 프로세스 내재화
       - 업무백로그-운영을 프로세스화
       - 운영 이슈 개선 위한 프로세스
- 프로세스	
    + 소규모 릴리즈	
       - 변화에 유연, 롤백 용이
       - `Cycle-time` 감소, 피드백 강화
    + 지속적 통합 `Cont. Integration`
       - 개발초기-릴리즈 간 요구 반영
       - `CMDB` 코드 통합, `Test`, `Release`
- 도구	
    + 어플리케이션 릴리즈 자동화	
       - 개발팀은 형상관리 기반 배치
       - 운영팀은 표준화`GW` 사용
    + 프로비저닝	
       - 코드 자동 설치, 시스템 구성
       - `Tool`: 퍼펫`Puppet`, 셰프`Chef`
