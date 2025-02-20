---
title: "스프링부트 스웨거 오류)Failed to start bean 'documentationPluginsBootstrapper'"
date: 2025-02-20 22:40:00 +0800
categories: [Programming, SpringBoot]
tags: [Programming, SpringBoot]
image:
  path: /assets/img/posts/2025-02-20-스프링부트 스웨거 오류 documentationPluginsBootstr/swagger-ui.png 
---
예전에 스프링부트와 스웨거를 썼을 때 겪었던 문제점을 기록한 것입니다.
<hr>
<br>

## Concept

<br>
Swagger를 사용하면, Spring으로 RestAPI를 개발하고 그에 대한 문서를 정리하여 클라이언트 및 서버 개발자들에게 공유하는 작업을 편리하게 할 수 있고 API 테스트를 할 수 있습니다.
<hr>
<br>


## Problem

<br>
<img src="/assets/img/posts/2025-02-20-스프링부트 스웨거 오류 documentationPluginsBootstr/swagger_error.png" alt="swagger-ui">

<br>

    Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
    2022-11-15 16:52:53.496 ERROR 6820 --- [  restartedMain] o.s.boot.SpringApplication               : Application run failed

    org.springframework.context.ApplicationContextException: Failed to start bean 'documentationPluginsBootstrapper'; nested exception is java.lang.NullPointerException: Cannot invoke "org.springframework.web.servlet.mvc.condition.PatternsRequestCondition.toString()" because the return value of "springfox.documentation.spi.service.contexts.Orderings.patternsCondition(springfox.documentation.RequestHandler)" is null

<br>
Failed to start bean 'documentationPluginsBootstrapper'; nested exception is java.lang.NullPointerException
<br>

swagger을 사용하려는데 위와 같은 오류가 발생
<hr>
<br>


## Solution

<br>

    spring.mvc.pathmatch.matching-strategy = ANT_PATH_MATCHER

<br>
주소 : http://localhost:8080/swagger-ui.html
<br>

<img src="/assets/img/posts/2025-02-20-스프링부트 스웨거 오류 documentationPluginsBootstr/swagger-ui.png " alt="swagger-ui">
<hr>
<br>

## Reference

<br>
<https://stackoverflow.com/questions/72357737/i-am-getting-this-error-failed-to-start-bean-documentationpluginsbootstrapper>









