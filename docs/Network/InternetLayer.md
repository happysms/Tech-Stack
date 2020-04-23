# 라우팅과 인터넷 계층
*written by sohyeon, hyemin 💡*

<br>

### 글 목차
### [1. 인터넷 계층의 역할](#1-인터넷-계층의-역할-1)
### [2. IPv4와 IPv6](#2-ipv4와-ipv6-1)
### [3. IP 어드레스의 활용](#3-ip-어드레스의-활용-1)
### [4. 라우터와 라우팅 프로토콜](#4-라우터와-라우팅-프로토콜-1)
### [5. ICMP](#5-icmp-1)
### [6. DNS](#6-dns-1)
### [7. DHCP](#7-dhcp-1)

- - -

## 1. 인터넷 계층의 역할

<img src="./resources/internetLayer.jpg" width="400px">

`인터넷 계층`은 네트워크 인터페이스 계층과 협력하여 다른 컴퓨터에게 데이터를 전달하는 역할을 한다.  

하드웨어에 의존해야 하는 부분은 네트워크 인터페이스 계층이 담당하고  
인터넷 계층은 `IP 어드레스`라고 하는 식별자 정보를 실마리로 데이터를 전달할 수 있는 체계를 제공한다.  

### 1) 라우터와 라우팅

* 라우터 : 데이터를 목적지까지 전달할 수 있도록 도와주는 네트워크 장비
           네트워크와 네트워크를 연결하는 역할을 함

* 라우팅 : 데이터가 최종 목적지에 도달할 수 있도록 라우터가 경로를 찾아가는과정

## 2. IPv4와 IPv6

둘 다 인터넷 계층에서 사용되는 중요한 프로토콜로  
IP 어드레스를 결정할 때 사용하는 비트의 길이가 서로 다르다.

### 1) IPv4

현재까지 컴퓨터 어드레스 지정에 가장 많이 사용되는 인터넷 계층의 프로토콜이다.  
`32비트`의 IP어드레스가 사용된다.

전체 32비트를 8비트씩 4개 단위로 끊은 후 10진수로 변환해 표기한다.  

    ex) 192.168.100.1

### ● IPv4 패킷

<img src="./resources/IPv4packet.jpg" width="500px">

- 서비스 타입 : 패킷의 우선 순위를 결정
- 프로토콜 : 트랜스포트 계층의 어느 프로토콜에 전달할지를 판단하는 번호 부분
- 생존 기간 : 생존 기간 정보를 설정 가능하고, 
             만약 생존 기간을 초과한 패킷이 네트워크상에서 발견되면 그 패킷을 소멸하도록 규정하고 있다.  

### ● MTU (Maximum Trasmission Unit)

한번에 전송할 수 있는 데이터 크기를 의미한다.  

라우터가 데이터를 송신하기 전 통신 경로 전체의 MTU를 살펴본 후  
MTU보다 작은 크기의 패킷을 만들도록 설정해 데이터 유실을 방지하기도 한다.  

패킷을 분할, 복원하는 작업을 위해 헤더에 다양한 필드가 존재한다.

- 식별자 : 같은 데이터인지 식별
- 분할 플래그 : 분할 허가 플래그와 이후 남은 분할 부분이 더 있는지 표시
- 프래그먼트 옵셋 : 원래 데이터에서의 위치 값을 표현

식별자나 IP 어드레스 정보 들을 보고 분할된 조각을 모아서 복원하게 된다.  

### 2) IPv6

인터넷의 급격한 성장으로 인해 IPv4의 32비트 어드레스가 머지않아 고갈될 상황에 이르렀다.  
이를 방지하기 위해 128비트 어드레스로 만든 IPv6의 보급이 가속화 되고 있다.  

    IPv4의 생명을 연장할 수 있는 기술들도 나오고 있어 당분간은 IPv4와 IPv6를 병행해서 사용하게 될 것으로 보인다.  

### ● IPv6 패킷

<img src="./resources/IPv4packet.jpg" width="500px">

- 트래픽 클래스 : 패킷의 우선순위를 결정
- 페이로드의 길이 : 데이터 부분의 길이
- 홉 리미트 : IPv4의 생존 기간과 같은 역할
- 확장 헤더 : 옵션 설정

    - IPv6는 라우터에서 데이터를 분할하지 않는 방식으로 사양이 만들어져 있어서
      분할 관련 필드는 옵션으로 되어 있다.

