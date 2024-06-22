# DB 컨테이너

### 도커이미지 생성

```bash
docker pull mysql:8.4.0
```

### 실행

```bash
docker run -it -e MYSQL_ROOT_PASSWORD=1234 mysql:8.4.0 /bin/bash
```

/bin/bash : 컨테이너 내부의 bash 환경으로 들어간다는 뜻

`/etc/init.d/mysql start` : MySQL Deamon 시작 명령어

#### 옵션

- `-it` : -it를 함께 사용하면, 컨테이너 내부에서 쉘을 실행하고, 사용자가 직접 명령어를 입력하고 실행할 수 있는 환경을 제공한다

  - `-i` : 컨테이너의 표준 입력(stdin)을 활성화하여, 사용자가 컨테이너 내부에서 상호작용할 수 있도록 한다

  - `-t`: 가상 터미널을 할당하여, 사용자가 터미널을 통해 컨테이너와 상호작용할 수 있도록 한다. 이 옵션은 주로 쉘을 실행할 때 사용된다

- `-e` : 컨테이너 내부에서 사용할 환경변수를 설정한다

docker run 명령어를 사용해서 접속하면 새로운 컨테이너가 만들어지기 때문에 원래 있던 컨테이너 접속하기 위해서는 다음 명렁어를 사용

```bash
docker exec -it [컨테이너 ID]
```

컨테이너가 꺼졌다가 커졌을 때는 Deamon을 다시 실행시켜야 함

```bash
/etc/init.d/mysql start
```
