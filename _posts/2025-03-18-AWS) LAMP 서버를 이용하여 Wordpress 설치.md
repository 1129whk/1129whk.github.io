---
title: "AWS) LAMP 서버를 이용하여 Wordpress 설치"
date: 2025-03-18 20:00:00 +0800
categories: [Cloud, AWS]
tags: [Cloud, AWS]
image:
  path: /assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/20-worldpress blog.png
---

## Objective

Linux에 Apache, MySQL, PHP 설치하고, 궁극적으로 Wordpress 설치하기

LAMP는 웹사이트 운영에 자주 쓰이는 소프트웨어 번들인 'Linux, Apache, MySQL, Php'를 의미

<hr>
<br>

## Solution

- putty 실행하여 로그인

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/1-putty.png" alt="putty">
<br>
<br>

- EC2 VM의 Linux Version 확인

<br>

            car /etc/system-release

<br>

- Amazon Linux 전용 패키지 설치 명령어 및 yum 명령어를 사용하여, Apache, PHP, MySQL을 설치

<br>

            sudo amazon-linux-extras install lamp-mariadb10.2-php7.2 php7.2 -y

            sudo yum install -y httpd mariadb-server

<br>

- Apache의 실행 및 실행되었는지 확인

<br>

            sudo systemctl start httpd

            ps -ef | grep httpd

<br>

실행이 안 되었으면 아래와 같이 나오는 목록이 없습니다.

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/2-list.png" alt="list">
<br>
<br>

<br>

            sudo systemctl status httpd

<br>

실행 중인 것을 확인할 수 있습니다.

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/3-status.png" alt="status">
<br>
<br>

- 마찬가지로 PHP도 실행하기

<br>

            sudo systemctl start php-fpm

            sudo systemctl status php-fpm

<br>

- Apache, php-fpm의 재시작 시 자동으로 시작할 수 있도록 설정

<br>

            sudo systemctl enable httpd

            sudo systemctl enable php-fpm

<br>

확인

<br>

            sudo systemctl status httpd

<br>

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/4-active.png" alt="active">
<br>
<br>

- AWS - 인스턴스 메뉴 -> 목록에서 인스턴스 ID 클릭 -> 아래에서 보안 탭 -> 보안 그룹 클릭

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/5-security group.png" alt="security group">
<br>
<br>

- 인바운드 규칙 편집 버튼 -> 규칙 추가 버튼 -> 0.0.0.0/0 선택(아무나 접속 가능하게 됨) -> 규칙 저장 버튼

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/6-inbound rule.png" alt="inbound rule">
<br>
<br>

적용되었습니다.
<br>

- 구매한 도메인 주소를 사용하여 Apache Demo 페이지 접근 테스트

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/7-Apache Demo.png" alt="Apache Demo">
<br>
<br>

- Apache의 document root

<br>

            cd /var/www
            ls -alt

<br>

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/8-Apache document root.png" alt="Apache document root">
<br>
<br>

ec2 user라서, 해당 디렉토리에 대한 권한을 조정해야 wordpress를 설치를 하고, 해당 디렉토리에 접근할 수 있습니다.
<br>

- 관리자 권한으로 유저의 권한을 조정

<br>

            groups
            sudo usermod -a -G apache ec2-user

<br>

ec2유저를 아파치 그룹에 넣기

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/9-ec2 user.png" alt="ec2 user">
<br>
<br>

오른쪽 마우스 클릭 -> Duplicate Session
<br>

- 새 창에서 다시 확인

<br>

            groups

<br>

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/10-apache confirm.png" alt="apache confirm">
<br>
<br>

권한을 변경함

<br>

            cd /var/www
            ls -alt

            sudo chown -R ec2-user.apache /var/www
            ls -alt

<br>

권한을 받았으면 ec2 유저가 해당 디렉토리에 들어가서 파일을 작성 가능.

<br>

            cd html
            ls

            echo "<?php phpinfo(); ?>"> /var/www/html/phpinfo.php

            pwd
            ls -alt
            cat phpinfo.php

<br>

php 모듈이 동작하는 지 확인
<br>

- php 연동 확인 테스트

<br>

            pwd

<br>

/var/www/html : 이 위치가 document root
<br>

- phpinfo.php 를 웹에서 확인

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/11-phpinfo.png" alt="phpinfo">
<br>
<br>