### 3) 터널링과 듀얼 스택

IPv4와 IPv6는 어드레스나 패킷 어느 것으로도 서로 호환이 되지 않는다.  
두 가지를 병행할 수 있도록 `터널링`과 `듀얼 스택`이라는 기법을 사용할 수 있다.

- 터널링 : IPv4 네트워크를 IPv6 패킷이 지나가야 한다면,
           IPv4 패킷 안에 IPv6 패킷을 넣어서 보내는 방법이다.  

- 듀얼 스택 : 하나의 장비에 두 종류의 어드레스를 모두 할당한 후 둘 다 사용 가능하도록 한다.  

## 3. IP 어드레스의 활용

### 1) 네트워크 부와 호스트 부

<img src="./resources/ipadress.jpg" width="300px">

IP 어드레스는 주소 할당 방법에 따라 `네트워크 부`와 `호스트 부`로 나뉜다.  
(호스트는 네트워크에 연결된 컴퓨터나 네트워크 장비를 말한다.)  

<img src="./resources/ipadress2.jpg" width="600px">

라우터는 송신지 IP 어드레스의 네트워크 부의 정보를 보고  
데이터를 송신할 목적지가 같은 네트워크 안에 있는지 다른 네트워크에 있는지 판단한다.  

    <네트워크의 여러 의미>

    - 넓은 의미
    : 여러 컴퓨터가 연결되어 데이터를 주고받을 수 있는 것

    - 인터넷 계층에서의 의미
    : IP 어드레스의 네트워크 부가 같은 컴퓨터들의 그룹

### 2) 어드레스 클래스

하나의 IP 어드레스 안에서 어디까지가 네트워크 부이고 어디까지가 호스트 부인지  
미리 고정하여 결정해 둔 것
네트워크 부는 고정 크기를 갖는다.  

<img src="/images/Network/resources/addressClass.jpg" width="600px">

클래스 D는 멀티캐스트로 사용되는 특수한 어드레스다.  

### ● 제약

클래스 A의 어드레스는 한 개의 네트워크당 약 1677만 대의 호스트의 어드레스를 할당할 수 있지만  
실제로는 그렇게 많은 호스트를 하나의 네트워크에 연결하는 경우는 거의 없다.  
따라서 수많은 어드레스가 사용되지 않고 **낭비**된다. 

### 3) 서브넷 마스크

어드레스 클래스를 사용한 네트워크를 좀더 세분화하기 위해 사용하는 방법  

어드레스 클래스와 달리 네트워크 부의 길이를 비트 단위로 유연하게 늘려서 사용 가능하다.  
서브넷 마스크는 IP 어드레스에 추가되는 정보이므로 32비트 길이만큼의 정보가 더 필요하다.  

<img src="./resources/subnetmask.jpg" width="600px">

- IP 어드레스는 네트워크상에서 호스트를 식별하기 위해 사용되는데,  
  전체 32비트 중 네트워크 부를 제외한 호스트 부 부분만 자유롭게 할당하여 사용할 수 있다.  

- 호스트 부는 8비트이기 때문에 한 네트워크에서 254대만큼의 어드레스를 할당할 수 있다.
  (모든 비트가 1이거나 0인 경우는 제외)  

- 서브넷 마스크를 활용하면 네트워크를 더 세분화하여 `서브넷`을 만들 수 있다.
  각 서브 네트워크 안에서 호스트 62대까지 할당 가능하다.

## 4. 라우터와 라우팅 프로토콜

- 라우터 : 네트워크 간의 패킷을 전달하는 것, 연결한 네트워크 개수만큼의 IP 어드레스를 여러개 갖는다.  

- 라우팅 : 인터넷에서 데이터가 목적지까지 전달되기 위해  
           라우터가 자신과 연결된 다른 라우터를 찾아나가면서 최종 목적지까지 연결되는 경로는 찾는 과정

- 라우팅 테이블 : 목적지 호스트가 속한 네트워크 정보와 그 네트워크로 도달하기 위해 경유해야하는 
                  라우터의 정보가 들어있다. 라우팅에 활용된다.

