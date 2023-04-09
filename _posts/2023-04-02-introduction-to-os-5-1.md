---
layout:       post
title:        "chapter5-1. 프로세스간 통신."
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스 간 통신은 하나의 컴퓨터에 존재하는 여러 프로세스끼리의 통신과 네트워크로 연결된 다른 컴퓨터에 있는 프로세스와의 통신이 있다. 프로세스 간 통신 종류는 다음과 같이 크게 세 종류로 나뉜다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>1. 프로세스 내부 데이터 통신</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하나의 프로세스 내에 2개 이상의 스레드가 존재하는 경우의 통신이다. 프로세스 내부의 스레드는 전역 변수나 파일을 이용해 데이터를 주고받는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>2. 프로세스 간 데이터 통신</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 같은 컴퓨터에 있는 여러 프로세스끼리 통신하는 경우다. 공용 파일 또는 OS가 제공하는 파이프를 사용해 통신한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>3. 네트워크를 이용한 데이터 통신</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여러 컴퓨터가 네트워크로 연결되 있을 때 프로세스는 소켓을 이용해 데이터를 주고받는다. 소켓을 이용하는 프로세스 간 통신을 네트워킹이라 한다. 다른 컴퓨터에 있는 함수를 호출해 통신하는 원격 프로시저 호출(Remote Procedure Call - RPC)도 여기에 해당한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스 간 통신 분류</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스 간 통신은 동시에 실행되는 프로세스끼리 데이터를 주고받는 작업을 의미한다. 이 통신은 데이터가 전송되는 방향에 따라 다음과 같이 나뉜다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>1. 양방향 통신</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>데이터를 동시에 양방향으로 전송하는 구조. 일반적인 통신은 모두 양방향 통신이다(ex - 소켓 통신).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>2. 반양방향 통신</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 데이터를 양쪽 방향으로 전송할 수 있지만 동시 전송은 불가능한 통신이다. 특정 시점에 한 방향만 데이터를 전송할 수 있다(ex - 무전기).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>3. 단방향 통신</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 모스 신호처럼 한쪽 방향으로만 데이터를 전송할 수 있는 구조다. 프로세스 간 통신에서는 전역 변수와 파이프, 파일이 단방향 통신에 해당한다. 전역변수를 1개만 사용했을 때 양쪽에서 데이터를 보내면 둘 중 하나는 지워진다. 따라서 전역 변수로 양방향 통신을 하려면 두 개의 변수가 필요하다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>통신 구현 방식에 따른 분류</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b></b>&nbsp; 전역 변수를 사용하는 방식에서 데이터를 수신하는 쪽이 데이터가 왔는지를 알기 위해 수시로 전역 변수 값을 점검한다. 이렇게 상태 변화를 알기 위해 무한히 체크하며 기다리는 것을 바쁜 대기(busy waiting)라고 한다. Busy waiting은 리소스 낭비가 심하다. 이 문제를 해결하기 위해 데이터가 도착하면 알려주는 동기화(synchronization)를 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스간 통신은 동기화 기능 유무에 따라 다음과 같이 나뉜다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 대기가 있는 통신(blocking communication/synchronouse communication)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>동기화를 지원하는 방식이다. 데이터 수신 측은 데이터 수신 시까지 대기 상태에 머물러있는다(ex - 파이프, 소켓).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 대기가 없는 통신(non-blocking communication/asynchronous communication)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>동기화를 지원하는 않는 통신 방식이다. 데이터 수신측은 busy waiting을 사용해 데이터 도착 여부를 확인한다(ex - 전역 변수, 파일).</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스 간 통신 종류</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>전역 변수를 이용한 통신</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 공동으로 관리하는 메모리를 사용해 데이터를 주고받는다. 데이터 송신 측은 전역 변수나 파일에 값을 쓰고, 수신 측은 전역변수 값을 읽는다. 전역 변수를 이용한 통신은 부모-자식 프로세스와 같이 직접적으로 관련 있는 프로세스 간에 사용한다. 아래 그림은 두 프로세스가 양방향 통신을 위해 전역 변수 R, L을 정의해 사용하는 그림이다. 두 프로세스 모두 전역 변수에 읽기/쓰기를 한다.&nbsp;</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1200" data-origin-height="430"><span data-url="https://blog.kakaocdn.net/dn/bQmaFS/btr7hx44ftS/Ru0izLJG1JlIotYa5510j0/img.png" data-lightbox="lightbox"><img src="/img/2023-04-02-introduction-to-os-5-1/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbQmaFS%2Fbtr7hx44ftS%2FRu0izLJG1JlIotYa5510j0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="598" height="214" data-origin-width="1200" data-origin-height="430"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정에는 문제가 있다. 하나의 프로세스가 전역 변수에 데이터를 언제 쓰는지 알기 위해 나머지 프로세스는 전역변수를 계속 활용해야 한다.</span></p>
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>파일을 이용한 통신</b><b></b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 파일 입출력 코드는 크게 읽기(open), 쓰기(write)/읽기(read), 닫기(close) 세가지로 나뉜다. 프로세스가 읽기/쓰기를 위해 입출력 관리 프로세스에게 의뢰하므로 파일 입출력도 통신이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1154" data-origin-height="352"><span data-url="https://blog.kakaocdn.net/dn/W9WSg/btr7fY3H4Qs/xpHr5woH3D9WOXw8d1hc40/img.png" data-lightbox="lightbox"><img src="/img/2023-04-02-introduction-to-os-5-1/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FW9WSg%2Fbtr7fY3H4Qs%2FxpHr5woH3D9WOXw8d1hc40%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="594" height="181" data-origin-width="1154" data-origin-height="352"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>파일 열기</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; open()에서는 사용하고자 하는 파일 존재 유무와 파일 접근 권한(읽기/쓰기 권한)이 있는지 체크한다. 유효하다면 file descriptor를 반환한다. 파일을 연 뒤에는 file descriptor만을 통해 파일에 접근 가능하다. 작업을 끝나면 file descriptor를 반환해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>읽기 또는 쓰기</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; file descriptor는 파일에 대한 접근 권한을 가지고 있다. 따라서 파일 읽기/쓰기를 위해 file descriptor를 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>파일 닫기</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; close 함수를 이용해 파일을 닫는다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">5</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">6</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">7</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">8</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">9</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">10</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">11</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">12</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">16</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">17</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdio.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>unistd.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>fcntl.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;fileDescriptor;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">char</span>&nbsp;buffer[<span style="color: #0099cc;">5</span>];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;fileDescriptor&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;open(<span style="color: #63a35c;">"com.txt"</span>,&nbsp;O_RDWR);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;하드디스크로&nbsp;쓰기</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;write(fileDescriptor,&nbsp;<span style="color: #63a35c;">"Test"</span>,&nbsp;<span style="color: #0099cc;">5</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;하드디스크로&nbsp;읽기,&nbsp;buffer로&nbsp;5바이트&nbsp;읽기</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;read(fileDescriptor,&nbsp;buffer,&nbsp;<span style="color: #0099cc;">5</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;close(fileDescriptor);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #0099cc;">0</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 파일을 이용한 통신은 부모-자식 프로세스 간 통신에서 많이 사용된다. OS가 프로세스 동기화를 제공하지 않는다. 따라서 자체적인 동기화를 위해 wait() 함수를 이용해 자식 프로세스 작업이 끝날 때까지 기다렸다 작업을 시작한다.</span></p>
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>파이프를 이용한 통신</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>OS가 제공하는 동기화 통신 방식이다. 파일 입출력과 마찬가지로 open()을 통해 file descriptor를 얻고 close() 함수로 작업을 끝낸다. 파이프를 이용한 통신은 단방향이므로 양방향 통신을 위해선 2개의 파이프를 사용해야 한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1564" data-origin-height="424"><span data-url="https://blog.kakaocdn.net/dn/dcNNWS/btr7C1p3Z49/yHIYKpBXktMVSymfV2mcK0/img.png" data-lightbox="lightbox"><img src="/img/2023-04-02-introduction-to-os-5-1/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdcNNWS%2Fbtr7C1p3Z49%2FyHIYKpBXktMVSymfV2mcK0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="646" height="175" data-origin-width="1564" data-origin-height="424"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 파이프 종류는 anonymouse pipe와 named pipe로 나뉜다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>anonymouse pipe</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>부모와 자식 프로세스 또는 같은 부모를 가진 프로세스와 같이 서로 관련있는 프로세스 간 통신에 사용된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>named pipe</b><b></b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>FIFO라 불리는 특수 파일을 이용해 서로 관련 없는 프로세스 간 통신에 사용된다.</span></p>
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>소켓을 이용한 통신</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여러 컴퓨터에 있는 프로세스 간 통신을 네트워킹이라 한다. 네트워킹 상황에서의 통신은 원격 프로시저 호출이나 소켓을 이용한다. 원격 프로시저 호출은 다른 컴퓨터에 있는 함수를 호출하는 것이다. 일반적으로 원격 프로시저 호출은 소켓을 이용해 구현한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1444" data-origin-height="760"><span data-url="https://blog.kakaocdn.net/dn/cZjyHA/btr7xVwXRvO/v2xFg5TNiBWWrYRa8oZ1Q1/img.png" data-lightbox="lightbox"><img src="/img/2023-04-02-introduction-to-os-5-1/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcZjyHA%2Fbtr7xVwXRvO%2Fv2xFg5TNiBWWrYRa8oZ1Q1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="527" height="277" data-origin-width="1444" data-origin-height="760"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 소켓은 프로세스 동기화를 지원하기 때문에 데이터 수신측이 busy waiting을 하지 않아도 된다. 소켓은 양방향 통신을 위해 한 개만 사용해도 된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>정리</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 동기화를 지원하는프로세스 간 통신에는 open()과 close() 함수가 사용된다. 이런 구조를 open-read/write-close 구조라 한다. 프로세스 간 통신을 요약하면 다음과 같다.</span></p>
<table style="border-collapse: collapse; width: 70.6977%; height: 90px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">종류</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">운영체제 동기화 지원</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">open()/close() 사용</span></td>
</tr>
<tr>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">전역 변수</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">X(busy waiting)</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">X</span></td>
</tr>
<tr>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">파일</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">X(wait() function)</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">O</span></td>
</tr>
<tr>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">파이프</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">O</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">O</span></td>
</tr>
<tr>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">소켓</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">O</span></td>
<td style="width: 33.3333%;"><span style="font-family: 'Noto Serif KR';">O</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p></div>