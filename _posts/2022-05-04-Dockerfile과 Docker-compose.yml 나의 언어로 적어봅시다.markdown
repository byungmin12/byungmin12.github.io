# Dokerfile for react

```docker
# Base 이미지
FROM node:14.15.1-alpine3.12

# 빌드된 산출물을 실행시키기 위해 필요한 serve 모듈
RUN npm install -g serve

# 작업 공간
RUN mkdir /app
WORKDIR /app

COPY package.json .
RUN npm install
COPY . .
RUN npm run build



# 실행 명령어
ENTRYPOINT ["serve", "-s", "build"]
```

FROM : node tjfcl

RUN: 명령어 수행

WORKDIR : 디렉토리 설정

COPY : 복사

ENTRYPOINT : 명령어 실행
CMD : 명령어 실행

> ENTRYPOINT와 CMD의 차이를 서술하시오

> 주의
> RUN은 Local에서 실행
> 나머지들은 DOCKER 내부에서 실행된다고 생각해야함
> 잊지말자 내가 Dockerfile을 작성하면서 만났던 모든 에러는 이 문제와 관련이 있었다.

> 위에서 serve를 인스톨하고 사용하는 이유
> build에서 만들 파일을 Docker에 띄우기위해서

# docker-compose.yml

dockerfile을 docker에서 구동(?)하기 위해서는 매우 복작한 명령어는 작성해야함

그것을 간단 docker-compose up -d --build만 하면 쇼로로롱

```yml
version: "3.4"

services: # 컨테이너들을 정의
  ml-lv: # 컨테이너 이름
    build:
      context: ./ # 도커파일이 위치한 위치
      dockerfile: dockerfile # 도커파일 이름
    ports:
      - "3000:3000" # port 맵핑
    stdin_open: true # 리액트 앱을 돌리때 필요한 옵션 , 리액트앱을 끌때 필요
```
