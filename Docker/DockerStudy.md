## <이론>

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/573fb7bf-d6a1-4a18-9d36-f6a50689953a/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/573fb7bf-d6a1-4a18-9d36-f6a50689953a/Untitled.png)

컨테이너는 VM ?

- Virtual Machine(centOS, busyBox, Ubuntu) 은 하드웨어를 가상화 한거임
- 즉, 소프트웨어로 구현된 하드웨어

- 컨테이너는 하드웨어 가상화가 아님
- OS 에서 지원하는 기능을 사용
- 격리된 환경에서 프로세스를 실행

→ 도커의 컨테이너는 하드웨어 가상화가 없이, 격리된 환경에서 실행되는 '프로세스'

이미지 ?

- 특정 프로세스를 실행하기 위한 환경
- 계층화된 파일 시스템 ( 이미지에 이미지를 얹음)
- 이미지는 파일들의 집합
- 프로세스가 실행되는 환경도 결국 파일들의 집합

도커의 기본 아키텍쳐

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16a7816b-3fa9-497d-82d7-ba12c67743e7/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16a7816b-3fa9-497d-82d7-ba12c67743e7/Untitled.png)

각 세개는 모두 프로세스

왼쪽이 클라이언트. 서버가 클라이언트 명령어( 메세지) 를 받아서 도커 컨테이너를 실행시켜줌

도커 서버는 맥os 에 xhyve vm 에 설치되어있음

- Xhyve : macOS 의 가상화 방식
- 컨테이너 = Xhyve에서 실행된 프로세스
- vm 과 다르게 Xhyve 는 호스트 머신과 자연스럽게 결합되어있어 네트워크 / 볼륨 등 호스트 머신처럼 사용 가능
- Xhyve 가 아니여도 Virtual Box 방식도 있음. 근데 이런식으로 하면 컨테이너가 호스트의프로세스가 아닌 가상머신의 프로세스가 되어서 네트워크, 볼륨 설정이 까다로움. 클라이언트는 환경변수를 참조해서 서버에 접속하게 된다.
- 이외에도 리눅스 서버위에 도커 서버와 컨테이너를 설치해서 사용해도 됨

컨테이너가 필요한 이유

컴퓨터의 환경은 보편적이지 않다. 하드웨어, OS, 시스템 설정, 소프트웨어 전부 다르기 때문에 서버관리가 힘들다.

so, 도커를 이용해 도커파일(어플리케이션/프로세스 실행 환경까지 최소한의 파일/명령어 집합) 를 이용해 이미지를 만들어 깨끗한환경을 제공해준다.)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53ac9c60-547a-4bff-b68c-2b71e2eaba7a/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53ac9c60-547a-4bff-b68c-2b71e2eaba7a/Untitled.png)

## <실습>

docker

```jsx
docker run ubuntu:16.04
docker run --rm -it ubuntu:16.04 /bin/sh

ls
exit

docker run --rm -it centos:7 /bin/sh

docker run -d -p 4568:4567 -e ENDPOINT=https://workshop-docker-kr.herokuapp.com -e PARAM_NAME=heein subicura/docker-workshop-app:2

//위 명령어치고 0.0.0.0:4568 들어가면 https://workshop-docker-kr.herokuapp.com 여기에 내가 접속했다는것을 확인할 수 있음

docker run -d -p 4569:4567 -e ENDPOINT=https://workshop-docker-kr.herokuapp.com/ -e PARAM_NAME=heein  -e PARAM_MESSAGE=heeeeeejin subicura/docker-workshop-app:3
```

-d 는 백그라운드 실행

-e 는 환경변수를 지정하겠다는거임(ENDPOINT, PARAM_NAME)

-rm 끝나고 지우겠다

-it 셸에서 실행

\ 를 통해 개행가능

이미지(docker-workshop-app:2)는 한번 만들면 변경 불가

[버전2 이미지]

호스트 포트를 4568로 바꾸고, 2번 태그 이미지를 사용.

e 옵션으로 환경변수를 설정해주었슴.

이 이미지는 접속할 경우, 접속기록을 http://workshop-docker-kr.herokuapp.com/ 에 남긴다

[버전3 이미지]

메세지를 남길 수 있도록 개발해놨음

위의 내용까지가 컨테이너를 만든거임

Redis

- 메모리에 key, value 를 저장하고 읽을 수 있는 storage
- 테스트를 하려면 텔넷에 접속해야함

```jsx
docker run --name=redis -d -p 1234:6379 redis

docker run --rm -it mikesplain/telnet docker.for.mac.localhost 1234
// telnet 의 기능을 가상머신에서 다운받아서 사용.
// 누군가 이미지를 만들어놓으면 웹서버가 아니라 단순한 cmd program 들도 그 이미지를 사용할 수 있게 한다.
// mikesplain/telnet 이 이미지이고, 뒤에 있는것이 다 인자값이다.

keys * // 현재 레디스에 저장되어있는 데이터 확인
SET hello world   //헬로라는 키에 워드라는 데이트에 넣고
GET hello     //헬로 키로 데이터 검색
```

→ 레디스가 잘 실행이 되었다는 것을 알 수 있다.

→ telnet 이라는것이 내 local 환경이 아니라, 컨테이너 환경 위에서 돌아가서 컨테이너에서 밖의 호스트의 ip를 모르기때문에 telnet 주소에 docker.for.mac.localhost 를 이용해서 docker에서 만들어준 dns 를 사용한다.

MySQL

- docker.hub.mysql 에 mysql 이미지들을 확인할 수 있고, 어떤 환경변수를 쓰면 되는지 확인할 수 있다.

```jsx
docker run -d -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=true --name mysql mysql:5.7
```