- 라우팅 프로토콜 : 네트워크상의 각 라우터가 누구랑 연결되어 있는지 정보를 교환할 때 사용되는 프로토콜  
                   (BGP, OSPF, RIP 등 ... )

- 자율 시스템 : 인터넷 서비스 제공자가 사용하는 규모가 큰 네트워크에서 몇 개의 네트워크를 묶어 관리하는 단위 

### 1) 정적 라우팅

네트워크 관리자가 직접 수작업으로 라우팅 테이블을 설정하는 방식  
네트워크 간의 접속 형태가 복잡하면 정적 라우팅으로 설정하는 것이 사실상 불가능하기 때문에  
대부분은 동적 라우팅을 사용한다.

### 2) 동적 라우팅

라우팅 프로토콜을 사용하여 자동적으로 경로 정보를 수집한 후 라우팅 테이블을 설정하는 방식  

경로를 찾는 방식에 따라 `거리 벡터형`과 `링크 상태형`의 두 가지가 많이 사용된다.  

### ● 거리 벡터형

RIP(Routing Information Protocol) 프로토콜이 사용하는 방식  
목적지까지의 거리를 살펴보고 짧은 경로를 선택하는 방식  
이때 거리는 경유하는 라우터의 수를 의미하는 홉의 수로 센다.  

비교적 구성이 간단한 LAN 네트워크에 적합하다.  

### ● 링크 상태형

OSPF(Open Shortest Path First) 프로토콜이 사용하는 방식  
네트워크의 통신 상태 정보를 맵으로 관리하면서 상태가 가장 좋은 경로를 선택하는 방식  
복잡하고 변화가 잦은 네트워크 구성에 적합

## 5. ICMP

`ICMP 프로토콜`은 데이터 전송 중에 문제가 생길 경우 장애 상황을 통보하기 위해 사용된다.  

### ● ICMP 메세지

|타입|의미|
|:---:|:---|
|0|에코 응답, 수신 측 장비가 존재한다고 확인해 줄 때 사용|
|3|데이터가 도착하지 않음|
|4|회선 상태가 혼잡|
|5|경로 상태가 최적이 아님|
|8|에코 요청, 수신 측 장비가 존재하는지 확인할 때 사용|
|9|라우터가 보내는 응답, <br> 네트워크에 새로 연결된 장비에게 사용 가능한 라우터 정보를 알려주기 위해 사용|
|10|장비가 보내는 요청, 네트워크에 새로 연결되었을 때 라우터를 찾기 위해 사용|
|11|생존 기간이 지난 패킷을 삭제했음을 알려줌|

## 6. DNS

서로 다른 컴퓨터를 구분하는 식별자로는 IP 어드레스와 호스트명이 있는데,  
이들 정보를 관리하기 위해 `DNS`와 `도메인명`이라는 것이 만들어 졌다.  

도메인의 표현 방식이 호스트명을 계층적인 형태로 표현하고 있으나,  
실제로는 단순히 분류 체계의 성격으로 표현하고 있을 뿐  
실제 네트워크 형태가 계층적이라는 의미는 아님

    URL
    http://www.sample.co.kr/

    -> 호스트명(www) + 도메인명(sample.co.kr)

    -> 118.103.124.63

- 도메인명에 대응하는 IP 어드레스 정보가 필요하면 DNS 서버에 질의하면 된다.
    
    1. 도메인명으로 IP 어드레스를 질의
    2. IP 어드레스 정보를 회신
    3. IP 어드레스로 접속

### ● 도메인 계층 구조

도메인명은 계층 구조 형태를 마침표로 구분하여 표현한다.  

<img src="./resources/domain.jpg" width="700px">

## 7. DHCP

`DHCP`는 네트워크에 속한 호스트들에게 IP 어드레스와 서브넷 마스크 등의 정보를 자동으로 설정한다.  

TCP/IP가 제대로 동작하기 위해서는 네트워크에 속한 각 호스트의 IP 어드레스가 중복되지 않아야 한다.  
네트워크의 호스트들에 IP 어드레스를 할당하고 중복되지 않게 자동으로 관리해준다.  

<br> 

## Reference & Additional Resources
  
> TCP/IP 쉽게, 더 쉽게
> 한국인터넷정보센터 (어드레스 클래스 이미지)
> https://ddooooki.tistory.com/31 (도메인 계층 구조 이미지)