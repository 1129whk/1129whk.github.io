---
title: "AWS) 탄력적IP(EIP) 생성 및 EC2 연결"
date: 2025-03-15 23:40:00 +0800
categories: [Cloud, AWS]
tags: [Cloud, AWS]
image:
  path: /assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/7-domain list.png
---

## Objective

<br>
생성한 EC2에 EIP(Elastic IP) 및 DNS와 연동하기

가비아 사이트에서 도메인 구매

<hr>
<br>

## Solution

<br>
- 검색창에 EC2 검색 -> 탄력적 IP 좌측 메뉴 선택 -> 탄력적 IP 주소 할당

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/1-elastic IP adress.png" alt="elastic IP adress">
<br>
<br>

- 다음과 같이 선택. 기본 선택 그대로 두었습니다. -> 할당

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/2-default.png" alt="default">
<br>
<br>

- 고정 IP가 할당되었습니다. -> 작업 -> 탄력적 IP 주소 연결

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/3-list.png" alt="list">
<br>
<br>

- 빈 칸을 클릭하면 자동으로 인스턴스와 프라이빗 IP 주소가 나왔습니다. 그대로 설정하였습니다. -> 연결

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/4-instance.png" alt="instance">
<br>
<br>

- 목록에서 '연결된 인스턴스 ID' 클릭 -> 다음 화면에서, 인스턴스 ID 클릭

다음과 화면이 조회됩니다.

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/5-instance ID.png" alt="instance ID">
<br>
<br>

- 가비아 사이트에서 도메인 구매

<https://www.gabia.com/>

<br>
<br>

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/6-domain.png" alt="domain">
<br>
<br>

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/7-domain list.png" alt="domain list">
<br>
<br>

- 관리 버튼으로 들어갑니다.

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/8-manage.png" alt="manage">
<br>
<br>

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/9-DNS host.png" alt="DNS host">
<br>
<br>

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/10-DNS manage tool.png" alt="DNS manage tool">
<br>
<br>

- DNS 설정 선택

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/11-DNS setting.png" alt="DNS setting">
<br>
<br>

- 탄력적 IP 주소와 만든 사이트의 주소를 연결하기 : 탄력적 IP 주소를 복사 -> A타입 선택 -> 호스트와 복사한 탄력적 IP 주소를 붙여넣기 -> TTL 선택 -> 확인 버튼 -> 저장 버튼

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/12-TTL.png" alt="TTL">
<br>
<br>

- 아래와 같이 확인

<br>

      ping (호스트).(사이트 주소) -t

<br>

<img src="/assets/img/posts/2025-03-15-AWS) 탄력적IP(EIP) 생성 및 EC2 연결/12-TTL.png" alt="TTL">
<br>
<br>

탄력적 IP 주소는 사이트의 서버로 쓰게될 EC2 가상머신의 IP주소가 됩니다.
<br>

<hr>

## Reference

<br>

<https://www.youtube.com/watch?v=h-yOoHbH_Dw >
