---
title: "VueJS와 Spring Boot 연동 (MariaDB 사용) - ERR_CONNECTION_REFUSED 및 CORS 오류 해결"
date: 2025-02-28 23:45:00 +0800
categories: [Programming, VueJS]
tags: [Programming, VueJS]
image:
  path: /assets/img/posts/2025-02-28-VueJS와 Spring Boot 연동/result.png
---

## Objective

<br>
VueJS에서 Spring Boot로 개발한 API를 사용하기.

그리고 'ERR_CONNECTION_REFUSED 및 CORS'오류 해결하기.

<hr>
<br>

## Problem

<br>
Spring Boot에서의 포트번호 확인

<br>

        server.port = 9000

<br>
application.properties 파일에서 9000번으로 설정했습니다.
<br>

- GET http://localhost:9000/board net::ERR_CONNECTION_REFUSED 오류 해결

<br>
<img src="/assets/img/posts/2025-02-28-VueJS와 Spring Boot 연동/error connection.png" alt="error connection">

<br>
연결이 안 되는 오류를 아래와 같이 application.properties 파일에 코드를 추가했습니다.

<br>

        #VueJS 연동
        spring.mvc.pathmatch.matching-strategy = ANT_PATH_MATCHER

<br>

- CORS policy 오류 하지만 다른 오류가 나게 됩니다.

<br>
<img src="/assets/img/posts/2025-02-28-VueJS와 Spring Boot 연동/CORS policy error.png" alt="CORS policy error">
<br>

<br>

        Access to fetch at 'http://localhost:9000/board' from origin 'http://localhost:8080' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.

<br>

위의 오류를 해결하기 위해 WebConfiguration.java 파일에서 아래의 코드를 추가했습니다.

```java
        @Override
        public void addCorsMappings(CorsRegistry registry) {
            registry.addMapping("/**").allowedOrigins("http://localhost:8080");
        }
```

VS Code 에서 npm run serve를 했을 때, 아래와 같이 포트번호 8080을 쓰고 있기 때문데 다음 포트번호를 허용했습니다.

<br>
<img src="/assets/img/posts/2025-02-28-VueJS와 Spring Boot 연동/port number.png" alt="port number">
<br>

개발자도구 Console에 있던 모든 오류가 사라졌습니다

## Result

<br>
<img src="/assets/img/posts/2025-02-28-VueJS와 Spring Boot 연동/result.png" alt="result">
<br>

이렇게 HeidiSQL 에서 데이터를 입력했고

<br>
<img src="/assets/img/posts/2025-02-28-VueJS와 Spring Boot 연동/data confirm.png" alt="data confirm">
<br>

VueJS를 실행했을 때 오류 없이 데이터들을 확인할 수 있었습니다.
<br>

## Reference 1

<br>

<https://stackoverflow.com/questions/73688911/jenkins-build-and-deployment-of-spring-boot-client-microservice-fails-because-of>

<br>

## Reference 2

<br>
<https://stackoverflow.com/questions/35091524/spring-cors-no-access-control-allow-origin-header-is-present>
