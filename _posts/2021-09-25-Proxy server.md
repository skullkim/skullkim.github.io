---
layout:       post
title:        "Proxy server"
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
                            <p data-ke-size="size16">&nbsp; Proxy server는 웹페이지 같은 유저 쪽에 있는 인터넷에서 데이터를 찾아오는 서버이다. 이는 서버와 클라이언트 사이에서 다리 역할을 하고 요청, 응답을 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 프록시 서버는 중간자 역할을 수행하고 해당 웹페이지를 검색한다. 유저가 웹사이트에 방문을 하면 프록시 서버는 유저의 컴퓨터에서 요청을 받고 사용자를 대신해 웹페이지를 검색해 컴퓨터로 전송한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 프록시 서버는 다음과 같은 종류가 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; - Forward proxy server: 여러 클라이언트에서 서버로 오는 요청을 처리한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; - Reverse proxy server: Forward proxy server와는 반대로 동작한다.</p>
<p data-ke-size="size16">&nbsp; 따라서 forward proxy는 클라이언트를 위한거고, reverse proxy는 서버를 위한거다. 따라서 Reverse proxy는 클라이언트를 대신해 한 개 이상의 서버에 요청을 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; Reverse proxy는 nginx 인스턴스에서 실행할 수 있다. 이를 이용하면 내부 서버 앞에 있는 데이터를 접근하지 못하게 할 수 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Reverse proxy</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>Reverse proxy는 요청 응답 프로세스 사이에 위치하며 웹사이트의 요청들이 올바른 서버로 리다이렉트 되었는지를 검증한다. 모든 종류의 reveres proxy들은 요청을 다른 방식으로 처리 한다. Caching, security, content optimization proxy등은 요청을 수행하는데에 사용되는 reverse proxy이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 요청이 통과될 수 있게 여러 reverse proxy들이 쌓이는 것을 proxy stack이라 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 많이 사용되는 reverse proxy 이자 reverse stack인 것은 varnish cache이다. Varnish Cache는 cache에서 응답을 함으로써 응담 시간을 줄인다. Varnish cache는 HTTP를 캐싱하고 있고 응답의 출처가 지질학적으로 가깝게 있기 때문에 웹사이트를 더 빠르게 로딩할 수 있다. 요청을 들어 오면 이 요청은 Varnish cache로 가서 varnish cache가 해당 요청을 원 서버로 보낼지를 결정한다.</p>
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