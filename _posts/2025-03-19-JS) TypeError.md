---
title: "JS) TypeError"
date: 2025-03-19 19:46:00 +0800
categories: [Programming, JavaScript]
tags: [Programming, JavaScript]
image:
  path: /assets/img/posts/2025-03-19-JS) TypeError/1-TypeError.png
---

## Problem

개발자 도구에서 'Uncaught TypeError: response.forEach is not a function' 오류를 볼 수 있었습니다.

<img src="/assets/img/posts/2025-03-19-JS) TypeError/1-TypeError.png" alt="TypeError">

<hr>
<br>

## Solution

Reference에서 First option을 참고했는데 response가 object와 같은 Array인 NodeList type이라서 해당 오류가 발생하였고 아래와 같이 해결했습니다.

<img src="/assets/img/posts/2025-03-19-JS) TypeError/2-TypeError Solution.png" alt="TypeError Solution">

<hr>
<br>

## Reference

<https://stackoverflow.com/questions/35969974/foreach-is-not-a-function-error-with-javascript-array>
