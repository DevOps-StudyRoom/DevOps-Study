## Install Test
https://docs.fluentd.org/v/0.12/articles/docker-logging-efk-compose

* docker-compose.yml  
    + apache webserver, fluentd, elasticsearch, kibana, grafana 5개의 Docker 컨테이너 설정  

```
# docker-compose.yml
version: '3'

volumes:
  grafana-data: {}

networks:
  internal:
    driver: bridge

services:
  web:
    image: httpd
    ports:
      - "80:80"
    depends_on:
      - "fluentd"
    links:
      - "fluentd"
    logging:
      driver: "fluentd"
      options:
        fluentd-address: localhost:24224
        tag: httpd.access
    networks:
      - default
      - internal
        

  fluentd:
    build: ./fluentd
    volumes:
      - ./fluentd/conf:/fluentd/etc
    depends_on:
      - "elasticsearch"
    links:
      - "elasticsearch"
    ports:
      - "24224:24224"
      - "24224:24224/udp"
    networks:
     - default
     - internal
    restart: always

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.10.2
    environment:
      - "discovery.type=single-node"
    expose:
      - "9200"
    ports:
      - "9200:9200"
    networks:
      - default
      - internal
    restart: always

  kibana:
    image: kibana:7.10.1
    depends_on:
      - "elasticsearch"
    links:
      - "elasticsearch"
    ports:
      - "5601:5601"
    networks:
      - default
      - internal
    restart: always
        
  grafana:
    image: grafana/grafana
    volumes:
      - grafana-data:/var/lib/grafana
    environment:
      - GF_SECURITY_ADMIN_USER=pass
      - GF_SECURITY_ADMIN_PASSWORD=pass
      - GF_USERS_ALLOW_SIGN_UP=false
    links:
      - elasticsearch
    ports:
      - "3000:3000"
    networks:
      - default
      - internal
    restart: always
``` 

* Fluentd Dockerfile  
  + elasticsearch plugin 설치  
  + Plugin으로 연동 하기 위해 Image 계속 생성  
  + log를 Elasticsearch로  전송  

```
# fluentd/Dockerfile
FROM fluent/fluentd:v1.12.0-debian-1.0
USER root
RUN ["gem", "install", "fluent-plugin-elasticsearch", "--no-document", "--version", "4.3.3"]
USER fluent
```

* Fluent.conf  
  + Fluent 설정 파일  
  + Docker logging driver로 로그 수집 뒤 elasticsearch로 전달  

```
# fluentd/conf/fluent.conf
<source>
  @type forward
  port 24224
  bind 0.0.0.0
</source>
<match *.**>
  @type copy
  <store>
    @type elasticsearch
    host elasticsearch
    port 9200
    logstash_format true
    logstash_prefix fluentd
    logstash_dateformat %Y%m%d
    include_tag_key true
    type_name access_log
    tag_key @log_name
    flush_interval 1s
  </store>
  <store>
    @type stdout
  </store>
</match>
```

## 결과
![localhost_5601](https://user-images.githubusercontent.com/57735723/117109209-443ae000-adbf-11eb-81a7-f912b57e2304.png "kibana")
![localhost_3000](https://user-images.githubusercontent.com/57735723/117109275-5ddc2780-adbf-11eb-9e9e-1ac2afdc2db6.png "gragana") 
![localhost_80](https://user-images.githubusercontent.com/57735723/117113084-f4f7ae00-adc4-11eb-888c-288a6d08a6b8.png "httpd")
![docker-compose up](https://user-images.githubusercontent.com/57735723/117111763-0e97f600-adc3-11eb-97ef-62f53cbe0b68.png "docker-compose up")
![docker ps](https://user-images.githubusercontent.com/57735723/117112373-ee1c6b80-adc3-11eb-8c3b-637afcd5d08f.png "docker ps")

