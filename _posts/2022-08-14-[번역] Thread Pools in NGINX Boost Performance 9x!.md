---
layout:       post
title:        "[번역] Thread Pools in NGINX Boost Performance 9x!"
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx가 비동기, 이벤트 드리븐을 사용한다. 따라서 전통적인 서버 아키텍처처럼 매 요청마다 그에 상응하는 프로세스나 스레드를 생성하는 대신 여러 커넥션과 요청들을 하나의 워커 프로세스에서 처리한다. 이런 동작 과정을 위해 Nginx는 non-blocking 형태의 소켓과<a href="https://man7.org/linux/man-pages/man7/epoll.7.html" target="_blank" rel="noopener"> epoll</a>, <a href="https://www.freebsd.org/cgi/man.cgi?query=kqueue" target="_blank" rel="noopener">kqueue</a>와 같은 효율적인 방법을 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx는 프로세스 갯수가 적고 정적이기 떄문에 메모리 낭비가 적고 CPU 주기가 컨텍스트 스위칭으로 낭비되지 않는다. 이러한 접근법의 이점은 Nginx로 증명되었다. Nginx는 수백만개의 동시 요청과 스케일을 무리없이 감당한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하지만 비동기, 이벤트 드리븐 방식도 문제가 존재한다. 바로 blocking이다. 안타깝게도 많은 서드파티 모듈들은 blocking call을 사용하고 있다. 그리고 사용자들은 이런 단점들을 인식하지 못한다. Blocking 연산은 Nginx 퍼포먼스를 저하시키므로 반드시 방지해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 현재 Nginx의 코드로는 모든 blocking 연산을 비할 수 없다. 이를 해결하기 위해 새로운 "thread pool" 매커니즘이 <a href="https://hg.nginx.org/nginx/rev/466bd63b63d1?_ga=2.29225978.773025756.1660218315-2056848361.1660218315" target="_blank" rel="noopener">Nginx 버전 1.7.11</a>과 <a href="https://www.nginx.com/blog/nginx-plus-r7-released/#thread-pools" target="_blank" rel="noopener">Nginx Plus Release 7</a> 부터 적용되었다. 이 thread pool이 무엇인지, 어떠게 사용되는지는 뒤에서 다루자. 우선 현재 Nginx가 가지고 있는 문제점들을 살펴보자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;<i> Nginx Plus R7에 대해 알고 싶다면 <a href="https://www.nginx.com/blog/nginx-plus-r7-released/" target="_blank" rel="noopener">Announcing NGINX Plus R7</a>을 참고하자</i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i>&nbsp; NGINX Plus R7의 새로운 기능을 자세히 알고 싶다면 다음 글들을 참고하자</i></span></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';"><i><a href="https://www.nginx.com/blog/http2-r7/">HTTP/2 Now Fully Supported in NGINX&nbsp;Plus</a></i></span></li>
<li><span style="font-family: 'Noto Serif KR';"><i><a href="https://www.nginx.com/blog/socket-sharding-nginx-release-1-9-1/">Socket Sharding in NGINX</a></i></span></li>
<li><span style="font-family: 'Noto Serif KR';"><i><a href="https://www.nginx.com/blog/dashboard-r7">The New NGINX&nbsp;Plus Dashboard in Release&nbsp;7</a></i></span></li>
<li><span style="font-family: 'Noto Serif KR';"><i><a href="https://www.nginx.com/blog/tcp-load-balancing-r7">TCP Load Balancing in NGINX&nbsp;Plus&nbsp;R7</a></i></span></li>
</ul>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>The Problem</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx가 가진 문제점에 대해 더 잘 이해하기 위해 Nginx의 동작 방식을 살펴보자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 통상적으로, Nginx는 이벤트 핸들러이다. 이 핸들러는 커널로부터 오는 커넥션에서 발생한 이벤트들과 관련된 정보들을 받는 컨트롤러다. 이런 정보들을 가지고 운영체제에게 어떤 일을 해야 하는지를 알리기 위해 운영체제에게 명령어를 준다. 사실상 Nginx가 운영체제를 조정해 모든 일을 하고, 운영체제는 그처 바이트를 읽고 보내는 일만 한다. 따라서 Nginx는 적시에 빠르게 대응해야 한다.&nbsp;</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_1.png">
    </span>
    <figcaption>워커 프로세스는 커널로부터 이벤트를 수신하고 처리한다.</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 이벤트는 타임아웃, 소켓이 읽기또는 쓰기 준비 상태 중임을 알리는 알림, 에러 발생 알림일 수 있다. Nginx는 대량의 이벤트들을 받고 하나씩 처리하며 각 이벤트에 필요한 작업을 한다. 따라서 모든 작업은 단일 스레드 내의 큐상에서 간단한 루프로 완료된다. Nginx는 큐에서 이벤트를 꺼내와 소켓을 읽거나 씀음으로써 반응한다. 대개의 경우, 이 작업은 매우 빠르며 Nginx는 큐에 있는 모든 이벤트를 순식간에 처리한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_2.png">
    </span>
    <figcaption>단일 스레드에의 하나의 루프에서 모든 처리가 관리된다.</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하지만, 엄청나게 무거운 연산이 발생한다면 무슨일이 발생할까? 전체 이벤트 프로세싱 사이클이 연산 종료까지 멈춰있을 것이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 따라서 blocking 연산은 이벤트를 관여하는 사이클 연산을 일정 시간 멈추게 하는 것이라 정의하자. 연산은 여러 이유로 blocking될 수 있다. 그리고 이련 연산들을 처리할 때는 사용가능한 시스템 리소스가 존재하고 큐에 존재하는 이벤트들이 이 리소스들을 사용할 수 있어도 워커 프로세스가 해당 이벤트에 대한 기타 연산을 할 수 없으며 다른 이벤트 역시 처리할 수 없다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 판매원 한명과 여러명의 고객이 매장에 있다고 해보자. 고객들은 줄(큐 처럼)서있다. 이 줄의 맨 앞 고객이 판매원에게 매장에 존재하지 않는 물건을 요구했다 하자. 그러면 판매원은 창고에 물건을 가지러 가는 동안 고객들은 줄을 서서 대기해야 한다. 이는 고객 경험을 크게 저하시킬 것이다. 고객들이 기다리는 시간은 물건을 창고에서 찾아 가져오는 시간 만큼 들어나는 반면 다른 고객들이 사야하는 물건은 스토어에 존재할 수도 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_3.png">
    </span>
    <figcaption>고객들이 하나의 고객 주문이 완료되길 기다리고 있다</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 메모리에 캐싱되지 않은(스토어에 존재하지 않는) 파일 을 읽어야 하는 요청이 왔을 때 디스크에서(창고에서) 파일을 읽어와야 하기 때문에 Nginx에서도 비슷한 상황이 발생한다. 하드드라이버는 느리다, 큐에서 대기중인 요청들은 하드드라이버를 조회하지 않을 수도 있다. 그럼에도 어쩔 수 없이 대기하고 있다. 이때문에 레이턴시는 증가하고 리소스를 전부 활용하지 못한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_4.png">
    </span>
    <figcaption>하나의 blocking 연산은 뒤따라오는 연산들을 일정 시간 지연시킨다</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 일부 운영체제의 경우 파일 읽기, 전송을 위한 비동기 인터페이스를 제공하고 Nginx는 이 인터페이스를 사용할 수 있다. FreeBSD가 이 예시에 해당한다. 하지만, 리눅스 환경도 같을 것이라는 보장을 할 수 없다. 비록 리눅스는 파일 읽기를 위한 비동기 인터페이스를 제공하지만, 중대한 문제점들을 가지고 있다. 이 문제들 중에는 파일 접근과 버퍼에 대한 정렬 요구사항이 있지만 Nginx는 이를 잘 처리하고 있다. 하지만 이 비동기 인터페이스가 0_DIRECT flag를 파일 디스크립터에 설정하는 것을 필요로 하는 것이 문제가 된다. 즉, 파일에 액세스할 때 메모리에 존재하는 캐시를 우회해 하드 디스크 로드가 증가한다. 이는 많은 경우를 최적화가 되지 않는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 문제들을 해결하기 위해 thread pool이 Nginx 1.7.11과 Nginx Plus Release 7에서 소개되었다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 thread pool과 동작 방식에 대해 살펴보자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Thread Pools</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>다시 위에서 예시로 들었던 판매원 상황으로 돌아가 보자. 판매원이 상황을 개선하기 위해 배달 서비스를 고용했다 해보자. 이제 고객이 창고에 있는 물건을 필요로 할 때마다 판매원은 배달 서비스에게 이를 요청하면 된다. 그러면 배달 서비스가 물건을 창고로 가지러 가는 사이에 판매원은 다른 고객의 주문을 처리할 수 있다. 이제 원하는 상품이 스토어에 존재하지 않는 고객들만 배달을 기다리면 되고 다른 고객들은 원하는 물건을 즉시 받을 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_5.png">
    </span>
    <figcaption>배달 서비스를 사용해 큐를 block하지 않는다.</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 예시를 Nginx에 빗대어 보면, thread pool이 배달 서비스 역할을 한다고 볼 수 있다. Thread pool은 task queue와 task queue를 처리하는 여러개의 스레드로 구성되 있다. 워커 프로세스가 오랜 시간이 요구되는 연산을 해야 할 때, 직접 이 연산을 처리하는 대산 풀에 존재하는 큐에 작업을 배치해 사용 가능한 스레드에서 작업을 수행하고 처리한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_6.png">
    </span>
    <figcaption>워커 프로세스가 blocking 연산을 스레드 풀에게 넘긴다</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 방식은 큐가 하나 더 존재하는 것과 같다. 하지만 thread pool에 있는 task queue 속도는 특정 리소스에 의해 제한된다. 드라이브가 데이터를 생성하는 속도보다 더 빠르게 데이터를 읽어올 수 없다. 이제, 적어도 드라이브가 다른 이벤트들의 처리를 지연시키진 않는다. 오직 드라이브에 접근해야 하는 요청들만 대기하면 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 디스크에서 데이터를 읽어오는 연산은 blocking 연산의 대표적인 예시이다. 하지만, Nginx에서의 thread pool 구현은 주된 작업 처리 사이클에 적절하지 않은 작업들에 사용될 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 현재는 오직 3가지 기본 연산에만 thread pool로 연산을 넘기고 있다. 대부분의 운영체제에 존재하는 read() 시스템 호출, 리눅스에 존재하는 sendfile(), 임시 파일들(캐시 등)을 쓰기 위해 리눅스에서 사용되는 aio_write(). 앞으로도 thread pool 구현에 대한 테스트와 벤치마킹을 지속할 것이며, 명확한 이점이 존재한다면 앞으로의 버전에서 다른 연산들 역시 thread pool에 넘길 수 있게 할것이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; aio_write() 시스템 호출의 thread pool 지원은 <a href="https://hg.nginx.org/nginx/rev/fc72784b1f52?_ga=2.1103863.773025756.1660218315-2056848361.1660218315" target="_blank" rel="noopener">Nginx 1.9.13</a>과 <a href="https://www.nginx.com/blog/nginx-plus-r9-released/#aio-write" target="_blank" rel="noopener">Nginx Plus R9</a>에서 추가되었다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Benchmarking</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>이제 이론에서 실전으로 넘어가 보자. Thread pool을 사용하는 것의 효율을 입증하기 위해 최악의 blocking 연산과 non-blocking 연산을 섞은 종합적인 벤치마크를 해보자.&nbsp;&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 벤치마크로 원하는 결과를 얻기 위해 메모리 만으로는 감당할 수 없는 양의 데이터 셋이 필요하다. 48GB 램을 가지고 있는 머신에서 4MB 파일로 256GB의 랜덤 데이털를 생성하고 Nginx 1.9.0이 이를 제공하게 벤치마크를 구성했다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx 환경 설정은 다음과 같다.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">worker_processes&nbsp;<span style="color: #0099cc;">16</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">events&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;accept_mutex&nbsp;off;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">http&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;include&nbsp;mime.types;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;default_type&nbsp;application<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>octet<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>stream;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;access_log&nbsp;off;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;sendfile&nbsp;on;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;sendfile_max_chunk&nbsp;512k;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;server&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;listen&nbsp;<span style="color: #0099cc;">8000</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;root&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>storage;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 환경 설정에서 볼 수 있듯이, 퍼포먼스 향상을 위해 일부 설정을 적용했다. <a href="https://nginx.org/en/docs/http/ngx_http_log_module.html?&amp;_ga=2.241185988.773025756.1660218315-2056848361.1660218315#access_log" target="_blank" rel="noopener">loggin</a>과 <a href="https://nginx.org/en/docs/ngx_core_module.html?&amp;_ga=2.241185988.773025756.1660218315-2056848361.1660218315#accept_mutex" target="_blank" rel="noopener">accept_mutex</a>를 비활성화 했으며, <a href="https://nginx.org/en/docs/http/ngx_http_core_module.html?&amp;_ga=2.269015351.773025756.1660218315-2056848361.1660218315#sendfile" target="_blank" rel="noopener">sendfile</a>을 허용하고, <a href="https://nginx.org/en/docs/http/ngx_http_core_module.html?&amp;_ga=2.269015351.773025756.1660218315-2056848361.1660218315#sendfile_max_chunk" target="_blank" rel="noopener">sendfile_max_chunk</a>를 설정했다. sendfile_max_chunk를 설정하면 Nginx가 모든 파일을 한번에 보내는 대신 512KB(위 설정에서 sendfile_max_chunk 양을 512KB로 설정했다)씩 잘라서 보내기 떄문에&nbsp; blocking 연산인 sendfile()에 사용하는 최대 시간을 줄일 수 있다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 해당 Nginx가 설치된 컴퓨터는 Intel Xeon E5645(12 core, 24 HT-thread) 프로세스와 10-Gbps 네트워크 인터페이스를 가지고 있다.&nbsp; 디스크 서브시스템은 Western Digital WD1003FBYX 하드 드라이브로 구성되 있으며 RAID10 array로 배치되있다. 운영체제는 Ubuntu server 14.04.1 LTS를 사용하고 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/W+uyiOyXrV0gVGhyZWFkIFBvb2xzIGluIE5HSU5YIEJvb3N0IFBlcmZvcm1hbmNlIDl4IQ==/img_7.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 클라이언트는 두 개의 머신으로 이루어져 있다. 그 중 하나에서는 <a href="https://github.com/wg/wrk" target="_blank" rel="noopener">wrk</a>가 Lua 스크립트를 사용해 로드를 생성한다. 이 스크립트는 200개의 동시 커넥션을 사용해 서버로부터 파일들을 무작위로 요청한다. 각 요청은 캐시 누락, disk에서의 blocking 읽기가 발생할 수 있다. 여기선 이 부하를 랜덤(random) 부하 라고 부르자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 또 다른 클라이언트 머신에서는 위에서 언급한 wrk의 복사본을 사용한다. 이 복사본은 50개의 동시 커넥션을 사용해 같은 파일을 여러번 요청한다. 이 파일은 빈번히 접근되기 때문에 항상 메모리에 존재하게 된다. 통상적인 상황에서는 Nginx가 이 요청을 빠르게 처리할 것이다. 하지만 만약 워커 프로세스가 다른 요청들에 의해 blocking 된 상황이라면 성능이 저하된다. 이 부하를 정적(constant) 부하라 하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 퍼포먼스는 ifstat를 사용해 서버 시스템의 처리량을 측정하고 두 번쨰 클라이언트에서 wrk의 결과를 받아 측정할 것이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; thread pool 사용 없이 실행한 첫 번째 실행은 다음과 같은 결과가 나왔다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">%&nbsp;ifstat&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>bi&nbsp;eth2</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">eth2</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Kbps&nbsp;in&nbsp;&nbsp;Kbps&nbsp;out</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">5531.</span><span style="color: #0099cc;">24</span>&nbsp;&nbsp;<span style="color: #0099cc;">1.</span>03e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">4855.</span><span style="color: #0099cc;">23</span>&nbsp;&nbsp;<span style="color: #0099cc;">812922.</span><span style="color: #0099cc;">7</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">5994.</span><span style="color: #0099cc;">66</span>&nbsp;&nbsp;<span style="color: #0099cc;">1.</span>07e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">5476.</span><span style="color: #0099cc;">27</span>&nbsp;&nbsp;<span style="color: #0099cc;">981529.</span><span style="color: #0099cc;">3</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">6353.</span><span style="color: #0099cc;">62</span>&nbsp;&nbsp;<span style="color: #0099cc;">1.</span>12e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">5166.</span><span style="color: #0099cc;">17</span>&nbsp;&nbsp;<span style="color: #0099cc;">892770.</span><span style="color: #0099cc;">3</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">5522.</span><span style="color: #0099cc;">81</span>&nbsp;&nbsp;<span style="color: #0099cc;">978540.</span><span style="color: #0099cc;">8</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">6208.</span><span style="color: #0099cc;">10</span>&nbsp;&nbsp;<span style="color: #0099cc;">985466.</span><span style="color: #0099cc;">7</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">6370.</span><span style="color: #0099cc;">79</span>&nbsp;&nbsp;<span style="color: #0099cc;">1.</span>12e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">6123.</span><span style="color: #0099cc;">33</span>&nbsp;&nbsp;<span style="color: #0099cc;">1.</span>07e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 결과에서 확인할 수 있듯이 이 환경 설정으로는 총 1Gbps의 트래픽을 생성한다. top 명령어를 통해 모든 워커 프로세스들은 대부분의 연산 시간을 blocking I/O에 소비하는 것을 알 수 있다.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">23</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">24</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">25</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">26</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">27</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">top&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">10</span>:<span style="color: #0099cc;">40</span>:<span style="color: #0099cc;">47</span>&nbsp;up&nbsp;<span style="color: #0099cc;">11</span>&nbsp;days,&nbsp;&nbsp;<span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">32</span>,&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;user,&nbsp;&nbsp;load&nbsp;average:&nbsp;<span style="color: #0099cc;">49.</span><span style="color: #0099cc;">61</span>,&nbsp;<span style="color: #0099cc;">45.</span><span style="color: #0099cc;">77</span>&nbsp;<span style="color: #0099cc;">62.</span><span style="color: #0099cc;">89</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Tasks:&nbsp;<span style="color: #0099cc;">375</span>&nbsp;total,&nbsp;&nbsp;<span style="color: #0099cc;">2</span>&nbsp;running,&nbsp;<span style="color: #0099cc;">373</span>&nbsp;sleeping,&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;stopped,&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;zombie</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">%Cpu(s):&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;us,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;sy,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;ni,&nbsp;<span style="color: #0099cc;">67.</span><span style="color: #0099cc;">7</span>&nbsp;id,&nbsp;<span style="color: #0099cc;">31.</span><span style="color: #0099cc;">9</span>&nbsp;wa,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;hi,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;si,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;st</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">KiB&nbsp;Mem:&nbsp;&nbsp;<span style="color: #0099cc;">49453440</span>&nbsp;total,&nbsp;<span style="color: #0099cc;">49149308</span>&nbsp;used,&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">304132</span>&nbsp;free,&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">98780</span>&nbsp;buffers</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">KiB&nbsp;Swap:&nbsp;<span style="color: #0099cc;">10474236</span>&nbsp;total,&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20124</span>&nbsp;used,&nbsp;<span style="color: #0099cc;">10454112</span>&nbsp;free,&nbsp;<span style="color: #0099cc;">46903412</span>&nbsp;cached&nbsp;Mem</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;PID&nbsp;USER&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PR&nbsp;&nbsp;NI&nbsp;&nbsp;&nbsp;&nbsp;VIRT&nbsp;&nbsp;&nbsp;&nbsp;RES&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SHR&nbsp;S&nbsp;&nbsp;%CPU&nbsp;%MEM&nbsp;&nbsp;&nbsp;&nbsp;TIME<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;COMMAND</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4639</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28152</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">496</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">7</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">17</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4632</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28196</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">11</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4633</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28324</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">540</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">11</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4635</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28136</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">480</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">12</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4636</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28208</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">14</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4637</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28208</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">10</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4638</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28204</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">12</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4640</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28324</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">540</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">13</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4641</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28324</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">540</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">13</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4642</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28208</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">11</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4643</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28276</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">29</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4644</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28204</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">11</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4645</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28204</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">17</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4646</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28204</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">12</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4647</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28208</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">532</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">17</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4631</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">756</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">252</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">00</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4634</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">47180</span>&nbsp;&nbsp;<span style="color: #0099cc;">28208</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">536</span>&nbsp;D&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">11</span>&nbsp;nginx<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4648</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">25232</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1956</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1160</span>&nbsp;R&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">08</span>&nbsp;top</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">25921</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">121956</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2232</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1056</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">97</span>&nbsp;sshd</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">25923</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">40304</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4160</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2208</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">53</span>&nbsp;zsh</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 경우 CPU가 대부분의 시간 동한 유휴 상태이며 디스크 하위 시스템에 의해 트래픽이 제한되었다. wrk의 결과 역시 매우 낮게 나왔다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Running&nbsp;1m&nbsp;test&nbsp;@&nbsp;http:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">192.</span><span style="color: #0099cc;">0.</span><span style="color: #0099cc;">2.</span><span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">8000</span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">1</span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">1</span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #0099cc;">12</span>&nbsp;threads&nbsp;and&nbsp;<span style="color: #0099cc;">50</span>&nbsp;connections</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Thread&nbsp;Stats&nbsp;&nbsp;&nbsp;Avg&nbsp;&nbsp;&nbsp;&nbsp;Stdev&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Max&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;Stdev</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;Latency&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">7.</span>42s&nbsp;&nbsp;<span style="color: #0099cc;">5.</span>31s&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">24.</span>41s&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">74.</span><span style="color: #0099cc;">73</span>%</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;Req<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>Sec&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">15</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">36</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1.</span><span style="color: #0099cc;">00</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">84.</span><span style="color: #0099cc;">62</span>%</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #0099cc;">488</span>&nbsp;requests&nbsp;in&nbsp;<span style="color: #0099cc;">1.</span>01m,&nbsp;<span style="color: #0099cc;">2.</span>01GB&nbsp;<span style="color: #066de2;">read</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Requests<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>sec:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">8.</span><span style="color: #0099cc;">08</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Transfer<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>sec:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">34.</span>07MB</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 파일들은 메모리에서 제공되어야 했다. 위 결과에서 볼 수 있는 대량의 레이턴시들은 워커 프로세스들이 첫 번째 클라이언트에서 온 200개의 커넥션에 의해 생성된 드라이브에서 파일을 읽어오기 때문에 발생했다. 이로 인해 제때 요청들을 처리할 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 thread pool을 사용해보자. 이를 위해 <a href="https://nginx.org/en/docs/http/ngx_http_core_module.html?&amp;_ga=2.201267176.773025756.1660218315-2056848361.1660218315#aio" target="_blank" rel="noopener">aio</a>를 location 블록에 추가하자.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;root&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>storage;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;aio&nbsp;threads;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 그 후, Nginx 설정을 다시 로드하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 같은 방법으로 실험을 해보면 다음과 같은 결과를 볼 수 있다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">%&nbsp;ifstat&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>bi&nbsp;eth2</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">eth2</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Kbps&nbsp;in&nbsp;&nbsp;Kbps&nbsp;out</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">60915.</span><span style="color: #0099cc;">19</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">59978.</span><span style="color: #0099cc;">89</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">60122.</span><span style="color: #0099cc;">38</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">61179.</span><span style="color: #0099cc;">06</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">61798.</span><span style="color: #0099cc;">40</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">57072.</span><span style="color: #0099cc;">97</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>50e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">56072.</span><span style="color: #0099cc;">61</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">61279.</span><span style="color: #0099cc;">63</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">61243.</span><span style="color: #0099cc;">54</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>51e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">59632.</span><span style="color: #0099cc;">50</span>&nbsp;&nbsp;<span style="color: #0099cc;">9.</span>50e<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0099cc;">06</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 서버는 9.5Gbps의 트래픽을 생성한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Nginx가 더 많은 트래픽을 생성할 수도 있지만, 네트워크 최대 용량에 도달했다. 따라서 이번 테스트에서는 Nginxrk 네트워크 인터페이의 한계로 인해 퍼포먼스가 한계에 붙이쳤다고 할 수 있다. 워커 프로세스들은 대부분의 시간을 sleeping 상태나 새로운 이벤트 대기에 사용한다(top의 S 상태에 있다).</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">23</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">24</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">25</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">26</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">27</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">top&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">10</span>:<span style="color: #0099cc;">43</span>:<span style="color: #0099cc;">17</span>&nbsp;up&nbsp;<span style="color: #0099cc;">11</span>&nbsp;days,&nbsp;&nbsp;<span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">35</span>,&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;user,&nbsp;&nbsp;load&nbsp;average:&nbsp;<span style="color: #0099cc;">172.</span><span style="color: #0099cc;">71</span>,&nbsp;<span style="color: #0099cc;">93.</span><span style="color: #0099cc;">84</span>,&nbsp;<span style="color: #0099cc;">77.</span><span style="color: #0099cc;">90</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Tasks:&nbsp;<span style="color: #0099cc;">376</span>&nbsp;total,&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;running,&nbsp;<span style="color: #0099cc;">375</span>&nbsp;sleeping,&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;stopped,&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;zombie</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">%Cpu(s):&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">2</span>&nbsp;us,&nbsp;&nbsp;<span style="color: #0099cc;">1.</span><span style="color: #0099cc;">2</span>&nbsp;sy,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;ni,&nbsp;<span style="color: #0099cc;">34.</span><span style="color: #0099cc;">8</span>&nbsp;id,&nbsp;<span style="color: #0099cc;">61.</span><span style="color: #0099cc;">5</span>&nbsp;wa,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;hi,&nbsp;&nbsp;<span style="color: #0099cc;">2.</span><span style="color: #0099cc;">3</span>&nbsp;si,&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;st</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">KiB&nbsp;Mem:&nbsp;&nbsp;<span style="color: #0099cc;">49453440</span>&nbsp;total,&nbsp;<span style="color: #0099cc;">49096836</span>&nbsp;used,&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">356604</span>&nbsp;free,&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">97236</span>&nbsp;buffers</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">KiB&nbsp;Swap:&nbsp;<span style="color: #0099cc;">10474236</span>&nbsp;total,&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">22860</span>&nbsp;used,&nbsp;<span style="color: #0099cc;">10451376</span>&nbsp;free,&nbsp;<span style="color: #0099cc;">46836580</span>&nbsp;cached&nbsp;Mem</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;PID&nbsp;USER&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PR&nbsp;&nbsp;NI&nbsp;&nbsp;&nbsp;&nbsp;VIRT&nbsp;&nbsp;&nbsp;&nbsp;RES&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SHR&nbsp;S&nbsp;&nbsp;%CPU&nbsp;%MEM&nbsp;&nbsp;&nbsp;&nbsp;TIME<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;COMMAND</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4654</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309708</span>&nbsp;&nbsp;<span style="color: #0099cc;">28844</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">596</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">9.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">08.</span><span style="color: #0099cc;">65</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4660</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309748</span>&nbsp;&nbsp;<span style="color: #0099cc;">28920</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">596</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">6.</span><span style="color: #0099cc;">6</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">14.</span><span style="color: #0099cc;">82</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4658</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28424</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">520</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">40</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4663</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28476</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">572</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">32</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4667</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309584</span>&nbsp;&nbsp;<span style="color: #0099cc;">28712</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">588</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3.</span><span style="color: #0099cc;">7</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">05.</span><span style="color: #0099cc;">19</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4656</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28476</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">572</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">84</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4664</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28428</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">524</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">29</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4652</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28476</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">572</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">46</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4662</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309552</span>&nbsp;&nbsp;<span style="color: #0099cc;">28700</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">596</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2.</span><span style="color: #0099cc;">7</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">05.</span><span style="color: #0099cc;">92</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4661</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309464</span>&nbsp;&nbsp;<span style="color: #0099cc;">28636</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">596</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">59</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4653</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28476</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">572</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1.</span><span style="color: #0099cc;">7</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">70</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4666</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28428</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">524</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">63</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4657</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309584</span>&nbsp;&nbsp;<span style="color: #0099cc;">28696</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">592</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">64</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4655</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">30958</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">28476</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">572</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">7</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">02.</span><span style="color: #0099cc;">81</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4659</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28468</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">564</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">20</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4665</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">309452</span>&nbsp;&nbsp;<span style="color: #0099cc;">28476</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">572</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">71</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">5180</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">25232</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1952</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1156</span>&nbsp;R&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">45</span>&nbsp;top</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4651</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20032</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">752</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">252</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">00</span>&nbsp;nginx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">25921</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">121956</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2176</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1000</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">01.</span><span style="color: #0099cc;">98</span>&nbsp;sshd</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">25923</span>&nbsp;vbart&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">40304</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3840</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2208</span>&nbsp;S&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>:<span style="color: #0099cc;">00.</span><span style="color: #0099cc;">54</span>&nbsp;zsh</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; CPU 자원이 아직 많이 남아있는 것을 알 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; wrk 결과는 다음과 같다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Running&nbsp;1m&nbsp;test&nbsp;@&nbsp;http:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">192.</span><span style="color: #0099cc;">0.</span><span style="color: #0099cc;">2.</span><span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">8000</span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">1</span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">1</span><span style="color: #a71d5d;">/</span><span style="color: #0099cc;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #0099cc;">12</span>&nbsp;threads&nbsp;and&nbsp;<span style="color: #0099cc;">50</span>&nbsp;connections</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Thread&nbsp;Stats&nbsp;&nbsp;&nbsp;Avg&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stdev&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Max&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;Stdev</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;Latency&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">226.</span>32ms&nbsp;&nbsp;<span style="color: #0099cc;">392.</span>76ms&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1.</span>72s&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">93.</span><span style="color: #0099cc;">48</span>%</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;Req<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>Sec&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20.</span><span style="color: #0099cc;">02</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">10.</span><span style="color: #0099cc;">84</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">59.</span><span style="color: #0099cc;">00</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">65.</span><span style="color: #0099cc;">91</span>%</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #0099cc;">15045</span>&nbsp;requests&nbsp;in&nbsp;<span style="color: #0099cc;">1.</span>00m,&nbsp;<span style="color: #0099cc;">58.</span>86GB&nbsp;<span style="color: #066de2;">read</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Requests<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>sec:&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">250.</span><span style="color: #0099cc;">57</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Transfer<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>sec:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0.</span>98GB</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4MB 파일을 서비스하는 평균 시간이 7.42초에서 226.32 밀리 세컨드(33배 더 적다)로 줄어들었다. 초당 처리하는 요청 건수 또한 31배 늘었다(8건 -&gt; 250건)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 결과는 워커 프로세스가 읽기에서 blocking 되있는 동안, 요청들이 더이상 이벤트 큐에서 프로세싱을 기다리지 않고, 여유분의 thread 들에 의해 처리됨을 의미한다. 디스크 서브시스템을 사용해 첫 번째 클라이언트의 랜덤 부하를 처리할 수 있고 Nginx는 나머지 CPU 자원과 네트워크 용량으로 메모리에서 두 번째 클라이언트 요청을 처리한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Still Not a Silver Bullet</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>위 벤치마크에서 thread pool 사용이 퍼포먼스 향상을 이끈 이유는 대부분의 파일 전송과 읽기 연산이 하드드라이브에서 발생하지 않기 떄문이다. 만약 RAM에 데이터셋을 저장할 수 있는 충분한 공간이 존재한다면, 운영체제는 자주 사용하는 파일들을 캐싱할 것이다. 이를 page-cache라 부른다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; page-cache는 대부분의 일반적 상황에서 Nginx의 퍼포먼스를 좋게 만든다. page-cache에서 읽어오는 동작은 빠르며 blocking도 아니다. 즉, thread pool로 작업을 주는 것은 오버헤드가 존재한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 따라서 만약 충분한 양의 RAM이 존재하고 데이터셋이 크지 않다면, Nginx는 thread pool 없이도 충분히 최적화된 방법을 사용하고 있다고 볼 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Thread pool에게 읽기 연산을 전가하는 것은 특정 테스크에만 적용할 수 있는 테크닉이다. 자주 요청으로 들어오는 컨텐트들의 용량이 운영체제의 VM cache를 초과할 때 사용할 수 있다. 부하가 높은 Nginx 기반 스트리밍 서버가 이 경우에 해당한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 읽기 연산을 thread pool로 전가하는 작업을 개선할 수 있으면 좋겠다. 이를 위해 필요한 파일들이 메모리에 존재하는지를 알아내는 효율적인 방법이며 후자의 경우(위 벤치마킹에서 정적 부하의 경우)만 다른 스레드에 테스크를 전가해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다시 판매원 예시로 돌아가 보자. 현재 판매원은 고객이 요청한 아이템이 스토어에 존재하는지 알지 못한다. 따라서 모든 주문을 배달 서비스에 넘기거나 스스로 요청을 처리한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 운영체제에 파일들이 메모리에 존재하는 지를 판단할 수 있는 기능이 없다는 것이 문제의 원인이다. 이 기능을 <a href="https://lwn.net/Articles/371538/" target="_blank" rel="noopener">fincore()</a> 시스템 호출로 201년에 리눅스에 추가하려 했지만 실패했다. 그 후 이 기능을 RFW_NONBLOCK 플래스와 preadv2() 시스템 호출로서 적용하려는 시도가 존재했었다(자세한 사항은 <a href="https://lwn.net/Articles/612483/" target="_blank" rel="noopener">Nonblocking buffered file read operations</a>와 <a href="https://lwn.net/Articles/636967/" target="_blank" rel="noopener">Asynchronous buffered read operations</a>를 참고하자). 이 패치들이 적용 될지는 아직 불투명하다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 한편으로는, FreeBSD 유저들은 이 문제에 대해 고민하지 않아도 된다. FreeBSD는 이미 충분히 좋은 파일 읽기 비동기 인터페이스를 가지고 있다. Free BSD 유저들은 thread pool 대신 이 인터페이스를 사용하면 된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Configuring Thread Pools</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>Thread pool을 사용해서 이익을 취할 수 있는 경우가 있다면, 다음과 같은 설정을 사용하면 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 설정은 쉽고 유연하다. 우선 Nginx 1.7.11 이상의 버전이 필요하다. configure 커멘드에 --with-threads 아규먼트를 함께 사용해 컴파일되야 한다. Nginx Plus를&nbsp; 사용한다면 Release 7 또는 그 이후 버전이 필요하다. 가장 간단한 경우 세팅이 매우 쉽다. 적절한 컨텍스트에 aio threads를 추가하기만 하면 된다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;in&nbsp;the&nbsp;<span style="color: #63a35c;">'http'</span>,&nbsp;<span style="color: #63a35c;">'server'</span>,&nbsp;or&nbsp;<span style="color: #63a35c;">'location'</span>&nbsp;context</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">aio&nbsp;threads;</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이는 thread pool를 사요하기 위한 최소한의 세팅이다. 이 세팅은 다음 세팅을 함축한 것이다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;in&nbsp;the&nbsp;<span style="color: #63a35c;">'main'</span>&nbsp;context</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread_pool&nbsp;default&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">32</span>&nbsp;max_queue<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">65536</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;in&nbsp;the&nbsp;<span style="color: #63a35c;">'http'</span>,&nbsp;<span style="color: #63a35c;">'server'</span>,&nbsp;or&nbsp;<span style="color: #63a35c;">'location'</span>&nbsp;context</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">aio&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>default;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 설정은 default라 불리는 thread pool을 정의한다. Default thread pool은 32개의 워킹 스레드와 최대 65536개의 테스크를 담을 수 있는 테스크 큐를 가지고 있다. 만약 테스트 큐가 감당할 수 있는 테스크 양을 초과한다면 Ngixn는 요청을 reject하고 다음과 같은 로그를 내보낸다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread&nbsp;pool&nbsp;<span style="color: #63a35c;">"NAME"</span>&nbsp;queue&nbsp;overflow:&nbsp;N&nbsp;tasks&nbsp;waiting</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 이 에러는 스레드들&nbsp; 테스트 큐에 테스크가 추가되는 속도만큼 빠르게 테스크를 감당할 수 없을 수도 있다는 것을 의미한다. 큐 사이즈를 증가시켜서 이 문제를 해결할 수 있지만, 증가시켜도 문제가 해결되지 않는다면, 시스템이 그만큼의 요청을 감당할 수 없음을 의미한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 설정에서 볼 수 있듯이 <a href="https://nginx.org/en/docs/ngx_core_module.html?&amp;_ga=2.127400139.773025756.1660218315-2056848361.1660218315#thread_pool" target="_blank" rel="noopener">thread_pool</a>을 사용해 스레드 갯수, 큐의 최대 길이, 특정 thread pool의 이름을 설정할 수 있다. thread_pool을 여러개 설정해서 독립된 thread pool을 여러개 성성하고 서로 다른 목적으로 사용할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;in&nbsp;the&nbsp;<span style="color: #63a35c;">'main'</span>&nbsp;context</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread_pool&nbsp;one&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">128</span>&nbsp;max_queue<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">0</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread_pool&nbsp;two&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">32</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">http&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;server&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>one&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aio&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>one;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>two&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aio&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>two;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;#&nbsp;...</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 max_queue 파라미터를 명시하지 않았다면 기본값인 65536을 사용하게 된다. max_queue의 값으로 0을 사용한다면, 설정한 스레드 갯수 만큼 테스크를 감당하게 된다. 즉, 테스크가 큐에서 대기하지 않는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 3개의 하드 드라이브를 사용하는 서버가 있다고 해보자. 이 서버를 백엔드에서 오는 모든 응답을 캐싱하는 chaching proxy로 사용한다 해보자. 예상되는 캐시 데이터의 양은 상요 가능한 램 용량보다 훨씬 크다. 이는 개인 용도의 CDN을 위한 캐싱 노드다. 이 경우 드라이브에서 최고 성능을 달성하는 것이 가장 중요하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이를 해결하는 한 가지 방법은 RAID 배열을 설정하는 것이다. 이 방식은 장단점이 존재한다.&nbsp;</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">23</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">24</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">25</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">26</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">27</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">28</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">29</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">30</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">31</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">32</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">33</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;We&nbsp;assume&nbsp;that&nbsp;each&nbsp;of&nbsp;the&nbsp;hard&nbsp;drives&nbsp;is&nbsp;mounted&nbsp;on&nbsp;one&nbsp;of&nbsp;these&nbsp;directories:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>mnt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>disk1,&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>mnt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>disk2,&nbsp;or&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>mnt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>disk3</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;in&nbsp;the&nbsp;<span style="color: #63a35c;">'main'</span>&nbsp;context</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread_pool&nbsp;pool_1&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">16</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread_pool&nbsp;pool_2&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">16</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">thread_pool&nbsp;pool_3&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">16</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">http&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;proxy_cache_path&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>mnt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>disk1&nbsp;levels<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">2</span>&nbsp;keys_zone<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>cache_1:256m&nbsp;max_size<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>1024G&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;use_temp_path<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>off;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;proxy_cache_path&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>mnt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>disk2&nbsp;levels<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">2</span>&nbsp;keys_zone<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>cache_2:256m&nbsp;max_size<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>1024G&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;use_temp_path<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>off;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;proxy_cache_path&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>mnt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>disk3&nbsp;levels<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">1</span>:<span style="color: #0099cc;">2</span>&nbsp;keys_zone<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>cache_3:256m&nbsp;max_size<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>1024G&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;use_temp_path<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>off;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;split_clients&nbsp;$request_uri&nbsp;$disk&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">33.</span><span style="color: #0099cc;">3</span>%&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">33.</span><span style="color: #0099cc;">3</span>%&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">*</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;server&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#&nbsp;...</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_pass&nbsp;http:<span style="color: #999999;">//backend;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_cache_key&nbsp;$request_uri;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_cache&nbsp;cache_$disk;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;aio&nbsp;threads<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>pool_$disk;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sendfile&nbsp;on;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 설정에서 thread_pool은 각 디스크에 독립된 전용 thread pool을 정의한다. proxy_cache_path는 각 디스크에 독립된 전용 캐시를 정의한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; <a href="https://nginx.org/en/docs/http/ngx_http_split_clients_module.html?_ga=2.132135880.773025756.1660218315-2056848361.1660218315" target="_blank" rel="noopener">split_clients</a> 모듈은 캐시들 사이에서 로드밸런싱을 위해 사용된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; use_temp_path=off 파라미터는 관련된 캐시 데이터가 위치한 디렉터리들에에 임시 파일들을 저장할 것을 의미한다. 이를 위해선 캐시를 업데이트 할 때 응답 데이터를 드라이브 간에서 복사하는 것을 피해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이런 세팅은 드라이브들이 동시에 독립적으로 분리된 thread pool들과 상호작용하기 때문에&nbsp;현재의 디스크 서브시스템을 최고의 퍼포먼스로 사용할 수 있다. 각 드라이브에는 16개의 독립된 스레드들과 파일 읽기, 전송을 위한 전용 테스트 큐가 제공된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 예시는 Nginx가 얼마나 유연하게 하드웨어에 특화될 수 있는지를 보여준다. 이는 Nginx 사용자가 Nginx에게 머신, 데이터셋과 상호작용할 수 있는 가장 좋은 방법을 알려주는 것과 같다. 또 한, Nginx를 세부적으로 튜닝함으로써 소프트웨어, 운영체제, 하드웨어가 모든 시스템 리소스를 가능한 효율적인 방법으로 사용하게 하기 위해 최적화 시킬 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - <a href="https://www.nginx.com/blog/thread-pools-boost-performance-9x/#thread_pool" target="_blank" rel="noopener">Thread Pools in NGINX Boost Performance 9x!</a></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></p>
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