---
layout:       post
title:        "Chapter 2. Story 5. IP와 이더넷의 패킷 송/수신 동작"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- network
- ComputerScience
- 성공과 실패를 결정하는 1%의 네트워크 원리
- 도서
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>패킷의 기본</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; TCP가 속한 레이어는 접속, 송/수신, 연결 끊기에서 통신 상대와 대화 시 필요한 데이터를 IP 담당 레이어에 의뢰해 패킷의 모습으로 만들어 상대에게 도착하게 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 패킷은 크게 헤더와 데이터 두 부분으로 나뉜다. 헤더는 패킷 맨 앞에 있는 제어정보이다. 데이터는 패킷으로 운반하는 패킷의 내용이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="440" data-origin-height="152"><span data-url="https://k.kakaocdn.net/dn/dTadAW/btrQ2dWgVi0/hdUr0IeDnz12ElqeLDgLT0/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FdTadAW%2FbtrQ2dWgVi0%2FhdUr0IeDnz12ElqeLDgLT0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="440" data-origin-height="152"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; TCP/IP 패킷은 다음과 같은 모양을 가진다</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="858" data-origin-height="440"><span data-url="https://k.kakaocdn.net/dn/I841F/btrQ5kAmsmy/Bheo6zudxy00nZC6T8F6L0/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FI841F%2FbtrQ5kAmsmy%2FBheo6zudxy00nZC6T8F6L0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="560" height="287" data-origin-width="858" data-origin-height="440"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같은 패킷이 송신 기기에서 만들어지면, 다음과 같은 과정을 통해 송수신이 이루어진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 패킷을 가장 가까운 중계장치에 송신한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 중계장치가 패킷 헤더를 조사해 패킷의 목적지를 식별한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 중계장치는 수신처 방향에 대한 정보가 있는 표에 있는 정보와 헤더의 목적지 정보를 결합해 수신처가 표의 어느 방향에 있는지를 판단한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 방향이 판단됐으면 그와 관련된 케이블로 패킷 신호를 보낸다. 그러면 패킷은 다음 중계장치에 도착한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다음 중계장치에 도착해서도 2~4 과정을 되풀이한다. 또 한, 송신처에서 수신처로 패킷을 송신하면, 받았다는 것을 증명하기 위해 다른 패킷을 송신 측으로 송신한다. 즉, 시점에 따라 송신 측과 수신 측이 바뀐다. 이 때문에 송신처와 수신처를 명확히 구분하지 않는 것이 편리할 수 있다. 이때, 송신처와 수신처를 묶어서 엔드 노드라 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; TCP/IP 패킷 구조는 위에서 서술한 패킷 기본 동작 과정에서 발전한 것이다. TCP/IP는 허브와 라우터라는 패킷 중계 장치를 사용하는데, 이 둘은 각각 다음과 같은 역할을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 라우터가 목적지를 확인해 다음 라우터를 나타낸다. 라우터는 IP 규칙을 따리기 때문에 IP가 목적지를 확인해 다음 IP 중계장치를 나타낸다고도 할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 허브가 서브넷 안에서 패킷을 운반해 다음 라우터에 도착한다. 허브는 이더넷 규칙을 따르기 때문에 서브넷 안에 있는 이더넷이 중계 장치까지 패킷을 운반한다고도 할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같은 동작 과정 때문에 TCP/IP 패킷에는 MAC header(이더넷용 헤더)와 IP용 헤더가 포함된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 클라이언트가 IP 헤더, Mac 헤더를 추가하고 패킷 송신 전까지 다음과 같은 과정을 거친다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 수신 측 IP를 IP header에 기록한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 수신측수신 측 IP로 수신 측을 찾을 수 있는 라우터를 조사한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 패킷이 도착할 수 있게 이더넷에 의뢰한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 이더넷에서 라우터에 할당된 이더넷의 주소(MAC 주소)를 조사하고, MAC 헤더에 기록한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. 이더넷에게 어느 라우터에 패킷이 도착하면 좋은지를 전달한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 클라이언트에서 위와 같은 과정을 거칠 때 사용하는 레이어는 구조는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="302" data-origin-height="438"><span data-url="https://k.kakaocdn.net/dn/btLAdq/btrQ4aZAGz8/LBGVwxplaWaZtaKrTfySL1/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbtLAdq%2FbtrQ4aZAGz8%2FLBGVwxplaWaZtaKrTfySL1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="214" height="310" data-origin-width="302" data-origin-height="438"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 클라이언트가 패킷을 송신하면 다음과 같은 과정을 거친다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1754" data-origin-height="988"><span data-url="https://k.kakaocdn.net/dn/bOmIxB/btrQ65cs1On/GRoRzvExdW3nSo0DsG5s1K/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbOmIxB%2FbtrQ65cs1On%2FGRoRzvExdW3nSo0DsG5s1K%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1754" data-origin-height="988"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 송신된 패킷은 이더넷의 원리에 따라 허브에 도착한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 허브에 있는 패킷의 목적지를 판단하기 위한 표가 이더넷의 헤더의 수신처 정보와 표를 결합해 패킷의 목적지를 판단하고 중계한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2-1. 만약 허브가 여러 개면 허브를 순차적으로 경유한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 라우터에는 IP용 표가 존재해 이 표와 IP 헤더의 수신처를 결합해 다음 라우터를 결정한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 다음 라우터에 패킷을 건네기 위해 다음 라우터의 맥 주소를 조사하고, 이를 맥 헤더에 기록한다. 이때, 맥 헤더를 바꾸어 쓴다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4-1. 만약 라우터가 여러 개면 또다시 허브를 경유하고 다음 라우터를 순차적으로 경유한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. 위와 같은 과정을 반복하면 목적지에 패킷이 도착한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같이 TCP/IP 네트워크에서 패킷을 목적지에 전달하기 위해 IP와 이더넷이 역할을 분담하는 이유는 유연성에 있다. 위 동작 과정에서 이더넷 부분을 LAN, FTTH 등 패킷을 운반할 수 있는 다른 것으로 대체해 적재적소에 사용할 수 있다. 이렇게 이더넷을 다른 것으로 대체하는 방대한 네트워크를 구축하기 위해선 유연성이 필요하다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>패킷 송/수신 동작의 개요</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; IP 담당 부분은 패킷을 상대에게 송출하는 역할만 한다. 실질적으로 패킷을 운반하는 것은 허브와 라우터다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 패킷 송/수신 동작에서 IP 레이어는 다음과 같은 역할을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 패킷 송/수신 동작은 TCP 레이어가 IP 레이어에 패킷 송신을 의뢰하는 것으로부터 출발한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. TCP 레이어는 세그먼트를 IP 레이어에 부가한다. 이 세그먼트가 패킷의 내용물이 되고, 동시에 통신 상대의 IP주소를 나타낸다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. IP 레이어는 이제 세그먼트 앞에 IP header와 MAC header(제어 정보)를 기록한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp;- IP 헤더는 IP 프로토에 규정된 규칙에 따라 IP 주소로 표시된 수신 측까지 패킷을 전달할 때 사용되는 제어정보를 기록</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp;- MAC 헤더는 이더넷 등의 LAN을 사용해 가장 가까운 라우터까지 패킷을 운반할 때 사용하는 제어정보를 기록</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 패킷을 네트워크용 하드웨어(이더넷, 무선 LAN 등)에 건네준다. 이 하드웨어는 종류마다 이름이 다르므로 여기서는 이들을 랜 어댑터라 통칭하겠다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 랜 어댑터에 패킷을 건네줄 때, 패킷은 비트로 구성된 디지털 데이터가 된다. 이를 랜 어댑터에 의해 전기나 빛의 신호 상태로 바꾸어 케이블에 송출된다. 이 신호는 라우터, 허브를 경유해 수신 측까지 전달된다. 수신 동작은 송신 동작의 반대다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정에서 IP 패킷 송/수신 동작은 패킷 역할에 관계없이 모두 같다. 반면, TCP 레이어의 데이터 송/수신 동작에는 몇 개의 데이터가 있고, 각 단계에서 다양한 세그먼트가 등장한다. IP 레이어가 서로 다른 세그먼트를 같은 과정으로 처리할 수 있는 이유는 IP 레이어가 TCP 헤더와 데이터 조각을 하나의 바이너리 데이터로 간주하기 때문이다. 이 때문에 IP 레이어는 세그먼트에 데이터가 있는지, 순번이 바뀌었는지 등의 문제에 관여하지 않는다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>수신처 IP 주소를 기록한 IP 헤더를 만든다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 언급한 IP 헤더는 다음과 같은 필드를 가진다.</span></p>
<table style="border-collapse: collapse; width: 100%; height: 257px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr style="height: 19px;">
<td style="width: 33.6047%; height: 19px;" colspan="2"><span style="font-family: 'Noto Serif KR';">필드 명칭</span></td>
<td style="width: 9.41854%; height: 19px;"><span style="font-family: 'Noto Serif KR';">길이(비트)</span></td>
<td style="width: 56.9769%; height: 19px;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 13.0233%; height: 17px;" rowspan="13"><span style="font-family: 'Noto Serif KR';">IP 헤더(20 바이트 ~)</span></td>
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">버전</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">4</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">IP 프로토콜의 버전. 현재는 4버전을 사용한다</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">헤더 길이(IHL)</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">4</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">IP 헤더의 길이, 프로토콜 옵션의 유무에 따라 헤더 길이가 달라지므로 헤더의 길이를 명시</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">서비스 유형(ToS)</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">8</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">패킷을 운반할 때의 우선 순위 등을 나타낸다. 처음 정의한 사양이 모호해 최근ㄷ엔 DiffServ라는 사양으로 이 필드의 사용법을 재정의 했다.</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">전체 길이</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">IP 메시지 전체의 길이</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">ID 정보(Identification)</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">각 패킷을 식별하는 번호, 보통 패킷의 참조 번호가 여기에 기록된다. 단, IP 클라이언트에 따라 분할된 패킷은 모두 값이 같다.</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">플래그</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">3</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">실질적으로 사용되는 부분이 2비트다. 하나의 비트로 조각 나누기(fragmentation)가 가능한지, 나머지 하나로 패킷을 조각으로 나눈 것인지를 나타낸다.</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">프래그먼트 오프셋</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">13</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">이 패킷에 저장된 부분이 IP 메시지의 맨 앞부분 부터 몇 번째 바이트에 위치한지를 나타낸다.</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">생존 기간(TTL)</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">8</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">네트워크에 루프를 만들 수 있을 때 패킷이 영구적으로 순환되지 않제 생존기간을 지정한다. 라우터를 경유할 때마다 이 값을 1씩 감소시킨다.</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">프로토콜 번호</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">8</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">프로토콜의 번호가 기록된다.</span><br><span style="font-family: 'Noto Serif KR';">- TCP: 06(hex)</span><br><span style="font-family: 'Noto Serif KR';">- UDP: 11(hex)</span><br><span style="font-family: 'Noto Serif KR';">- ICMP: 01(hex)</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">헤더 체크썸</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">오류 검사용 데이터, 현재는 사용하지 않는다.</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">송신처 IP 주소</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">32</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">패킷을 발신한 쪽의 IP 주소</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">수신처 IP 주소</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">32</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">패킷을 전달한 상태의 IP 주소</span></td>
</tr>
<tr style="height: 17px;">
<td style="width: 20.5814%; height: 17px;"><span style="font-family: 'Noto Serif KR';">옵션</span></td>
<td style="width: 9.41854%; height: 17px;"><span style="font-family: 'Noto Serif KR';">가변 길이</span></td>
<td style="width: 56.9769%; height: 17px;"><span style="font-family: 'Noto Serif KR';">위의 헤더 필드 이외의 제어 정보를 기록할 때 헤더 옵션 필드를 추가. 거의 사용하지 않는다.</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 필드에서 가장 중요한 부분은 수신처 IP 주소이다. 이 IP 주소는 애플리케이션에서 통지된 상태 IP 주소다. IP 레이어는 그저 패킷을 전송할 뿐, IP 주소의 올바름 여부를 체크하지 않는다. 이에 대한 책임은 애플리케이션에 있는 것으로 간주한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 송신처 IP의 경우 이 컴퓨터에 할당된 IP 주소를 설정한다 생각하기 쉽다. 클라이언트용 PC에 랜 어댑터가 하나라면 맞는 말이지만, 랜 어댑터가 여러 개면 틀린 개념이 된다. IP는 사실 랜 어댑터에 할당된다. 따라서 여러 개의 랜 어댑터가 하나의 PC에 장착된 경우 어느 IP 주소를 설정해야 할지 판단해야 한다. 이는 패킷을 수신하는 상대의 라우터를 결정하는 것과 같다. 상대의 라우터가 결정되면 패킷을 송신해야 하는 랜 어댑터가 결정되고, 랜 어댑터가 결정되면 IP 주소가 결정되기 때문이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 라우터가 IP용 표를 사용해 다음 라우터를 결정한다 했다. 이 IP용 표를 경로표라 부른다. ubuntu 22.04에서 "route -n" 명령어를 통해 본 경로표 내용은 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1296" data-origin-height="242"><span data-url="https://k.kakaocdn.net/dn/cHqHXs/btrRb7OregG/RmVZBofUnPUHXkKHTQ9i2K/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FcHqHXs%2FbtrRb7OregG%2FRmVZBofUnPUHXkKHTQ9i2K%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1296" data-origin-height="242"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 경로표에서 Destination 항목을 소켓의 수신처 IP와 비교해 어느 행에 데이터가 있는지 찾는다. Iface 항목은 네트워크용 인터페이스를 나타내고, 인터페이스에서 패킷을 송신하면 수신 측에 패킷을 전해줄 수 있다는 의미다. Gateway는 다음 라우터에 IP 주소를 기록한다. 위 테이블에서 Genmask(net mask)가 0.0.0.0으로 등록돼 있다. 이는 기본 게이트웨이로 다른 곳에 일치하는 것이 없으면 이 행에 해당하는 것으로 간주한다. 위와 같은 정보를 통해 IP 헤더의 송신처 IP 주소를 설정한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; IP header의 프로토콜 번호 필드는 패킷 내용물을 어디에서 의뢰받았는지를 나타낸다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>이더넷용 MAC 헤더를 만든다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>IP 헤더를 만든 후 IP 헤더 앞부분에 MAC 헤더를 추가한다. 맥 헤더를 사용하는 이유는 이더넷에서는 TCP/IP 개념이 통용되지 않아 이더넷의 수신처 판단 구조를 사용해야 하기 때문이다. 맥 헤더는 다음과 같은 필드를 가지고 있다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 37.5581%;" colspan="2"><span style="font-family: 'Noto Serif KR';">필드의 명칭</span></td>
<td style="width: 10.9303%;"><span style="font-family: 'Noto Serif KR';">길이 (비트)</span></td>
<td style="width: 51.5116%;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr>
<td style="width: 18.2558%;" rowspan="3"><span style="font-family: 'Noto Serif KR';">MAC 헤더(14 바이트)</span></td>
<td style="width: 19.3023%;"><span style="font-family: 'Noto Serif KR';">수신처 MAC 주소</span></td>
<td style="width: 10.9303%;"><span style="font-family: 'Noto Serif KR';">48</span></td>
<td style="width: 51.5116%;"><span style="font-family: 'Noto Serif KR';">이 패킷을 전달하는 상대의 MAC 주소, LAN 에서의 패킷 배송은 이 주소를 바탕으로 한다.</span></td>
</tr>
<tr>
<td style="width: 19.3023%;"><span style="font-family: 'Noto Serif KR';">송신처 MAC 주소</span></td>
<td style="width: 10.9303%;"><span style="font-family: 'Noto Serif KR';">48</span></td>
<td style="width: 51.5116%;"><span style="font-family: 'Noto Serif KR';">이 패킷을 송신한 측의 MAC 주소, 패킷을 받았을 때 이 값에 따라 수신측을 판단.</span></td>
</tr>
<tr>
<td style="width: 19.3023%;"><span style="font-family: 'Noto Serif KR';">이더 타입(Ether Type)</span></td>
<td style="width: 10.9303%;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 51.5116%;"><span style="font-family: 'Noto Serif KR';">사용하는 프로토콜의 종류. TCP/IP 통신에선느 0800과 0806 두 종류만 사용한다.</span><br><span style="font-family: 'Noto Serif KR';">- 0000-05DC -&gt; IEEE 802.3</span><br><span style="font-family: 'Noto Serif KR';">- 0800 -&gt; IP protocol</span><br><span style="font-family: 'Noto Serif KR';">- 0806 -&gt; ARP protocol</span><br><span style="font-family: 'Noto Serif KR';">- 86DD -&gt; IPv6</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 필드에서 수신처 MAC 주소와 송신처 MAC 주소는 각각 수신처와 송신처의 MAC 주소를 나타낸다. IP와 유사하지만, IP는 32비트, MAC은 48 비트라는 점이 다르다. 또 한, IP 주소는 서브넷과 호스트 번호로 나뉘어 있지만 MAC 주소는 48비트를 한 개의 값으로 생각한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이더 타입이라는 항목의 IP 헤더의 프로토콜 번호 같이 내용물이 어디에서 의뢰되었는지 나타낸다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 맥 헤더를 만드는 과정은 다음과 같다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>이더 타입 필드 설정</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; IP 프로토콜을 나타내는 값을 설정한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>송신처 MAC 주소 설정</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; LAN 어댑터 자체의 맥 주소를 설정한다. 맥 주소를 랜 어댑터 제조 시 내장 ROM에 기록돼 있다. OS를 기동해 랜 어댑터 초기화 시 맥 주소를 읽어와 메모리에 보관한다. 송/수신 과정에서 헤더에 세팅하는 맥 주소는 이 메모리에서 읽어온다. 이 동작은 LAN driver가 진행한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>수신처 MAC 주소 설정</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>맥 헤더를 만드는 시점에는 수신 측 MAC 주소를 알 수 없다. 이때, 경로표에 있는 Gateway 항목에 기록돼 있는 IP 주소의 기기가 패킷을 건네줄 상대가 된다. 하지만 수신 측의 IP 번호는 여전히 모르므로 IP 주소에서 MAC 주소를 조사하는 과정을 진행해야 한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>ARP(Address Resolution Protocol)로 수신처 라우터의 MAC 주소를 조사한다.</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>수신처 MAC 주소를 알기 위해 ARP를 사용한다. ARP는 이더넷에 연결돼 있는 전원에게 브로드캐스팅을 해서 IP 주소에 대응되는 MAC 주소를 찾는다. 경로표 내용이 올바르다면 상대 MAC 주소는 같은 서브넷에 존재하게 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 패킷을 보낼 때마다 이 동작을 하면 너무 많은 요청을 보내게 된다. 따라서 한번 조회한 MAC 주소를 ARP 캐시에 저장한다. 따라서 패킷을 송신할 때 우선 ARP 캐시를 조회한다. 만약 MAC 주소가 캐시에 없다면 ARP를 조회한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; ARP 캐시에 MAC 주소를 영구 보관하면 IP 주소를 설정해 고쳐진 경우 등의 이유로 캐싱된 MAC 주소와 실제 주소가 다른 문제가 발생한다. 이를 막기 위해 주기적으로 (OS 마다 다르지만&nbsp;수 분 정도) ARP 캐시를 삭제한다. 이때, ARP 캐시 내용이 유효한지를 검사하지 않고 무조건 삭제한다. 그럼에도 IP 주소를 다시 설정한 직후에는 ARP 캐시에 이전 값이 남아있어 제대로 된 통신을 할 수 없게 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같은 과정들을 통해 MAC 헤더를 만드는 것 까지가 IP 레이어의 역할이다. MAC 헤더는 이더넷에서 사용하므로 IP 레이어 밖의 일이라 생각하기 쉽다. 하지만, IP 담당 부분에서 패킷을 완성하면 랜 이더넷은 그저 패킷만 송신하면 된다. 따라서 특수한 패킷이 와도 하나의 랜 어댑터로 대응할 수 있다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 맥 주소를 구분하는 구분자로는 ':'과 '-'가 존재한다. 그 때문에 00-80-C8-2D-82-EA와 00:80:C8:2D:82:EA 는 같은 맥주소를 의미한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>이더넷의 기본</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이더넷은 다수의 컴퓨터가 여러 상대와 자유롭게 적은 비용으로 통신하기 위해 고안된 통신 기술이다. 이더넷의 원형은 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="930" data-origin-height="468"><span data-url="https://k.kakaocdn.net/dn/b21Ozu/btrRc9dY0x1/sJ7HEHCZ1noFm9JL785lh1/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2Fb21Ozu%2FbtrRc9dY0x1%2FsJ7HEHCZ1noFm9JL785lh1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="461" height="232" data-origin-width="930" data-origin-height="468"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;트랜시버는 연결한 케이블 사이에 신호를 흘리는 역할만 한다. 따라서 송신 측이 신호를 보내면 모든 기타 컴퓨터에 신호가 도착한다. 이때, 맥 헤더에 맥 주소를 통해 수신 측이 누구인지를 판단하고 수신 측은 패킷을 수신한다. 기타 기기는 패킷을 폐기한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 시간이 흘러 위와 같은 방식이 다음과 같이 변했다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="788" data-origin-height="564"><span data-url="https://k.kakaocdn.net/dn/oPmGr/btrRd7mtQNf/HmD76fCC7hINxMoOgtIGkK/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_6.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FoPmGr%2FbtrRd7mtQNf%2FHmD76fCC7hINxMoOgtIGkK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="518" height="371" data-origin-width="788" data-origin-height="564"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 비록 위와 같이 구조는 바뀌었지만 신호가 전원에게 전달되는 기본 적인 성질은 같다. 리피터 허브는 구형의 신호를 증폭해 중계하는 방식의 허브를 말한다. 셰이드 허브, 공유 허브라 고도한다. 또 한, 트랜시버 케이블과 트위스트 페어 케이블에서 흐르는 신호가 다르기 때문에 단순히 케이블만 대체되었다고 볼 수는 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이후에는 다음과 같이 리피터 허브 대신 스위칭 허브를 사용한 형태로 바뀌었다. 스위칭 허브는 수신처 MAC 주소에 따라 그에 맞는 상대에게만 패킷을 중계한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="778" data-origin-height="572"><span data-url="https://k.kakaocdn.net/dn/NyLFz/btrRd7fH7a8/AGopeL2mApY20yDc6D9E81/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_7.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FNyLFz%2FbtrRd7fH7a8%2FAGopeL2mApY20yDc6D9E81%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="524" height="385" data-origin-width="778" data-origin-height="572"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같은 변화가 있지만 MAC 헤더의 수신처 MAC 주소로 상대에게 패킷을 전달하고, 송신처&nbsp; MAC 주소로 송신처를 나타낸 후, 이더 타입으로 패킷의 내용물을 나타낸다는 성질은 변하지 않는다. 따라서 이 세 가지 성질을 만족하는 것을 이더넷이라 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이더넷에 접속된 기기는 클라이언트, 스위치를 불문하고 모두 이더넷이라는 하나의 사양에 기초해 동작한다. 이더넷도 IP와 마찬가지로 패킷의 내용물을 보지 않기 때문에 이더넷의 송/수신 동작은 TCP 동작 단계에 상관없이 모두 공통이다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>IP 패킷을 전기나 빛의 신호로 변환해 송신한다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>IP 패킷은 메모리에 존재하는 디지털 데이터다. 이를 상대에게 송신하고 싶다면 전기나 빛의 신호로 변환해 네트워크 케이블로 송출해야 한다. 이것이 송/수신 동작의 본질이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 디지털 데이터를 전기나 빛의 신호로 변환하는 동작을 LAN 어댑터가 실행한다. LAN 어댑터를 제어하기 위해서는 LAN 드라이버가 필요하다. 또 한, LAN 어댑터 구조는 제조 업체나 기종에 따라 달라지므로 LAN 드라이버는 LAN 어댑터 제조 업체가 준비한 전용 제품을 사용한다. 주요 업체 LAN 드라이버는 OS에 기본 설치돼 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; LAN 어댑터의 개념적인 구조는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1398" data-origin-height="1240"><span data-url="https://k.kakaocdn.net/dn/DS2DJ/btrQ6Hi4Oa6/uo0pIvBqkUEOlsQCYyi95k/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_8.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FDS2DJ%2FbtrQ6Hi4Oa6%2Fuo0pIvBqkUEOlsQCYyi95k%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1398" data-origin-height="1240"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 구조를 통해 패킷을 송신하는 과정을 설명하기 전에 LAN 어댑터를 초기화하는 동작을 우선 살펴보자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; LAN 어댑터는 다른 하드웨어와 마찬가지로 초기화 작업이 필요하다. 전원을 공급하면 OS 시동 시 LAN 드라이버가 하드웨어 초기화 작업을 수행한다. 여기서 모든 하드웨어에서 공통으로 수행하는 하드웨어 이상 검사, 초기 설정 등 작업뿐만 아니라 송/수신 동작을 제어하는 MAC 회로에 MAC 주소를 설정하는 작업도 진행한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; LAN 어댑터의 ROM 에는 전 세계 적으로 고유한 맥 주소를 제조 시에 기록한다. 이 주소를 읽어와 MAC 회로에 설정한다. 일부 LAN 어댑터의 경우 명령이나 설정 파일에서 MAC 주소를 받아 설정하는 경우도 있다. 이 경우 ROM에 존재하는 MAC 주소를 무시한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>패팃에 3개의 제어용 데이터를 추가한다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>LAN 드라이버는 IP 담당 부분에서 패킷을 받으면 그것을 LAN 어댑터의 버퍼 메모리에 복사한다. 복사가 끝나면 MAC 회로에 명령을 보내 MAC 회로의 작업이 시작된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MAC 회로는 송신 패킷을 버퍼 메모리에서 추출해 맨 앞에 프리앰블, 스타트 프레임 디 리미 터를 추가하고, 맨 끝에 FCS(Frame Check Sequence라는 오류 검출용 데이터를&nbsp; 추가한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1516" data-origin-height="784"><span data-url="https://k.kakaocdn.net/dn/xuGZH/btrRdaxi78F/j2H1LE2sPthIM832uHzLxK/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_9.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FxuGZH%2FbtrRdaxi78F%2Fj2H1LE2sPthIM832uHzLxK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="661" height="342" data-origin-width="1516" data-origin-height="784"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프리앰블은 1과 0이 번갈아가면서 나타나는 비트열이 56비트 이어진 것이다. 이 비트를 신호로 바꾸면 일정한 파형이 된다. 스타트 프레임 딜리미터는 8비트로 끝이 11이다. 이 때문에 파형이 변해 패킷의 개시로 간주한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1220" data-origin-height="762"><span data-url="https://k.kakaocdn.net/dn/cBufts/btrRcInJMQM/Ck9TAJNDkjHNnJRwNla9Ck/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_10.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FcBufts%2FbtrRcInJMQM%2FCk9TAJNDkjHNnJRwNla9Ck%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="512" height="320" data-origin-width="1220" data-origin-height="762"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 디지털 데이터를 전기 신호로 나타낼 때는 0과 1의 비트 값을 전압, 전류의 값에 대응시킨다. 신호에서 데이터를 읽을 때는 반대로 실행한다. 실제 신호에서는 0과 1이 바뀌는 시점을 통해 각 비트의 구분이 어디까지 인지를 판단해 전류의 값을 읽는다. 하지만 특정 전류가 이어지는 경우, 신호의 변화가 없어져 비트를 구분할 수 없다. 이를 해결하기 위해 클록을 사용한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1898" data-origin-height="868"><span data-url="https://k.kakaocdn.net/dn/rDOTk/btrRcNimjzN/kR7pApQvAudIuUqDKlzRR0/img.png" data-lightbox="lightbox"><img src="/img/2022-11-15-ip-ethernet/img_11.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FrDOTk%2FbtrRcNimjzN%2FkR7pApQvAudIuUqDKlzRR0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1898" data-origin-height="868"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;클록을 사용하는 방식의 경우 케이블이 길어지면 신호선의 길이가 다라져서 데이터 신호화 클록 신호가 전달되는 시간에 차이가 생기기 때문에 클록이 틀어진다. 따라서 클록 신호와 데이터 신호를 합쳐서 보낸다. 이때, 클록 신호는 일정 주기로 모습이 변하는 신호이므로 변화의 타이밍을 알고 있다면, 클록 신호와 데이터 신호가 합쳐진 신호에서 클록 신호를 추출할 수 있다. 그 후 데이터 신호 역시 추측할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 클록 신호는 100 메가비트/초 와 같이 변화하는 주기가 결정돼 있다. 따라서 잠시 신호를 엿볼 수 있으면 주기를 파악할 수 있다. 이를 위해 특별한 신호를 패킷 앞에 부가하는데 이것이 프리앰블이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스타트 프레임 딜리미터는 마지막 비트 패턴이 조금 다르다. 이를 이용해 스타트 프레임 딜리미터는 패킷의 시작을 나타내고 이를 감지해 데이터를 추출하기 시작한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; FCS는 패킷을 운반하는 도중 잡음 등의 영향으로 파형이 흐트러져 데이터가 변한 것을 검출하는 용도로 사용된다. 32비트 비트열이며, 패킷의 맨 앞부분부터 맨 끝까지 특정 계산식에 기초해 계산한 것이다. 이 계산식은 계산의 바탕이 된 데이터의 값이 1비트라도 달라지면 계산한 결과도 달라지게 고안되었다. 따라서 송신 도중 데이터가 변하면 수신 측이 계산한 FCS가 달라진다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>허브를 향해 피킷을 송신한다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 신호를 송신하면 된다. 신호를 송신하는 동작에는 1. 리피터 허브를 사용한 반이중 모드와 2. 스위칭 허브를 사용한 전이중 모드 두 가지가 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 반이중 모드는 다음과 같이 동작한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 신호 충돌을 피하기 위해 케이블에 다른 기기가 송신한 신호가 흐르는지 조사한다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 신호가 흐르면 신호가 멈출 때까지 기다린다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 신호가 더 이상 흐르기 않으면 송신 동작을 시작한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정에서 말하는 송신 동작이란 MAC 회로가 프리앰블의 맨 앞부터 1비트씩 순차적으로 디지털 데이터를 전기 신호로 변환하고, 이것을 PHY(Physical Layer Device) 또는 MAU(Mediumn Attachment Unit)라는 송수신 부분에 보낸다. 이때 디지털 데이터를 신호로 변환하는 속도가 전송 속도다. 1초에 10메가비트 분량의 디지털 데이터를 신호로 변환해 보낼 수 있다면, 10메가비트/초가 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이더넷 케이블은 종류나 전송 속도에 따라 몇 가지 신호 규정이 있다. 하지만 MAC 회로는 이러한 규정을 신경 쓰지 않는다. 따라서 PHY(MAU)가 실제 케이블에 송출할 수 있는 형식으로 신호를 변환한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; PHY(MAU) 회로는 받은 신호를 송신 전 수신 케이블에서 신호가 오는지 확인한다. 신호가 오지 않는다면 송신 동작을 시작한다. 신호 송신 완료까지 신호선에 신호가 안 들어오면 송/수신 동작이 끝난다. 이더넷이라는 통신 방식은 송신한 신호가 상대에게 도착했는지를 확인하지 않는다. 이더넷 사양에서 케이블 길이가 최대 100미터로 정해져 있으므로 오류가 잘 발생하지 않는다. 만약 발생한다면 프로토콜 스택의 TCP가 이를 검출한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 낮은 확률이지만, 복수의 기기가 송신에 들어가면 수신 신호가 들어오는 경우가 있다. 그러면 서로의 신호가 섞여 분간할 수 없는 상태가 되는데 이를 충돌이라 한다. 충돌이 발생하면 송신 동작을 멈추고&nbsp;충돌이 발생한 다른 기기에게 재밍 신호를 보내 충돌을 알린다. 그 후 잠시 멈추었다 다시 송신을 재개한다. 이때, 멈추는 시간이 같다면 다시 충돌이 발생하므로, MAC 주소를 기반으로 난수를 생성해 대기 시간을 계산한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이더넷이 혼잡해 다른 기기와 충돌이 발생할 경우, 대기 시간을 2배로 늘린다. 이 방식으로 10번을 시도했음에도 충돌이 발생하면 오류로 판단한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>돌아온 패킷을 받는다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 리피터 허브는 받은 신호를 접속된 모든 케이블에 송출한다. 그러면 해당 케이블과 연결된 모든 기기가 신호를 받게 된다. 신호를 받은 기기는 다음과 같은 과정을 통해 데이터를 수신한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. PHY(MAU)가 신호를 공통 형식으로 변환해 MAC 회로에 전송한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. MAC 회로는 신호를 디지털 데이터로 변환해 버퍼 메모리에 저장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 신호 마지막에 있는 FCS를 이용해 오류 유무를 검사한다. 오류가 있다면 오류 패킷으로 간주하고 폐기한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 오류가 없다면, 자신의 MAC 주소와 MAC헤더의 송신처 MAC 주소를 비교해 자신에게 오는 패킷인지를 검사한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. 자신에게 오는 패킷이면 버퍼 메모리에 저장한다. 아니라면 폐기한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 6. 패킷을 수신한 사실을 컴퓨터 본체에 통지한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 6번 동작을 인터럽트라는 구조를 사용해 실행한다. 컴퓨터 본채는 LAN 어댑터를 항상 감시하지 않기 때문에 LAN 어댑터가 컴퓨터 본채가 실행하는 작업에 끼어들어 패킷 도착을 알린다. 이 과정을 디테일하게 서술하면 다음과 같다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. LAN 어댑터가 확장 버스 슬롯에 있는 인터럽트용 신호선에 신호를 보낸다. 이 신호선은 컴퓨터 본체 측의 인터럽트 컨트롤러를 통해 CPU에 연결돼 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 신호가 흐르면 CPU는 실행하고 있던 작업을 일시 중지하고 OS 내부의 인터럽트 처리용 프로그램으로 전환한다. 여기서 LAN 드라이버가 호출돼 LAN 어댑터를 제어하면서 송/수신 동작을 실행한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 인터럽트 구조에는 번호가 존재한다. 이 번호를 LAN 어댑터 설치 시 번호를 하드웨어로 설정한다. 인터럽트 처리 프로그램은 이 번호와 드라이버가 대응되게 드라이버 소프트웨어를 등록한다. 그러면 LAN 어댑터가 인터럽트를 걸면 LAN 드라이버가 호출된다. 현재는 PnP(Plug and Play) 사양에 따라 번호를 자동으로 설정하기 때문에 오작동이 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 인터럽트 구조에 의해 LAN 드라이버가 동작하고 LAN 어댑터의 버퍼 메모리에서 수신한 패킷을 추출하면, LAN 드라이버는 MAC 헤더의 타입 필드로부터 프로토콜을 판별한다. 이때, LAN 드라이버는 해당 패킷이 어느 애플리케이션의 것인지를 판별하지 않는다. 그저 타입 필드에 대응되는 프로토콜 스택에 패킷을 전달하기만 한다. 그러면 프로토콜 스택이 어느 애플리케이션에 대응하는 패킷인지 판단하고 적절한 조치를 취한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>서버의 응답 패킷을 IP에서 TCP로 넘긴다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 LAN 드라이버 MAC 해더의 타입 필드로 확인된 프로토콜로 패킷을 건넨다. 프로토콜이 TCP/IP 라면 IP 담당 부분은 IP 헤더를 조사해 포맷에 문제가 없는지 확인한다. 만약 수신처 IP 주소가 다르면 오류가 있다는 의미다. 오류가 발생하면 IP 레이어는 ICMP라는 메시지를 사용해 통신 상대에게 오류를 통지한다. 주요 ICMP 메시지는 다음과 같다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">메시지 종류</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">타입</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Echo reply</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">0</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">Echo 메시지 응답</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Destination unreachable</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">3</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">어떠한 이유로 패킷을 목적지에 건네줄 수 없는 경우에는 폐기하고, 이것을 알리기 위해 발신처에 이 메시지를 보낸다. 원인으로는 수신처 IP 주소가 경로표에 존재하지 않는 경우, 수신처 포트 번호에 해당하는 소켓이 존재하지 않는 경우 등이 있다.</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Source quench</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">4</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">라우터의 중계 능력을 초과해 패킷을 보낸 경우 능력을 초과한 부분의 패킷은 폐기된다. 이렇게 폐기된 것을 송신측에 알릴 때 이 메시지를 사용한다.다만, 능력 부족으로 이 메시지 조차 송신이 안될때도 있다. 이 메시지를 받았다면 패킷 송신 속도를 늦춰야 한다.</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Redirect</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">5</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">경로표에서 중계 목적지 조사 시, 패킷 출력 포트와 패킷 수신 포트가 같다면, 해당 라우터를 중계하지 않고 다음 라우터에 직접 패킷을 송신할 수 있다. 이 경우 다음 라우터의 IP 주소를 나타내고 여기에 직접 패킷을 보내도록 통지한다.</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Echo</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">8</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">ping 명령에 사용하는 메시지, 이 메시지를 받은 상대는 Echo reply 라는 메시지를 돌려주고, 이것으로 상대가 동작하고 있는지 확인할 수 있다.</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Time exceeded</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">11</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">IP 헤더의 TTL 필드에 나타낸는 패킷 생존 기간의 값이 만료되면 라우터는 패킷을 폐기한다. 이때 폐기한 사실을 알리기 위해 발신처에 이 메시지를 보낸다.</span></td>
</tr>
<tr>
<td style="width: 17.8682%;"><span style="font-family: 'Noto Serif KR';">Parameter problem</span></td>
<td style="width: 5.8914%;"><span style="font-family: 'Noto Serif KR';">12</span></td>
<td style="width: 76.2403%;"><span style="font-family: 'Noto Serif KR';">IP 헤더 필드의 값 등에 오류가 있는 경우 패킷을 폐기한다. 이 때 폐기한 사실을 알리기 위해 이 메시지를 사용한다.</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 수신처 IP가 올바르면 이를 수신한다. 이때, 한 가지 동작을 더 하는 경우가 있다. IP 프로토콜은 fragmention이라는 기능을 지원한다. 패킷 운반 도중 통신 회선이나 LAN 중에는 짧은 패킷만 운반할 수 있는 경우가 있다. 따라서 하나의 패킷을 여러 조각으로 잘라야 한다. 패킷 분할 여부는 IP 헤더의 플래그 항목을 통해 판별한다. 분할됐다면 IP 레이어 메모리에 임시 보관하며 IP 헤더의 ID 정보가 일치하는 패킷이 도착하기를 기다린다. ID 정보가 같다는 의는 하나의 패킷이었다는 의미다. 그 후 프래그먼트 오프셋(fragment offset)이라는 항목을 통해 패킷의 순서를 판별해 원래 모습으로 되돌린다. 이렇게 원래 모습으로 되돌리는 동작을 리어셈블링(reassembling)이라 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 IP 레이어가 패킷을 TCP 레이어로 보낸다. 그러면 TCP 레이어는 IP 헤더에 기록된 송/수신처 IP와 TCP 헤더에 기록된 송/수신처 port를 이용해 소켓을 찾는다. 그리고 소켓에 명시된 상태에 따라 적절한 행동을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 설명에서 TCP 레이어가 IP 헤더를 조사한다는 부분이 어색하게 느껴질 수 있다. 엄밀히 말하면 IP 헤더는 IP 레이어에서만 담당하고, TCP 헤더는 TCP 레이어에서만 담당해야 하기 때문이다. 그리고 IP 레이어가 송/수신 IP 등 중요 정보를 TCP에 통지하는 식이 돼야 한다. 하지만, 이러면 IP 레이어와 TCP 레이어 간의 통신이 잦아져 실행 효율이 저하된다. 따라서 담당 범위를 여유 있게 해석하는 것이 현실적이다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 성공과 실패를 결정하는 1%의 네트워크 원리</span></p></div>