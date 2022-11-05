---
layout:       post
title:        "[번역]Inside NGINX: How We Designed for Performance &amp; Scale"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- nginx
---

<head></head>
<body id="tt-body-page" class="">
<div id="wrap" class="wrap-right">
    <div id="container">
        <main class="main ">
            <div class="area-main">
                <div class="area-view">
                    <div class="article-header"></div>
                    <hr>
                    <div class="article-view">
                        <div class="contents_style">
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx는 설계 방식 덕분에 우수한 웹 퍼포먼스를 보이고 있다. 수 많은 WS와 WAS가 스레드 또는 프로세스 기반 아키텍처를 사용하는 반면, nginx는 접속을 수백 수천개의 동시 접속으로 확장할 수 있는 정교한 event-driven 아키텍처를 사용하고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://www.nginx.com/resources/library/infographic-inside-nginx/">&nbsp; Inside NGINX</a>&nbsp;는 고수준 프로세스 아키텍처부터 저수준으로 내려가면서 Nginx가 여러개의 커넥션을 싱글 프로세스로 처리하는 과정을 서술하고 있다. 이 글은 한발 더 나아가 더 디테일하게 Nginx의 동작 과정을 서술하려 한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Setting the Scene - The NGINX Process Model</b></span></h2>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp; &nbsp;&nbsp;</b>Nginx의 설계를 이해하기 위해선 Nginx가 어떻게 동작하는지 알아야 한다. Nginx는 하나의 마스터 프로세스와 워커프로세스, 헬퍼 프로세스들로 이루어져 있다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;service&nbsp;nginx&nbsp;restart</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;"></span><span style="color: #a71d5d;">*</span>&nbsp;Restarting&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;ps&nbsp;-ef&nbsp;--forest&nbsp;|&nbsp;grep&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">root&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;nginx:&nbsp;master&nbsp;process&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>usr<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>sbin<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>nginx&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>c&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>etc<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>nginx<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>nginx.conf</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">nginx&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32476</span>&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;&nbsp;_&nbsp;nginx:&nbsp;worker&nbsp;process</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">nginx&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32477</span>&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;&nbsp;_&nbsp;nginx:&nbsp;worker&nbsp;process</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">nginx&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32479</span>&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;&nbsp;_&nbsp;nginx:&nbsp;worker&nbsp;process</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">nginx&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32480</span>&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;&nbsp;_&nbsp;nginx:&nbsp;worker&nbsp;process</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">nginx&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32481</span>&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;&nbsp;_&nbsp;nginx:&nbsp;cache&nbsp;manager&nbsp;process</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">nginx&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">32482</span>&nbsp;<span style="color: #0099cc;">32475</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13</span>:<span style="color: #0099cc;">36</span>&nbsp;?&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>:<span style="color: #0099cc;">00</span>&nbsp;&nbsp;_&nbsp;nginx:&nbsp;cache&nbsp;loader&nbsp;process</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 예제에서는 쿼드코어 서버에서 nginx가 동작하고 있다. Nginx의 마스터 프로세스는 4개의 워커 프로세스와 disck cache를 완리하는 한 쌍의 cache helper process를 생성한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Why Is Architecture Important?</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>모든 유닉스 애플리케이션의 근간은 스레드 또는 프로세스이다. 스레드, 프로세스는 운영체제가 CPU 코어에서 실행되게 스케줄할 수 있는 명령어들의 집합이다. 대부분의 복잡한 애플리케이션들이 멀티 쓰레드, 멀티 프로세스를 사용하는 이유는 다음과 같다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 더 많은 컴퓨팅 코어를 동시에 사용할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 스레드와 프로세스를 통해 간단하게 동시 연산을 할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스와 스레드는 리소스를 소비한다. 이들은 메모리와 운영체제 자원을 사용하고 컨텍스트 스위칭을 한다. 대부분의 현대적 서버들은 수백개의 활성화된 작은 프로세스, 스레드들을 동시에 감당할 수 있다. 하지만, 메모리를 많이 사용하거나 무거운 I/O로 인한 컨텍스트 스위칭이 대량으로 발생한다면 퍼포먼스는 심각하게 저하된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 네트워크 애플리케이션을 설계할 때는 일반적으로 각 커넥션 하나 당 하나의 스레드 또는 프로세스를 할당한다. 이 아키텍처는 간단하고 적용하기 쉽다. 하지만 이 설계는 수천개의 커넥션을 동시에 감당하지 못한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>How Does Nginx Work?</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>Nginx는 사용 가능한 하드웨어 리소스에 맞게 조정된 범용 프로세스 모델을 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 마스터 프로세스는 설정(configuration) 읽기, 포트 바인딩, 여러개의 child process 생성 등 마스터 프로세스만 할 수 있는 연산을 수행한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - cache loader process는 Nginx 시작 초기에 실행되서 disck cache를 메모리에 올리고 종료된다. cache loader processsms 보수적으로 스케줄하기 때문에 리소스 사용량이 적다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - cache manager process는 주기적으로 실행되며 disk cache에 할당된 용량을 사용해 실행된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - worker process는 모든 일을 한다. 네트워크 연결, 디스크에 읽고 쓰기, 업스트림 서버와 커뮤니케이션하기 등의 일을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx는 하나의 워커 프로세스당 CPU 코어 하나를 할당하는 것을 권장하고 있다. 이는 worker_processes에 auto 파라미터를 줌으로서 설정할 수 있다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">worker_processes&nbsp;auto;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx 서버가 active 상태가 되면, 각 워커 프로세스가 여러 커넥션들을 non-blocking 방식으로 처리한다. 이를 통해 컨텍스트 스위칭 비용을 줄인다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 각 워커 프로세스는 싱글 스레드이며 독립적으로 실행된다. 워커 프로세스간에 커뮤니케이션은 공유된 메모리를 사용해 이루어진다. 이 공유된 메모리는 공유된 캐시 데이터, session persistence data, 등 공유된 리소스를 위한 메모리다.</span></p>
</div>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Inside the Nginx Worker Process</b></span></h2>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 각 Nginx 워커 프로세스는 Nginx 환경 설정에 의해 초기화 되고 마스터 프로세스에 의해 수신 소켓(listen socket) 세트가 제공된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 워커 프로세스는 수신 소켓에의 이벤트를 대기하는 것으로 시작한다. 이벤트는 Nginx 측으로 들어오는 새로운 커넥션에 의해 초기화된다. 이 커넥션들은 상태 머신에 할당된다. HTTP 상태 머신이 일반적으로 사용된다, 하지만 Nginx는 스트림(raw TCP) 트래픽과 메일 프로토콜을 위한 상태머신들도 사용하고 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img_2.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 상태 머신은 본질적으로 Nginx에게 요청 처리 방식을 알려주는 명령의 집합이다. Nginx와 같은 기능을 하는 웹 서버들은 대부분 비슷한 상태 머신을 사용하고 있다. 이런 상태 머신들의 차이는 구현에 존재한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Scheduling the State Machine</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>상태 머신을 체스 룰에 빗대어 생각해보자. 아래의 모든 설명에서 Nginx의 동작을 체스에 빗대어 설명할 것이다. 각 HTTP 트랜잭션은 하나의 체스 게임이다. 체스 판의 한 편은 웹 서버이(이 웹서버를 체스 장인이라 해보자)며 빠른 결정을 내릴 수 있다. 다른 한편에는 원격 클라이언트가 존재하며 상대적으로 느린 네트워크로 애플리케이션에 접속하고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 그러나, 이 게임의 룰은 복잡해 질 수 있다. 예를 들어, 웹 서버가 프록시와 커뮤니케이션 해야 한다거나, 서드 파티 모듈들이 게임의 룰을 확장하거나 할 수 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>A Blocking State Machine</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;스레드, 프로세스는 운영체제가 CPU 코어에서 실행되게 스케줄할 수 있는 명령어들의 집합이라는 것을 상기시켜 보자. 많은 웹 서버들과 웹 애플리케이션들은 커넥션 하나 당 하나의 스레드 또는 하나의 프로세스를 사용해 체스 게임을 진행한다. 각 프로세스, 스레드는 게임을 끝날때 까지 진행할 수 있는 명령어들을 포함하고 있다. 이 때, 프로세스는 서버에 의해 실행되며 대부분의 시간을 블록된(blocked)채로 기다린다(클라이언트가 다음 동작을 완료하길 기다려야 하기 때문이다).</span></p>
<p></p><figure class="imageblock alignCenter" width="488" height="446">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img_3.png" width="488" height="446">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 웹 서버 프로세스는 수신 소켓에서 새로운 커넥션을 기다린다(listen).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 새로운 게임이 시작되면, 새로운 게임을 진행한다. 말을 한번 욺직일 때마다 클라이언트의 응답을 기다린다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 게임이 종료되면, 웹 서버 프로세스는 클라이언트가 새로운 게임을 시작하길 원하는지를 알기 위해 대기한다(keepalive 커넥션과 관련있다). 만약 커넥션이 종료된다면(클라이언트가 연결을 끊거나 timeout된다면), 해당 웹 서버 프로세스는 새로운 게임을 대기하기 위해 반환된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여기서 중요한 것은 모든 HTTC 커넥션(각 체스 게임)은 전용 프로세스, 스레드가 필요하다는 것이다. 이 아키텍처는 심플하고 서드 파티 모듈을 사용해 확장하기 쉽다. 그러나, 여기에는 심각한 불균형이 존재한다. 단일 파일 디스크립터와 적인 양의 메모리로 대표되는 경량 HTTP 커넥션이 무거운 운영체제 객체인 분리된 스레드, 프로세스에 매핑된다. 이는 개발 편의를 위한것이지만, 낭비가 심각하다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Nginx is a True Grandmaster</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>한 명의 체스 장인이 수십명의 플레이어와 동시에 체스게임을 진행하는 장면을 본적 있는가? 이것이 Nginx 워커 프로세스가 "체스"를 플레이하는 방식이다. 각 워커(통상적으로 각 CPU 코어 하나 당 하나의 워커가 존재하는 것을 기억하라.)는 동시에 수백개의 체스 게임을 진행할 수 있는 체스 장인이다.</span></p>
<p></p><figure class="imageblock alignCenter" width="453" height="428">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img_4.png" width="453" height="428">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 워커 프로세스는 수신 소켓과 연결 소켓(connection socket)에서 이벤트를 기다린다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 이벤트가 소켓에서 발생하면 워커는 이들을 처리한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 수신 소켓에서의 이벤트는 클라이언트가 새로운 체스 게임을 시작한다는 의마다. 워커는 새로운 연결 소켓을 생성한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 연결 소켓에서의 이벤트는 클라이언트가 새로운 말을 욺직였다는 의미다. 워커는 신속히 응답한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 워커는 네트워크 트래픽을 block하지 않고 클라이언트의 응답을 기다린다. 클라이언트가 말을 욺직였다면 워커는 즉시 욺직임을 기다리고 있는 다른 게임들로 넘어가거나 새로운 플레이어를 기다린다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Why Is This Faster Than a Blocking, Multiprocess Architecture?</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx는 하나의 워커 프로세스가 수백 수척개의 커넥션을 감당할 수 있게 높은 확장성을 가지고 있다. 각 새로운 거넥션은 파일 디스크립터를 생성하고 워커 프로세스에서 소량의 추가 메모리를 사용한다. 따라서 하나의 커넥션은 오직 소량의 오버헤드만 존재하게 된다. Nginx 프로세스들은 CPU에 고정된 상태로 남아있을 수 있다. 그러면 컨텍스트 스위칭을 상대적으로 줄일 수 있고 완료해야 하는 일이 없을 경우에 발생하게 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 블로킹 환경에서 커넥션 하나 당 프로세스 하나를 사용하는 접근법은 각 커넥션이 많은 양의 리소스와 오버헤드를 사용하게 한다. 또 한, 컨텍스트 스위칭도 빈번히 발생한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 더 자세한 설명이 필요하다면 <a href="https://www.aosabook.org/en/nginx.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 올바른 <a href="https://www.nginx.com/blog/tuning-nginx/" target="_blank" rel="noopener">시스템 튜닝</a>을 한다면, Nginx는 하나의 워커 프로세스가 동시에 발생하는 HTTP 커넥션은 수백 수천개까지 감당할 수 있게 확장할 수 있다. 또 한, 트래픽 급증도 착오없이 감당할 수 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Updating Configuration and Upgrading Nginx</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 적은 수의 워커 프로세스를 가지는 Nginx 프로세스 아키텍처는 환경 세팅을, 심지어는 Nginx 바이너리를 효율적으로 업데이터 하게 해준다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img_5.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx 환경 세팅을 업데이트 하는 것은 아주 간단한 작업이다. 일반적으로 "nginx -s reload" 명령어를 입력하기만 하면 된다. 이 명령어는 디스크에 존재하는 환경 설정을 체크하고 마스터 프로세스에게 SIGHUP 신호를 보낸다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 마스터 프로세스가 SIGHUP 신호를 받으면, 다음 두 가지 일을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 환경 설정을 다시 로딩하고 새로운 워커 프로세스 집합을 포크한다. 이 새로운 워커 프로세스들은 새로운 환경 설정을 사용해 즉시 커넥션과 프로세싱 프래픽을 받아 처리한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 이전에 사용된 워커 프로세스가 정상적으로 종료되게 신호를 보낸다. 이 워커 프로세스들은 새로운 커넥션을 더이상 받지 않는다. 현재 진행중인 각 HTTP 요청이 종료되면 종료 대상이 되는 워커프로세스들은 커넥션을 중단한다(keepalive를 하지 않는다). 모든 커넥션이 종료된 후, 워커 프로세스들은 종료된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이런 프로세스를 다시 로딩하는 과정은 CPU와 메모리 사용량을 약간 증가시킬 수 있다, 하지만 리소스를 활성화된 커넥션들로 부터 받아오는 것에 비하면 미미한 사용량이다. 환경 설정을 1초에 여러번 리로드할 수도 있다. 흔치 않은 경우지만, 몇번의 리로딩을 거치는 동안 이전의 워커 프로세스들이 커넥션을 종료하지 못하고 종료되길 기다리는 경우가 발생한다. 하지만, 이런 문제는 금방 해결된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx의 바이너리 업그레이드는 고가용성을 달성했다. 바이너리 업그레이드를 통해 서비스의 중단, 커넥션 중지 없이도 소프트웨어를 업그레이드할 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV1JbnNpZGUgTkdJTlg6IEhvdyBXZSBEZXNpZ25lZCBmb3IgUGVyZm9ybWFuY2UgJmFtcDsgU2NhbGU=/img_6.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 바이너리 업그레이드의 접근법은 환경 설정 리로딩과 비슷하다. 새로운 Nginx 마스터 프로세스가 기존 마스터 프로세스와 동시에 동작한다. 그리고 수신 소켓을 공유한다. 두 마스터 프로스세들은 모두 활성화 되있고, 각자의 워커 프로세스가 트래픽을 감당한다. 이제 기존 마스터 프로세스를 종료시키면 된다. 더 자세한 동작과정은 <a href="https://nginx.org/en/docs/control.html?_ga=2.201724119.773025756.1660218315-2056848361.1660218315" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 Nginx 최적화에 관심있다면 다음 글들을 참고하자.</span></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';"><a href="https://www.nginx.com/resources/webinars/installing-tuning-nginx/">Installing and Tuning NGINX for Performance</a></span></li>
<li><span style="font-family: 'Noto Serif KR';"><a href="https://www.nginx.com/blog/tuning-nginx/">Tuning NGINX for Performance</a>&nbsp;</span></li>
</ul>
<figure id="og_1660366955287" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="How to Get Started With NGINX - NGINX" data-og-description="In this webinar, we help you get started using NGINX, the de facto standard building block for modern microservices-based architectures. During this practical workshop, we take you through installing and configuring NGINX as a web server, load balancer, an" data-og-host="www.nginx.com" data-og-source-url="https://www.nginx.com/resources/webinars/installing-tuning-nginx/" data-og-url="https://www.nginx.com/resources/webinars/how-to-get-started-with-nginx/" data-og-image="https://scrap.kakaocdn.net/dn/cZXJmv/hyPq7AJy6H/TJAkzF84y0DqMTUHSicQP0/img.png?width=1000&amp;height=600&amp;face=0_0_1000_600"><a href="https://www.nginx.com/resources/webinars/installing-tuning-nginx/" target="_blank" rel="noopener" data-source-url="https://www.nginx.com/resources/webinars/installing-tuning-nginx/">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/cZXJmv/hyPq7AJy6H/TJAkzF84y0DqMTUHSicQP0/img.png?width=1000&amp;height=600&amp;face=0_0_1000_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">How to Get Started With NGINX - NGINX</p>
<p class="og-desc" data-ke-size="size16">In this webinar, we help you get started using NGINX, the de facto standard building block for modern microservices-based architectures. During this practical workshop, we take you through installing and configuring NGINX as a web server, load balancer, an</p>
<p class="og-host" data-ke-size="size16">www.nginx.com</p>
</div>
</a></figure>
<figure id="og_1660366928348" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="Tuning NGINX for Performance - NGINX" data-og-description="Learn about some common Linux and NGINX settings that can be tuned to obtain optimal performance." data-og-host="www.nginx.com" data-og-source-url="https://www.nginx.com/blog/tuning-nginx/" data-og-url="https://www.nginx.com/blog/tuning-nginx/" data-og-image="https://scrap.kakaocdn.net/dn/NdxzB/hyPpLzh5Q7/Lbh9bk7XlnB9UcE23vEeKK/img.png?width=500&amp;height=300&amp;face=0_0_500_300,https://scrap.kakaocdn.net/dn/rHtPt/hyPq5QsEsw/836yKCFbLxqYJckHwb6CFK/img.png?width=700&amp;height=1001&amp;face=0_0_700_1001,https://scrap.kakaocdn.net/dn/REM9S/hyPqSKlmvI/kH8k7RWmeyXsqnzVkkv060/img.jpg?width=300&amp;height=300&amp;face=78_65_221_221"><a href="https://www.nginx.com/blog/tuning-nginx/" target="_blank" rel="noopener" data-source-url="https://www.nginx.com/blog/tuning-nginx/">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/NdxzB/hyPpLzh5Q7/Lbh9bk7XlnB9UcE23vEeKK/img.png?width=500&amp;height=300&amp;face=0_0_500_300,https://scrap.kakaocdn.net/dn/rHtPt/hyPq5QsEsw/836yKCFbLxqYJckHwb6CFK/img.png?width=700&amp;height=1001&amp;face=0_0_700_1001,https://scrap.kakaocdn.net/dn/REM9S/hyPqSKlmvI/kH8k7RWmeyXsqnzVkkv060/img.jpg?width=300&amp;height=300&amp;face=78_65_221_221');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">Tuning NGINX for Performance - NGINX</p>
<p class="og-desc" data-ke-size="size16">Learn about some common Linux and NGINX settings that can be tuned to obtain optimal performance.</p>
<p class="og-host" data-ke-size="size16">www.nginx.com</p>
</div>
</a></figure>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';"><a href="https://www.aosabook.org/en/nginx.html">The Architecture of Open Source Applications&nbsp;– NGINX</a></span></li>
</ul>
<figure id="og_1660366940337" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="The Architecture of Open Source Applications (Volume 2): nginx" data-og-description="nginx (pronounced &quot;engine x&quot;) is a free open source web server written by Igor Sysoev, a Russian software engineer. Since its public launch in 2004, nginx has focused on high performance, high concurrency and low memory usage. Additional features on top of" data-og-host="www.aosabook.org" data-og-source-url="https://www.aosabook.org/en/nginx.html" data-og-url="https://www.aosabook.org/en/nginx.html" data-og-image=""><a href="https://www.aosabook.org/en/nginx.html" target="_blank" rel="noopener" data-source-url="https://www.aosabook.org/en/nginx.html">
<div class="og-image" style="background-image: url();">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">The Architecture of Open Source Applications (Volume 2): nginx</p>
<p class="og-desc" data-ke-size="size16">nginx (pronounced "engine x") is a free open source web server written by Igor Sysoev, a Russian software engineer. Since its public launch in 2004, nginx has focused on high performance, high concurrency and low memory usage. Additional features on top of</p>
<p class="og-host" data-ke-size="size16">www.aosabook.org</p>
</div>
</a></figure>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/">Socket Sharding in NGINX Release 1.9.1</a></span></p>
<figure id="og_1660366951362" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="Socket Sharding in NGINX OSS Release 1.9.1" data-og-description="Learn how enabling the SO_REUSEPORT socket option, newly supported in NGINX&nbsp;1.9.1, can improve performance by load balancing connections across workers" data-og-host="www.nginx.com" data-og-source-url="https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/" data-og-url="https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/" data-og-image="https://scrap.kakaocdn.net/dn/c45opj/hyPpJg9TPX/kdDJhDqM6tfg4E6KOYQ7Tk/img.png?width=500&amp;height=300&amp;face=0_0_500_300,https://scrap.kakaocdn.net/dn/bgEgD0/hyPpGY19IF/uOITBE9T8U3R6toBSOgCbk/img.png?width=700&amp;height=1001&amp;face=0_0_700_1001,https://scrap.kakaocdn.net/dn/pknuR/hyPqXrlnCJ/oJT679ZZKnwpSSEfvczPq0/img.png?width=595&amp;height=333&amp;face=0_0_595_333"><a href="https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/" target="_blank" rel="noopener" data-source-url="https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/c45opj/hyPpJg9TPX/kdDJhDqM6tfg4E6KOYQ7Tk/img.png?width=500&amp;height=300&amp;face=0_0_500_300,https://scrap.kakaocdn.net/dn/bgEgD0/hyPpGY19IF/uOITBE9T8U3R6toBSOgCbk/img.png?width=700&amp;height=1001&amp;face=0_0_700_1001,https://scrap.kakaocdn.net/dn/pknuR/hyPqXrlnCJ/oJT679ZZKnwpSSEfvczPq0/img.png?width=595&amp;height=333&amp;face=0_0_595_333');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">Socket Sharding in NGINX OSS Release 1.9.1</p>
<p class="og-desc" data-ke-size="size16">Learn how enabling the SO_REUSEPORT socket option, newly supported in NGINX&nbsp;1.9.1, can improve performance by load balancing connections across workers</p>
<p class="og-host" data-ke-size="size16">www.nginx.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - <a href="https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/" target="_blank" rel="noopener">Inside NGINX: How We Designed for Performance &amp; Scale</a></span></p>
                        </div>
                        <br>
                        <div class="tags"></div>
                    </div>
                    
                </div>
            </div>
        </main>
    </div>
</div>


</body>