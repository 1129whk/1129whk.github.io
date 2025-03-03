---
title: "AWS) Putty를 이용한 EC2 연결"
date: 2025-03-03 22:50:00 +0800
categories: [Cloud, AWS]
tags: [Cloud, AWS]
image:
  path: /assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/11-result.png
---

## Objective

<br>
생성한 EC2 가상머신에 putty를 이용해서 실제 터미널에 접근
<br>
<br>

### Puttygen 설치

<br>
키 변환 프로그램. 사용자 키 페어 파일을 putty 형식으로 변환할 수 있습니다.
<br>
<br>

### Putty 설치

<br>
키를 사용하고 putty를 이용해서 EC2에 접근

<hr>
<br>

## Solution

<br>

- Puttygen 실행 -> Load -> 키 파일 선택(All Files선택해서 조회)

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/1-Puttygen.png" alt="Puttygen">
<br>
<br>

- Save private key -> yes -> PuTTY 형식으로 선택하고, 임의의 파일 이름 입력

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/2-Save private key.png" alt="Save private key">
<br>

- 창닫기 -> 키를 변환하는 과정이 끝났습니다.

<br>

- Putty 실행 -> SSH-Auth -> ppk 파일 선택

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/3-SSH-Auth.png" alt="SSH-Auth">
<br>
<br>

- AWS 콘솔에 로그인 -> EC2 메뉴-인스턴스 메뉴 -> 인스턴스

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/4-Instance menu.png" alt="Instance menu">
<br>
<br>

- 퍼블릭 IPv4 주소 복사 -> putty 실행 -> IPv4 주소를 붙여넣기 -> Open

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/5-IPv4 Address.png" alt="IPv4 Address">
<br>
<br>

- amazon linus tool을 썼기 때문에 기본 계정 : ec2-user 입력.

키 파일로 접근했기 때문에 비밀번호는 패스하게 됩니다.

timezone이 달라서, 서버시간을 한국시간으로 변경해야 합니다.

리눅스에서 $ 표시는 일반 사용자를 의미하고, 관리자 권한이 필요한 명령어를 쓰게 되면 'sudo'라는 명령어를 써야 반영이 됩니다.

-> 로컬 시간 삭제

<br>

        ec2-user

        sudo rm /etc/localtime

        sudo ln -s /usr/share/zoneinfo/A

        sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

<br>

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/6-localtime.png" alt="localtime">
<br>

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/7-localtime change.png" alt="localtime change">
<br>
<br>

- 정보가 변경되었는지 확인

<br>
        
        cat /etc/sysconfig/clock

<br>

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/8-clock.png" alt="clock">
<br>

<br>

        sudo vi /etc/sysconfig/clock

<br>

아래 화면으로 넘어갔습니다.
<br>
<br>

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/9-UTC.png" alt="UTC">
<br>
<br>

- 텍스트를 변경 -> ESC -> 하단의 'INSERT' 사라짐 -> ':' 콜론을 입력 -> 'wq' 입력하고 빠져나오기

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/10-Zone change.png" alt="Zone change">
<br>
<br>

- 다시 아래의 명령어로 정보가 변경되었는지 확인 -> 재시작

<br>

        cat /etc/sysconfig/clock

        sudo reboot

<br>

- 오른쪽 마우스 클릭 -> Restart Session

- 다시 로그인

<br>

<img src="/assets/img/posts/2025-03-03-AWS) Putty를 이용한 EC2 연결/11-result.png" alt="result">

<hr>
<br>

## Reference

<https://asf.alaska.edu/how-to/data-recipes/connect-to-your-ec2-instance-using-putty-v1-1/>

<https://stackoverflow.com/questions/34394279/how-to-set-aws-amazon-server-time-cant-find-etc-sysconfig-clock-file>
