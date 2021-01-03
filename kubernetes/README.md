# 쿠버네티스

## 오브젝트 목록 출력
```bash
kubectl get ${object-name} 
```

- pods
- replicasets
- deployment
- namespaces

## Pod
> Pod 안에는 독립적인 서비스를 올릴 수 있는 컨테이너가 구성되어 있다. 컨테이너는 Service와 연결할 수 있도록 port를 가지고 있다.

### Pod Template
```
apiVersion: v1 # 오브젝트 API 버전
kind: Pod # 리소스 종류
metadata:
  name: my-nginx-pod # Pod 고유 이름
  labels:
    app: nginx 
spec:
  containers:
  - name: my-nginx-container # 컨테이너 이름
    image: nginx:latest # 컨테이너 이미지
    ports:
    - containerPort: 80
      protocol: TCP
```

### container의 bash shell 실행
```bash
kubectl exec -it ${pod-name} -c ${container-name} bash
```

### Pod 삭제 방법
```bash
kubectl delete -f ${yaml-file}
kubectl delete pods ${pod-name}
```

### Pod 생성
```bash
kubectl apploy -f nginx-pod.yaml
```

## Replicaset
> 정해진 수의 동일한 Pod이 생성되도록 관리한다. 노드 장애 등의 이유로 Pod을 사용할 수 없으면, 다른 노드에서 Pod을 다시 생성한다.

### Replicaset 생성
```bash
kubectl apploy -f replicaset-nginx.yaml
```

## Deployment
> 애플리케이션의 업데이트와 배포를 편하기 위해서 사용한다. 컨테이너 애플리케이션 배포하고 관리하는 역할을 담당한다. 무중단 서비스를 위해 Pod의 롤링 업데이트 전략을 설정할 수 있다.

### Deployment 생성
```bash
kubectl apploy -f deployment-nginx.yaml
```

## Service
> Service는 관리하는 Pod들을 연결하고 외부에서 접근할 수 있도록 엔드포인트를 제공한다. 여러 Pod 들을 로드밸런싱 해주며 고유한 DNS 이름을 가질 수 있다. Pod는 IP 가지고 있지만 클러스터 내에서만 접근이 가능하며, 새로 생성될 때마다 매번 IP가 변경된다.

쿠버네티스 `ServiceTypes`는 원하는 서비스 종류를 지정할 수 있도록 해준다. 기본 값은 `ClusterIP` 이다.

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

### Service Template

```
apiVersion: v1
kind: Service
metadata:
  name: service-name
spec:
  selector:
    app: pod
  ports:
  - port: 80
    targetPort: 8080
type: ClusterIP
```


## Namespace
> 리소스를 논리적으로 구분하기 위해 Namespace 오브젝트를 제공한다.

### Namesapce 생성
```bash
kubectl create namespace development
```

### 특정 Namespace의 Pod, Service 목록 출력
```bash
kubectl get pods,services -n development
```

### 서비스의 DNS 이름에 대한 FQDN
```bash
<서비스 이름>.<네임스페이스 이름>.svc.cluster.local
```