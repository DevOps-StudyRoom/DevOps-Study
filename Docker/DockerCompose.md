# DockerCompose  

https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose  

http://raccoonyy.github.io/docker-usages-for-dev-environment-setup/  


* DocekrCompose 개요 
    컨테이너 여럿을 띄우는 오커 애플레ㅣ케이션을 정의하고 실행하는 도구  
    (단일 컨테이너에서 개발-테스트-운용 단계에서도 활용 가능)  
    도커 실행 옵션을 미리 적어둔 문서  

* Docker와 DockerCompose 차이점  
    `Dockerfile` vs `Dockerfile-dev`: 서버 구성을 문서화한 것(=클래스 선언이 들어 있는 파일)  
    `docker build` vs `docker-compose build`: 도커 이미지 만들기(=클래스 선언을 애플리케이션에 로드)  
    `docker run`의 옵션들 vs `docker-compose.yml`: 이미지에 붙이는 장식들(=인스턴스의 변수들)  
    `docker run` vs `docker-compose up`: 장식 붙은 이미지를 실제로 실행(=인스턴스 생성)  

* docker-compose.yml 파일  및 구성 
    + version  
        파일 규격 버전  
    
    + services  
        실행하려는 컨테이너들을 정의  
    
    + volumes  
        컨테이너 실행시 --volume 옵션과 동일  
        상대 경로로 지정 가능  

    + environment  
        환경 변수 설정  
        docker run의 -e 옵션과 동일  

    + build  
        context는 docker build 명령을 실행할 디렉토리 경로  
        dockerfile에는 개발용 도커 이미지를 빌드하는데 사용할 Dockerfile 지정  
    
    + port  
        port 번호 지정  
        docker run의 -p 옵션과 동일  
    
    + commad
        docker run의 컨테이너를 실행할 때 명령어 부분  
    
    + 예제 코드  
        ``` sh
        version: '3'

        services:
        db:
            image: postgres
            volumes:
            - ./docker/data:/var/lib/postgresql/data
            environment:
            - POSTGRES_DB=sampledb
            - POSTGRES_USER=sampleuser
            - POSTGRES_PASSWORD=samplesecret
            - POSTGRES_INITDB_ARGS=--encoding=UTF-8

        django:
            build:
            context: .
            dockerfile: ./compose/django/Dockerfile-dev
            environment:
            - DJANGO_DEBUG=True
            - DJANGO_DB_HOST=db
            - DJANGO_DB_PORT=5432
            - DJANGO_DB_NAME=sampledb
            - DJANGO_DB_USERNAME=sampleuser
            - DJANGO_DB_PASSWORD=samplesecret
            - DJANGO_SECRET_KEY=dev_secret_key
            ports:
            - "8000:8000"
            command: 
            - python manage.py runserver 0:8000
            volumes:
            - ./:/app/
        ```

* docker compose 주요 명령어

    + `up`  
        docekr-compose.yml 파일의 내용에 따라 이미지를 빌드하고 서비스 실행  
        `-d`: 서비스 실행 후 콘솔로 빠져나오기  
        `--force-recreate`: 컨테이너를 지우고 새로 만들기  
        ` --build`: 서비스 시작 전 이미지 새로 만들기  
    
    + `ps`  
        현재 환경에서 실행 중인 각 서비스의 상태 보기  
    
    + `stop, start`
        서비스를 멈추거나, 멈춰있는 서비스 시작  
    
    + `down`  
        서비스 지우기 컨테이너와 네트워크를 삭제  
        `--volume`: 볼륨까지 삭제
    
    + `exec`  
        실행 중인 컨테이너에서 명령어 실행  

    + `logs`  
        서비스의 로그 확인  
        `-f`:  셸로 빠져나오지 않고 계속 로그 출력  


