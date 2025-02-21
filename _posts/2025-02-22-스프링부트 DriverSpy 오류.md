---
title: "스프링부트 DriverSpy 오류"
date: 2025-02-22 07:00:00 +0800
categories: [Programming, SpringBoot]
tags: [Programming, SpringBoot]
image:
  path: /assets/img/posts/2025-02-22-스프링부트 DriverSpy 오류/DriverSpy Error.png 
---
예전에 스프링부트 DriverSpy 라이브러리를 썼을 때 겪었던 문제점을 기록한 것입니다.
<hr>
<br>


## Concept

<br>
driverSpy는 주로 Spring Boot 애플리케이션에서 데이터베이스와 관련된 SQL 쿼리나 트랜잭션을 추적하고 디버깅하는 데 사용되는 기능입니다. 이 기능은 데이터베이스 드라이버의 동작을 감시하는 역할을 합니다.
<hr>
<br>


## Problem

<br><img src="/assets/img/posts/2025-02-22-스프링부트 DriverSpy 오류/DriverSpy Error.png" alt="DriverSpy Error">

<br>

    There was an unexpected error (type=Internal Server Error, status=500).
    nested exception is org.apache.ibatis.exceptions.PersistenceException: ### Error querying database. Cause: java.lang.RuntimeException: Driver net.sf.log4jdbc.sql.jdbcapi.DriverSpy claims to not accept jdbcUrl, jdbc:log4jdbc:mysql://localhost:3306/

<br>
DriverSpy 라이브러리를 사용하다가 'Driver net.sf.log4jdbc.sql.jdbcapi.DriverSpy claims to not accept jdbcUrl' 오류가 발생했습니다.
<hr>
<br>


## Solution

<br>
저는 mysql을 썼고, DB driver가 없어서 발생된 문제이기 때문에 'mvn mysql connector'라고 검색하여 다음과 같은 의존성 라이브러리를 pom.xml에 추가하였습니다.

<br>

    <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.31</version>
    </dependency>

<br>
오류가 해결되었고 콘솔 창에서 로그를 확인할 수 있었습니다.





