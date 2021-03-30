# 쿠버네티스

- 컨테이너 오케스트레이션(Container Orchestration):
    - 컨테이너 배포 관리
    - <컨테이너 배포 프로세스의 최적화>에 목적을 맞추고 있으며,     이것의 자동화를 컨테이너 오케스트레이션(Container Orchestration)라 칭함.

- 이 컨테이너 오케스트레이션을 도와주는 도구중 하나가 쿠버네티스(Kubernetes)

- 자동 배포뿐만 아니라 다음과 같은 기능을 포함
    - 컨테이너 자동 배치 및 복제
    - 컨테이너 그룹에 대한 로드 밸런싱
    - 컨테이너 장애 복구
    - 클러스터 외부에 서비스 노출
    - 컨테이너 추가 또는 제거로 확장 및 축소
    - 컨테이너 서비스간의 인터페이스를 통한 연결 및 네트워크 포트 노출 제어

- 흐름
![흐름](https://tech.osci.kr/assets/images/97465347/9.png)
![흐름2](https://tech.osci.kr/assets/images/97465347/10.png)
    - 하나의 마스터노드와 여러개의 워커노드로 구성
        - 마스터노드 : Worker Nodes의 관리 주체. 전반적인 결정, 이벤트 감지, 반응 담당
            - 요청은 master의 api서버를 호출하고, api 서버는 노드의 kubectl에 명령을 전달
            - 일반적으로 3대로 구성하여 서비스가 안정적으로 운영되도록 함
        - 워커노드 : 할당된 Task를 수행하는 시스템
            - 노드에서 작업을 진행하고 결과나 로그를 반환
            - 실제 컨테이너들이 생성. pod생성, 네트워크와 볼륨 설정.

![다이어그램](https://tech.osci.kr/assets/images/97465347/11.png)
![다이어그램2](https://miro.medium.com/max/875/1*NQXVT1WQZpd7ACD2Lo3cxw.png)
- 구성
    - pod : 쿠버네티스의 가장 작은 작업단위 요소
        - 워커노드 안에 pod가 들어가게 되고, pod안에는 containerized된 application이 들어가는 구조
        - pod 안에있는 컨테이너들끼리 볼륨을 공유하며, 컨테이너가 죽고 재시작되어도 pod가 살아있는한 Shared Volume 유지
        - 각각의 pod는 다른 ip를 가짐. pod안에 있는 컨테이너끼리 내부통신 가능
        - 한개 이상의 컨테이너, 스토리지, 네트워크 속성을 가짐
    
    - kubectl
        - api server에 보내는 복잡한 http 요청을 쉽게 하기위한 CLI

    - api serer
        - 요청의 권한체크, 실행, 거부등 모든 요청 처리

    - etcd
        - 쿠버네티스 클러스터의 모든 설정내용과 상태 저장
        - key-value형태의 데이터베이스
    - kubelet
        - pod의 생명주기 관리
        - master의 요청수행, 로그 전달
    
    








