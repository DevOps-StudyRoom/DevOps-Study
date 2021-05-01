![Rancher 이미지](https://rancher.com/img/logo-square.png)

- [`Rancher`](https://rancher.com/)

  > Rancher is not a container orchestrator. It's a complete container management platform that includes everything you need to manage containers in production. You can quickly deploy multiple Docker and Kubernetes clusters across multiple clouds with the click of a button.

  - `Rancher`란?
    ![세부사항](https://user-images.githubusercontent.com/69498804/96835487-99944d00-147e-11eb-883d-602a97991ed7.png)
    - 컨테이너를 채택한 팀을위한 완벽한 소프트웨어 스택
    - `Rancher`는 `Kubernetes` 클러스터 관리를 단순화하는 오픈소스 플랫폼
    - 모든 인프라에서 여러 `Kubernetes` 클러스터를 관리해야하는 운영 및 보안 문제를 해결하는 동시에 `DevOps `팀에 컨테이너화 된 워크로드 실행을위한 통합 도구를 제공
    - 도커 환경에서 실행되며 쿠버네티스를 도커 환경에서 구축
      - 간단하게 컨테이너를 관리하기 위한 플랫폼
      - `Docker` 및 `Kubernetes` 클러스터를 신속하게 배포
  - 실행되는 각각의 컨테이너에 대한 리소스 사용율을 확인할 수 있음
    
   - `Rancher`를 쓰는 이유?
      - 다양한 `On-Premise` 지원
      - 다양한 `Public Cloud` 지원
      - 다양한 기능 및 통합 관리 제공
        - 통합 멀티 클러스터 관리
        - 앱 카탈로그
      - 간편한 `UI`      
  
  ![Rancher GUI](https://cdn.thenewstack.io/media/2019/06/34a23cbe-401253e6-screen-shot-2019-06-21-at-18.04.24-1024x559.png)
  
    - `GUI`로 돌아가는 전반적인 쿠버네티스의 형태를 파악할 수 있음
      - `CUI`를 제공하는 쿠버네티스보다 쉽고 간편함
      - web기반 GUI와 command line 인터페이스로 쿠버네티스 클러스터를 구성할 수 있고 확장 또한 쉽게 가능
        - `kubernetes`를 웹기반으로 쉽게 관리
      - 이미 존재하는 클러스터도 `import`하여 `rancher` 인터페이스로 관리가 가능
      - 제공되는 리포지토리에서 필요한 `application`들을 쉽게 배포
    - 결론적으로 무수히 많은 서버를 `Docker Container`를 통해 관리하고, `Docker Container`를  쿠버네티스를 통해 관리하고, 쿠버네티스를 더 쉽게 관리하는 것이 `Rancher`
    - 컨테이너 워크로드를 보다 쉽게 관리할 수 있도록 도와주는 멀티 클러스터 관리 플랫폼
  - 모니터링, 알람, 알림서비스, 로깅 등의 기능을 제공
  
![Rancher의 구조](https://rancher.com/docs/one-point-x/img/rancher/rancher_overview_2.png)
  
![Rancher의 구조](https://rancher.com/docs/img/rancher/platform.png)
  
  - `Rancher` 설치
    - `sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher`
    - `docker run -d --restart=unless-stopped -p 80:80 -p 443:443 -v /host/certs:/container/certs -e SSL_CERT_DIR="/container/certs" rancher/rancher:latest`
  
  - 최초 접속시
    - admin 계정의 비밀번호 및 server 주소를 설정
  

> Docker를 통해 각각의 노드(Container)를 생성하고, Rancher를 통해 해당 노드를 일괄적으로 관리할 수 있습니다!! 최근 Rancher와 쿠버네티스가 합쳐진 서비스가 나와 일괄적으로 설치하고 서비스를 개발할 수 있습니다.

### 참고자료

- [Rancher 사용법 정리](https://couplewith.tistory.com/entry/Rancher%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-Kubernetes-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0%EB%A5%BC-%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)

- [Rancher 사용법 정리](https://www.joinc.co.kr/w/man/12/docker/rancher/install2.0)
- [Rancher 설치 자세하게](https://blog.crois.net/2019/09/17/rancher-rancher-%EC%84%A4%EC%B9%98/)

