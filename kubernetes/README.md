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