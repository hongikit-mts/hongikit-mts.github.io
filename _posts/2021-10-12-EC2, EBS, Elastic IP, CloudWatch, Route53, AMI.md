---
layout: post
title: "AWS SA 준비(EC2, EBS, Elastic IP, CloudWatch, Route53, AMI)"
author: Sungbin
categories: 
tags: [AWS]
image: assets/images/aws4/Untitled.png
sitemap:
  changefreq: daily
  priority: 1.0
---
# AWS EC2, EBS, Elastic IP, CloudWatch, Route53, AMI

개념 정리 

### EC2

- EC2는 AWS에서 가장 기본적이면서 널리 쓰이는 인프라이다. EC2는 인터넷에 연결된 가상서버를 제공한다.
- EC2를 사용해야 하는 이유는 효율성과 비용 절감에 있다. EC2는 클릭 몇 번으로 서버를 생성할 수 있기 때문에 실제 서버를 구축하는 것보다 훨씬 간편하고 효율적이다. 또한, 사용한 만큼만 요금을 지불하면 되므로 비용도 절감할 수 있다.
- 
- EC2 인스턴스 세부 설정 화면이 나온다. 각 옵션에 대해 자세히 알아보자.

![Untitled](https://user-images.githubusercontent.com/85655740/136878614-c868e0e0-dc6c-405d-bcda-f23ffe8eadc4.png)

인스턴스 수 – 생성할 인스턴스 개수이다.

구매옵션 – 스팟 인스턴스로 구매 옵션이다.

네트워크 – VPC 네트워크를 선택하는 옵션이다.

서브넷 – 가용영역을 선택하는 옵션이다.

퍼블릭 IP – 공인 IP를 할당하는 옵션이다.

IAM 역할 – IAM 역할 설정

종료 방식 – EC2 인스턴스 안에 설치된 운영체제를 종료했을 때 옵션

종료 방지 기능 활성화 – 실수로 삭제하는 것을 방지하는 옵션

모니터링 – CloudWatch 세부 모니터링 사용 옵션

테넌시 – 가상 서버 실행 방식을 설정하는 옵션 (공유 인스턴스와 전용 인스턴스를 선택할 수 있다.)

고급 세부 정보 – 사용자 데이터에는 인스턴스를 시작할 때 사용자 데이터를 자동화된 일반적인 구성 작업을 수행하는데 사용할 수 있는 인스턴스에 전달 할 수 있으며 인스턴스가 시작된 후 스크립트를 실행할 수도 있다.

```jsx
Ex) !/bin/hash

yum -y install httpd

systemctl enable httpd

systemctl start httpd

echo <html><h1>Hello Form Your Web Server</h1></html>

/var/www/hrml/index.html
```

를 입력하면 인스턴스 실행시키면 httpd 자동으로 깔리고 저 문구의 웹을 실행시킨다.

### EBS

- EBS는 EC2 인스턴스에 장착하여 사용할 수 있는 가상 저장 장치이다. EBS는 EC2 인스턴스에서 제공하는 기본 용량보다 더 사용해야 할 때, 운영체제를 중단시키지 않고 용량을 자유롭게 늘리고 싶을 때, 영구적인 데이터 보관이 필요할 때, RAID 등의 고급 기능이 필요할 때 사용
- 볼륨 포맷 CLI (mkfs -t ext4 /dev/sdf)
- 볼륨 마운트 CLI (mount /dev/sdf /mnt)
- 볼륨 제거 CLI (umount /mnt)

### Security Group

- EC2 인스턴스에 적용할 수 있는 방화벽 설정 EX) 리눅스 서버의 ssh 접속 포트인 22번만 여는 것은 기본이고, 여기에 접속 가능한 IP 대역까지 설정한다.

![Untitled 1](https://user-images.githubusercontent.com/85655740/136878656-d8abbae6-9e52-4b9c-9ddb-9baa3debe003.png)

### Elastic IP

- Elastic IP는 고정된 IP를 제공한다. EC2 인스턴스를 생성하면 기본적으로 공인 IP가 부여된다. 하지만 이 IP 주소는 EC2 인스턴스가 실행되고 있는 동안에만 윺효하며 EC2 인스턴스가 중단되면 IP 주소는 반납된다. 따라서 유동 IP이다.

그런데 DNS 서버를 통해 도메인에 IP 주소를 연결해놓았는데 IP 주소가 바뀌면 매우 곤란 해집니다. 그래서 Elastic IP를 사용하여 절대 바뀌지 않게 한다.

그러나, 인스턴스를 쓰는 동안에는 비용이 안나가지만 인스턴스를 중지시켜 놀 때는 비용 발생이 된다.

### AMI

- EC2 인스턴스를 생성하기 위한 기본 파일이다. AWS에서는 빈 EC2 인스턴스에 직접 OS를 설치할 수는 없다. 그렇기 때문에 미리 OS가 설치된 AMI를 이용하여 EC2 인스턴스를 생성하게 된다. 이 AMI는 단순히 OS만 설치되는 것이 아니라 각종 서버 애플리케이션, 데이터베이스, 방화벽 등의 네트워크 솔루션, 각종 비즈니스 솔루션 등도 함께 설치될 수 있다

.

![Untitled 2](https://user-images.githubusercontent.com/85655740/136878721-b92756b3-5e1c-4e54-a20d-5b09451175bf.png)

- 마켓플레이스는 유저들이 올리는 이미지 파일

### CloudWatch

- CloudWatch에서는 각 AWS 리소스의 특징에 따라 다양한 값들을 모니터링 할 수 있다.

### Route 53

- Route 53은 전반적인 도메인을 관리할 수 있다. Ec2, ELB, S3, CloudFront와 연동 가능한 서비스이며 대규모 글로벌 서비스를 할 때 유용하다.
- Weighted Round Robin은 서버 IP 주소 또는, 도메인(ELB) 마다 가중치를 부여하여 트래픽을 조절하는 기능입니다. 그림 17-2처럼 가중치에 따라 한쪽에는 80%의 트래픽이 가고, 다른 한쪽은 20%의 트래픽이 갑니다(가중치에 따라 클라이언트에 IP 주소를 알려주는 비율이 달라집니다).

![Untitled 3](https://user-images.githubusercontent.com/85655740/136878812-36c14f08-b455-41a5-be61-fd2006c98387.png)