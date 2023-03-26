---
title: "applicaiton.yml에 옵션들"
excerpt: "이제는 좀 알고 쓰자 applicaiton.yml"

categories:
  - Spring
tags:
  - [Spring]

permalink: /spring/applicaitonyml/

toc: true
toc_sticky: true

date: 2023-03-25
last_modified_at: 2023-03-25
---
매번 사용할 때마다 검색하거나 다른 사람 것을 복붙하는등 매번 시간이 아깝기도 해서 이번 기회에 정리를 해보자!

<br>

# 애플리케이션 설정 파일 


스프링 부트 프로젝트의 src/main/resources를 열어보면 application.properties 또는 application.yml 파일이 있는것을 볼 수 있다. (처음 생성하면 .properties가 있고 확장자명을 .yml로 변경해서 사용하면 편하다 
   
# spring.profiles.
```
spring:
  profiles:
    actvie: dev # prod, test
```
- 각각 다른 application-dev.yml, application-prod.yml, application-test.yml를 생성해서 사용할 수 있다.
  
# spring.datasource
```
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://db:3306/gitrank?serverTimezone=Asia/Seoul
    username: root
    password: 1234
    hikari:
      maximum-pool-size: 5
      minimum-idle: 3
```
- 데이터베이스 관련 설정을 작성하면 된다.
- hikari: hikariCP는 가벼운 용량과 빠른 속도를 가지는 JDBC의 커넥션 풀 프레임워크이다.

  
# spring.jpa
```
spring:
  jpa:
    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
    open-in-view: false
    show-sql: true
    hibernate:
      format_sql: true
      ddl-auto: create
```
 - database-platform:
   - JPA 데이터베이스 플랫폼을 지정
 - open-in-view
   - OSIV(Open Session In View)는 웹 요청이 완료될 때까지 동일한 EntityManager를 갖도록 해줌
   - 스프링부트에서 OSIV가 기본값으로 true인데, 성능과 확장상 면에서 안좋다고함
- show-sql
  - 콘솔에 JPA 쿼리를 출력
- hibernate.format_sql
  - 콘솔에 출력되는 JPA 쿼리를 가독성있게 표현
- hibernate.format_sql
  - 데이터베이스 초기화 전략을 설정
    - none
      - 아무것도 실행하지 않는다
    - create
      - SessionFactory가 시작될 떄 기존테이블을 삭제 후 다시 생성
    - update
      - 변경된 스키마만 반영
    - validate
      - 엔티티와 테이블이 정상적으로 생성되었는지 확인

# spring.data
```
  data:
    web:
      pageable:
        max-page-size: 20
        default-page-size: 20
```
- 페이지네이션 관련 설정이다

# spring.sql
```
  sql:
    init:
      mode: always
```
- schema.sql, data.sql 사용할 수 있다.

<br>
일단 한번이라도 본 것만 정리해봤다.  <br>
검색해보니까 처음보는게 너무 많다. ㅠㅠ 화이팅..