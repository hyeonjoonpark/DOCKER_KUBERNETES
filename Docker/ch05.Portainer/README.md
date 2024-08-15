# Portainer

Portainer CE는 Docker, Swarm, Kubernetes 및 ACI 환경을 관리하는데 사용할 수 있는 컨테이너화 된 애플리케이션을 위한 경량 서비스 제공 플랫폼이다.

배포와 사용이 간단하게 설계되었고, 이 애플리케이션을 통해 'Smart' GUI 및 광범위한 API를 통해 docker에서 사용하는 대부분의 리소스를 관리할 수 있음

### Portainer 컨테이너 생성

```bash
docker pull portainer/portainer-ce
```

```bash
docker volume create [볼륨 이름]
```

기본적으로 9000번 포트 사용

```bash
docker run -d -p 9000:9000 -v /var/run/docker.sock [볼륨 이름]:/data --restart=always portainer/portainer-ce --name [컨테이너 이름]
```

#### 옵션

- `-d` : 컨테이너를 백그라운드에서 실행합니다.

- `-p 9000:9000` : 호스트의 9000번 포트를 컨테이너의 9000번 포트에 매핑합니다. Portainer의 웹 인터페이스는 기본적으로 9000번 포트를 사용합니다.

- `-v /var/run/docker.sock:[볼륨 이름]` : /data: Docker 소켓(docker.sock)을 컨테이너에 마운트하고, 생성한 볼륨을 /data 디렉토리에 마운트합니다. 이를 통해 컨테이너가 Docker 데몬과 상호작용할 수 있습니다.

- `--restart=always` : 컨테이너가 중지되거나 Docker 데몬이 재시작될 때 자동으로 컨테이너를 재시작합니다.

- `--name [컨테이너 이름]` : 컨테이너에 사용자가 지정한 이름을 부여합니다.

- `portainer/portainer-ce` : 실행할 이미지 이름입니다.
