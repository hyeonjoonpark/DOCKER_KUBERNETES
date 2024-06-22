# DOCKER_KUBERNETES

도커와 쿠버네티스 DevOps 공부 레포지토리

[https://hub.docker.com](https://hub.docker.com/) 도커 허브 웹사이트

### 목차

1. 컨테이너 기술
2. PWD(Play With Docker)
3. 웹서버(Nginx)
4. DB 컨테이너

---

### Docker 명령어

#### Docker 이미지 생성

```bash
docker pull [도커이미지]:[태그]
```

`ex) docker pull nginx:1.23.1-alpine`

태그는 보통 버전을 작성함

#### Docker 이미지 확인

```bash
docker images
```

#### Docker 이미지 삭제

`docker images` 명령어로 이미지 확인

```bash
docker rmi [이미지 ID]
```

_Option_

`-f` : 강제삭제

#### Docker 이미지를 컨테이너로 띄우는 명령어

```bash
docker run -d -p 8001:8000 --name=webserver [pull 받은 이미지]
```

`ex) docker run -d -p 8001:8000 --name=webserver nginx:1.23.1-alpine`

옵션

- -d : 백그라운드로 띄움
- -p : 포트 퍼블리시 (호스트 포트 : 80)

  호스트포트 = 리눅스 환경(리눅스 기본포트 0 ~ 65536)

- --name : 컨테이너 이름 지정

#### 컨테이너 확인 명령어

```bash
docker ps
```

#### Docker 프로세스 중단

```bash
docker stop [컨테이너 이름]
```

중단된 컨테이너 확인

- docker ps -a

#### 컨테이너 삭제

```bash
docker rm [컨테이너 이름]
```

#### 컨테이너 실행 유지 및 빠져나오기

exit 명령어를 사용하면 컨테이너가 중단되기 때문에 escape sequences (Ctrl + C + Q) 단축키를 사용한다

#### Docker Proxy

```bash
docker instpect [컨테이너 이름] | grep -i ipa
```

`NAT(Network Address Translation)` : 사설 IP주소를 공인 IP주소로 바꿔주는 주소변환 방식

`NAPT(Network Address Port Translation)` : IP 주소의 변환과 동시에 포트번호로 변환하는 것
