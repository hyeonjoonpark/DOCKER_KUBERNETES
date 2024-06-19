# 웹서버(Nginx)

- Nginx는 Web Server로 널리 사용됨
- Nginx는 Reverse Proxy 구현가능
- Nginx는 API 트래픽 처리가 가능한 고급 http 기능 보유, API gateway 구현가능

---

#### 이미지 pull

```bash
docker pull nginx
```

alpine version

```bash
docker pull nginx:1.25.0-alpine
```

- 배포판 리눅스와 alpine 리눅스의 차이 : alpine이 훨씬 더 경량적이다

---

#### Default 포트 확인

```bash
docker image history nginx:1.25.0-alpine
```

nginx는 Default가 80포트

---

#### 컨테이너 실행

`ex) docker run -d -p 8001:8000 --name=webserver nginx:1.25.0-alpine`

---

#### 컨테이너 학인

```bash
docker ps
```

0.0.0.0:8001->80

외부에서 들어온 모든 IP에서 8001로 패킷 전달 시 컨테이너 내부의 80포트로 전달 됨

8001번을 80번으로 연결하는 역할을 하는 것이 `docker proxy`

```bash
docker port webserver
```

`docker port [컨테이너 이름]` 로 확인 가능
