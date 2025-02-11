> Q. 서비스를 어디서든 쉽게 도커 이미지로 다운받도록 하려면 어떻게 해야할 것인가.
>
>A. 이미지를 도커 허브(Docker Hub) 또는 다른 컨테이너 레지스트리에 호스팅한다.
> 이 과정을 통해, 인터넷이 연결된 어디서든 서비스 이미지를 내려받을 수 있다.

---

### 도커 이미지 배포가 어떤 개념일까

- 도커 이미지 배포는, 서비스를 도커 이미지 형태로 패키징하고, 이 이미지를 다양한 환경에서 실행 및 관리하기 위한 과정을 의미
- 도커 이미지 배포는 애플리케이션의 이식성을 향상시키고, 환경 간에 일관성을 제공하여 개발 및 운영 프로세스를 간편화한다
- 즉, 도커 이미지를 배포해서 다른 곳에서도 배포된 이미지를 통하여 서비스를 간편히 설치 할 수 있도록한다.

---

### 도커 이미지 배포는 어떤 방식이 있을까

1. 도커 허브(Docker Hub)
    - 도커 이미지를 저장하고 공유하는 공식 레지스트리 서비스
    - 사용자는 이미지를 올리고(docker push) 이미지를 내려받기(docker pull)만 하면 되므로 매우 간단하게 사용 가능하다. 단, 무료 사용자는 비공개(Private) 저장소의 수에 제한이 있고,
      공개(Public) 저장소는 무료로 사용할 수 있으므로 만든 이미지를 다른 사용자에게 공개해도 상관없다면 도커 허브를 사용
2. 사설 레지스트리
    - 회사나 조직 내부에서 도커 이미지를 저장하고 관리하기 위해 사설 도커 레지스트리를 구축
    - 사용자가 직접 이미지 저장소 및 사용되는 서버, 저장 공간 등을 관리해야 하므로 도커 허브보다는 사용성에서 까다롭다. 회사의 내부망과 같이 보안이 중요한 곳에서 도커 이미지를 배포해야 한다면 도커 사설
      레지스트리가 더 좋은 방안
    - 예시 : AWS ECR, Google Container Registry, Azure Container Registry 등등
3. 도커 이미지를 파일로 전송
    - 이미지를 tar 파일로 저장하고 필요한 곳으로 복사하여 배포할 수 있다
    - docker save로 이미지를 tar 파일로 저장하고, docker load로 해당 파일에서 이미지를 불러온다

⇒ 도커 허브에 올리는게 가능할까? 도커허브에 올리고 라이선스를 판매하는 식으로.. 비공개 이미지도 지원, 그렇지만 다른 레지스트리에 비해 보안 기능이 제한적이다

⇒ 사설 레지스트리 배포 방법 찾아보기

---

### 도커 이미지를 레지스트리에 푸시하는 플로우

1. 도커 이미지 빌드
    - 도커 파일(Dockerfile)을 작성하여 도커 이미지로 빌드
2. 도커 허브 계정 생성
3. 도커 이미지 태그 지정
    1. <계정명>/<이미지명>:<태그> 형식
4. 도커 허브에 로그인
    1. 터미널이나 명령 프롬프트에서 docker login 명령어를 통해 로그인
5. 이미지 푸시
    1. 생성한 태그를 사용하여 이미지를 도커 허브에 푸시 docker push <계정명>/<이미지명>:<태그>

**<이미지 사용 테스트>**

1. 도커 허브에서 이미지 pull
    1. docker pull <계정명>/<이미지명>:<태그> 명령어로 도커 이미지 다운로드
2. docker-compose 사용
    1. docker-compose.yml 파일이 있는 디렉토리에서 docker-compose up 명령어를 실행하여 컨테이너를 시작
3. 실행

---

### docker-compose.yml 파일 공유

1. docker-compose 파일 준비
2. GitHub과 같은 코드 관리 시스템에 공유
    1. 다른 사용자가 쉽게 접근하고 사용할 수 있도록
3. 환경변수 처리
    1. docker-compose.yml 파일 내에서 환경 변수를 참조하도록 설정하고, 실제 값은 사용 환경에서 설정