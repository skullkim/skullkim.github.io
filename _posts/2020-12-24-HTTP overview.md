---
layout:       post
title:        "HTTP overview"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- HTTP
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
                            <p>&nbsp; HTTP(Hypertext Transfer Protocol)은 애플리케이션 계층의 프로토콜로 hypertext 문서들을 전속하는게 사용된다. 이는 웹 클라이언트와 웹 서버사이의 커뮤니케이션을 위해 고안되었지만 다른 용도로도 사용이 가능하다. HTTP는 client-server model을 따르기게 클라이언트가 커넥션을 열고 요청을 만든 후 응답이 올때까지 기다린다. HTTP는 stateless라는 특징을 가지고 있다. statless는 서버가 요청과 응답 간의 어떠한 데이터도 저장하지 않는다는 의미이다. HTTP는 TCP/IP기반이지만 신뢰하는 어떠한 trasnport layer도 사용이 가능하다. 또 한 UDP처럼 메시지 전송 도중 데이터가 유실되지 않는다.&nbsp;</p>
<p>&nbsp; HTTP는 웹과 client-server protocol에서 데이터 교환의 기초이다. 즉, 요청들은 수령자(web browser)에 의해 초기화 된다. 가져온 하위 문서에서 전체 문서가 재구성된다.&nbsp;</p>
<p>&nbsp; 클라이언트와 서버는 독립된 메시지들을 교환하면서 교신을 한다. 클라이언트가 보내는 메시지를 요청(request)이라 하고 서버가 보내는 메시지를 응답(response)이라 한다.&nbsp;</p>
<p>&nbsp; HTTP가 1990년대 초기에 확장가능한 프로토콜로 고안된 이후 지금까지 수없이 진화해 왔다. HTTP는 애플리케이션층에 프로토콜로서 TCP, TLS로 암호화된 TCP 커넥션 위에서 작동된다. 또 한 이론적으론 신뢰할 수 있는 다른 transport layer도 사용이 가능하다. HTTP는 확장성으로 인해 hypertest 문서 뿐만 아니라 음악, 비디오 등 다른 형식의 파일도 전송이 가능하다. 또 한 HTTP는 문서의 일부분만 업데이트할 수 있다.</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SFRUUCBvdmVydmlldw==/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p><b>Components of HTTP-based system</b></p>
<p>&nbsp; &nbsp;HTTP는 client-server protocol로써 하나의 유저 에이전트가 요청들을 요청한다. 대부분의 경우 유저 에이전트는 웹 브라우저이지만 웹을 크롤링하는 로봇같이 웹 브라우저가 아닌 경우도 존재한다.&nbsp;</p>
<p>&nbsp; 각 요청들은 하나의 서버에 보내지고 이 서버는 요청을 통해 응답을 제공한다. 서버와 클라이언트 사이에는 수많은 엔터티들이 존재한다. 이들은 일괄적으로 프락시 라고 불리며 이들을 각각 다른 연산을 수행하고 게이트웨이 캐시 등으로 사용된다.&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SFRUUCBvdmVydmlldw==/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; 실제로는 위 그림보다 더 많은 컴퓨터들이 서버와 클라이언트 사이에 존재하고 이들이 요청을 핸들링한다. 하지만 HTTP의 계층적 디자인 덕분에 이들은 네트워크와 transport layer에 숨겨져있고 HTTP는 그 위에있는 애플리케이션 층에서 동작한다. 네트워크 문제를 진단하는것은 중요하지만 HTTP 소개글에서 하위 계층은 대부분 무시된다.</p>
<p><b>Client: the user-agent</b></p>
<p>&nbsp; 유저 에이전트는 유저편에서 작동하는 툴이다. 이 역할은 기본적으로 웹 브라우저에 의해 실행된다. 또 한 엔지니어에 의해 사용되는 프로그램들이나 웹 개발자들이 그들의 애플리케이션을 디버그 하는 것도 유저 에이전트의 한 종류이다.&nbsp;</p>
<p>&nbsp; 브라우저는 항상 요청을 초기화 하는 엔터티이다.&nbsp;</p>
<p>&nbsp; 웹 페이지를 나타내기 위해서 브라우저는 요청을 보내 페이지를 나타내는 HTML파일을 받는다. 그 후 이 파일을 파싱하고 실행 스크립트, 레이아웃 정보(CSS)와 해당 페이지가 담고있는 부가 리소스와 관련된 추가적인 요청을 보낸다. 이후 웹브라우저는 이 리소스들을 섞어서 하나의 완성왼 문서(웹 페이지)를 유저에게 보여준다. 브라우저에 의해 실행되는 스크립트들은 이 후에도 더 많은 리소스들을 가져오거나 웹 페이지를 적절히 업데이트할 수 있다.</p>
<p>&nbsp; 웹페이지는 hypertext document이다. 즉, 그 텍스트 중에 일부분은 새로운 웹페이지를 가져올 수 있는 링크이며 이 링크는 그들의 유저 에이전트를 가리키고 웹을 통해 안내해준다. 이런 이벤트가 발생했을때 브라우저는 이것을 HTTP 요청으로 변환하고 더 나아가 HTTP 응답을 유저에게 보낸다.</p>
<p><b>The Web server</b></p>
<p>&nbsp; 커뮤니케이션 채널의 반대편에는 서버가 존재한다. 서버는 클라이언트에 의해 요청된 문서를 서비스한다. 하나의 서버는 사실상 하나의 기계로 나타난다. 이는 실제로 서버의 집합이 되어 로드(load balancing)를 공유하거나 다른 컴퓨터(캐시, DB 등)를 조죄하는 복잡한 소프트웨어 조각이 필요할 수 있기 때문이다.&nbsp;</p>
<p>&nbsp; 하나의 서버가 한대의 기계이지 않을 수 도 있다. 하지만 여러개의 소프트웨어 인스턴스들이 같은 기계에 의해 호스트될 수 있다. HTTP/1.1에선 Host헤더로 하나의 IP주소를 공유할 수 도 있다.</p>
<p><b>Proxies</b></p>
<p>&nbsp; 프락시는 클라이언트와 서버 사이에 위치해 있고 클라이언트의 모든 요청을 받아 서버에게 전달한다. 이 애플리케이션은 사용자를 위한 ㅠ프락시로 동작하고 사용자를 대신해 서버에 접근한다. 프락시는 주로 보안을 위해 사용되고 요청과 응답을 필터링한다.&nbsp;</p>
<p>&nbsp;프락시는 다음과 같은 기능을 한다.</p>
<p>&nbsp; 1. 캐싱(이 캐시는 퍼블릭일수도, 프라이빗할수도 있다, 브라우저 캐시처럼)</p>
<p>&nbsp; 2. 필터링(like antivirus scan)</p>
<p>&nbsp; 3. 로드 밸런싱(여러대의 서버들이 서로다른 요청들을 받는다)</p>
<p>&nbsp; 4. 인증(다른 리소스들에 대한 접근 컨트롤)</p>
<p>&nbsp; 5. 로깅(스토리지의 기록 정보를 허용한다.)</p>
<p><b>Basic aspects of HTTP</b></p>
<p><b>1. HTTP is simple</b></p>
<p><b>&nbsp;&nbsp;</b>HTTP는 심지어 HTTP/2에서 HTTP 메시지를 캡슐화해서 프레임들에 넣은 것이라도 간단하고 사람이 읽을 수 있게 디자인 되었다. HTTP메시지는 사람이 읽을 수 있고 이해할 수 있다. 개발자에게 더욱 간단한 테스트를 제공하고 초보자를 위해 복잡성을 줄였다.</p>
<p><b>2. HTTP is extensible</b></p>
<p><b>&nbsp;&nbsp;</b>HTTP헤더는 이 프로토콜을 쉽게 확장할 수 있게 하고 그것을 경험하게 해준다. 클라이언트와 서버간의 새로운 헤더에 대한 합의를 통해 새로운 기능을 추가할 수 있다.&nbsp;</p>
<p><b>3. HTTP is stateless, but not sessionless</b></p>
<p>&nbsp; HTTP는 stateless하다. 동일한 연결에서 연속적으로 수행되는 두개의 요청에는 아무연 연관이 없다. 이는 직접적으로 특정페이지와 늘 상호작용을 하는 유저들에게 문제가 될 가능성이 있다. (ex. 온란 쇼핑 장바구니). 하지만 HTTP 자기자신은 stateless하지만 HTTP 쿠키들은 stateful 세션들을 허용한다. 헤더의 확장성을 활용해 HTTP 쿠키들이 이 워크플로우에 넣어지고 세션이 각 요청에 만들어짐을 허용해 같은 내용 또는 같은 상태를 공유한다.&nbsp;</p>
<p><b>4. HTTP and connections</b></p>
<p>&nbsp; 커넥션은 전송계층에 의해 관리된다. 그러므로 기본적으로는 HTTP의 관할에서 벗어나 있다. 전송계층이 연결의 기반일 필요는 없지만 신뢰할 수 있거나 메시지를 송수신 도중 잃지 않아야한다. 인터넷에서 가장 많이 사용하는 두개의 프로토콜에선 TCP는 신뢰하지만 UDP는 그렇지 않다. 따라서 HTTP는 TCP표준을 신뢰한다.&nbsp;</p>
<p>&nbsp; 클라이언트와 서버가 요청/응답 쌍을 교환하기 전에 그들은 반드시 TCP 커넥션을 생성해야한다. HTTP/1.0의 디폴트 동작은 분리된 TCP커넥션을 각 HTTP 요청/응답쌍을 위해 여는것이다. 이는 여러개의 요청이 연속적으로 전송될때 하나의 TCP연결을 공유하는 것 보다는 덜 효율적이다.&nbsp;</p>
<p>&nbsp; 이 결점을 완화시키기 위해 HTTP/1.1은 pipelining과 persistent connection을 도입했다. 이를 통해 기본적인 TCP 커넥션은 부분적으로 Connectino 헤더를 사용해 조종될 수 있다. HTTP/2.0은 한번에 연결로 메시지들을 멀티플랙싱 함으로써 한발 더 나아가 커넥션을 효율적으로 유지하는데 도움이 되었다.</p>
<p><b>5. What can be controlled by HTTP</b></p>
<p>&nbsp; HTTP의 확장성은 시간이 지남에 따하 웹의 제어와 기능을 향상시켰다. 다음은 HTTP로 조작 가능한 기능이다.</p>
<p>1. Caching</p>
<p>&nbsp; 문서들이 어떠게 캐싱될지는 HTTP에의해 조작 될 수 있다. 서버는 어느것을 캐싱할지, 얼마 동안 캐싱할지에 대한 것을 프락시와 클라이언트에게 지시할 수 있다.&nbsp;</p>
<p>2. Relaxing the origin constraint</p>
<p>&nbsp; 개인 정보 침해를 막기위해 웹 브라우저는 웹 페이들 간의 엄격한 분할을 강제한다. 같은 곳에서 온 페이지들만이 웹페이지의 모든 정보에 접근할 수 있다. <span style="color: #000000;">이런 제약조건이 서버에 부담이 되지만 HTTP헤더는 이런 엄격한 분할을 서버측에서 완화할 수 있다. 문서가 서로 다른 도메인에서 소싱된 정보의 패치워크가 되도록 허용하고 심지어 이를 보안상의 이유로 이 일을 할 수 있다.</span></p>
<p><span style="color: #000000;">3. Authentication</span></p>
<p><span style="color: #000000;">&nbsp; 일부 페이지들은 보호되어 오직 특정 유저들만 접근할 수 있다. 기본적인 인증은 HTTP에서 제공되고 이는 WWW-Authenticate와 비슷한 헤더 또는 HTTP 쿠키를 사용한 특정 세션의 세팅을 사용한다.</span></p>
<p><span style="color: #000000;">4. Proxy and tunneling</span></p>
<p><span style="color: #000000;">&nbsp; 서버나 클라이언트들은 종종 인트라넷에 위치하고 다른 컴퓨터들로부터 그들의 IP를 숨긴다. 그러면 HTTP 응답은 이 네트워크 장벽을 교차하기 위해 프락시를 통과한다. 모든 프락시들이 HTTP프락시는 아니다. 예들들어 SOCKS 프로토콜의 경우 로우레벨에서 연산을 한다. 다른 프로토콜의 경우 ftp를 예로들자면 이는 이런 프락시에 의해 관리될 수 있다.</span></p>
<p><span style="color: #000000;">5. session</span></p>
<p><span style="color: #000000;">&nbsp; HTTP쿠키들을 사용해 요청을 서버의 상태와 연결할 수 있게 해준다. 이는 HTTP의 기본이 stateless protocol임에도 불구하고 세션을 만든다. 이는 이커머스 장바구니에서 유용할 뿐만 아니라 유저가 아웃풋을 구성하는것을 허용하는 어떠한 사이트에서도 유용하다.&nbsp;</span></p>
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