---
title: "프로젝트 구조 변경 Changing structure of Dynamic Web Project"
date: 2025-02-19 18:00:00 +0800
categories: [Etc, IDE]
tags: [Etc, IDE]
image:
  path: /assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/WebContent.jpeg  
---
아주 예전에 이클립스로 배울 때 겪었던 문제점을 기록한 것입니다.
<hr>
<br>

## Topic

<br>
[프로젝트 구조 바꾸기] Changing structure of Dynamic Web Project : WebContent folder inclucing META-INF and WEB-INF folder for Dynamic Web Project
<hr>
<br>


## Problem

<br>
스프링 설치 후, Dynamic Web Project를 생성하면, WebContent 폴더가 생성되지 않고, 다음과 같은 구조가 보였습니다.

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/WebContent.jpeg" alt="WebContent">
<hr>
<br>


## Solution

<br>

Dynamic Web Project를 초기 생성할 때, WebContent 폴더를 Content directory field에 들어가게 구조를 변경하였습니다.

### 1. Project name 입력 -> Next

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/Project name.jpeg" alt="Project name">


### 2. build path에서 'src\main\java' 폴더를 삭제.

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/build path.jpeg" alt="build path">


### 3. 'src' 폴더를 추가.

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/Add Folder.jpeg" alt="Add Folder">

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/Src.jpeg" alt="Src">


### 4. Default output folder 가 build\classes' 로 되어 있는지 확인하고 맞으면 Next.

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/Default output folder.jpeg" alt="Default output folder">


### 5. Content directory 이름을 WebContent' 로 변경 -> Finish

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/directory change.jpeg" alt="directory change">


### 6. 프로젝트 구조에 'META-INF'와  'WEB-INF'를 포함하는  'WebContent' 폴더가 있는지 확인.

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/WebContent Check.jpeg" alt="WebContent Check">


### 7. 프로젝트의 Properties  -> Java Build Path -> Libraries 

: Libraries 에서 'EAR Libraries', 'Server Runtime', 'Web App Libraries' 가 있는지 확인.
없으면 'Add Library'를 선택해서 추가할 수 있습니다.

<img src="/assets/img/posts/2025-02-19-프로젝트 구조 변경 Changing structure of Dynamic Web Project/Libraries.jpeg" alt="Libraries">
<hr>
<br>


## Reference

<https://stackoverflow.com/questions/10186134/webcontents-folder-not-visible-from-eclipse-project-view>

