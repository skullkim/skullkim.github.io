---
layout:       post
title:        "지속커넥션과 keep-alive"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- HTTP
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><b>개략적인 HTTP 통신 과정</b></h2>
<p data-ke-size="size16">&nbsp; 이론적으로 HTTP는 TCP를 사용하기 때문에 하나의 요청-응답에 대해 하나의 커넥션을 맺는다. 따라서 하나의 요청-응답을 진행한다면 다음과 같이 3-way-handshake, 4-way-handshake를 매번 진행해야 한다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="948" data-origin-height="638"><span data-url="https://blog.kakaocdn.net/dn/bAeVlo/btrRst5odaa/ZufkRCCMPrzaazawkvfsg0/img.png" data-lightbox="lightbox"><img src="/img/2022-11-18-keep-alive/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAeVlo%2FbtrRst5odaa%2FZufkRCCMPrzaazawkvfsg0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="616" height="415" data-origin-width="948" data-origin-height="638"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 하지만 하나의 웹 페이지를 로딩할 때는 다수의 정적 파일을 로딩해야 하기 때문에 같은 서버에 여러 번 요청을 하게 된다(이를 사이트 지역성(site locality)이라 한다). 즉, 하나의 클라이언트와 서버가 불필요한 커넥션 과정을 여러 번 거쳐야 한다.</p>
<h2 data-ke-size="size26"><b>지속 커넥션</b></h2>
<p data-ke-size="size16">&nbsp; 위 문제를 해결하기 위해 HTTP/1.1은 처리가 완료되어도 TCP 커넥션을 유지해서 다음 HTTP 요청-응답에 재사용할 수 있다. 이런 커넥션을 지속 커넥션이라 한다.&nbsp; 지속 커넥션을 끊기 위해선 클라이언트 또는 서버가 임의로 커넥션을 끊어주어야 한다.</p>
<h3 data-ke-size="size23"><b>지속 커넥션 VS 병렬 커넥션</b></h3>
<p data-ke-size="size16">&nbsp; 지속 커넥션은 병렬 커넥션에 비해 다음과 같은 이점을 가진다.</p>
<p data-ke-size="size16">&nbsp; 1. 커넥션을 맺는 과정을 줄여준다</p>
<p data-ke-size="size16">&nbsp; 2. TCP slow start가 매번 발생하지 않는다</p>
<p data-ke-size="size16">&nbsp; 3. 커넥션 수를 줄여준다.</p>
<p data-ke-size="size16">&nbsp; 하지만 지속 커넥션을 지속적으로 유지한다면, 불필요한 커넥션이 다수 존재하게 되며, 이는 클라이언트와 서버의 불필요한 리소스 소모를 야기한다. 따라서 적은 수의 병렬 커넥션을 맺고, 그것을 지속 커넥션으로 유지하는 것이 가정 효과적이며 많은 웹 애플리케이션이 이 방식을 사용한다.</p>
<p data-ke-size="size16">&nbsp; 지속 커넥션을 지원하는 방식은 HTTP 버전마다 다르다. HTTP/1.0은 'keep-alive' 커넥션을 사용하고 HTTP/1.1은 '지속' 커넥션을 사용한다.</p>
<p data-ke-size="size16">&nbsp; keep-alive가 HTTP/1.0에서 지원하는 사양이긴 하나, 초기 HTTP/1.0부터 keep-alive를 지원하지는 않는다. keep-alive는 추후에 추가된 사양이다. 이 때문에 HTTP/1.0을 정의한 <a href="https://www.rfc-editor.org/rfc/rfc1945" target="_blank" rel="noopener">RFC1945</a>에는 'keep-alive'라는 단어 자체가 존재하지 않는다. 그에 반해 HTTP/1.1을 정의한 HTTP/1.1 이전 명세인&nbsp;<a href="https://www.rfc-editor.org/rfc/rfc2068" target="_blank" rel="noopener">RFC2068</a>의 경우 keep-alive를 서술한 "<a href="https://www.rfc-editor.org/rfc/rfc2068#section-19.7.1.1" target="_blank" rel="noopener">19.7.1 Compatibility with HTTP/1.0 Persistent Connections</a>"에서 다음과 같은 문구를 찾아볼 수 있다. "HTTP/1.0&nbsp;experimental&nbsp;implementations&nbsp;of&nbsp;persistent&nbsp;connections&nbsp;are&nbsp;faulty,&nbsp;and&nbsp;the&nbsp;new&nbsp;facilities&nbsp;in&nbsp;HTTP/1.1&nbsp;are&nbsp;designed&nbsp;to&nbsp;rectify&nbsp;these&nbsp;problems."</p>
<p data-ke-size="size16">&nbsp;</p>
<h2 data-ke-size="size26"><b>HTTP/1.0의 Keep-Alive 커넥션</b></h2>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>keep-alive는 HTTP/1.1부터 사용하지 않지만 아직도 브라우저와 서버 간의 keep-alive 핸드 셰이크가 널리 사용되고 있다. 따라서 HTTP 애플리케이션이 이를 처리할 수 있게 개발해야 한다.</p>
<p data-ke-size="size16">&nbsp; HTTP/1.0에서 keep-alive를 사용해 커넥션을 유지하고 싶다면 요청에 'Connection:Keep-Alive' 헤더를 포함시켜야 한다. 그 후, 이 요청을 받은 서버가 다음 요청도 같은 커넥션을 통해 받고자 한다면 응답에 'Connection:Keep-Alive'를 포함시킨다. 만약 응답에 'Connection:Keep-Alive'가 없다면, 클라이언트는 서버가 keep-alive를 지원하지 않고, 서버 커넥션을 끊은 것으로 간주한다.</p>
<p data-ke-size="size16">&nbsp; Keep-Alive 헤더는 커넥션을 연결하길 바라는 요청일 뿐이다. 따라서 클라이언트, 서버가&nbsp;Keep-Alive 헤더를 받는다고 무조건 지속 커넥션을 할 필요는 없다.</p>
<h3 data-ke-size="size23"><b>Keep-Alive 커넥션 제한과 규칙</b></h3>
<p data-ke-size="size16">&nbsp; Keep-Alive를 올바르게 사용하기 위해선 다음과 같은 사용방법을 따라야 한다.</p>
<p data-ke-size="size16">&nbsp; 1. Keep-Alive는 HTTP/1.0에서 기본으로 사용되지 않으며, 사용 시 Connection: Keep-Alive 요청 헤더를 보내야 한다.</p>
<p data-ke-size="size16">&nbsp; 2. 커넥션 유지를 위해선 요청, 응답 메시지에 모두 Connection: Keep-Alive를 포함해야 한다.</p>
<p data-ke-size="size16">&nbsp; 3. 클라이언트는 응답 헤더에 Connection: Keep-Alive가 없다면 서버가 응답 후 커넥션을 끊은 것임을 알 수 있다.</p>
<p data-ke-size="size16">&nbsp; 4. 엔티티 본문이 정확한 Content-Length을 가져야 하며, 본문은 multipart media type 또는 chunked transfer encoding으로 인코드 돼야 한다. 그래야 트랜잭션이 끝나는 시점에 기존 메시지 끝과 새로운 메시지 시작점을 정확히 알 수 있다.</p>
<p data-ke-size="size16">&nbsp; 5. 프락시와 게이트웨이는 Connection 헤더의 규칙을 철저히 지켜야 한다. 프락시와 게이트웨이는 메시지를 전달하거나 캐시에 넣기 전에 Connection 헤더에 명시된 모든 헤더 필드와 Connection 헤더를 제거해야 한다.</p>
<p data-ke-size="size16">&nbsp; 6. keep-alive 커넥션은 Connection 헤더를 인식하지 못하는 프락시 서버와 맺어지면 안 된다.</p>
<p data-ke-size="size16">&nbsp; 7. HTTP/1.0을 따르는 기기로부터 받는 모든 Connection 헤더 필드는 무시해야 한다.</p>
<p data-ke-size="size16">&nbsp; 8. 클라이언트는, 응답을 모두 받기 전에 커넥션이 끊어졌을 경우, 요청을 다시 보낼 수 있게 준비되어 있어야 한다.</p>
<h3 data-ke-size="size23"><b>Keep-Alive와 멍청한(dump) 프락시</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>위 Keep-Alive 커넥션 제한과 규칙 중 6번 항목이 이 문제와 연관 있다.&nbsp;</p>
<h4 data-ke-size="size20"><b>Hop-by-Hop Header</b></h4>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>hop-by-hop header는 현재 요청을 처리하고 있는 프락시에 의해 처리되고 소비되도록 고안된 헤더다. 이와 반대되는 헤더는 end-to-end header이다. <a href="https://www.rfc-editor.org/rfc/rfc2616.html#section-13.5.1" target="_blank" rel="noopener">RFC 2616 section-13.5.1</a>에 따르면 HTTP/1.1은 다음과 같은 헤더들을 hop-by-hop header로 간주한다.</p>
<p data-ke-size="size16">&nbsp; - Connection</p>
<p data-ke-size="size16">&nbsp; - Keep-Alive</p>
<p data-ke-size="size16">&nbsp; - Proxy-Authenticate</p>
<p data-ke-size="size16">&nbsp; - Proxy_Authorization</p>
<p data-ke-size="size16">&nbsp; - TE</p>
<p data-ke-size="size16">&nbsp; - Trailers</p>
<p data-ke-size="size16">&nbsp; - Transfer-Encoding</p>
<p data-ke-size="size16">&nbsp; - Upgrade</p>
<p data-ke-size="size16">&nbsp; 위 헤더들을 제외한 나머지 헤더들은 end-to-end 헤더다.</p>
<p data-ke-size="size16">&nbsp; 따라서 'Connection: Keep-Alive'는 hop-by-hop header다. 그럼에도 일부 프락시가 Connection 헤더를 이해하지 못하고, 이를 원 서버에 전달해 잘못된 커넥션이 맺어지는 경우가 발생한다. 구체적인 문제 발생 방식은 다음과 같다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1766" data-origin-height="566"><span data-url="https://blog.kakaocdn.net/dn/bOvecd/btrRthDzg7h/iNY1F0thAq8Rv3x7yL8in1/img.png" data-lightbox="lightbox"><img src="/img/2022-11-18-keep-alive/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOvecd%2FbtrRthDzg7h%2FiNY1F0thAq8Rv3x7yL8in1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="667" height="214" data-origin-width="1766" data-origin-height="566"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 1. 클라이언트는 프락시에 Connection: Keep-Alive를 요청에 담아 보내 프락시와 커넥션을 유지하기를 요청한다.</p>
<p data-ke-size="size16">&nbsp; 2. Connection은 hop-by-hop header이지만, 프락시는 Connection이라는 헤더를 이해하지 못해 그대로 서버에 전송한다.</p>
<p data-ke-size="size16">&nbsp; 3. 서버에 Connection: Keep-Alive가 도착하면, 서버는 프락시가 연결을 유지하려 한다는 것으로 이해한다. 그 후, 서버는 응답에 Connection: Keep-Alive를 담아 응답한다.</p>
<p data-ke-size="size16">&nbsp; 4. 프락시는 응답에 있는 Connection: Keep-Alive를 이해하지 못해 클라이언트에게 그대로 응답한다.</p>
<p data-ke-size="size16">&nbsp; 5. 응답으로 Connection: Keep-Alive를 받은 클라이언트는 프락시가 연결 유지를 수락한 것으로 간주해 프락시와의 연결을 유지한다.</p>
<p data-ke-size="size16">&nbsp; 6. 이제 프락시는 서버가 커넥션을 끊기를 기다리지만, 서버는 위 과정을 통해 커넥션을 유지하고 있기 때문에 커넥션을 끊지 않는다. 따라서 프락시는 커넥션을 끊기를 기다린다.</p>
<p data-ke-size="size16">&nbsp; 7. 커넥션을 유지하고 있던 클라이언트가 같은 커넥션으로 다른 요청을 보낸다. 같은 커넥션으로부터 요청이 오는 것을 예상 못한 프락시는 요청을 무시한다. 클라이언트는 아무런 응답 없이 로드 중이라는 표시만 띄운다.</p>
<p data-ke-size="size16">&nbsp; 9. 클라이언트는 이제 자신이나 서버가 타임아웃이 나서 커넥션이 끊길 때까지 기다린다.</p>
<h2 data-ke-size="size26"><b>HTTP/1.0의 지속 커넥션</b></h2>
<p data-ke-size="size16">&nbsp; HTTP/1.1에서는 Keep-Alive 커넥션을 지원하지 않는다. 대신 설계가 개선된 지속 커넥션을 지원한다. 지속 커넥션은 기본으로 활성화되어 있다. 지속 커넥션을 끊고 싶다면, Connection: close 헤더를 명시하면 된다. 만약 요청으로 Connection: close를 보냈음에도 응답으로 Connection: close가 오지 않았다면, 서버가 커넥션을 유지하는 것으로 간주한다.</p>
<h3 data-ke-size="size23"><b>지속 커넥션의 제한과 규칙</b></h3>
<p data-ke-size="size16">&nbsp; 1. 클라이언트가 요청에 Connection: close 헤더를 포함해 보냈으면, 클라이언트는 그 커넥션으로 추가 요청을 보낼 수 없다.</p>
<p data-ke-size="size16">&nbsp; 2. 클라이언트가 해당 커넥션으로 추가 요청을 보내지 않을 것이라면, Connection: close를 헤더에 넣어 요청해야 한다.</p>
<p data-ke-size="size16">&nbsp; 3. 커넥션에 있는 모든 메시지가 자신의 정확한 길이를 Content-Length로 가지고 있거나 chunked transfer encoding으로 인코드 되어 있어야 한다.</p>
<p data-ke-size="size16">&nbsp; 4. HTTP/1.1 프락시는 클라이언트와 서버 각각에 대해 별도의 지속 커넥션을 맺고 관리해야 한다.</p>
<p data-ke-size="size16">&nbsp; 5. HTTP/1.1 프락시는 클라이언트가 커넥션 관리 기능에 대한 클라이언트 지원 범위를 모른다면, 커넥션을 맺으면 안 된다. 그렇지 않으면, 위에서 언급한, 잘못된 Connection 헤더 전달 문제가 발생한다.</p>
<p data-ke-size="size16">&nbsp; 6. 서버는 메시지 전송 도중 커넥션을 끊지 않고, 한 개 이상의 응답을 한다. 하지만, HTTP/1.1 기기는 Connection 헤더의 값과는 상관없이 언제든지 커넥션을 끊을 수 있다.</p>
<p data-ke-size="size16">&nbsp; 7. HTTP/1.1 애플리케이션은 중간에 커넥션이 끊겨도 다시 커넥션을 복구할 수 있어야 한다.</p>
<p data-ke-size="size16">&nbsp; 8. 클라이언트는 전체 응답을 받기 전에 커넥션이 끊기면, 문제가 없을 경우 다시 요청을 보낼 준비가 돼야 한다.</p>
<p data-ke-size="size16">&nbsp; 9. 하나의 사용자 클라이언트는 서버 과부하 방지를 위해 넉넉잡아 두 개의 지속 커넥션만 유지해야 한다. 따라서 사용자가 N명이면, 프락시는 서버나 상위 프락시에 약 2N개의 커넥션을 유지해야 한다.</p></div>