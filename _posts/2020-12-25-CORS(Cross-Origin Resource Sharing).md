---
layout:       post
title:        "CORS(Cross-Origin Resource Sharing)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- HTTP
- CORS
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
                            <p><b>오리진:<a href="https://iskull-dev.tistory.com/65" target="_blank" rel="noopener">iskull-dev.tistory.com/65</a></b></p>
<figure id="og_1608897800673" contenteditable="false" data-ke-type="opengraph" data-og-type="article" data-og-title="Origin" data-og-description="Web content origin은 스킴, 호스트, URL의 포트로 정의되고 이는 origin에 접근하는데에 사용된다. 2개의 객체가 같다는 의미는 이 두개의 객체가 같은 스킴, 호스트, 포트를 사용한다는 의미이다. 일부 " data-og-host="iskull-dev.tistory.com" data-og-source-url="https://iskull-dev.tistory.com/65" data-og-url="https://iskull-dev.tistory.com/65" data-og-image="https://scrap.kakaocdn.net/dn/cv4EKI/hyIGqoisMQ/rnJL3kqtA7KGdlz4WHaKz1/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/jidID/hyIHHoq2TG/h8cAuKQ32of1SkBdSNlHR1/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/i35nj/hyIGssTWrs/D0FYVs1kyWvwVmYwYNbttK/img.png?width=264&amp;height=200&amp;face=0_0_264_200"><a href="https://iskull-dev.tistory.com/65" target="_blank" rel="noopener" data-source-url="https://iskull-dev.tistory.com/65">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/cv4EKI/hyIGqoisMQ/rnJL3kqtA7KGdlz4WHaKz1/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/jidID/hyIHHoq2TG/h8cAuKQ32of1SkBdSNlHR1/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/i35nj/hyIGssTWrs/D0FYVs1kyWvwVmYwYNbttK/img.png?width=264&amp;height=200&amp;face=0_0_264_200');">&nbsp;</div>
<div class="og-text">
<p class="og-title">Origin</p>
<p class="og-desc">Web content origin은 스킴, 호스트, URL의 포트로 정의되고 이는 origin에 접근하는데에 사용된다. 2개의 객체가 같다는 의미는 이 두개의 객체가 같은 스킴, 호스트, 포트를 사용한다는 의미이다. 일부</p>
<p class="og-host">iskull-dev.tistory.com</p>
</div>
</a></figure>
<p><b>SOP(Same-origin policy)</b></p>
<p>&nbsp; &nbsp;어떤 오리진에서 불러온 문서나 스크립트가 다른 오리진에서 가져온 리소스와 상호작용하는 것을 제한하는 보안방식이다. 이는 자바스크립트 보안 정책중에 하나이다.</p>
<p>&nbsp; 이 SOP때문에 다른 오리진을 사용하면 corss domain 이슈가 발생한다. 이 이슈를 해결하기 위해 가장 많이 사용하는 방법으로는 1. JSONP, 2. Reverse Proxy, 3. Flash socket이 있다. 그 후 W3C에서 cross domain 이슈를 해결하기 위한 권장사항으로 CORS를 발표했다.</p>
<p>&nbsp;</p>
<p><b>CORS</b></p>
<p>&nbsp; CORS는 HTTP헤더 기반의 매커니즘이다. 이 매커니즘은 서버가 로딩을 허용한 리소스 외의 어떠한 다른 오리진을 나타내게 하는 매커니즘이다. 또 한 CORS는 브라우저가 corss-origin 리소스를 호스팅하는 서버에 사전 확인 요청을 하는 매커니즘에 의존해 서버가 실제 요청을 허용하는지 확인다. 이 사전 확인 요청에서 브라우저는 HTTP 메서드와 실제 요청에서 사용할 헤더를 포함하는 헤더를 사용한다.</p>
<p><b>Cross-origin 예시</b></p>
<p>&nbsp; https://domain-a.com에서 제공하는 프론트엔드 자바스크립트는 XMLHttpRequest를 사용해 https://domain-b.com/data.json에 대한 요청을 만든다.&nbsp;</p>
<p>&nbsp; 보안상의 이유료 브라우저들은 스크립트에서 초기화된 cross-origin HTTP요청을 제한한다. 예를 들어 XMLHttpRequest와 Fetch API는 same-origin policy를 따른다. 즉 이러한 API들을 사용하는 웹 애플리케이션은 <span style="color: #333333;">애플리케이션이 올바를 CORS헤더를 포함한 다른 오리진에서 온 응답으로 인해 로드되지 않는 한 </span>같은 오리진에서온 리소스만 요청할 수 있다.&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; CORS 메커니즘은 보안 cross-origin요청을 지원하고 데이터는 브라우저와 서버사이를 오간다. 현대의 브라우저들은 API안에서 CORS를 사용한다.(XMLHttpRequest, Fetch등).</p>
<p><b>What requests use CORS?</b></p>
<p>&nbsp; cross-origin shargin 표준은 cross-site HTTP 요청을 다음과 같은 것들을 위해 허용할 수 있다.</p>
<p>&nbsp; 1. XMLHttpRequest 또는 Fetch API의 호출</p>
<p>&nbsp; 2. 웹 폰트</p>
<p>&nbsp; 3. <a href="https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Tutorial/Using_textures_in_WebGL" target="_blank" rel="noopener">WebGL textures</a></p>
<p>&nbsp; 4. drawImage()의 의해 그려진 이미지/비디오 프레임들</p>
<p>&nbsp; 5. <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes/Shapes_From_Images" target="_blank" rel="noopener">CSS Shapes from images</a></p>
<p><b>Functional overview</b></p>
<p>&nbsp; cross-origin recourse 표준은 일을 새로운 HTTP헤더들을 추가함으로써 공유한다. 이 헤더들은 서버들이 어느 오리진들이 웹 브라우저에서 정보를 읽도록 허용하는지를 서술하게 한다. 부가적으로, 서버 데이터에 부작용을 야기할 수 있는 HTTP 요청의 경우 명세서는 브라우저가 이런 요청을 사전에 검증하도록 한다. 서버에게 HTTP OPTIONS 요청 메서드로 지원하는 메서드들을 요청한다. 그 후 서버가 허용한 메서드가 클라이언트가 원하는 메서드이명 실제 요청을 보낸다. 또한 서버가 클라이언트에게 인증서를 요청에 포함해 보내야 할지를 알릴 수 있다.&nbsp;</p>
<p>&nbsp; CORS장애는 에러를 발생시키지만 보안상의 이유로 자바스크립트에서 에러를 명세하는것은 허용되지 않는다. 모든 코드는 단지 에러가 발생했다는 것만 알고있다. 어떤 부분이 잘못되었는지를 판단할 수 있는 유일한 기준은 브라우저 콘솔에 있는 에러이다.&nbsp;</p>
<p><b>Examples of access control scnarios</b></p>
<p>CORS는 다음과 같은 3가지의 방식으로 사용할 수 있다.</p>
<p>&nbsp; 1. Simple requests</p>
<p>&nbsp; 2. preflighted requests</p>
<p>&nbsp; 3. request with credentials</p>
<p><b>1. Simple requests</b></p>
<p><b>&nbsp; </b>Simple reuqest는 다음 조건을 모두 충족하는 요청이다.</p>
<p>&nbsp; 1. 다음 중 하나의 메서드: GET, HEAD, POST</p>
<p>&nbsp; 2. 유저 에이전트가 자동으로 설정한 헤더 외에 사용가능한 헤더는 오직 Fetch명세에서 <a href="https://fetch.spec.whatwg.org/#cors-safelisted-request-header" target="_blank" rel="noopener">CORS-safelisted request-header</a>로 정의한 헤더 뿐이다.</p>
<p>&nbsp; &nbsp; Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-width, Width,</p>
<p>&nbsp; &nbsp;Content-Type.</p>
<p>&nbsp; Content-Type의 경우 다음과 같은 값들만 허용된다: application/x-www-form-urlencoded, multipart/form-data, text/plain</p>
<p>&nbsp; 3. 요청에 사용되는 XMLHttpRequestUpload객체에는 이벤트 리스터가 등록되어 있지 않아야한다. 이들은 XMLHttpRequest.upload프로퍼티를 사용한다.</p>
<p>&nbsp; 4. 요청에 ReadableStream객체가 사용된다.</p>
<p>예시:&nbsp;</p>
<p>&nbsp; https://foo.example의 웹 컨텐츠가 <a href="https://bar.other도메인의">https://bar.other도메인의</a> 컨텐츠를 호출하길 원한다 하자. 여기서 foo.example이 다음과 같은 자바스크립트 코드를 사용한다면&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>foo.example</figcaption>
</figure><p></p>
<p>&nbsp;</p>
<p>브라우저는 시작줄의 URL에 /resources/publicdata/를 넣고 헤더에 Origin: https://foo.example를 추가해 요청을 보낸다.</p>
<p>서버는 이에 대한 응답으로 헤더에 Access-Control-Allow-Origin를 포함해 응답을 전송한다. 만약 Access-Control-Allow-Origin:*이면 모든 도메인에 대해 접근을 허용한다는 의미이고 *대신 https://foo.example이 적혀 있다면 이 도메인에 한해서 접근을 허용한다는 의미이다.&nbsp;</p>
<p><b>2. Preflighted requests</b></p>
<p>&nbsp; preflighted request의 경우 유저 OPTIONS 메서드를 통해 다른 도메인의 리소스로 HTTP 요청을 보내서 실제 요청을 보내기에 안전한지 확인을 하고 안전하다면 요청을 보낸다.&nbsp;</p>
<p>다음은 preflight 요청을 할때의 자바스크립트 파일과 요청응답이다.&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img_2.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>브라우저는 위의 자바스크립트 코드 스니펫이 사용중인 요청 파라미터를 기반으로 전송을 해야 서버가 실제 요청 파라미터로 요청을 보낼 수 있는지를 판단할 수 있다.</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img_3.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>preflight request/response</figcaption>
</figure><p></p>
<p>preflight request에서:</p>
<p>Access-Control-Request-Method는 실제 요청을 보낼때 사용되는 메서드를 기술한다.&nbsp;</p>
<p>Access-Control-Request-Headers는 실제 요청에서 어떤 헤더를 전송할지를 알려준다.</p>
<p>preflight response에서:</p>
<p>Access-Control-Allow-Origin은 CORS를 허용하는 도메인을 나타낸다</p>
<p>Access-Control-Allow-Methods는 실제 요청에서 허용하는 메서드를 나타알려준다</p>
<p>Access-Control-Allow-Headers는 실제 요청에서 허용하는 헤더를 알려준다</p>
<p>Access-Control-Masx-Age는 다른 preflight request를 조내지 않고도 preflight request에 대한 응답을 캐시할 수 있는 시간을 제공한다. 단위는 초이며 이 값이 클수록 각 브라우저의 최대 캐싱 시간의 우선순위가 높다.</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img_4.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>real request/response</figcaption>
</figure><p></p>
<p><b>3. Requests with credentials</b></p>
<p><b>&nbsp;&nbsp;</b>XMLHttpRequest나 Fetch는 인증 정보(credentialed) 요청을 사용한다. credentialed request는 HTTP cookies와 HTTP Authentication정보를 인식한다. cross-site XMLHttpRequest나 Fetch 호출에서 브라우저는 자격 증명을 보내지 않는다. XMLHttpRequest객체나 Request생성자가 호출될때 특정 플래그를 설정해야한다.&nbsp;</p>
<p>&nbsp; http://foo.example에서 불러온 컨텐츠는 쿠키를 설정하는 <a href="http://bar.other">http://bar.other</a> 리소스에 simple GET request를 작성한다. foo.example는 다음과 같은 자바스크립트를 포함한다.</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img_5.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>invocation.withCredentials는 쿠키와 함께 호출하기 위한 XMLHttpRuequest의 플래그를 보여준다. withCredentials는 불리안 값을 갖고 기본적으로는 쿠키 없이 호출이 이루어진다. 이는 simple GET request이기 때문에 preflighted되지 않는다. 하지만 브라우저는 Control-Allow-Credentials:true헤더가 없는 응답을 거부한다. 따라서 호출된 웹 컨텐츠에 응답을 제공하지 않는다.&nbsp;</p>
<p>&nbsp; 다음은 클라이언트와 서버의 통신 예시이다.&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/Q09SUyhDcm9zcy1PcmlnaW4gUmVzb3VyY2UgU2hhcmluZyk=/img_6.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>요청에서 Cookie: pageAccess=2는 <a href="http://bar.other의">http://bar.other의</a> 컨텐츠를 대상으로 하는 쿠키가 포함되있다. 이때 응답에서 Access-Control-Allow-Credentials: true 헤더를 사용하지 않으면 응답은 무시되고 웹 컨텐츠는 제공되지 않는다.&nbsp;</p>
<p><b>3.1 Credentialed request and wildcards</b></p>
<p><b>&nbsp;&nbsp;</b>credentialed request에 응답할때 서버는 Access-Control-Allow-Origin 헤더에 와일드카드('*')대신에 URL을 반드시 지정해야한다.</p>
<p>만약 이 헤더의 값이 와일드 카드이면 요청이 실패한다.&nbsp;</p>
<p><b>Third-party cookies</b></p>
<p>&nbsp; CORS응답에 설정된 쿠키에는 일반적인 third-pary cookie정책이 적용된다.</p>
<p>&nbsp;</p>
<p>CORS에서 사용되는 요청, 응답 헤더에 대한 설명은 아래 링크를 참고하자</p>
<p><a href="https://iskull-dev.tistory.com/67" target="_blank" rel="noopener">iskull-dev.tistory.com/67</a></p>
<figure id="og_1608965100085" contenteditable="false" data-ke-type="opengraph" data-og-type="article" data-og-title="CORS request header, response header" data-og-description="HTTP 응답 헤더 아래에 서술된 헤더들은 서버가 접근 제어 요청을 위해 보내는 HTTP응답 헤더이다. Access-Control-Allow-Origin: | * 단일 출처를 지정해 브라우저가 해당 출처가 리소스에 접근되도록 허용" data-og-host="iskull-dev.tistory.com" data-og-source-url="https://iskull-dev.tistory.com/67" data-og-url="https://iskull-dev.tistory.com/67" data-og-image="https://scrap.kakaocdn.net/dn/bWZ0VK/hyIHNWWuAw/34kuSK6fHICKJi1NG59Bh1/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/bdMPYn/hyIHNQaamH/WbBayPs1DNajuiLiEEcEyK/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/cxy0qr/hyIHBa7EFb/38Smjkiyk0PLljEKWwzIl1/img.png?width=264&amp;height=200&amp;face=0_0_264_200"><a href="https://iskull-dev.tistory.com/67" target="_blank" rel="noopener" data-source-url="https://iskull-dev.tistory.com/67">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/bWZ0VK/hyIHNWWuAw/34kuSK6fHICKJi1NG59Bh1/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/bdMPYn/hyIHNQaamH/WbBayPs1DNajuiLiEEcEyK/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/cxy0qr/hyIHBa7EFb/38Smjkiyk0PLljEKWwzIl1/img.png?width=264&amp;height=200&amp;face=0_0_264_200');">&nbsp;</div>
<div class="og-text">
<p class="og-title">CORS request header, response header</p>
<p class="og-desc">HTTP 응답 헤더 아래에 서술된 헤더들은 서버가 접근 제어 요청을 위해 보내는 HTTP응답 헤더이다. Access-Control-Allow-Origin: | * 단일 출처를 지정해 브라우저가 해당 출처가 리소스에 접근되도록 허용</p>
<p class="og-host">iskull-dev.tistory.com</p>
</div>
</a></figure>
<p>&nbsp;</p>
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