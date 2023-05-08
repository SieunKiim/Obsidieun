컨테이너화된 애플리케이션을 쉽게 배포, 관리, 스케일링할 수 있도록 도와주는 컨테이너 오케스트레이션 서비스이다.
- ECR, Docker 등의 서드 파티 도구와 통합된다.

***ECS는 Kubernetes나 Docker Swarm과 비슷한 역할을 한다***

## ECS의 구성요소
> - Task definition (작업정의)
> - Task
> - Service
> - Container Instance
> - Cluster


#### Task definition
원하는 Docker 컨테이너를 생성할 때, 어떤 설정으로 몇 개 이상 생성 할 지를 정의한다.
- 컨테이너의 이미지, CPU/메모리 리소스 할당, Port 매핑, Volume, 등의 설정이 포함된다. (기존 docker run 명령에 사용했던 옵션 대부분)

ECS는 컨테이너 오케스트레이션 서비스이므로 컨테이너가 필요에 따라 자동으로 실행 혹은 종료될 수 있다.
따라서, 자동으로 생성 가능하도록 설정을 하나의 단위로 정의하는 행위라고 생각하면 된다.


### Task
Task definition에서 정의된 대로 배포된 Container들을 Task라고 부른다.
- 즉 한개의 Task 안에는 하나 이상의 컨테이너들이 포함되어 있으며, ECS는 Task단위로 실행하게 된다. (컨테이너 그룹 이라고 생각하면 편하다)

>Task는 Cluster에 속한 인스턴스 ( = EC2)에 배포되게 된다.
>또한 여러 EC2가 하나의 Task에 속할 수 있다.


### Service
Task들의 life cycle을 관리하는 부분이다.
Task는 각각 개별적인 기능을 갖는 단위이므로, Cluster당 몇개를 배포할지와 Task들을 ELB에 연동하는 부분을 관리한다.

> ***즉, 오토스케일링과 로드벨런싱을 관리하는 역할이다.***


### Container Instance (= EC2)
Task를 올리기 위해 등록된 EC2 인스턴스를 Container Instance라고 부른다.
	컨테이너는 EC2에 배포되도록 설계되어있다.
- 하나의 Container Instance에는 각기 다른 Task가 여러 개 있을 수 있다.


### Cluster
Task가 배포되는 인스턴스들을 논리적인 그룹으로 묶는 단위
- Task를 배포하기 위한 인스턴스는 반드시 Cluster에 등록되어야 한다.

