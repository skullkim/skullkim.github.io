---
layout:       post
title:        "JWT(JSON Web Token)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- JWT
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
                            <p><b>JWT는</b></p>
<p>&nbsp; 1. 전자서명된 URL-safe(URL로 이용 가능한 문자만 사용됨)한 JSON이다</p>
<p>&nbsp; 2. claim을 JSON 구조로 표현한 RFC7519표준이다.</p>
<p>&nbsp; &nbsp; RFC7519는 JWT를 기술한 RFC이다.&nbsp;</p>
<p>&nbsp; &nbsp; claim은 payload에 담는 정보의 한 조각으로 name: value쌍을 이루고있다.</p>
<p>&nbsp; &nbsp; claim은 registered claim, public claim, private claim이 세종류로 나눠져있다.</p>
<p>&nbsp; 3.요청 헤더에 JWT토큰을 넣고 요청을 보내기에 서버는 별도의 인증없이 헤더에 포함된 JWT토큰을 통해 인증한다.</p>
<p>&nbsp; 4. JWT는 HMAC 알고리즘 또는 RSA를 이용한 공개키, 비밀키 쌍으로 서명할 수 있다.</p>
<p>&nbsp; &nbsp; HMAC(keyed-hash message authentication code, hash-based message authentication code)는 암호학에서 암호화 해시 함수와&nbsp; &nbsp; &nbsp; &nbsp; 기밀 암호화 키를 수반하는 특정한 유형의 메시지 인증 코드(MAC)이다.</p>
<p><b>JWT, JWS(JSON Web Signatrue), JWE(JSON Web Encryption)</b></p>
<p>&nbsp; JWS는 JSON 데이터 구조를 사용하는 서명 표준이다(RFC7515). 이는 JSON으로 전자서명을 해서 URL-safe문자열로 변환한것이다</p>
<p>&nbsp; JWE는&nbsp; JSON데이터 구조를 사용하는 암호화 방식이다(RFC7516). 이는 JSON을 암호화해 URL-safe문자열로 표현한 것이다.</p>
<p><b>JWT 구조</b></p>
<p>&nbsp; JWT구조는 다음과같이 3개의 파트로 이뤄져 있다</p>
<p>&nbsp; x.y.z</p>
<p>&nbsp; x: header-&gt; 토큰 타입과 해시 암호화 알고리즘으로 구성되 있다.&nbsp;</p>
<p>&nbsp; y: payload-&gt; 토큰에 담을 claim을 포함한다. palyload는 한번에 여러개의 claim을 넣을 수 있다.</p>
<p>&nbsp; z: signature-&gt; 비밀키를 포함하고 암호화되어있다.&nbsp;</p>
<p><b>기존 토큰 인증 방식과 JWT</b></p>
<p>&nbsp; 기존 토큰 인증 방식의 경우 참조에 의한 호출형태로 모든 서비스는 할상 상호작용할때 다시 접속해야한다. 따라서 토큰은 이후 모든 서비스 호출에 사용된다.</p>
<p>&nbsp; JWT는 값에 의한 호출을 사용한다. 토큰이 필요한 모든 정보를 가지고 있어서 참조가 필요없어지기에 마이크로서비스 자체적으로 유효성을 검증한다.&nbsp;</p>
<p><b>로그인에서의 JWT 동작과정</b></p>
<p>&nbsp; 1. 사용자가 id와 password를 입력하고 요청을 보낸다.</p>
<p>&nbsp; 2. 서버가 요청을 확인하고 비밀키를 통해 access token을 발급한다.</p>
<p>&nbsp; 3. JWT토큰을 클라이언트에 전달한다.&nbsp;</p>
<p>&nbsp; 4. 클라이언트에서 API를 요청할때 헤더에 access token을 담아서 보낸다.</p>
<p>&nbsp; 5. 서버는 JWT Signature를 확인하고 payload에서 사용자 정보를 확인해 데이터를 반환한다.&nbsp;</p>
<p>&nbsp; 6. 서버는 클라이언트에 대한 정보를 저장하지 않기 때문에 토큰 기반 인증 메커니즘을 제공한다. JWT는 모든 정보를 토큰에 포함시키기 때문에 서버와의 커뮤니케이션 오버헤드를 최소화 할 수 있다. 오버헤드는 어떤 처리를 하기위해 들어가는 간접적인 처리시간을 의미한다.&nbsp;</p>
<p><b>장점</b></p>
<p><b>&nbsp;&nbsp;</b>1. 사용자 인증에 필요한 모든 정보가 토큰에 담겨있기때문에 별도의 인증 저장소가 필요없다.</p>
<p>&nbsp; 2. 분산 마이크로 서비스 환경에서 중앙 집중식 인증 서버와 DB에 의존하지 않는 간단한 방식을 제공한다.&nbsp;</p>
<p>&nbsp; 3. URL 파라미터와 헤더로 사용한다.</p>
<p>&nbsp; 4. 스케일 아웃에 용이하다.&nbsp;&nbsp;</p>
<p>&nbsp; &nbsp; &nbsp;스케일 아웃은 접속된 서버의 대수를 늘려서 처리 능력을 향상시키는 방법이다.</p>
<p>&nbsp; 5. 디버깅, 유지보수가 용이하다</p>
<p>&nbsp; 6. REST서비스로 제공가능하다.&nbsp;</p>
<p>&nbsp; 7. 내장된 만료</p>
<p>&nbsp; 8. 독립적인 JWT</p>
<p><b>단점</b></p>
<p><b>&nbsp;&nbsp;</b>1. 세션이나 쿠키는 세션 ID가 변질되면 지워지지만 JWT는 휴효기간 만료까지 지속적으로 사용이 가능하다. 따라서 정보 탈취의 가능성이 존재한다.</p>
<p>&nbsp; 2. playload는 별도로 암호화 되어있지 않아서 이를 탈취해 디코딩하면 정보확인이 가능하므로 담을 수 있는 데이터가 제한적이다.</p>
<p>&nbsp; 3. 세션, 쿠기 방식에 비해 JWT의 길이가 길기때문에 요청이 많아지면 리소스 낭비가 커진다.</p>
<p>&nbsp;</p>
<p><b>JWT-RFC7519</b></p>
<p><b><a href="https://tools.ietf.org/html/rfc7519" target="_blank" rel="noopener">tools.ietf.org/html/rfc7519</a></b></p>
<figure id="og_1608725727607" contenteditable="false" data-ke-type="opengraph" data-og-type="website" data-og-title="RFC 7519 - JSON Web Token (JWT)" data-og-description="[Docs] [txt|pdf] [draft-ietf-oaut...] [Tracker] [Diff1] [Diff2] [IPR] [Errata] Updated by: 7797, 8725 PROPOSED STANDARD Errata Exist Internet Engineering Task Force (IETF) M. Jones Request for Comments: 7519 Microsoft Category: Standards Track J. Bradley I" data-og-host="tools.ietf.org" data-og-source-url="https://tools.ietf.org/html/rfc7519" data-og-url="https://tools.ietf.org/html/rfc7519" data-og-image=""><a href="https://tools.ietf.org/html/rfc7519" target="_blank" rel="noopener" data-source-url="https://tools.ietf.org/html/rfc7519">
<div class="og-image" style="background-image: url();">&nbsp;</div>
<div class="og-text">
<p class="og-title">RFC 7519 - JSON Web Token (JWT)</p>
<p class="og-desc">[Docs] [txt|pdf] [draft-ietf-oaut...] [Tracker] [Diff1] [Diff2] [IPR] [Errata] Updated by: 7797, 8725 PROPOSED STANDARD Errata Exist Internet Engineering Task Force (IETF) M. Jones Request for Comments: 7519 Microsoft Category: Standards Track J. Bradley I</p>
<p class="og-host">tools.ietf.org</p>
</div>
</a></figure>
<p><b>JWS-RFC7515</b></p>
<p><a href="https://tools.ietf.org/html/rfc7515" target="_blank" rel="noopener">tools.ietf.org/html/rfc7515</a></p>
<figure id="og_1608725767149" contenteditable="false" data-ke-type="opengraph" data-og-type="website" data-og-title="RFC 7515 - JSON Web Signature (JWS)" data-og-description="[Docs] [txt|pdf] [draft-ietf-jose...] [Tracker] [Diff1] [Diff2] [IPR] [Errata] PROPOSED STANDARD Errata Exist Internet Engineering Task Force (IETF) M. Jones Request for Comments: 7515 Microsoft Category: Standards Track J. Bradley ISSN: 2070-1721 Ping Ide" data-og-host="tools.ietf.org" data-og-source-url="https://tools.ietf.org/html/rfc7515" data-og-url="https://tools.ietf.org/html/rfc7515" data-og-image=""><a href="https://tools.ietf.org/html/rfc7515" target="_blank" rel="noopener" data-source-url="https://tools.ietf.org/html/rfc7515">
<div class="og-image" style="background-image: url();">&nbsp;</div>
<div class="og-text">
<p class="og-title">RFC 7515 - JSON Web Signature (JWS)</p>
<p class="og-desc">[Docs] [txt|pdf] [draft-ietf-jose...] [Tracker] [Diff1] [Diff2] [IPR] [Errata] PROPOSED STANDARD Errata Exist Internet Engineering Task Force (IETF) M. Jones Request for Comments: 7515 Microsoft Category: Standards Track J. Bradley ISSN: 2070-1721 Ping Ide</p>
<p class="og-host">tools.ietf.org</p>
</div>
</a></figure>
<p><b>JWE-RFC7516</b></p>
<p><b><a href="https://tools.ietf.org/html/rfc7516" target="_blank" rel="noopener">tools.ietf.org/html/rfc7516</a></b></p>
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