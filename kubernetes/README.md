# 쿠버네티스

### yaml 파일을 쿠버네티스에 실행
```bash
kubectl apply -f ${yaml-file}
```

### 특정 오브젝트 목록
```bash
kubectl get ${object-name} 
```

### Pod 내 container의 bash shell 실행
```bash
kubectl exec -it ${pod-name} -c ${container-name} bash
```

### Pod 삭제 방법
```bash
kubectl delete -f ${yaml-file}
kubectl delete pods ${pod-name}
```