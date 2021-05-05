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
![localhost_5601](https://user-images.githubusercontent.com/57735723/117115535-3178d900-adc8-11eb-95b5-3b100c8799c1.png "kibana")
![localhost_3000](https://user-images.githubusercontent.com/57735723/117115589-42c1e580-adc8-11eb-9fa6-ae90817146a4.png "grafana")
![localhost_80](https://user-images.githubusercontent.com/57735723/117115621-540af200-adc8-11eb-92c2-94f3fb6c0e13.png "httpd")
![docker-compose up](https://user-images.githubusercontent.com/57735723/117115643-5e2cf080-adc8-11eb-9f11-00b8d584473a.png "docker-compose up")
![docker ps](https://user-images.githubusercontent.com/57735723/117115700-6edd6680-adc8-11eb-9f70-bd69a4a1c99d.png "docker ps")
