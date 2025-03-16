---
title: "AWS) 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정"
date: 2025-03-16 23:40:00 +0800
categories: [Cloud, AWS]
tags: [Cloud, AWS]
image:
  path: /assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/1-biling.png
---

## Objective

<br>
실제 사용이 아니라 학습을 했으면 AWS 비용결제를 막는 것이 필요합니다.

따라서 aws 비용 결제를 막기 위해 청구서 확인 및 사용항목을 삭제했습니다.

<hr>
<br>

## Solution

<br>
- aws console 접속 -> 검색창에 Billing -> 청구될 요금을 확인

<img src="/assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/1-biling.png" alt="biling">
<br>
<br>

- 사용하는 항목인 ec2로 검색 -> 인스턴스 메뉴 -> 해당 인스턴스 체크하고 인스턴스 종료 버튼 -> 인스턴스 상태가 '종료 중'으로 변경되고 기다리면 목록에서 삭제됨

(목록에서 삭제까지 시간이 꽤 걸렸습니다.)

<img src="/assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/2-instance status.png" alt="instance status">
<br>
<br>

- Elastic Block Store 메뉴 아래의 볼륨 메뉴 -> 해당 볼륨 체크하고 볼륨 분리 버튼

<img src="/assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/3-volume.png" alt="volume">
<br>
<br>

- '분리'를 쓰고 분리 버튼

<img src="/assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/4-volume separation.png" alt="volume separation">
<br>
<br>

- 체크하고 볼륨 삭제 버튼

<img src="/assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/5-volume delete.png" alt="volume delete">
<br>
<br>

- CloudWatch 에서 알람 설정

검색창에 CLoudWatch -> 경보-모든경보 메뉴 -> 지역을 미국 버지니아 북부로 변경(다른 지역에 대한 관리도 가능) -> 경보 생성 버튼 눌러서 입력해서 설정

<img src="/assets/img/posts/2025-03-16_AWS) aws 비용 결제를 막기 위해 항목 삭제 및 CloudWatch에서 비용 알람 설정/6-CloudWatch alarm.png" alt="CloudWatch alarm">
