## 내가 볼려 작성하는 OSI 7 계층 요약

osi 7 layer은 국제표준 iso가 발표한 네트워크 모델입니다.

## 1. Physical Layer 물리계층
0과 1의 나열을 아놀로그 신호로 바꾸어 전선으로 흘려보냄
아날로그 신호가 들어오면 0과 1의 나열로 해석한다
phy칩

하드웨어적으로 구현되어있다.

## 2. Data Link Layer
같은 네트워크에 있는 여러 대의 컴퓨터들이 데이터를 주고받기위해서 필요한 모듈
Framing 작업을 한다
> Framing 작업이란?
> 0000 데이터 1111 로 묶는것
> 이래야 데이터의 시작과 끝일 알 수 있다.

랜카드에 구현되어있다. (하드웨어적 구현)

## 3. Network Layer
목적지 주소로 데이터를 전송하기위해 ip 주소를 이용해 라우팅을 하고 데이터를 넘겨주는 계층

운영체제의 커널에 구현되어있다

## 4. Transport Layer
해당 컴퓨터에 실행되는 포트에 맞는 프로세스에 데이터를 전달하는 계층

해당 부분도 운영체제의 커널에 구현되어 있다

## 5. Session Layer

## 6. Presentation Layer

## 7. Application Layer

## TCP/IP 소켓 프로그래밍
운영체제의 Transport Layer api를 활용하여 통신 가능한 프로그램을 만드는 프로그래밍
누구든 Application Layer프로토콜을 만들수 있다는것이 장점

