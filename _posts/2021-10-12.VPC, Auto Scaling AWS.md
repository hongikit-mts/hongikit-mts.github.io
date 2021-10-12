---
layout: post
title: "AWS SA 준비(VPC, Auto Scaling)"
author: Sungbin
categories: 
tags: [AWS]
image: assets/images/aws4/Untitled 5.png
sitemap:
  changefreq: daily
  priority: 1.0
---

# AWS VPC, Auto Scaling

개념 정리 및 실습 진행

### VPC

![Untitled](AWS%20VPC,%20Auto%20Scaling%20b8b12c9f4cfe4bd1b1b4170c0d8bcaf9/Untitled.png)

![Untitled](AWS%20VPC,%20Auto%20Scaling%20b8b12c9f4cfe4bd1b1b4170c0d8bcaf9/Untitled%201.png)

![Untitled](AWS%20VPC,%20Auto%20Scaling%20b8b12c9f4cfe4bd1b1b4170c0d8bcaf9/Untitled%202.png)

- VPC생성에 보면 CIDR은 CIDR 표기법으로 된 IP 대역이다.
- CIDR은 192.168.0.0/16을 입력하였다. 즉 이 말은 192.168.0.0/16의 서브넷 마스크는 255.255.0.0 이며 이진수로 바꾸었을 때 1이 16개이다. 그래서 192.168.0.0~192.168.255.255을 뜻한다. (VPC와 서브넷은CIDR 표기법으로 IP대역을 설정한다.)

![Untitled](AWS%20VPC,%20Auto%20Scaling%20b8b12c9f4cfe4bd1b1b4170c0d8bcaf9/Untitled%203.png)

- 서브넷 생성은 아까 만든 VPC선택 해주고 나머지도 VPC와 비슷하다.
- 서브넷에 대한 개념도 확실히 알아 두자 서브넷이란 하나의 IP 네트워크 주소를 지역적으로 나누어 이 하나의 네트워크 IP 주소가 실제로 여러 개의 서로 연결된 지역 네트워크로 사용할 수 있도록 하는 방법이다.

![Untitled](AWS%20VPC,%20Auto%20Scaling%20b8b12c9f4cfe4bd1b1b4170c0d8bcaf9/Untitled%204.png)

- 인터넷 게이트웨이 생성도 어려울게 없었다. 생성하고 VPC와 연결할 수 있다.
- 그렇다, 인터넷 게이트웨이도 말 그대로 외부 인터넷에 접속할 수 있게 하기위해서 사용한다. (VPC에 속한 서브넷에서 외부 인터넷에 접속하려면 인터넷 게이트웨이가 필요)

### Auto Scaling

- 오토스케일링은 트래픽이 늘어나면 자동으로 EC2 인스턴스를 생성하여 서비스를 확장하는 기능이다. 오토스케일링은 실제로 서비스를 제공하는 AWS 리소스가 아니라서 사용 요금이 없다. (트래픽이 폭주할 때도 손쉽게 대처 가능하며 사용자가 많지 않은 새벽시간에는 EC2 인스턴스의 개수를 줄여 비용을 절감시킨다.)
- 보통 오토스케일링은 ELB와 함께 사용한다. 오토스켈링은 생성한 EC2 인스턴스를 ELB 로드 밸런서에 연결하고, ELB로드 밸런서는 새로 생성된 EC2 인스턴스에 트래픽을 분산한다.

[올바른 예]

![Untitled](AWS%20VPC,%20Auto%20Scaling%20b8b12c9f4cfe4bd1b1b4170c0d8bcaf9/Untitled%205.png)

[실습도 어렵지 않았다. 기본적인 핵심 서비스는 실습은 쉬우나 많이 쓰이는 서비스들 이기 때문에 더 심화 적인 개념을 알아야한다고 느꼈다.]