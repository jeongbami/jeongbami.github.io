---
title: springboot를 이용한 게시판 및 mysql 연동 -1. 환경셋팅/DB연동
date: 2022-12-29 10:01:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# 게시판 주요 기능
1. 글쓰기 (/board/save)
2. 게시글 목록 (/board/)
3. 게시글 조회 (/board/{id})
4. 게시글 수정 (/board/update/{id})
5. 게시글 삭제 (/board/delete/{id})
5. 페이징처리 (/board/paging)

# resource
- main>resources>application.yml

```yml
# 서버 포트 설정
server:
  port: 8080

# database 연동 설정
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/db_codingrecipe?serverTimezone=Asia/Seoul&characterEncoding=UTF-8
    username: user_codingrecipe
    password: 1234
  thymeleaf:
    cache: false

  # spring data jpa 설정
  jpa:
    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
    open-in-view: false
    show-sql: true
    hibernate:
      ddl-auto: create
```

- applicatioin.yml

```yml
spring.datasource.url=jdbc:mysql://10.160.64.100:13307/op_371435a8_ec81_4ab7_9661_7a47043d6d02
    + jdbc:mysql://{mysql_proxy_ip}:{port}/{datasource}
spring.datasource.username=232355719a91aab3
spring.datasource.password=2b84d6727d3203b3
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver (manifest.yml 참조)
```

# mysql table 생성
- console창에서 table 사용 말하기  
    `mysql> use op_371435a8_ec81_4ab7_9661_7a47043d6d02;`
- Query 재생
- Query문 작성
- application.properties 수정
   `spring.datasource.url=jdbc:mysql://localhost:3306/{table_name}?serverTimezone=UTC&characterEncoding=UTF-8``

# input name == query name == variable name
- 다 같게해야 편함


# 오류


- 오류 1) mysql 권한 확인하기

```shell
Access denied for user '232355719a91aab3'@'%' to database 'op_371435a8_ec81_4ab7_9661_7a47043d6d02.board'
```

  + 권한 확인

  ```shell
  mysql> show grants for 232355719a91aab3;
  +-----------------------------------------------------------------------------------------------+
  | Grants for 232355719a91aab3@%
  +-----------------------------------------------------------------------------------------------+
   GRANT USAGE ON *.* TO '232355719a91aab3'@'%'                                                  |
   | GRANT ALL PRIVILEGES ON `op_371435a8_ec81_4ab7_9661_7a47043d6d02`.* TO '232355719a91aab3'@'%' |
   +-----------------------------------------------------------------------------------------------+
   ```


- 오류2) primarykey 사용 안할 시 strict_mode 해제하기(근데 불가능함.) 

```shell
# dercona-XtraDB-Cluster
- Method-1: Connect to mysql server and check variables
```

  + strict_mode 조회
  
  ```shell
  mysql> SHOW VARIABLES LIKE "pxc_strict_mode";
  +-----------------+--------+
  | Variable_name   | Value  |
  +-----------------+--------+
  | pxc_strict_mode | MASTER |
  +-----------------+--------+
  1 row in set (0.00 sec)
  ```

  + disabled pxc_strict_mode 해제
  ```shell
  mysql> SET GLOBAL pxc_strict_mode=DISABLED;
  Query OK, 0 rows affected (0.00 sec)
  
  mysql> SHOW VARIABLES LIKE "pxc_strict_mode";
  +-----------------+----------+
  | Variable_name   | Value    |
  +-----------------+----------+
  | pxc_strict_mode | DISABLED |
  +-----------------+----------+
  1 row in set (0.00 sec)
  
  However, this value will be reverted back to MASTER is the VM is restarted or recreated. Also, disabling the pxc-strict-mode is not discouraged by Percona (The vendor that provides this HA topology) as the pxc-strict-mode is an important safety guard. Therefore, to safely work around this issue, add a primary key or a unique (not null) key to this table. There are other implications to not doing that that could have performance or data integrity implications for replication.
  ```

일단..그냥 테이블 삭제 후 다시 생성해줬다.

- 오류 3 DB에 데이터가 안들어감

```shell
# unknwon caloum board_content
```
  
  + colum명 바꿔주기 
  
  기존
  
  ```shell
  CREATE TABLE `board` (
    `boardIndex` INT(10) NOT NULL AUTO_INCREMENT,
    `userId` VARCHAR(20) NULL DEFAULT NULL COLLATE 'utf8_general_ci',
    `boardTitle` VARCHAR(20) NULL DEFAULT NULL COLLATE 'utf8_general_ci',
    `boardContent` TEXT NULL DEFAULT NULL COLLATE 'utf8_general_ci',
    PRIMARY KEY (`boardIndex`) USING BTREE,
    UNIQUE INDEX `userId` (`userId`) USING BTREE
   )
   COLLATE='utf8_general_ci'
   ENGINE=InnoDB
   ;
   ```

언더바 삽입

```shell
CREATE TABLE `board` (
  `board_index` INT(10) NOT NULL AUTO_INCREMENT,
  `user_id` VARCHAR(20) NULL DEFAULT NULL COLLATE 'utf8_general_ci',
  `board_title` VARCHAR(20) NULL DEFAULT NULL COLLATE 'utf8_general_ci',
  `board_content` TEXT NULL DEFAULT NULL COLLATE 'utf8_general_ci',
  PRIMARY KEY (`board_index`) USING BTREE,
  UNIQUE INDEX `user_id` (`user_id`) USING 
  )
  COLLATE='utf8_general_ci'
  ENGINE=InnoDB
  ;
  ```
  언더바 삽입했더니 데이터가 들어왔따. 이유가뭐지.. java에서 카멜케이스가 DB이름이 _로 해야 맵핑된다네요..

- 오류 4 JPA 설치 에러 
  - javax persistence dependency 추가
  - guild.gradle.kts의 jpa 부분에 버전을 명시해줌 (:2.6.2)