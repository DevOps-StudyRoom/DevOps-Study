# Object
Kubernetes Object:  
https://bcho.tistory.com/1256  
https://baek.dev/post/6/  
https://baek.dev/post/8/  
https://baek.dev/post/9/  

* Pod  
  쿠버네티스의 최소 배포 단위  
  재생성된 pod는 새로운 IP 부여  
  pod 안에는 여러 컨테이너가 들어갈 수 있다  
  컨테이너는 port를 가지고 있지만 서로 같은 port를 가질 순 없다  


* Label  
  쿠버네티스의 리소스를 선택하는 데 사용, 목적에 따라 분류 및 연결  
  각 리소스는 라벨을 가질 수 있고 검색 조건에 따라 특정 라벨을 가지고 있는 리소스만을 선택 가능  
  key&value로 구성  

* Service  
  내부에서만 접근할 수 있는 Pod들을 응용 프로그램으로 표시하는 네트워크 서비스  
  pod는 재시작 하면 IP가 새로 할당되어 Service를 이용  
  + ClusterIP  
  클러스터 내에서만 접근이 가능한 IP  
  클러스터 내에서 다른 오브젝트들이 접근 가능  
  + NodePort  
  클러스터 밖에 있지만 내부 네트워크 접근 전용(내부망 연결)  
  모든 노드에 같은 Port 할당  
  + Load Balancer  
  로드 밸런서를 사용하여 서비스를 외부에 노출  
  각각의 Node에 트래픽 분산  

* Volume  
  + emptyDir  
  Pod 생성 시 만들어지고 삭제 시 없어짐(일시적)  
  최초 생성 될때 볼륨이 비어있음  
  + hostPath  
  파일이나 디렉토리를 마운트함  
  Node의 Path를 볼륨으로 사용해서 pod 재생성 되어도 유지됨  
  + PVC/PV  
  PVC - 사용자에 의해 어떤 저장소를 사용할지에 대한 요청  
  PV - 관리자에 의해 제공된 이용 또는 동적 프로비저닝 된 클러스터에 저장하는 부분  

* ConfigMap, Secret  
  외부로부터 전달받도록 사용하는 쿠버네티스 오브젝트(개발환경, 테스트환경, 사용환경을 따로 운영하기 위한)  
  + Env(file)  
  한번 주입되면 변경되지 않음, 반영 시 pod 재생성
  + Volume Mount(file)  
  file을 볼륨에 마운트해서 내용 변경시 pod도 변경  


* Namespace  
  쿠버네티스 클러스터내의 논리적 분리 단위  
  Pod, Service 등 Namespace 별로 생성, 관리 가능하고 사용자의 권한도 나누어서 부여 가능  

* ResourceQuota  
  네임스페이스의 자원 limit을 설정  
  pod에 반드시 requests와 limits를 명시  
  버전에 따라 제한 할 수 있는 오브젝트가 다르다  

* LimitRange  
  네임스페이스에 들어올 수 있는 Pod의 용량을 제한  
  min, max, maxLimitRequestRatio 설정 가능  

# Controller  
  * 기능  
    Auto Scaling : pod의 리소스가 다 찬 경우 새로운 파드 생성  
    Auto Healing : pod나 node가 다운된 경우 즉각 생성  
    Software Update : 컨트롤러를 통해 한 번에 업데이트 가능(에러시 롤백 가능)  
    Job : 일시적으로 pod를 만들어서 종료하는 기능  

  * ReplicaSet  
    + Template  
     Controller가 pod를 생성할 때 사용할 템플릿  
  
    + Replicas  
    Scale in/out에 관련한 옵션  

    + Selector(only ReplicaSet)  
    pod를 select하기 위한 옵션, 다양한 match옵션 제공(Exists, DoesNot Exists, In, Notln )  
  
  * Deployment  
    특정 소프트웨어 보다 상위 버전으로 배포된 애플리케이션  
    + ReCreate  
     기존 ReplicaSet의 pod을 삭제한 후 새 ReplicaSet의 pod 생성(다운타임 발생)  

    + Rolling Update  
    새 ReplicaSet의 pod를 생성한뒤 기존 ReplicaSet의 파드를 하나 삭제 시키는 작업을 replicas 설정 만큼 반복  

    + Blue/Green  
     Blue와 Green group을 구분하여 기존 버전의 애플리케이션과 새로운 버전의 애플리케이션을 구분하여 스위칭  

  * Canary  
   새로운 버전의 애플리케이션을 1개의 ReplicaSet으로 기존 버전의 애플리케이션에 추가 생성  
   에러나 장애가 없으면 새로운 버전의 애플리케이션의 ReplicaSet을 원하는 수만큼 늘림  
   기존 버전의 애플리케이션의 ReplicaSet을 0으로 조정하여 배포를 마침  
