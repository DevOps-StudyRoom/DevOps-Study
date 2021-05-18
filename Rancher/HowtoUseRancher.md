# How To Use Rancher?

### 준비사항!

- 리눅스 환경 조성! - Vmware, Ubuntu
- Docker 설치하기!!



### 설치방법

> ```
> docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher
> ```

### Rancher 접속방법

- Vmware Hosting IP 확인하기!!
  - Hostname -I
- https://`IP주소` 접속시 Rancher 실행됨!!
- 처음 접속시  admin으로 고정됨!! 
  - 비밀번호 생성 후, 동의화면 체크 진행

### Create the Cluster

1. Clusters Page로 들어가서 `Add Cluster` 클릭하기!
2. `Existing Nodes` 클릭!
3. Cluster 이름을 설정하고 기타 동료, 권한, 기타옵션을 설정!!
4. Cluster Options Page에서 Node Options를 전체 선택!! - > 관리자기 때문에~
5. Rancher 실행 명령문 복사해두기!!

```
sudo docker run -d --privileged --restart=unless-stopped --net=host -v /etc/kubernetes:/etc/kubernetes -v /var/run:/var/run  rancher/rancher-agent:v2.5.8 --server https://192.168.111.128 --token rwb2fzjqf458w2xpgzsf4gv5hpfwjwnzpxmwqv6zvxfzmmwq8ldwsr --ca-checksum c5bcb4ac4ed945b8b167f90522eeaf8398af15c0549e90655249a4f6dc882d8e --etcd --controlplane --worker
```

6. 추가된 Cluster에 본인의 이미지 파일 또는 API를 올리면 됩니당!!
   
   - 쿠버네티스를 올려서 사용하면 굳굳입니당!!
   
   ![img](https://github.com/DevOps-StudyRoom/DevOps-Study/blob/main/Rancher/example.png)

- [Rancher 공식 홈페이지](https://rancher.com/docs/rancher/v2.x/en/quick-start-guide/deployment/quickstart-manual-setup/#2-install-rancher)

