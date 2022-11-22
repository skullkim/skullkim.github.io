---
layout:       post
title:        "Chapter 2. Story 6. UDP 프로토콜을 이용한 송/수신 동작"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- network
- ComputerScience
- 성공과 실패를 결정하는 1%의 네트워크 원리
- 도서
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>수정 송신이 필요 없는 데이터의 송신은 UDP가 효율적이다.&nbsp;</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 대부분의 애플리케이션은 TCP 프로토콜을 사용해 데이터 송/수신을 실행한다. 하지만, DNS 서버에서 IP를 조회할 때처럼 UDP를 사용할 때도 있다. TCP는 데이터의 송신을 확실히 하면서도 효율적으로 동작하기 위해 상당히 복잡한 방식을 사용한다. 데이터 도착을 확인하고 도착하지 않았으면 다시 송신해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 데이터가 한 개의 패킷 안에 수용할 수 있다면, 없어진 패킷을 찾고, 재송신하는 과정이 필요 없다. 그냥 전부 다시 보내면 된다. 또 한, TCP 같은 복잡한 구조를 사용하지 않으면 접속하거나 연결을 끊을 때 제어용 패킷을 보낼 필요가 없다. 데이터를 보내면 보통은 회신이 돌아오기 때문에 수신 확인 응답을 대신할 수 있어서 수신 확인 응답 패킷이 필요 없어진다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>제어용 짧은 데이터</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; DNS 서버에 대한 조회 같이 제어용 송수신은 한 개의 패킷으로 끝나는 경우가 많다. 이때는 TCP가 아닌 UDP를 사용한다. UDP 헤더 구조는 다음과 같다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 30.5814%;" colspan="2"><span style="font-family: 'Noto Serif KR';">필드 명칭</span></td>
<td style="width: 11.6279%;"><span style="font-family: 'Noto Serif KR';">길이(비트)</span></td>
<td style="width: 57.7907%;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr>
<td style="width: 15.1163%;" rowspan="4"><span style="font-family: 'Noto Serif KR';">UDP 헤더(8 바이트)</span></td>
<td style="width: 15.4651%;"><span style="font-family: 'Noto Serif KR';">송신처 포트 번호</span></td>
<td style="width: 11.6279%;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 57.7907%;"><span style="font-family: 'Noto Serif KR';">이 패킷을 송신한 측의 포트 번호</span></td>
</tr>
<tr>
<td style="width: 15.4651%;"><span style="font-family: 'Noto Serif KR';">수신처 포트 번호</span></td>
<td style="width: 11.6279%;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 57.7907%;"><span style="font-family: 'Noto Serif KR';">이 패킷을 건네줄 상대의 포트 번호</span></td>
</tr>
<tr>
<td style="width: 15.4651%;"><span style="font-family: 'Noto Serif KR';">데이터 길이</span></td>
<td style="width: 11.6279%;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 57.7907%;"><span style="font-family: 'Noto Serif KR';">UDP 헤더 이후의 길이</span></td>
</tr>
<tr>
<td style="width: 15.4651%;"><span style="font-family: 'Noto Serif KR';">체크섬</span></td>
<td style="width: 11.6279%;"><span style="font-family: 'Noto Serif KR';">16</span></td>
<td style="width: 57.7907%;"><span style="font-family: 'Noto Serif KR';">오류 유무를 검사하기 위한 것</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 UDP 헤더 구조에서 볼 수 있듯이 UDP 헤더에는 window, ACK number 등이 존재하지 않는다. 따라서 데이터 송/수신 전에 제어정보를 주고받거나 접속 연결 끊기 단계가 없다. 그저 헤더를 추가하고 IP 레이어에 의뢰해 전송만 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 수신 역시 IP 헤더에 있는 송/수신처 IP와 UDP 헤더에 기록된 송/수신처 포트 번호를 이용해 소켓에 기록된 정보를 결합하고 데이터를 건넬 애플리케이션을 판단한 뒤 건네준다. 도중에 패킷이 유실돼도 신경 쓰지 않는다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; UDP가 송신할 수 있는 최대 길이는 IP 패킷 최대 길이에서 IP header와 UDP header를 뺀 것이다. 이는 MTU, MSS와는 다르다. MTU, MSS는 이더넷 같은 통신 회선 패킷의 최대 길이를 기반으로 산출된다. 그게 반해 IP 패킷 최대 길이는 IP 헤더의 전체 길이 필드로 산출한다. 전체 길이 필드는 16bit 이므로 65535byte가 IP 패킷의 최대 크기다. 여기서 프로토콜 옵션 설정이 없다면, IP header 20byte, UP header 8 byte를 제외한 65507 byte가 UDP의 데이터 최대 길이가 된다. 이렇게 큰 데이터를 통신 회선의 패킷이 수용할 수 없기 때문에, IP 담당 부분의 조각 나누기 기능으로 패킷을 분할해 실제 패킷 송신 동작을 한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>음성 및 동영상 데이터</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 음성이나 동영상 데이터를 보낼 때 UDP를 사용한다. 음성과 동영상은 결정된 시간 안에 데이터를 건네주어야 한다. 이때, TCP를 사용하게 되면 수신 확인 응답 등 과정에 의해 결정된 시간 안에 데이터를 송신하지 못한다. 그러면 재생 타이밍이 맞지 않게 되고, 중간에 끊긴 음성이나 영상을 다시 되돌릴 수 없기 때문에, 데이터가 잘 도착해도 의미가 없다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">출처 - 성공과 실패를 결정하는 1%의 네트워크 원리</p></div>