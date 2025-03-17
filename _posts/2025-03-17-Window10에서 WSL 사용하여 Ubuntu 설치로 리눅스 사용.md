---
title: "Window10에서 WSL 사용하여 Ubuntu 설치로 리눅스 사용"
date: 2025-03-17 23:35:00 +0800
categories: [Programming, Linux]
tags: [Programming, Linux]
image:
  path: /assets/img/posts/2025-03-17-Window10에서 WSL 사용하여 Ubuntu 설치로 리눅스 사용/3-Search Ubuntu.png
---

## Objective

<br>
윈도우 운영체제에서 Linux를 사용해보기 위함.

리눅스를 설치하기 위해서 가상 머신을 사용할 수 있지만 WSL(Windows Subsystem for Linux / Linux용 Windows 하위 시스템) 에 비해 많은 메모리와 용량을 차지하기 때문에 간단히 사용해볼 목적으로 WSL 사용 및 Ubuntu를 설치하게 되었습니다.

(다만, WSL을 사용하기 위해 Windows 10 버전 1607이상이 필요하기 때문에 설정에서 확인해야 합니다.)

<hr>
<br>

## Solution

<br>
- 윈도우 메뉴에서 'powershell'을 검색한 다음 '관리자로 실행'

<img src="/assets/img/posts/2025-03-17-Window10에서 WSL 사용하여 Ubuntu 설치로 리눅스 사용/1-search powershell.png" alt="search powershell">
<br>
<br>

- 다음을 복사해서 실행된 Window PowerShell 에 붙여넣은 다음 엔터. (WSL 사용을 허용하기 위함입니다.)

<br>

      dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

<br>

아래와 같이 작업완료가 되었습니다.

<img src="/assets/img/posts/2025-03-17-Window10에서 WSL 사용하여 Ubuntu 설치로 리눅스 사용/2-Window PowerShell.png" alt="Window PowerShell">
<br>
<br>

- 컴퓨터를 다시 시작.

- Microsoft Store로 들어가서 'Ubuntu'를 검색한 다음 설치. (다른 리눅스 배포판을 설치할 수도 있습니다.)

<img src="/assets/img/posts/2025-03-17-Window10에서 WSL 사용하여 Ubuntu 설치로 리눅스 사용/3-Search Ubuntu.png" alt="Search Ubuntu">
<br>
<br>

- Ubuntu 설치 완료된 모습

<img src="/assets/img/posts/2025-03-17-Window10에서 WSL 사용하여 Ubuntu 설치로 리눅스 사용/4-Install Ubuntu.png" alt="Search Ubuntu">
