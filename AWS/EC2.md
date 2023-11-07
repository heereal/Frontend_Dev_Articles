# AWS EC2
> [AWS EC2 개념 정리](https://velog.io/@server30sopt/AWS-EC2-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)

<br/>

## EC2 ( Elastic Compute Cloud) 란?
-  EC2는 AWS에서 **비용, 성능, 용량 면에서 탄력적인 클라우드 컴퓨터를 제공하는 서비스**라고 할 수 있다.
-  클라우드 컴퓨팅은 인터넷(클라우드)을 통해 **서버, 스토리지, 데이터베이스 등의 컴퓨팅 서비스**를 제공받는 것으로 AWS에서 원격으로 제어할 수 있는 가상의 컴퓨터를 한 대 빌리는 것이라고 생각할 수 있다.
-  EC2는 실제 서버를 구축하는 것보다 훨씬 간편하고 효율적이며 사용한 만큼만 요금을 지불하면 되므로 비용이 절감된다는 장점이 있다.

<br/>

## EC2 인스턴스란?
<img width="823" alt="image (7)" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/0a8fad48-f56f-47d5-a553-d947034e897f">

- AWS EC2 인스턴스를 생성한다는 것은 **AMI를 토대로 운영체제, CPU, RAM 혹은 런타임 등이 구성된 컴퓨터를 빌리는 것**을 의미한다.
- AWS는 범용 및 컴퓨팅, 메모리, 저장 최적화 성능 목적에 따라 타입별로 인스턴스에 이름을 부여해 구분하고 있다.

<br/>

## 인스턴스 구매 옵션
<img width="313" alt="image (10)" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/5d5f5b04-f49d-420c-9dee-1a52bf3a2b20">

- **온 디맨드 인스턴스 (On Demand Instance)** : 필요할 때 바로 생성해서 사용할 수 있는 방식. 과금은 1시간 단위로 이루어지며 1분을 사용했더라도 1시간으로 책정된다. 3가지 방식 중 요금이 가장 비싸다.
  - 공유 인스턴스 (Shared tenancy) : 하나의 물리적인 서버에 여러 개의 EC2인스턴스가 실행 → 다른 인스턴스가 서버 자원을 많이 소모한다면 현재 인스턴스의 성능에 영향이 있을 수 있다.
  - 전용 인스턴스(Dedicated tenacy) : 하나의 물리적인 서버에 하나의 EC2인스턴스가 실행 → 서버 내 다른 인스턴스가 없으므로 영향을 받지 않지만 공유 인스턴스 방식보다 비싸다.
- **예약 인스턴스 (Reserved Instacne)** : 일정한 예약금을 선불로 내면 인스턴스를 1년 또는 3년동안 예약할 수 있으며 시간당 요금이 대폭 할인된다. 온 디맨드 인스턴스와 마찬가지로 공유 인스턴스, 전용인스턴스로 나뉜다.
- **스팟 인스턴스 (Spot Instance)** : 경매 방식의 인스턴스. 인스턴스의 스펙을 설정하고 원하는 가격을 입력하여 입찰하면 높게 입찰한 사람한테 인스턴스가 할당된다.

<br/>

## 인스턴스 수명주기 (Instance Life Cycle)
<img width="825" alt="image (11)" src="https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/530fc61a-8293-44e6-a803-587cebf73d5d">

- EC2의 수명 주기는 **AMI로부터 실행이 되고나서 종료될 때까지 EC2가 거치는 과정**을 의미한다.
1. **pending state**: 제일 처음 AMI가 실행되었을 때 EC2를 가동하기 위해서 가상머신, ENI, EBS 등이 준비되는 과정이다.
2. **running state**: 실제로 EC2를 사용할수 있는 상태를 말한다. running 상태에서 할수 있는 것은 3가지가 있다.
   - 중지: 인스턴스를 잠깐 멈춰두는 것으로 중지 중에는 인스턴트 요금이 청구되지 않는다. (단 EBS 요금, Elastic IP 등의 다른 구성 요소는 청구될 수 있다.) 중지 후 재시작 할때 퍼블릭 IP가 변경된다.
   - 재부팅: 인스턴스를 다시 시작하는 것으로 재부팅하더라도 퍼블릭 IP가 변경되지 않는다.
   - 최대 절전모드: 메모리 내용을 보존해서 재시작 시 중단지점에서 시작할 수 있는 모드다.
3. **shutting-down state**: 설정에 따라 EBS도 같이 종료할 수도 있고 EBS는 남기고 인스턴스만 종료할 수 있다.
4. **terminated state**: 완전히 종료, 인스턴스가 영구적으로 삭제된다.

<br/>

## AMI (Amazon Machine Images)란?
- **EC2 인스턴스를 시작하는 데 필요한 정보가 들어있는 이미지** 즉, EC2의 복사본이라고 보면 된다.
- AMI 선택이라는 것은 Linux, Windows 등의 **운영체제를 선택**한다고 보면 된다.
- 인스턴스는 AMI의 사본으로 하나의 AMI로 여러 인스턴스 실행도 가능하다.

<br/>

## EBS (Elastic Block Store)란?
- EBS는 **EC2 인스턴스에 장착하여 사용할 수 있는 가상 저장 장치**다.
- 인스턴스가 연산에 관한 (CPU,메모리 등) 처리를 한다면, **데이터를 저장하는 역할**은 바로 EBS가 한다고 보면 된다.
- EBS는 EC2에 설치된 OS에서 그냥 일반적인 하드디스크나 SSD처럼 인식된다.

<br/>

## EBS 볼륨 생성 값
![image (12)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/c7e102e4-6e7f-455e-8e01-6b6378c289bb)

- **볼륨 (volume)** : EBS의 가장 기본적인 형태로 OS에서 바로 사용 가능한 형태이다.
- **이미지 (Image)** : AMI를 줄여 부르는 말. OS가 설치된 형태이며 이 AMI로 EC2 인스턴스를 생성한다.
- **스냅샷(Snapshot)** : EBS 볼륨의 전체 내용 중 특정 시점을 그대로 복사해 저장한 파일을 뜻한다. 따라서 **EBS 볼륨의 백업 파일** 성격을 가지고 있다. 
- **IOPS (Input/Output Operation Per Second)** : 저장 장치의 성능 측정 단위. AWS에서는 추가 비용을 지불하고 높은 성능(IOPS)의 EBS를 생성할 수 있다.
