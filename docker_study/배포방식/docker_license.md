> 도커 이미지 배포 방법과 라이선스 옵션을 파악하여 **Docker 이미지 배포 전략**을 선택하고자 합니다.

---

### **1. Docker License**

- 도커 엔진, CLI, compose는 직접 설치 시 무료
    - Apache Licencse
    - https://github.com/docker/compose/blob/main/LICENSE**Github 계정 연결**

      https://github.githubassets.com/favicon.ico

- 도커 데스크탑 - 상업적 이용 시 유료
    - [Docker Engine overview](https://docs.docker.com/engine/#licensing)

      https://docs.docker.com/assets/favicons/docs@2x.ico

---

### **2. Docker Hub License**

**(1) personal**

- 무료
- private repositories : 1개

**(2) pro**

- $5 / 6653.52원/월
- private repositories : 무제한
- Image pull rate : 1일 5000개
- `pro`이후부터 bitbucket을 연동해서 빌드 자동화 가능
    - 코드가 업데이트될 때마다 새 이미지를 자동으로 빌드하고 태그를 지정
- [Set up Automated Builds](https://docs.docker.com/docker-hub/builds/?_gl=1*n7m42e*_ga*OTg3MTkzMzA4LjE3MDkxMDg0MzQ.*_ga_XJWPQMJYHQ*MTcwOTU5NDg2Ny44LjEuMTcwOTU5NzI0Ny42MC4wLjA.)

  https://docs.docker.com/assets/favicons/docs@2x.ico

**(3) team**

- $9 / 11976.34원/월

**(4) business**

- $24 / 31936.92원/월
- 참고 : [Pricing | Docker](https://www.docker.com/pricing/)

  !https://www.docker.com/wp-content/uploads/2024/02/cropped-docker-logo-favicon-32x32.png

---

### **3. Docker Organization**

- Docker Hub 내에서 여러 사용자가 공동으로 작업하고 리소스를 공유할 수 있는 그룹 또는 팀을 의미
- 팀원들은 이미지를 업로드하고, 접근 권한을 관리하며, 프로젝트를 공동으로 작업할 수 있다
- 리포지토리 관리, 팀원 초대 및 역할 할당, 접근 권한 관리 등의 기능을 제공
- 도커 라이선스 플랜의 team / business 가 organization으로 운영됨
- 참고 : [Docker](https://hub.docker.com/billing/core/purchase?type=organization)

  https://hub.docker.com/favicon.ico

---

### **4. Docker private registry**

- Docker hub에 private image를 올리는 것은 제한이 있다. 개인 사용자의 경우 하나의 이미지만 private이 가능하고, organization의 경우에는 비용을 지불해야만 사용이 가능하다.
- 그렇지만 도커 사설 레지스트리(docker private registry)를 사용하여 사용자가 직접 이미지 저장소를 만드는 방법도 있다. 보안이 중요한 곳에서 사용되며, 사용자가 직접 이미지 저장소 및 사용되는
  서버, 저장 공간 등을 관리해야 한다
- 사설 Docker Registry를 인터넷에 공개적으로 접근 가능하게 설정하고 적절한 보안 조치(예: 인증, SSL/TLS 등)를 구현한다면, 다른 위치에서도 사설 Registry에 접속하여 이미지를 pull
  받을 수 있다. 이 과정에는 도메인 이름 설정, 포트 포워딩, 보안 설정 등 추가적인 네트워크 및 보안 구성이 필요할 수 있다.

⇒ 사설 레지스토리 생성 테스트 필요

---

### **5. public Cloud Service**

- 도커 이미지 호스팅 서비스를 이용하는 것
    - ex) Azure Container Registry, DigitalOcean, AWS ECR, Google Cloud 등
        - [The Best Docker Hosting Platforms of 2024](https://digital.com/best-docker-hosting/#Kamatera) - 대부분 유료 라이선스
          필요

          !https://digital.com/wp-content/uploads/2023/11/cropped-Digital-Favicon_512px-32x32.webp

---

### 5. 결론

- 만약 도커 이미지를 올리고 어디에서든 내려받을 수 있도록 해야한다면, 세 가지 방법을 사용할 수 있다.
    -
        1. Docker Hub라는 도커 공식 이미지 호스팅 서비스의 유료 플랜을 사용
    -
        2. 사설 도커 레지스트리를 생성하여 관리하는 것
    -
        3. 도커 이미지 호스팅 서비스를 이용하는 것
- 따라서, **사설 레지스트리**를 구축하여 테스트를 진행한 후, 다른 위치에서도 이미지 사용이 원활하다면 사설 레지스트리 사용을 고려해볼만 하다. 반면, 만약 사설 레지스트리 사용이 적합하지 않다고 판단되면
  Docker Hub의 유료 플랜을 이용하는 것이 바람직할 것 같다.

---

### 그 외 궁금한 것

- 기업에서는 도커허브 유료 플랜을 사용하면 되는데 왜 굳이 도커 이미지 호스팅 서비스를 사용하는 사람이 많을까?
    - 기업이 Docker Hub 유료 플랜 대신 다른 도커 이미지 호스팅 서비스를 사용하는 이유는 다양합니다. 주된 이유는 보안, 특정 기능 요구사항, 비용 효율성, 지원 수준, 사용자 정의 가능성 등에
      있습니다. 사설 호스팅 서비스를 사용하면 더 높은 수준의 보안 및 컨트롤을 제공하고, 기업의 특정 요구에 맞춘 사용자 정의가 가능해집니다. 또한, 특정 지역 또는 규제 준수 요구사항을 충족시킬 수 있으며,
      때로는 비용 절감이 가능하기도 합니다.
- 유명한 도커 호스팅 서비스 목록
    - [7 Best Free Docker Hosting Services Mar 2024](https://hostadvice.com/docker-hosting/free-docker-hosting/)

      !https://cdn.hostadvice.com/2021/11/cropped-favicon-32x32.png

    - [The Best Docker Hosting Platforms of 2024](https://digital.com/best-docker-hosting/)

      !https://digital.com/wp-content/uploads/2023/11/cropped-Digital-Favicon_512px-32x32.webp

- fly.io
    - Dockerfile을 사용하여 프로젝트 배포 가능 [Deploy via Dockerfile](https://fly.io/docs/languages-and-frameworks/dockerfile/)

      !https://fly.io/static/images/favicon/favicon-16x16.png

    - 유료플랜 [Fly.io Resource Pricing](https://fly.io/docs/about/pricing/)

      !https://fly.io/static/images/favicon/favicon-16x16.png

---

### Podman

- [Podman이란?](https://www.redhat.com/ko/topics/containers/what-is-podman)

  https://www.redhat.com/favicon.ico

- 리눅스 시스템에서 컨테이너를 개발, 관리, 실행하기 위한 오픈 소스 도구
- 데몬 없는 아키텍처를 사용하여 컨테이너 관리를 더 안전하고 쉽게 만들고, 컨테이너 사용자 정의를 위해 Buildah 및 Skopeo와 같은 도구와 통합.
- 컨테이너, 포드, 컨테이너 이미지, 볼륨을 실행 지원하며, 보안 위험을 줄이는 루트리스 컨테이너를 지원하여 더 안전한 컨테이너 운영을 가능하게 한다고 함.
- 관련자료
    - https://blog.naver.com/pjt3591oo/222997069333
    - [[Container] Podman 설치 및 사용법](https://tech.chhanz.xyz/container/2020/03/02/podman/)

      !https://tech.chhanz.xyz/assets/favicon.png

    - [Podman](https://podman.io/get-started)

      https://podman.io/favicon.ico

- (더 깊은 리서치 필요)