---
layout:       post
title:        "learning code refactoring"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- 회고 
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
                            <p data-ke-size="size16">&nbsp; 올해 여름 방학때 리액트를 시작하고 리액트를 좀 더 숙련되게 사용하기 위해 시작한 프로젝트이다. 그런데 중간에 멋사 플잭으로 인해 도커, 쿠버네티스를 공부해야 하는 상황이 되었고 이 프로잭트를 활용해 도커, 쿠버네티스를 공부해 볼려고 한다. 따라서 이번 글은 프로젝트를 하나 완벽히 끝내고 쓴 글이라기 보다는 그냥 실질적인 배포 이전 리액트로 플젝을 하면서 배운것을 정리하는 정도 이다.</p>
<p data-ke-size="size16">&nbsp; 리액트를 그동안 배우면서 책에 나와있는 아누 작은 플잭들을 결과만 보고 혼자 구현한거, 멋사에서 플잭을 하면서 전체 기능 중 일부만 구현해 본거랑 비교를 하면 확실히 배운게 더 많은거 같다. 이래서 혼자 플잭을 해봐야되...</p>
<p data-ke-size="size16">&nbsp; 우선 API 서버를 처음 구축해 본다. 기존 SSR를 사용한 플젝에서는 상태코드, Content-Type을 크게 신경쓰지 않았지만 이번 플젝에서는 일일이 다 설정해 보았다(완벽하지는 않겠지...). 또 한 실질적인 플젝에서 JWT를 처음 제대로 사용해 보았다. 기존 플젝에서는 세션-쿠키를 많이 사용했고 JWT를 사용해 보았을 때도 그냥 access token유효 기간을 엄청 길게 해서 사용했지만 이번에는 refresh token 까지 사용해 보았다.</p>
<p data-ke-size="size16">&nbsp; 클라이언트로 넘어가면 참 배운게 많다. Yup에 대한 좀 더 다양한 사용법을 배웠고 토큰 저장 방식에 대해서도 많이 배웠다. 맨 처음에는 그냥 전역 상태에다 저장을 했는다 새로고침 할때 마다 날라가더라. 그래서 access token은 로컬 스토리지에, refresh token은 쿠기에 저장 했다. 쿠키 관결해서도 좀 해맸는데 알고 보니 이것도 cors문제 중 하나였다. 토큰 만료시 refresh token으로 access token재발급을 하는 부분도 엄청 해맸다. 맨 첨에는 그냥 인증하는 코드를 생으로 작성했는데 잘 안되서 찾아 보니 axios interceptor 라는게 있더라. 그래서 그걸 사용했더니 이번에는 로컬 스토리지에 저장한 accessToken이 안지워 져서 한참을 해맨 결과 비동이 문제라는 것을 알게 되었다.</p>
<p data-ke-size="size16">&nbsp; 로그아웃을 할때 로직은 다음과 같다: access token이 유효하지 않다(비동기) -&gt; refreshToken으로 토큰 재발급, 저장(비동기) -&gt; 기존 토큰 지움(동기). 이렇다 보니 로그아웃을 하면 토큰이 지워지고 새로 발급 받은 토큰이 로컬스토리지에 저장되 로그아웃을 눌러도 로그아웃이 안된거 처럼 보였다. 토큰을 지우는 부분을 비동기로 처리해 문제를 해결했다.</p>
<p data-ke-size="size16">&nbsp; 리프레시 토큰으로 토큰을 재발급 받는 과정에서도 문제가 발생했다. 아무리 토큰은 재발급 받아도 유효하지 않다는 결과가 나왔다. 알고 보니 토큰을 발급하게 되면 자동으로 iat라는 토큰 발급 시각을 나타내는 프로퍼티가 자동으로 추가되는데, 얘를 리프레시 토근을 decode한 거에서 빼지 않고 그대로 이를 기반으로 access token을 만들어 생긴 문제였다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">JWT와 공격 취약점에 대해:<a href="https://iskull-dev.tistory.com/184" target="_blank" rel="noopener">https://iskull-dev.tistory.com/184</a></p>
<figure id="og_1630899986275" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="프론트에서 안전하게 JWT 인증 방식 처리하기." data-og-description="XSS(Cross-Site Scripting) &nbsp;공격자가 클라이언트 브리우저에 js를 삽입해 실행하는 공격이다. input tag를 통해 또는 url을 통해 js를 적어 클라이언트에서 실행이 가능하다면 사이트에 스크립트를 삽입해" data-og-host="iskull-dev.tistory.com" data-og-source-url="https://iskull-dev.tistory.com/184" data-og-url="https://iskull-dev.tistory.com/184" data-og-image="https://scrap.kakaocdn.net/dn/b2avZa/hyLuZO0E1A/SztYBikOCKu2cjiv5z8Igk/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/clzcgJ/hyLwbG3l6t/UICBRyl6ido2W6jG0JLSQ0/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/6v1qV/hyLwfCGSQ9/PLdWhvyYXSJK3VFTqg15Z1/img.png?width=264&amp;height=200&amp;face=0_0_264_200"><a href="https://iskull-dev.tistory.com/184" target="_blank" rel="noopener" data-source-url="https://iskull-dev.tistory.com/184">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/b2avZa/hyLuZO0E1A/SztYBikOCKu2cjiv5z8Igk/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/clzcgJ/hyLwbG3l6t/UICBRyl6ido2W6jG0JLSQ0/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/6v1qV/hyLwfCGSQ9/PLdWhvyYXSJK3VFTqg15Z1/img.png?width=264&amp;height=200&amp;face=0_0_264_200');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">프론트에서 안전하게 JWT 인증 방식 처리하기.</p>
<p class="og-desc" data-ke-size="size16">XSS(Cross-Site Scripting) &nbsp;공격자가 클라이언트 브리우저에 js를 삽입해 실행하는 공격이다. input tag를 통해 또는 url을 통해 js를 적어 클라이언트에서 실행이 가능하다면 사이트에 스크립트를 삽입해</p>
<p class="og-host" data-ke-size="size16">iskull-dev.tistory.com</p>
</div>
</a></figure>
<p data-ke-size="size16">프론트:<a href="https://github.com/skullkim/learning-code-frontend-refactoring" target="_blank" rel="noopener">https://github.com/skullkim/learning-code-frontend-refactoring</a></p>
<figure id="og_1630900040383" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/learning-code-frontend-refactoring: Refactoring teamproject2" data-og-description="Refactoring teamproject2. Contribute to skullkim/learning-code-frontend-refactoring development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/learning-code-frontend-refactoring" data-og-url="https://github.com/skullkim/learning-code-frontend-refactoring" data-og-image="https://scrap.kakaocdn.net/dn/IKB7n/hyLweKycpz/lODd6nAa1ujl5iokvlMuq0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/learning-code-frontend-refactoring" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/learning-code-frontend-refactoring">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/IKB7n/hyLweKycpz/lODd6nAa1ujl5iokvlMuq0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/learning-code-frontend-refactoring: Refactoring teamproject2</p>
<p class="og-desc" data-ke-size="size16">Refactoring teamproject2. Contribute to skullkim/learning-code-frontend-refactoring development by creating an account on GitHub.</p>
<p class="og-host" data-ke-size="size16">github.com</p>
</div>
</a></figure>
<p data-ke-size="size16">백:<a href="https://github.com/skullkim/learning-code-backend-refactoring" target="_blank" rel="noopener">https://github.com/skullkim/learning-code-backend-refactoring</a></p>
<figure id="og_1630900052701" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/learning-code-backend-refactoring" data-og-description="Contribute to skullkim/learning-code-backend-refactoring development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/learning-code-backend-refactoring" data-og-url="https://github.com/skullkim/learning-code-backend-refactoring" data-og-image="https://scrap.kakaocdn.net/dn/ehStP2/hyLuSoOlLK/PEAKkHZZY2rKtpKVgCIrq1/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/learning-code-backend-refactoring" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/learning-code-backend-refactoring">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/ehStP2/hyLuSoOlLK/PEAKkHZZY2rKtpKVgCIrq1/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/learning-code-backend-refactoring</p>
<p class="og-desc" data-ke-size="size16">Contribute to skullkim/learning-code-backend-refactoring development by creating an account on GitHub.</p>
<p class="og-host" data-ke-size="size16">github.com</p>
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