---
layout: post
title: "AWS SA 준비(네트워킹 및 콘텐츠 전송, 컴퓨팅, 관리 도구)"
author: Sungbin
categories: 
tags: [AWS]
image: assets/images/aws/Untitled.png
sitemap:
  changefreq: daily
  priority: 1.0
---
# AWS SA 준비(네트워킹 및 콘텐츠 전송, 컴퓨팅, 관리 도구)

네트워킹 및 콘텐츠 전송, 컴퓨팅, 관리 도구

### 네트워킹 및 콘텐츠 전송

- VPC – 클라우드에서 논리적으로 격리된 공간을 프로비저닝하고, 정의한 가상 네트워크에 AWS 리소스를 시작할 수 있다. 자체 IP 주소 범위 선택, 서브넷 생성, 라우팅 테이블 및 네트워크 게이트웨이 구성 등 가상 네트워킹 환경을 완벽하게 제어
- Virtual Private Cloud – AWS 클라우드 내 논리적으로 격리된 가상 네트워크
- 서브넷 – 격리된 리소스 그룹을 배치할 수 있는 VPC IP 주소 범위의 한 세그먼트
- 인터넷 게이트웨이 – 인터넷에 연결되는 VPC측 게이트웨이
- NAT 게이트웨이 – 프라이빗 서브넷에 있는 리소스가 인터넷에 액세스할 수 있게 해주는 고가용성 관리형 네트워크 주소 변환 서비스
- 가상 프라이빗 게이트웨이 – VPN에 연결되는 Amazon VPC측 게이트웨이
- 피어링 연결 – 피어링 연결을 사용하여 프라이빗 IP 주소를 통해 피어링 되는 두 VPC간 트래픽을 라우팅 할 수 있다.

