---
layout:       post
title:        "HTTP caching"
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
                            <p>&nbsp; 웹 사이트와 애플리케이션의 성능은 이전에 사용했던 리소스의 재활용을 통해 향상시킬 수 있다. 웹 캐시는 지연시간과 네트워크 트래픽을 줄여줘서 리소스를 보여주는데 필요한 시간을 줄여준다. <span style="color: #333333;">캐싱은 리소스의 복사본을 저장하고 있다가 요청시에 복사본을 제공하는 기술이다. 웹 캐시가 요청된 리소스를 저장소에 가지고 있을 경우 요청을 가로채서 리소스의 복사본을 반환한다. 하지만 모든 리소스가 영원히 불변은 아니므로 변한 이후에는 더이상 캐싱을 하면 안된다.</span></p>
<p><b><span style="color: #333333;">장점</span></b></p>
<p><b><span style="color: #333333;">&nbsp;&nbsp;</span></b><span style="color: #333333;">1. 모든 클라이언트의 요청을 서버가 처리할 일이 없으므로 서버의 부하를 줄여준다.</span></p>
<p><span style="color: #333333;">&nbsp; 2. 캐시자 원 서버에 비해 클라이언트와의 거리가 가까우므로 성능이 향상된다.&nbsp;</span></p>
<p><b>캐시의 종류</b></p>
<p><b>&nbsp;&nbsp;</b>캐시는 크게 1. private cache, 2. shared cache로 나뉜다.&nbsp;</p>
<p>1. private cache</p>
<p>&nbsp; 단일 사용자 전용으로 사용한다. 브라우저 설정에서 볼 수 있는 캐시가 이에 해당된다. 브라우저 캐시는 하나의 사용자에 의해 다운로드된 문서를 가지고 있고 이 덕분에 브라우저는 서버에 별도의 요청 없이도 뒤로가기, 저장, 소스로 보기 등을 사용할 수 있다.&nbsp; &nbsp;</p>
<p>&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SFRUUCBjYWNoaW5n/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>2. shared proxy cache</p>
<p>&nbsp; 한 명 이상의 사용자가 사용하는 캐시이다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SFRUUCBjYWNoaW5n/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p><b>캐싱 동작의 대상</b></p>
<p>&nbsp; 캐싱은 선택적이지만 캐시의 사용일 일반적으로 권장된다. HTTP 캐시들은 일반적으로 GET요청에 대해서만 캐싱을 하고 다른 메서드는 캐싱을 하지 않는다. 기본 캐시키(primary cache key)는 요청 메서드와 대상 URI로 구성되 있다.&nbsp;</p>
<p>&nbsp; 일반적인 캐싱 엔트리의 형태는 다음과 같다.</p>
<p>&nbsp; 1. 검색 요청의 성공적인 결과: 리소스를 포함하는 GET요청에 대한 200 OK응답</p>
<p>&nbsp; 2. 영구적인 리다이렉트: 301 Moved Permanently 응답</p>
<p>&nbsp; 3. 오류 응답: 404 Not Found</p>
<p>&nbsp; 4. 캐시 키로 사용하기 적절한 것이 정의된 경우의 GET이외의 응답</p>
<p>&nbsp; 캐시 엔트리는 요청이 컨텐츠 협상인 경우 두번째 키에 의해 구별되는 여러 개의 저장된 응답들로 구성될 수 있다.&nbsp;</p>
<p><b>캐싱 제어</b></p>
<p><b>1. Cache-control header</b></p>
<p>&nbsp; Cache-Control은 HTTP/1.1 기본 헤더 필드는 요청과 응답 양측에서 캐싱 메커니즘을 위한 디렉티브를 지정하는데 사용된다.&nbsp;</p>
<p>&nbsp; 1.1 Cache-Control: no-store</p>
<p>&nbsp; &nbsp; 캐시는 요청, 응답에 대해 어느것도 저장하면 안되고 요청은 서버로 전송되 매번 응답을 다운로드한다.</p>
<p>&nbsp; 1.2 Cache-Control: no-cache</p>
<p>&nbsp; &nbsp; 캐시된 복사본을 사용하지만 릴리즈 이전에 유효성 검증을 위해 원 서버로 요청을 보낸다</p>
<p>&nbsp; 1.3 Cache-Control: public</p>
<p>&nbsp; &nbsp; 응답이 어떤 캐시에 의해서든 캐시되어도 좋다는 것을 의미한다. 이는 보통 HTTP인증, 캐시 가능하지 않은 응답 상태 코드를 가진 페이지가 캐 시되어야 할때 사용한다.</p>
<p>&nbsp; 1.4 Cache-Control: private</p>
<p>&nbsp; &nbsp; 캐시가 단일 사용자를 위한 것이고 저장이 되어선 안된다는 것을 의미한다. 사설 브라우저 캐시는 이때 저장이 가능하다.</p>
<p>&nbsp; 1.5 Cache-Control: max-age-&lt;seconds&gt;</p>
<p>&nbsp; &nbsp; 리소스가 유효하다고 생각되는 최대 시간을 의미한다. 이 디렉티브는 요청 시간에 상대적이고 Expires가 설정되어 있어도 그 보다 우선순위가 높다. 변경되지 않을 파일에 대해 긴 시간동안 캐싱할 수 있다.</p>
<p>&nbsp; 1.6 Cache-Control: must-revalidate</p>
<p>&nbsp; &nbsp; 캐시는 오래된 리소스를 사용하기 전에 그 상태를 확인하고 만료된 리소스는 사용하면 안된다.&nbsp;</p>
<p>&nbsp; 2. Parama header</p>
<p>&nbsp; &nbsp; HTTP/1.0 헤더이다. Parama: no-cache는 캐시가 검증을 위해 원해 서버에 요청을 보내도록 강제한다는 점에서 Cache-Control: no-cache와 유사하다. 하지만 Pragma는 응답에 명세되지 않기에 HTTP/1.1 Cache-Control헤더를 신뢰성 있게 대체할 수 없다. 따라서 Parama는 HTTP/1.0클라이언트 와의 하위 호환성을 위해서만 사용되어야한다.&nbsp;</p>
<p><b>유효성(Freshness)</b></p>
<p>&nbsp; 리소스가 캐시 내에 저장되면 이론적으로는 이 캐시를 영구적으로 사용이 가능하다. 하지만 캐시의 저장소는 유한하기에 주기적인 리프레시를 해야한다. 이때 일부 파일은 제거된다. 이 과정을 캐시 축출(cache eviction)이라 한다.&nbsp;</p>
<p>&nbsp; 어떤 리소스는 서버상에서 변경되면 캐시가 변경되어야 하지만 HTTP는 client-server protocol이므로 서버가 캐시와 클라이언트에 접근할 수 없다. 따라서 서버가 리소스에 대한 만료시간을 알려주는 것이 최선이다. 이 경우 만료시간 이전에는 리소스가 유효(fresh)하고 만료시간이 지나면 리소스는 실효(stale)된다. 축출 알고리즘은 대게 유효 리소스에 특권을 부여한다.&nbsp;</p>
<p>&nbsp; 캐시가 실효된 리소스에 대한 요청을 받으면 이 리소스가 실제로 아직 유효한지를 알기 위해 If-None-Match와 같이 요청을 전달한다. 이러면 서버는 요청된 리소스의 본문을 전송하지 않고 304 Not Modified헤더를 돌려보내 대역폭을 절약한다.&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SFRUUCBjYWNoaW5n/img_2.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; 유효 수명의 경우 Cache-control: max-age=N이 있다면 이에 근거하지만 없다면 Expires헤더가 있는지 없는지를 검사하고 있다면 이의 값에서 Date헤더의 값을 뺀 결과가 유효수명이 된다.&nbsp;</p>
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