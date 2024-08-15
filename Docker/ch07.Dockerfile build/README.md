# Dockerfile build 방법

```bash
docker build -t IMAGENAME:TAG [-f DOCKERFILE_NAME] DOCKERFILE_LOCATION
```

### OPTION

`-t IMAGENAME:TAG` : 생성할 이미지명:버전

`DOCKERFILE_NAME` : 기본 Dockerfile이 아닌 다른 파일명인 경우 -f 사용

`DOCKERFILE_LOCATION` : 현재 경로이면 . | 다른경로이면 경로명 표시
