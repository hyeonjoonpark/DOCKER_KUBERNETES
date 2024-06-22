# DB 컨테이너

### 도커이미지 생성

```bash
docker pull mysql:8.4.0
```

### 실행

```bash
docker run -it -e MYSQL_ROOT_PASSWORD=1234 mysql:8.4.0 /bin/bash
```

#### 옵션

- `-it` : -it를 함께 사용하면, 컨테이너 내부에서 쉘을 실행하고, 사용자가 직접 명령어를 입력하고 실행할 수 있는 환경을 제공한다

  - `-i` : 컨테이너의 표준 입력(stdin)을 활성화하여, 사용자가 컨테이너 내부에서 상호작용할 수 있도록 한다

  - `-t`: 가상 터미널을 할당하여, 사용자가 터미널을 통해 컨테이너와 상호작용할 수 있도록 한다. 이 옵션은 주로 쉘을 실행할 때 사용된다

- `-e` : 컨테이너 내부에서 사용할 환경변수를 설정한다