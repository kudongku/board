## kubernetes

> 해당 레포지토리는 board front와 back의 상위 디렉토리로, board service의 kubernetes를 총괄하고 mysql 컨테이너를 관리하기 위함입니다.

### workflow
- 최초실행시 install 후 cluster를 생성해준다.
- docker image를 빌드한 후, dockerhub에 push해준다.
- deployment.yaml를 사용해 deploy해주고, port-forward를 통해 로컬에서 테스트를 진행한다.

---

### kind, kubectl install
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


### deployment
- mysql
```bash
kubectl apply -f mysql_deployment.yaml
kubectl port-forward service/mysql-service 3307:3306
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
