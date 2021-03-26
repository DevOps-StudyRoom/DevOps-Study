#Docker
-------
* Docker란
  + 컨테이너 기반의 가상화 플랫폼(오픈소)
  +  이미지를 컨테이너에 띄우고 실행하는 것
  +  도커를 관리하는 서비스 = 쿠버네티스
  +  한 개의 컨테이너 관리 = 도커, 여러개의 컨테이너 관리 =쿠버네티스
  + 이점:모듈성, 이미지 버전 제어, 롤백, 신속한 배포  


* Docker의 패러다임
  + 변경 불가능한 인프라 (Stateless, Scalable)
    + 서버를 구축한 이후 변경이나 업데이트를 할 수 없음
    + 변경이나 업데이트시 새로운 도커 이미지 생성 후 컨테이너 생성 기존 컨테이너는 삭제


* 컨테이너 란?
  + 웹이나 앱을 구동하는 환경을 격리한 공간
  + 마이크로서비스로 사용
    + 서비스 별로 나누어 컨테이너 생성 가능
    + 각 컨테이너별로 변경/조합 가능
    + 각각 분리되어 다른 기능들에 영향을 미치지 않음
    + 모놀리식과 반대되는 개념
  + 가상 머신에 프로그램을 띄우는 것과 유사


* 가상머신과 컨테이너의 차이
  + 가상머신
    + Server -> Hypervisor -> Guest OS -> VM
    + Os 및 커널을 통째로 가상화
    + 가상 머신의 모든 자원을 사용
  + 컨테이너
    + Server -> Host Os -> Docker Engine -> Container
    + 자원을 필요한 만큼 격리하여 할당
    + 이미지 파일의 크기가 작아 빠르게 실행 가능
  + 커널 = 운영체제의 핵심 하드웨어 자원을 나누고 시스템의 모든 것을 통제


* Docker 기술
  + Cgroups
    + 자원에 대한 제어를 가능하게 해주는 기능
    + 메모리
    + CPU
    + I/0
    + 네트워크
    + device 노드
  + Namespace
    + 게스트 머신별 독립적인 공간에서 충돌하지 않도록 하는 기능(독립적)
    + mnt(마운트): 파일 시스템을 마운트, 언마운트 가능
    + pid(프로세스): 프로세스 공간 할당
    + net(네트워크): network 충돌 방지
    + ipc(SystemV IPC): 통신통로 할당
    + uts(hostname): hostname 할당
    + user(UID): 사용자 할당

* Docker 컨테이너 실행과정
  1. Docker Client에서 실행 명령 입력
  2. 명령을 받은 Docker Sever(=Docker Daemon)는 Image Cache에서 이미지가 있는지 확인
      + 이미지가 있는 경우
    이미지를 실행하여 컨테이너 생성 후 Client로 출력
      + 이미지가 없는 경우
    Docker Hub에 검색해서 Image Cahce에 다운 후 컨테이너 생성, 출력
  +Docker file -> Docker Client -> Docker Server -> Usable image
  + Docker Client: 명령을 내리는 도구(수행하는 것은 없지만 상호작용하는 역활)
  + Docker Server: 이미지 생성, 컨테이너 실행 등을 담당(실제 수행)


* Docker file
  + Docker File은 image를 만들기 위한 명령어의 집합, 빌드 및 배포를 자동화 가능
  + 작성법
    FROM: <명령어> 생성할 이미지의 베이스 이미지

    WORKDR  </user/app> 명령어를 실행할 경로

    RUN: <명령어> 컨테이너 내부에서 입력한 커멘드를 수행, 도커와 관련 없음

    COPY <복사할 파일 경로> <이미지에서 파일이 위치할 경로>

    CMD: {command} 생성된 컨테이너에서 명령
    
