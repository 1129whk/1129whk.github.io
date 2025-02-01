---
title: "Several ports (8005, 8080) required by Tomcat v9.0 Server at localhost are already in use"
date: 2025-02-01 23:00:00 +0800
categories: [Etc, Error]
tags: [Etc, Error]
image:
  path: /assets/img/posts/2025-02-01-Several ports (8005, 8080) required by Tomcat v9.0 Server at localhost are already in use/port.png
  alt: 포트해결 사진
---

## Problem

<br>
윈도우에서 오류가 났고, 윈도우키+cmd를 입력하여 명령 프롬프트에서 오류해결 진행했습니다.

해당 포트를 이미 사용하고 있어서 실행 불가하다는 오류였습니다.

<br>
<img src="/assets/img/posts/2025-02-01-Several ports (8005, 8080) required by Tomcat v9.0 Server at localhost are already in use/port.png" alt="Error 사진">
<hr>
<br>


## Solution

<br>
Solution1이 더 편하다고 생각합니다. 원하는 포트 번호의 pid가 포함된 row를 보여주기 때문입니다.

Solution2은 목록을 보여주기 때문에 해당하는 포트의 pid를 찾아야 합니다.
<br>
<br>


### Solution1

<br>

    Ctrl+R : cmd
    netstat -ano |findstr 8080(port number)
    taskkill /f /pid (pid of port)

<br>


### Solution2

<br>

    Ctrl+R : cmd
    netstat -a -n -o -p tcp
    taskkill /f /pid (pid of port)

<hr>
<br>


## Reference

  <https://stackoverflow.com/questions/39632667/how-do-i-kill-the-process-currently-using-a-port-on-localhost-in-windows>