![Untitled](https://user-images.githubusercontent.com/85655740/136346632-d29eac18-0b15-4ccd-b019-15cc15261315.png)

- VPC 엔드포인트 – 인터넷 게이트웨이, VPN, NAT 디바이스 또는 방화벽 프록시를 사용하지 않고 AWS에서 호스팅 되는 서비스에 VPC내에서부터 비공개로 연결할 수 있다.

(엔드포인트를 활용하면 비용을 들지 않고 라우팅 테이블에서 추가하여 비용이 들지 않을 거 같은 생각)

- 송신 전용 인터넷 게이트웨이 - VPC에서 인터넷으로 IPv6 트래픽에 대하여 송신 전용 액세스를 제공하는 상태 저장 게이트웨이
- CloudFront – 엣지 로이케이션의 글로벌 네트워크를 사용해 최종 사용자에게 파일을 전송, 비즈니스 및 웹 애플리케이션 개발자에게 짧은 지연 시간과 빠른 데이터 전송 속도를 사용하여 간편하고 비용 효율적으로 배포할 방법을 제공 (CDN 서비스이며 고속 콘텐츠 전송 네트워크)
- Route 53 – DNS, 도메인 이름 등록, 상태 확인 웹 서비스 (관리뿐만 아니라 최종 사용자를 인터넷 애플리케이션으로 라우팅 할 수 있는 매우 안정적이고 비용 효율적인 방법 제공, DNS간의 리디렉션도 가능하다.)
- API Gateway – 예를들어 DNS를 개발도중에 바꿔야 한다면 나는 각 DNS설정을 다 바꿔 줘야하는 번거러움이 있다. 하지만 API Gateway를 사용한다면 서버는 API Gateway를 거쳐 지나가게 되는데 API Gateway에 DNS값들을 설정해 놓으면 알아서 해당 DNS위치로 지정되기 때문에 번거러움을 해결할 수 있다.
- Direct Connect – 고객의 온프레미스 사이트를 AWS에 연결할 때 인터넷의 대안으로 사용할 수 있는 네트워크 서비스(이전에는 인터넷을 통해 전송해야 했던 데이터를 이제는 AWS와 개인 데이터 센터 또는 기업 네트워크 간의 프라이빗 네트워크 연결을 통해 전달할 수 있다.)

### 컴퓨팅

- EC2 - 컴퓨팅 말그대로 컴퓨터를 생성하는데 단 1분만에 인스턴스를 만들는것
- Auto Scaling - 스케일업, 스케일아웃 등 만약 인스턴스가 모자르면 인스턴스의 수를 자동으로 늘려 성능을 그대로 유지
- ECR - 리포지토리 및 푸시 하고 예를들어 ECR 저장소에서 도커 이미지를 가져오는 것, 전세계 누구와도 이미지를 공유할 수 있다
- ECS - 관리형 클러스터에서 애플리케이션을 손쉽게 실행, 오케스트레이션 서비스로 도커 컨테이너를 지원한다. (따로 설치하고 운영할 필요가 없음)
- Batch - 여러개의 작업을 사람의 손으로 수동적으로 작업하지 않고 도구를 통해 작업을 일괄 관리하는 것
- 스팟 인스턴스 - AWS 클라우드에서 미사용 EC2 용량을 활용할 수 있다.
- AWS Elastic Beanstalk - 애플리케이션을 신속하게 배포하고 관리할 수 있다. (오토 스케일링이 편하다.)
- Fargate – EC2와 같은 별도의 컴퓨팅 자원에 의존하지 않고 컨테이너를 독립적으로 실행할 수 있다. 완전 관리형 컨테이너 서비스 컨테이너 배포
- EKS - 쿠버네티스 설치 없이 EKS만 설치하면 관리형 쿠버네티스를 바로 사용 가능
- Lambda - 코드 실행, 트리거로 다른 서비스도 같이 연결할 수 있고 자동으로 코드를 실행 시킬수 있다.
- ELB - 서버 트래픽 과부하가 되지 않게 차례대로 트래픽을 서버 차례대로 보내준다. (마치 교통안전 같음)

### 관리 도구

- CloudWatch – AWS 클라우드 리소스와 AWS에서 실행되는 애플리케이션을 위한 모니터링 서비스
- CloudFormation – 템플릿 및 스택으로 작업한다. 템플릿 경우 (JSON, YAML) 형식 자동화

간단히 말하면 인프라의 변경을 반복할 때 CloudFormation을 이용해 자동적이고 지속적으로 전달할 수 있다. Beanstalk은 클라우드에서 손쉽게 애플리케이션을 배포하고 실행할 수 있는 환경을 제공하고, 개발자 도구와 통합되며 애플리케이션 수명 주기를 한곳에서 관리할 수 있는 환경을 제공하는 반면 CloudFormation은 광범위한 AWS 및 서드 파티 리소스를 편리하게 배포할 수 있는 메커니즘 또 CloudFormation은 AWS 리소스 유형 중 하나도 Beanstalk 애플리케이션 환경을 지원

- CloudTrail – 사용자 계정에서 이루어진 활동을 기록하고, 로그 파일을 사용자의 S3 버킷으로 전달하는 웹 서비스. 그렇다면 CloudWatch는 AWS서비스 및 자원 활동에 초점을 맞추고, 그 상태와 성능에 대해 보고 하는 반면 CloudTrail은 AWS 환경에서 수행된 모든 작업의 로그이다. 즉 CloudWatch는 AWS 클라우드 리소스와 AWS에서 실행되는 애플리케이션의 모니터링 서비스이고, CloudTrail은 AWS 계정, 컴플라이언스, 운영 감사, 리스크 검사 기능을 하는 서비스 AWS 인프라 작업 관련 계정 활동을 기록하고 지속적으로 모니터링 및 유지
- AWS Config – AWS 리소스 인벤토리, 구성 기록, 구성 변경 알림을 제공하여 보안 하는 서비스, 이러한 기능을 바탕으로 규정 준수 감사, 보안 분석, 리소스 변경 추적, 문제 해결을 수행
- AWS OpsWorks – Chef를 사용하여 모든 형태 및 규모의 애플리케이션을 구성하고 운영하도록 도와주는 구성 관리 서비스
- AWS Service Catalog – IT 관리자가 승인된 제품의 카탈로그를 생성 및 관리하고 최종 사용자에 배포할 수 있다.

![Untitled 1](https://user-images.githubusercontent.com/85655740/136346758-a0876099-637e-4f8a-bead-947a034f41bf.png)
5261315.png

이렇게 예제로 LAMP에 대한 블로그처럼 이렇게 관리 배포함으로써 부서의 내부 사용자에게 일관성 있는 정보를 제공

- EC2 Systems Manager – AWS 서비스의 운영 데이터를 중앙집중화 하고 AWS 리소스 전체에서 작업을 자동화할 수 있다. 말 그대로 한곳에서 일상적인 작업을 수행할 수 있게 하는 것 즉 인프라를 보고 제어하기 위해 사용할 수 있는 AWS 서비스
- AWS Trusted Advisor – 지금까지 수많은 AWS 고객에게 제공된 AWS의 축적된 서비스 경험에서 얻은 유용한 모범 사례를 바탕으로 만들어진 애플리케이션 Advisor는 사용자의 AWS 환경을 조사하고 비용 절감, 시스템 성능 향상 또는 보안 결함 제거를 위한 권장 사항을 제시