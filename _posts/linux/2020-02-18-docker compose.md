## docker-compose
* docker의 컴포넌트들을 생성, 실행시 명령어에 매 번 옵션을 적어주기 귀찮
* docker-compose.yml에 이런 것들 + 컴포넌트간 관계 등을 적어두고 한 번에 실행

### docker-compose.yml
* 예시(mysql)
```
version: "3.5"
services:
  petnow_mysql:
    image: mysql
    volumes :
      - type: bind
        source: /var/ebs/sub1/mysql
        target: /var/lib/mysql
    restart: always
    ports:
      - 12396:3306
    environment:
      MYSQL_ROOT_PASSWORD: hoyun0112!
```

#### version
- docker, docker compose의 버전에 맞게 설정
#### volumes 
- 도커의 컴포넌트를 삭제하면 컴포넌트에 있던 데이터들도 삭제됨
- 영속성을 위해 도커를 실행하는 호스트에 데이터를 저장하기 위한 기능
##### type
- volume : 도커가 관리하는 곳에 데이터를 저장. docker/volumes/.../
- bind : 내가 원하는 경로를 지정할 수 있음. volume에 비해 권장되지 않음
- tmpfs : ?
##### source
- 호스트 내 저장하고자 하는 위치
##### target
- 컨테이너 내 데이터의 위치

### 명령어
```
sudo docker-compose up    //모든 컴포넌트들 실행
sudo docker-compose stop
```
