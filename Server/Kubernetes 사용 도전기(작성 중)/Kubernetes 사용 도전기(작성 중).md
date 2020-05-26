# Kubernetes 사용 도전기(작성 중)

---

# Kubernetes, 왜 사용할까??

---

# Kubernetes 주요 기능

---

# minikube로 Kubernetes 맛보기

## minikube, hyperkit 설치 및 클러스터 생성

로컬에서 간단하게 클러스터를 생성할 수 있는 minikube
minikube로 클러스터를 구성하려면 hypervisor가 필요한데, 나는 튜토리얼이 제시하는 hypervisor 목록 중 hyperkit을 선택했다.

- minikube, hyperkit 설치

```
brew install minikube hyperkit

```

minikube를 설치했다면, 정상 작동하는지 확인하자.

```
$ minikube version
minikube version: v1.6.2
commit: 54f28ac5d3a815d1196cd5d57d707439ee4bb392

```

- 클러스터 생성

```
minikube start --vm-driver=hyperkit

```

- 클러스터의 default vm driver 설정

```
minikube config vm-driver=hyperkit

```

`minikube start` 명령을 통해 클러스터가 구성이 되면 kubectl을 사용할 수 있다. kubectl를 통해 클러스터들을 관리할 수 있다.

우선 kubectl이 정상적으로 작동하는지 확인하자.

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.2", GitCommit:"59603c6e503c87169aea6106f57b9f242f64df89", GitTreeState:"clean", BuildDate:"2020-01-23T14:21:54Z", GoVersion:"go1.13.6", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.0", GitCommit:"70132b0f130acc0bed193d9ba59dd186f0e634cf", GitTreeState:"clean", BuildDate:"2019-12-07T21:12:17Z", GoVersion:"go1.13.4", Compiler:"gc", Platform:"linux/amd64"}

$ kubectl get nodes
NAME       STATUS   ROLES    AGE    VERSION
minikube   Ready    master   136m   v1.17.0

```

minikube의 status가 Ready로 되어있는데, 이것은 배포할 준비가 되어있다는 뜻이다.

## 애플리케이션 배포하기

다음과 같은 명령어를 통해 클러스터 노드에 애플리케이션을 배포를 할 수 있다.

```
kubectl create deployment \\[배포명\\]=\\[애플리케이션 경로(로컬 디렉토리 or 이미지 url)\\]

```

나는 튜토리얼에 제시된 샘플 앱의 이미지 url을 사용했다.

```
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1

```

---