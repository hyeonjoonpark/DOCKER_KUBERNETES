# Dockerfile 명령어

### IaC(Infrastructure as Code)가 필요한 이유

`IaC` : 코드형 인프라

커맨드 기반의 인프라 구성 시 사용자 실수 등의 인적 오류 가능성이 높다

-> 이러한 수고로운 작업을 하나의 이미지로 만들어 놓고 수정사항은 언제든지 변경이 가능하다면 개발업무에만 집중할 수 있다.

-> 코드형 인프라는 탄력성, 확장성, 반복성을 부여하여 동일한 환경을 보유한 서버 여러대를 운영, 관리할 수 있다.

### Dockerfile

Dockerfile은 Docker에서 동작하는 컨테이너의 구성정보를 프로비져닝한 텍스트 templete 파일이다

`프로비져닝(Provisioning)` : 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포하였다가 필요할 때 시스템을 즉시 사용할 수 있는 상태로 만들어 놓는 것

# Dockerfile 명령어

`FROM` 명령어

- (필수) 생성하려는 이미지의 베이스 이미지 지정으로
  hub.docker.com 에서 제공하는 공식이미지를 권장하며 이미지 태그는 도커허브에서
  여러 태그가 버전정보 처럼 제공된다

- 이미지를 선택할 때 작은 크기의 이미지(Slim)과 리눅스 배포판인 알파인(alpine)을 권장한다

- 태그를 넣지 않으면 latest로 지정된다

```Dockerfile
ex) FROM ubuntu:20.04
ex) FROM mysql:8.0.4
```

---

`MAINTAINER` 명령어

- 일반적으로 이미지를 빌드한 작성자 이름과 이메일을 작성한다.

사용방법

```Dockerfile
MAINTAINER hyeonjoonpark<pjjoon1379@gmail.com>
```

---

`LABEL` 명령어

- 이미지 작성 목적으로 버전, 타이틀, 설명, 라이선스 및 작성자 정보 등을 작성한다
- 하나 이상 작성이 가능하다

```Dockerfile
LABEL purpose = 'Nginx for Web Server' \
      version = '1.0' \
      description = 'Web Server application using Nginx'
```

아래와 같이 작성해도 된다. 그러나 위에 처럼 작성하는 것을 권장한다.

```Dockerfile
LABEL purpose = 'Nginx for Web Server'
LABEL version = '1.0'
LABEL description = 'Web Server application using Nginx'
```

---

`RUN` 명령어

- 설정된 기본 이미지에 패키지 업데이트, 각종 패키지 설치, 명령, 실행 등을 작성한다
- 하나 이상 작성이 가능하다.

예시)

```Dockerfile
RUN apt update
RUN apt -y install nginx
RUN apt -y install git

권장사항
- RUN 명령어의 개별 수를 줄여서 여러 설치 명령을 연결하면 이미지의 레이어 수가 감소
- Autoremove, autoclean, rm -rf /var/lib/apt/lists/* 를 사용하면
  저장되어 있는 apt 캐시가 삭제되기 때문에 이미지 크기 감소

RUN apt update && apt install -y nginx \
                    git \
                    vim \
                    curl && \
    apt clean -y && \
    apt autoremove -y \
    rm -rf /var/lib/apt/lists/* /var/tmp/*
```

---

`CMD` 명령어

- 생성된 이미지를 컨테이너로 실행할 때 실행되는 명령이고
  ENTRYPOINT 명령문으로 지정된 커멘드에 디폴트로 넘길 파라미터를 지정할 때 사용된다.
- 여러개의 CMD를 작성해도 마지막 하나만 처리된다

사용방법)

[shell 방식]

```Dockerfile
CMD apachectl -D FOREGROUND
```

[exec 방식]

```Dockerfile
CMD ["python", "app.py"]
```

---

`ENTRYPOINT` 명령어

- CMD 명령어와 마찬가지로 생성된 이미지가 켠테이너로 실행될 떄 사용되지만
  다른 점은 컨테이너가 실행될 때 명령어 및 인자 값을 전달하여 실행한다

- CMD는 하나만 실행되지만 ENTRYPOINT는 여러개 실행 가능하다

사용방법) CMD랑 유사하지만 인자 값을 사용하는 경우 유용

```Dockerfile
ENTRYPOINT ["npm", "start"]
```

---

`COPY` 명령어

- 호스트 환경의 파일, 디렉토리를 이미지 안에 복사하는 경우 사용
- 단순한 복사 작업만 지원한다
- 빌드 작업 디렉토리 외부의 파일은 COPY 할 수 없다
- COPY는 ADD보다 더 예측가능하고 오류가 덜 발생한다

```Dockerfile
COPY ./runapp.py /

주의) 작업 영역 전체를 복사하기 때문에 비효율적
COPY ./app
```

---

`ADD` 명령어

- 호스트 환경의 파일, 디렉토리를 이미지 안에 복사하는 것 뿐만 아니라, URL 주소에서 직접 다운로드 하여 이미지에 넣을 수도 있다.
- 압축파일(tar, tar.gz) 인 경우에는 지정된 경로에 압축을 풀어서 추가한다.
- 디렉토리 추가 시에는 /로 끝나야 한다.

사용방법)

```Dockerfile
ADD index.html /usr/share/nginx/html
ADD website.tar.gz /var/www/html
ADD http://example.com/view/customer.tar.gz /workspace/data/
```

---

`ENV` 명령어

- 이미지 안에 각종 환경변수를 지정하는 경우 사용한다

```Dockerfile
ENV JAVA_HOME=/usr/lib/jvm/java-17-oracle
ENV PATH /usr/local/nginx/bin:$PATH
```

---

`EXPOSE` 명령어

- 컨테이너가 호스트 네트워크를 통해 들어오는 트래픽을 리스닝하는 포트와 프로토콜을 지정하기 위해 사용한다.

- Nginx와 Apache는 기본적으로 80, 443을 사용

- 이미지 내에서 애플리케이션이 사용하는 포트를 사전에 확인하고 호스트와 연결되도록 구성하는 경우 설정하고 `docker run` 명령 사용시 `-p` 옵션을 통해 사용된다.

```Dockerfile
EXPOSE 80

또는

EXPOSE 80/tcp
```

---

`VOLUME` 명령어

- 볼륨을 이미지 빌드에 미리 설정하는 경우 작성한다.

예시)

```Dockerfile
VOLUME /var/log
```

---

`USER` 명령어

- 컨테이너의 기본 사용자는 root 이다.

```Dockerfile
USER hyeonjoonpark
```

---

`WORKDIR` 명령어

- 컨테이너 상에서 작업할 경로(디렉토리) 전환을 위해 작성한다.
- WORKDIR을 작성하면 RUN, CMD, ENTRYPOINT, COPY, ADD 명령문은 해당 디렉토리 기준으로 작성한다.
- 지정한 경로가 없으면 자동 생성되고, 컨테이너 실행 이후 컨테이너의 접속 `docker exec -it my_container bash` 하면 지정한 경로로 연결된다

```Dockerfile
WORKDIR /workspace
```

---

`ARG` 명령어

- docker build 시점에서 변수 값을 전달하기 위해 "--build-arg=인자" 를 정의하여 사용한다.

사용방법)

```Dockerfile
ARG db_name
```

Dockerfile에 ARG 변수를 정의하고 도커 빌드 시 변수값을 저장하면 이미지 내부로 인자가 전달된다

```bash
docker build --build-arg db_name=my_db
```

---
