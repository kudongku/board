## kubernetes

### workflow
#### 최초 실행시
- 최초실행시 install 후 cluster를 생성해준다.
- docker image를 빌드한 후, dockerhub에 push해준다.
- deployment.yaml를 사용해 deploy해주고, port-forward를 통해 로컬에서 테스트를 진행한다.
#### 업데이트 사항 반영시
- 백엔드의 경우에는 bootjar를 통해 새로운 jar파일을 만들어준다.
- docker image를 빌드한 후, dockerhub에 push해준다.
- deployment.yaml를 사용해 deploy해주고, port-forward를 통해 로컬에서 테스트를 진행한다.

---

### kind, kubectl install (한번만 해주면 된다.)
> https://kind.sigs.k8s.io/

```bash
brew install go # kind 설치시 필요
brew install kind # 로컬에서 kubernetes 를 가능하게 해주는 tool
brew install kubectl # kubectl 명령어를 사용하기 위함.
```

### create cluster (cluster 단위 당 한번씩 실행해주면 된다.)
```bash
kind create cluster
kind get clusters
kubectl config use-context [context-name]
kubectl config get-contexts
```
---
### docker image build and push to registry (container 단위로 필요시 사용한다.)
- mysql
```bash
docker pull mysql:8
docker tag mysql:8 kudongku/mysql:8
docker push kudongku/mysql:8
```

- spring backend
```bash
docker build -t kudongku/board-back-image .
docker push kudongku/board-back-image:latest
```

- next.js frontend
```bash
docker build -t kudongku/board-front-image .
docker push kudongku/board-front-image:latest
```

### deployment (image 빌드 후 push 되었을 때 사용한다.)
- mysql
```bash
kubectl apply -f mysql_deployment.yaml
kubectl port-forward service/mysql-service 3307:3306
```

- spring backend
```bash
kubectl apply -f back_deployment.yaml
kubectl port-forward service/board-service 8080:8080
```

- next.js frontend
```bash
kubectl apply -f front_deployment.yaml
kubectl port-forward service/board-front-service 3000:3000
```

---
### kubectl 관련 명령어
```bash
kubectl get pods # pods 목록 조회
kubectl describe service board-service # service 상세 조회
kubectl describe pod <pod-name> # pod 상세 조회
kubectl delete pod <pod-name> # pod 삭제
kubectl logs board-back-6b9949cd6c-4jd89 # pod 로그 조회
```
