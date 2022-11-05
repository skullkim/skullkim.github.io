---
layout:       post
title:        "Proof Key for Code Exchange(PKCE)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- Authorization
- OAuth
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로젝트에서 OAuth 로그인을 구현하기 위해 OAuth 플로우를 찾아보던 중 여러 플로우가 존재하는 것을 알게 되었다. 그 중, 이번 프로젝트에 사용할 방식인 PKCE를 정리해보려 한다. PKCE는 클라이언트가 네이티브 앱이나 SPA일때 추천되는 방식이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 퍼블릭 클라이언트가 엑세스 토큰을 요청했을 때, 인증 절차만으로는 해결할 수 없는 보안 문제에 노출된다. 이는 네이티브앱과 SPA가 가진 특징 때문이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 네이티브 앱들은 다음과 같은 문제를 가지고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 1. client secret을 안전하게 저장할 수 없다. 앱을 디컴파일링 하면 클라이언트 암호가 노출된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 2. Custom URL scheme을 통해 리다이렉트를 캡쳐해 악의적 애플리케이션이 인증 서버에서 인증 코드를 받을 수 있다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; SPA는 다음과 같은 문제를 가지고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 1. 모든 코드를 브라우저에서 볼 수 있기 때문에 client secret을 안전히 저장할 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이런 문제들을 해결하기 위해 <a href="https://datatracker.ietf.org/doc/html/rfc7636" target="_blank" rel="noopener">OAuth 2.0 RFC 7636</a>에 정의된 PKCE를 사용하는 것을 추천한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; PKCE는 기존 Authorization code flow를 강화한 버전으로 정적 클라이언트 암호를 대신해 동적으로 생성한 문자열을 사용한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>용어 정의</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; PCKE 플로우를 설명하기 전에 PCKE에서 사용하는 용어 부터 정의하고 가자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; <b>code verifier</b>: 앱에 의해 생성된 랜덤한 문자열이다. 동적으로 생성된 이 문자열은 첫 인증 요청과 마지막 엑세스 토큰 요청을 연결시킨다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; <b>code challenge</b>: code verifier에서 도출된 것이다. 이는 code verifier를 평문(plain)으로 사용하거나 S256를 이용해 생성해야 한다. 이 중 되도록이면 S256을 사용해야 하며 client verifier를 SHA256으로 암호화하고 base64로 인코딩해서 code challenge를 만들 수 있다. code challenge는 서버에서 복호화되고 동일 클라이언트에서 전송한 요청인지를 확인하는데 사용된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<b>code challenge method: </b>어떤 방법을 사용해 code verifier를 변환했는지를 서버에게 알린다. 비워놓으면 plain으로 인식한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>PKCE 플로우</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; PKCE는 다음과 같은 플로우를 가진다<br></span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/UHJvb2YgS2V5IGZvciBDb2RlIEV4Y2hhbmdlKFBLQ0Up/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">(OAuth tenant가 access token을 응답할 때 <a href="https://auth0.com/docs/secure/tokens/id-tokens" target="_blank" rel="noopener">ID token</a>도 같이 응답된다)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">SPA에서 PKCE를 사용하는 예시: <a href="https://auth0.com/docs/libraries/auth0-single-page-app-sdk" target="_blank" rel="noopener">링크</a></span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Standard Authorization Code Flow</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>PKCE의 장점을 더 잘 이해하기 위해 기존의 authorization code flow를 보자. 이는 SSR을 상정하고 나온 플로우이기 때문에 정적인 client sercret을 그대로 전송하게 된다. 해당 플로우는 <a href="https://datatracker.ietf.org/doc/html/rfc6749#section-4.1" target="_blank" rel="noopener">OAuth 2.0 RFC 6749, section 4.1</a>에 정의되 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/UHJvb2YgS2V5IGZvciBDb2RlIEV4Y2hhbmdlKFBLQ0Up/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처:</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce" target="_blank" rel="noopener">Authorization Code Flow with Proof Key for Code Exchange(PKCE)</a></span></p>
<figure id="og_1657455851926" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="Auth0" data-og-description="Get started using Auth0. Implement authentication for any kind of application in minutes." data-og-host="auth0.com" data-og-source-url="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce" data-og-url="https://auth0.com/docs/" data-og-image="https://scrap.kakaocdn.net/dn/fms8A/hyO1XmFuFS/XkwMmmTwlxb5xp0OBdwhDk/img.png?width=1200&amp;height=630&amp;face=0_0_1200_630"><a href="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce" target="_blank" rel="noopener" data-source-url="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/fms8A/hyO1XmFuFS/XkwMmmTwlxb5xp0OBdwhDk/img.png?width=1200&amp;height=630&amp;face=0_0_1200_630');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">Auth0</p>
<p class="og-desc" data-ke-size="size16">Get started using Auth0. Implement authentication for any kind of application in minutes.</p>
<p class="og-host" data-ke-size="size16">auth0.com</p>
</div>
</a></figure>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://dropbox.tech/developers/pkce--what-and-why-" target="_blank" rel="noopener">PCKE: What and Why?</a></span></p>
<figure id="og_1657455861290" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="PKCE: What and Why?" data-og-description="Come learn about the PKCE OAuth flow! How it works, why it’s valuable, and how to use it to authorize your Dropbox app." data-og-host="dropbox.tech" data-og-source-url="https://dropbox.tech/developers/pkce--what-and-why-" data-og-url="https://dropbox.tech/developers/pkce--what-and-why-" data-og-image="https://scrap.kakaocdn.net/dn/exuCB/hyO16jDcPp/RKKh4E1vK94cK5EgyY9xr0/img.png?width=800&amp;height=420&amp;face=0_0_800_420,https://scrap.kakaocdn.net/dn/Phqxx/hyO3p9F1QX/ip4OraZtLpqq3GGGAOqTyk/img.png?width=720&amp;height=700&amp;face=0_0_720_700,https://scrap.kakaocdn.net/dn/7G5nE/hyO2aTQip4/Fyqfal30X6bqy7No8yJAik/img.png?width=1440&amp;height=305&amp;face=0_0_1440_305"><a href="https://dropbox.tech/developers/pkce--what-and-why-" target="_blank" rel="noopener" data-source-url="https://dropbox.tech/developers/pkce--what-and-why-">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/exuCB/hyO16jDcPp/RKKh4E1vK94cK5EgyY9xr0/img.png?width=800&amp;height=420&amp;face=0_0_800_420,https://scrap.kakaocdn.net/dn/Phqxx/hyO3p9F1QX/ip4OraZtLpqq3GGGAOqTyk/img.png?width=720&amp;height=700&amp;face=0_0_720_700,https://scrap.kakaocdn.net/dn/7G5nE/hyO2aTQip4/Fyqfal30X6bqy7No8yJAik/img.png?width=1440&amp;height=305&amp;face=0_0_1440_305');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">PKCE: What and Why?</p>
<p class="og-desc" data-ke-size="size16">Come learn about the PKCE OAuth flow! How it works, why it’s valuable, and how to use it to authorize your Dropbox app.</p>
<p class="og-host" data-ke-size="size16">dropbox.tech</p>
</div>
</a></figure>
<p data-ke-size="size16"><a href="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow" target="_blank" rel="noopener">Authorization Code Flow</a></p>
<figure id="og_1657455876959" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="Auth0" data-og-description="Get started using Auth0. Implement authentication for any kind of application in minutes." data-og-host="auth0.com" data-og-source-url="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow" data-og-url="https://auth0.com/docs/" data-og-image="https://scrap.kakaocdn.net/dn/7FyoG/hyO1YFSr2n/ok4ymrVBXjWQzU1EN7wRtk/img.png?width=1200&amp;height=630&amp;face=0_0_1200_630"><a href="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow" target="_blank" rel="noopener" data-source-url="https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/7FyoG/hyO1YFSr2n/ok4ymrVBXjWQzU1EN7wRtk/img.png?width=1200&amp;height=630&amp;face=0_0_1200_630');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">Auth0</p>
<p class="og-desc" data-ke-size="size16">Get started using Auth0. Implement authentication for any kind of application in minutes.</p>
<p class="og-host" data-ke-size="size16">auth0.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp;</p>
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