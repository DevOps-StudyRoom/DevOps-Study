![Docker](https://subicura.com/assets/article_images/2017-01-19-docker-guide-for-beginners-1/docker-logo.png)

- 도커의 등장
  - 도커는 이미지를 통해서 다양한 환경을 제공
- 컨테이너는 무엇일까? --> 하드웨어 가상화 없는 격리된 환경에서 실행되는 프로세스
  - 컨테이너는 서로 다른 환경
  - OS에서 지원하는 기능을 사용
  - 격리된 환경에서 프로세스를 실행 --> 컨테이너는 격리된 환경에서 사용하는 프로세스
  - 컨테이너는 하드웨어를 가상화가 아님
  - 격리된 프로세스, 컨테이너는 프로세스!
    - ex) 각각의 VM도 서로 다른 환경
    - VM은 하드웨어 가상화 -> 소프트웨어로 구성된 하드웨어

![Docker-Container](https://codingthesmartway.com/wp-content/uploads/2019/02/010.png)

- 컨테이너는 왜 필요할까?
  - 특정 하드웨어 및 소프트웨어의 환경이 너무 다양함 --> 상태 관리가 어려움
    - Dockerfile은 깨끗한 환경에서 부터 애플리케이션 실행 환경까지 최단 경로로 이용
    - 이미지를 만들어 두고 프로세스를 만들어두면 작동원리의 보장이 가능
      - 하나의 이미지로 하나의 환경을 제공
      - 이미지의 공유가 가능
- 이미지
  - 특정 프로세스를 실행하기 위한 환경
    - 계층화된 파일 시스템
    - 이미지는 파일들의 집합
    - 프로세스가 실행되는 환경도 결과적으로 파일들의 집합!!

![Doker-Architecture](https://devopedia.org/images/article/101/8323.1565281088.png)

- 도커의 아키텍쳐

  - (리눅스 (docker  --- server ----container))

- 도커 설치하기

  - 리눅스에서 설치
    - `curl -s https://get.docker.com/ | sudo sh`
  - 윈도우, 맥에서도 설치 가능

- 도커 버전 확인하기

  - `docker version`

- 도커 컨테이너 실행하기 

  - `docker run ubuntu:16.04`

- 컨테이너 실행하기

  - `docker run --rm -it ubuntu:16.04 /bin/sh`

- 간단한 웹 애플리케이션을 컨테이너로 생성

  ```sh
  docker run -d -p 4567:4567 subicura/docker-workshop-app:1
  ```

  - detached mode(백그라운드 모드)로  실행하기  위해    -d 옵션을  추가
  - -p 옵션을  추가하여  컨 테이너의포트를  호스트의포트로  연결

- 컨테이너 실행하기 - > Web Application 실행하기 예제

  ```sh
  docker run -d -p 4568:4567 -e ENDPOINT=https://workshop-docker-kr.herokuapp.com/ -e PARAM_NAME=haha subicura/docker-workshop-app:2
  ```

  - 호스트 포트를 4568 로 바꾸고 2번 태그 이미지를 사용
  - `-e` 옵션으로 환경변수를 설정
  - `PARAM_NAME` 에 본인의이름이나 별명을 입력

- `Redis`

  - 메모리기반의  다양한  기능을  가진  스토리지

  - `docker run --name=redis -d -p 1234:6379 redis`

- `Mysql`

  ```sh
  docker run -d -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=true --name mysql mysql:5.7
  ```

  ```sh
  docker exec -it mysql mysql 
  create database wp CHARACTER SET utf8; 
  grant all privileges on wp.* to wp@'%' identified by 'wp'; 
  flush privileges; 
  quit
  ```

- `exec`

  - 실행중인도커 컨테이너에 접속할 때 사용

- `Wordpress`

  ```sh
  docker run -d -p 8080:80 -e WORDPRESS_DB_HOST=docker.for.linux.localhost -e WORDPRESS_DB_NAME=wp -e WORDPRESS_DB_USER=wp -e WORDPRESS_DB_PASSWORD=wp wordpress
  ```

- `Tensorflow`

  - 머신러닝 툴

  ```sh
  docker run -it -p 8888:8888 tensorflow/tensorflow
  ```

- `ps`

  - 실행중인 컨테이너 목록을 확인
  - `docker ps`
  - 중지된 컨테이너를 포함해서 확인
    - `docker ps -a`

- `stop`

  - 실행중인 컨테이너를 중지
  - `docker stop [options] container [container...]`

- `rm`

  - 종료된 컨테이너를 완전히 제거
  - `docker rm [options] container [container...]`

- `logs`

  - 로그를  확인 하는  방법
  - `docker logs [options] container`

- `images`

  - 도커가  다운로드한  이미지  목록
  - `docker images [OPTIONS] [REPOSITORY[:TAG]]`
  - 간단하게 도커 이미지 목록 확인
    - `docker images`

- `pull`

  - 이미지를  다운로드
  - `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`

- `rmi`

  - 이미지를  삭제
  - `docker rmi [OPTIONS] IMAGE [IMAGE...]`

- `network create`

  - 도커  컨테이너끼리  통신을  할  수  있는  가상  네트워크 생성
  - `docker network create [OPTIONS] NETWORK`

- `network connect`

  - 기존에 생성된 컨테이너에 네트워크를 추가
  - `docker network connect [OPTIONS] NETWORK CONTAINER`

![DockerCompose이미지](https://miro.medium.com/max/1000/1*JK4VDnsrF6YnAb2nyhMsdQ.png)

- `Docker Compose`

  - 복수 개의 컨테이너를 실행시키는 도커 애플리케이션이 정의를 하기 위한 툴
  - `docker-compose.yml` 에서 앱을 구성할 수 있는 서비스

  - 설치

    ```sh
    sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```

  - `docker-compose.yml`

  - 예제

    ```sh
    version: '2' 
    services: 
       db: 
         image: mysql:5.7 
         volumes: 
           - ./mysql:/var/lib/mysql 
         restart: always 
         environment: 
           MYSQL_ROOT_PASSWORD: wordpress 
           MYSQL_DATABASE: wordpress 
           MYSQL_USER: wordpress 
           MYSQL_PASSWORD: wordpress
       wordpress: 
         image: wordpress:latest 
         volumes: 
           - ./wp:/var/www/html 
         ports: 
           - "8000:80" 
         restart: always 
         environment: 
           WORDPRESS_DB_HOST: db:3306        WORDPRESS_DB_PASSWORD: wordpress
    ```

  - `up`

    - `docker-compose up -d`
    - `docker-compose.yml` 실행

- Docker의 Container 시스템

  - only read & writable

    - 읽기만 가능한 프로세스에 추가적으로 파일을 추가할 수 있음

  - 기본 우분투 컨테이너에 깃 프로그램 설치

    - `docker run -it ubuntu:latest --name git /bin/bash`

  - 기본 이미지와 프로그램이 설치된 이후의 이미지 비교

    - `docker diff git | grep git | head -n 10`

  - 프로그램이 추가된 이미지를 새롭게 `Commit`해서 이미지로 만듬

    ```sh
    docker images | grep ubuntu
    docker commit git ubuntu:git
    docker images | grep ubuntu
    ```

  - `Docker commit` 예제 정리

    ```sh
    docker run -it ubuntu:16.04 bash
    apt-get update
    apt-get install -y git
    git version
    ```

    ```sh
    docker ps
    docker diff [cotainer_id]
    docker commit [container_id] ubuntu:git
    docker run -it ubuntu:git bash
    git
    ```

    ![Dockerfile](https://blog.kakaocdn.net/dn/cpHQsb/btqD2FXLMtq/kB8gkF36DSJAgC4RIX4GaK/img.png)

  - `Dockerfile` 만들기

    ```sh
    FROM ubuntu:16.04
    RUN apt-get update 
    RUN apt-get install -y git
    docker build -t ubuntu:git02 .
    ```

    - `Dockerfile`

      - 이미지 생성 과정을 기술한 `Docker` 전용 `DSL`

      - `Docker`를 사용할때 가장 핵심적인 부분!!

      - `FROM`

        - 베이스 이미지 지정

      - `ADD`

        - 파일 추가

      - `RUN`

        - 명령어 실행

      - `WORKDIR`

        - 작업 디렉터리 변경

      - `ENV`

        - 환경변수 기본값 지정

      - `EXPOSE`

        - 컨테이너로 실행 시 노출시킬 포트

      - `CMD`

        - 이미지의 기본 실행 명령어 지정

      - `Dockerfile` 예제

        ```sh
        FROM nacyot/ruby-ruby:latest 
        RUN apt-get update 
        RUN apt-get install -qq -y libsqlite3-dev nodejs 
        RUN gem install foreman compass 
        WORKDIR /app 
        RUN git clone https://github.com/nacyot/docker-sample-project.git /app RUN git checkout v0.1 
        RUN bundle install --without development test 
        ENV SECRET_KEY_BASE hellodocker 
        ENV RAILS_ENV production 
        EXPOSE 3000 
        CMD foreman start -f Procfile
        ```

  - `Docker Repository`

    - =`Docker Hub`
    - 도커 이미지 또는 파일을 업로드하고 보관할 수 있는 저장소!
      - 깃허브와 비슷한 기능을 제공!!

![Docker 이미지 자동 배포](https://blog.kakaocdn.net/dn/c7oY8r/btqDdIVcBLB/A6hHxmw8Z4G1N94XcKKD01/img.png)

- 도커 이미지 자동 배포하기

  - `CI/CD`
    - `CI    Continuous Integration`
      - CI는  보통  테스트/빌드까지의과정
    - `CD    Continuous Delivery`
      -   CD는  추가로  전달/배포까지  포함
    - 빠르고  효과적으로  제품을  출시하기  위해  지속적으로  소스를  통합하고  빌드하고  테스트하고  배포 하는  과정
  - 배포과정 (원래 과정)
    1.   소스저장소에  최신  소스를  저장 
    2.   전체  소스를  다운로드 
    3.   테스트 
    4.   Docker  이미지  만들기 
    5.   Docker  이미지  저장하기 
    6.   애플리케이션  업데이트

  - 배포과정 (자동화 적용)
    1.   소스저장소에  최신  소스를  저장(개발자는  여기까지만  신경씁니다) 2.   전체  소스를  다운로드 
    3.   ~~테스트~~ 
    4.   ~~Docker  이미지  만들기~~ 
    5.   ~~Docker  이미지  저장하기~~ 
    6.   ~~애플리케이션  업데이트~~
  - 자동화 도구
    - Jenkins 
      - 빌드  /  테스트  /  코드  분석  /  배포  /  알람등  다양한  기능  제공
      - Master  /  Agent  구성  (하나의  Master에  수십  /  수백개의  Agent 사용가능)
      - 1,400여개가  넘는  플러그인  제공
      - 무료 프로그램
    - TravisCI 
    - CircleCI

  - Jenkins 실행

    - 기본  Jenkins 프로젝트에  docker와  docker‑compose가  설치된  도커  이미지를  사용

      ```sh
      docker run -u root --rm -p 8080:8080 --name jenkins -v $(데이터디렉토리):/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock subicura/jenkins:2
      ```

    - 자동화 배포 스크립트 예제

      - `https://github.com/subicura/docker-jenkins-workshop`

    - `stage` 형식

      ```sh
      node { 
          stage('Pull') { 
          } 
          stage('Unit Test') { 
          } 
          stage('Build') { 
          } 
          stage('Tag') { 
          } 
          stage('Push') { 
          } 
          stage('Deploy') { 
          } 
      }
      ```

    - `stage` 예제

      ```sh
      node { 
        withCredentials([[$class: 'UsernamePasswordMultiBinding', 
            credentialsId: 'dockerhub', 
            usernameVariable: 'DOCKER_USER_ID', 
            passwordVariable: 'DOCKER_USER_PASSWORD']]) { 
            stage('Pull') { 
                git 'https://github.com/subicura/docker-jenkins-workshop.git'       } 
            stage('Unit Test') { 
            } 
            stage('Build') { 
                sh(script: '''docker build --force-rm=true \ 
                  -t ${DOCKER_USER_ID}/ruby-app:latest .''') 
            } 
            stage('Tag') { 
            } 
            stage('Push') { 
            } 
            stage('Deploy') { 
            } 
        } 
      }
      ```

  ![무중단 배포](https://subicura.com/assets/article_images/2016-06-07-zero-downtime-docker-deployment/nginx-load-balance.png)

  - `Docker Swarm`

    - 이미지를 만들고 배포하는 명령어 (기존의 방법과 동일한 기능 제공)

      ```sh
      docker service update --image localhost:5000/ruby-app:${BUILD_NUMBER} ruby-app
      ```

  - `Kubernetes`

    - 명령어만  입력하면  알아서  여러개의컨테이너를  순차적으로  업데이트

      ```sh
      kubectl set image -f deploy/ruby-app.yml app=localhost:5000/ruby-app:${BUILD_NUMBER}
      ```