- 보안 취약점이 있어서 해당 파일을 지움

<br>

            ls -alt
            rm -f phpinfo.php
            ls -alt

<br>

- 웹에서 확인

'File not found.' 메시지가 보이며 파일이 지워진 것을 확인할 수 있습니다.
<br>

- mariadb 설치 및 상태 확인

<br>

            sudo systemctl start mariadb
            sudo systemctl status mariadb

<br>

- mysql 관리자 계정에 대한 DB 설정

<br>

            sudo mysql_secure_installation
            (enter)
            y
            (password)
            y
            y
            y
            y

<br>

<br>

    mysql -u root
    mysql -u root -p
    (password)

    show databases;

<br>

- 워드프레스에서 사용할 데이터베이스를 생성

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/12-database.png" alt="database">
<br>
<br>

- 워드프레스의 사용자와 비밀번호를 생성 및 적용 -> 테스트

<br>

            GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'localhost' IDENTIFIED BY '1234';
            FLUSH PRIVILEGES;
            show databases;

            exit
            mysql -u wordpress -p
            show databases;

<br>
- 워드프레스 설치

<br>

            exit
            pwd

            mkdir Downloads
            cd Downloads/
            pwd

<br>

home에서 디렉토리 만들고 위치확인

다운받고 확인하기 -> 압축풀기 -> 워드프레스 디렉토리로 이동 -> 해당 파일을 복사

<br>

            wget
            wget https://ko.wordpress.org/wordpress-5.0.11-ko_KR.zip
            ls -alt
            unzip wordpress-5.0.11-ko_KR.zip
            ls
            unzip wordpress-5.0.11-ko_KR.zip
            (Ctrl+C)
            ls
            cd wordpress/
            ls
            pwd
            cp -rp * /var/www/html/
            cd /var/www/html
            ls -alt

<br>

권한을 바꾸는 명령어

<br>

            cd ..
            sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
            find /var/www -type f -exec sudo chmod -0664 {} \;
            sudo chmod 777 /var/www/html -R

            ls
            cd html
            ls
            pwd

<br>

<br>

            ls -alt
            stat index.php
            ls -alt

<br>

파일변경

<br>

            mv wp-config-sample.php wp-config.php

<br>

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/13-file change.png" alt="file change">
<br>
<br>

- vi 에디터 사용하여 DB 정보 변경

<br>

            ls -alt
            ls
            vi wp-config.php

            (제일 밑으로 내려서 a를 눌러서 INSERT로 들어간다.)
            define('FS_METHOD','direct');

<br>

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/14-vi editor.png" alt="vi editor">
<br>
<br>

DB_NAME 부분에서 wordpress로 바꾸기 -> DB_USER 도 wordpress로 바꾸기 -> DB_PASSWORD'도 바꾸기 -> esc -> :wq

수정했던 데이터베이스 정보를 확인

<br>

            cat wp-config.php

<br>

권한 조정

<br>

            ls -alt
            sudo chown -R ec2-user.apache /var/www
            ls -alt

<br>

적용하기 위해 재시작

<br>

            sudo systemctl restart httpd && sudo systemctl restart php-fpm
            ps -ef | grep httpd
            ps -ef | grep php-fpm

<br>

- 도메인에 들어가서 확인하기

워드프레스 설치 화면에서 빈칸을 임의로 입력

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/15-wordpress domain.png" alt="wordpress domain">
<br>
<br>

워드프레스가 설치되어서 로그인이 가능하게 됨

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/16-worldpress login.png" alt="worldpress login">
<br>
<br>

웹사이트 서버가 동작하는 것을 확인

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/17-wordpress page.png" alt="wordpress page">
<br>
<br>

다시 도메인 주소로 들어가면 기본 테마를 확인할 수 있음

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/18-default theme.png" alt="default theme">
<br>
<br>

- 테마 변경하기

메뉴에서 테마디자인 -> 테마 -> 새로추가 버튼

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/19-theme change.png" alt="theme change">
<br>
<br>

- 원하는 테마 골라서 설치 버튼 -> 활성화 버튼

<img src="/assets/img/posts/2025-03-18-AWS) LAMP 서버를 이용하여 Wordpress 설치/20-worldpress blog.png" alt="worldpress blog">
<br>
<br>
