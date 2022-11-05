---
layout:       post
title:        "learning code refactoring production"
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
                            <p data-ke-size="size16">&nbsp; 2020년 1학기 부터 끌고온(?) 프로젝트가 드디어 끝났다. 정확히는 1학기때 끝냈으나 여름 방학때 리액트를 배우면서, docker, nginx를 배우면서 이 기술들을 적용해볼 프로젝트가 필요했고 1학기때 했던 프로젝트를 리팩토링해 프론트를 react로 하고 docker, nginx, https를 적용했다. 리팩토링을 하면서 배우게 된거는 다음 링크에 적어 두었다.</p>
<p data-ke-size="size16"><a href="https://iskull-dev.tistory.com/183?category=911357">https://iskull-dev.tistory.com/183?category=911357</a>&nbsp;</p>
<figure id="og_1635751149762" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="learning code refactoring" data-og-description="올해 여름 방학때 리액트를 시작하고 리액트를 좀 더 숙련되게 사용하기 위해 시작한 프로젝트이다. 그런데 중간에 멋사 플잭으로 인해 도커, 쿠버네티스를 공부해야 하는 상황이 되었고 이 프" data-og-host="iskull-dev.tistory.com" data-og-source-url="https://iskull-dev.tistory.com/183?category=911357" data-og-url="https://iskull-dev.tistory.com/183" data-og-image="https://scrap.kakaocdn.net/dn/XAs9a/hyMaVED1Uq/7C8wQKLZPbc4jAQ9Ru8JQk/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/cPCTOR/hyMaY9cNdV/6LnufHPiktpoIpugtblQw0/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/rr6UK/hyMaZ1kmzk/1KGy7emvB88vjTOupcQdO0/img.png?width=264&amp;height=200&amp;face=0_0_264_200"><a href="https://iskull-dev.tistory.com/183?category=911357" target="_blank" rel="noopener" data-source-url="https://iskull-dev.tistory.com/183?category=911357">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/XAs9a/hyMaVED1Uq/7C8wQKLZPbc4jAQ9Ru8JQk/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/cPCTOR/hyMaY9cNdV/6LnufHPiktpoIpugtblQw0/img.png?width=800&amp;height=800&amp;face=0_0_800_800,https://scrap.kakaocdn.net/dn/rr6UK/hyMaZ1kmzk/1KGy7emvB88vjTOupcQdO0/img.png?width=264&amp;height=200&amp;face=0_0_264_200');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">learning code refactoring</p>
<p class="og-desc" data-ke-size="size16">올해 여름 방학때 리액트를 시작하고 리액트를 좀 더 숙련되게 사용하기 위해 시작한 프로젝트이다. 그런데 중간에 멋사 플잭으로 인해 도커, 쿠버네티스를 공부해야 하는 상황이 되었고 이 프</p>
<p class="og-host" data-ke-size="size16">iskull-dev.tistory.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp; 인프라 부분 얘기를 하자면 다 처음 해보는 거라 많이 해맸다. nginx를 예전에 사용해 볼려고 시도를 했었지만 실패하고 이번 프로젝트에서 처음부터 다 다시 시작했다. docker 역시 처음 배우는 거라 인강을 보면서 개념을 익혔고 차근차근 단계를 밟아 나가면서 이번 프로젝트에 적용을 시킨 결과 결국에는 성공했다. HTTPS 역시 이번 프로젝트를 하면서 동작 과정을 처음으로 배우게 되었고 그 과정에서 HTTP가 동작하는 좀 더 세부적인 과정(3 way handshake같은)을 알 수 있었다.</p>
<p data-ke-size="size16">&nbsp; HTTPS를 적용시키기 위해 도메인도 하나 구매했다(skullkim-dev.com). 이 도메인은 단순히 이번 프로젝트를 위한 것이 아닌 내 포트폴리오 웹사이트를 만들기 위한 목적으로 구매한거다. 따라서 이 도메인을 재활용해 올해 내에 나의 포트폴리오 웹사이트를 만들 예정이다.&nbsp;</p>
<p data-ke-size="size16">프로젝트를 하면서 공부한 내용:</p>
<p data-ke-size="size16"><a href="https://iskull-dev.tistory.com/category/%EC%9D%B8%ED%94%84%EB%9D%BC" target="_blank" rel="noopener">https://iskull-dev.tistory.com/category/%EC%9D%B8%ED%94%84%EB%9D%BC</a></p>
<figure id="og_1635751499004" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="'인프라' 카테고리의 글 목록" data-og-description=" " data-og-host="iskull-dev.tistory.com" data-og-source-url="https://iskull-dev.tistory.com/category/%EC%9D%B8%ED%94%84%EB%9D%BC" data-og-url="https://iskull-dev.tistory.com/category/%EC%9D%B8%ED%94%84%EB%9D%BC" data-og-image="https://scrap.kakaocdn.net/dn/uIU0a/hyMaYg4PUx/ob3UczmpffEfyPKJtDnAEk/img.jpg?width=750&amp;height=734&amp;face=0_0_750_734,https://scrap.kakaocdn.net/dn/1enCt/hyMaZmK8Fr/VsaB2lIVu0Stt5WeIguKO1/img.jpg?width=750&amp;height=734&amp;face=0_0_750_734,https://scrap.kakaocdn.net/dn/dVPb3d/hyMaZNODFF/hyvXxuPTv0ie1qgpw0HQ4K/img.png?width=264&amp;height=200&amp;face=0_0_264_200"><a href="https://iskull-dev.tistory.com/category/%EC%9D%B8%ED%94%84%EB%9D%BC" target="_blank" rel="noopener" data-source-url="https://iskull-dev.tistory.com/category/%EC%9D%B8%ED%94%84%EB%9D%BC">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/uIU0a/hyMaYg4PUx/ob3UczmpffEfyPKJtDnAEk/img.jpg?width=750&amp;height=734&amp;face=0_0_750_734,https://scrap.kakaocdn.net/dn/1enCt/hyMaZmK8Fr/VsaB2lIVu0Stt5WeIguKO1/img.jpg?width=750&amp;height=734&amp;face=0_0_750_734,https://scrap.kakaocdn.net/dn/dVPb3d/hyMaZNODFF/hyvXxuPTv0ie1qgpw0HQ4K/img.png?width=264&amp;height=200&amp;face=0_0_264_200');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">'인프라' 카테고리의 글 목록</p>
<p class="og-desc" data-ke-size="size16">&nbsp;</p>
<p class="og-host" data-ke-size="size16">iskull-dev.tistory.com</p>
</div>
</a></figure>
<p data-ke-size="size16"><a href="https://iskull-dev.tistory.com/200?category=906431">https://iskull-dev.tistory.com/200?category=906431</a>&nbsp;</p>
<figure id="og_1635751514910" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="HTTPS" data-og-description="기존 HTTP는 클라이언트, 서버 사이의 요청, 응답을 평문으로 전송하기 때문에 중간에 이런 데이터들을 가로채서 볼 수 있었다(와이어샤크 등을 통해). 이런 문제를 해결하기 위해 클라리언트, 서" data-og-host="iskull-dev.tistory.com" data-og-source-url="https://iskull-dev.tistory.com/200?category=906431" data-og-url="https://iskull-dev.tistory.com/200" data-og-image="https://scrap.kakaocdn.net/dn/dYyM9f/hyMa5UNXo6/JQKUunkv6SN9h1Bcfko3Ak/img.png?width=361&amp;height=170&amp;face=0_0_361_170,https://scrap.kakaocdn.net/dn/AIwLD/hyMa1EQm0d/t950AlyOfJ0l6pQQjWSJd1/img.png?width=361&amp;height=170&amp;face=0_0_361_170,https://scrap.kakaocdn.net/dn/cNHWRn/hyMa0MI4mV/juZ1eRSYERlddBS82OwxVK/img.png?width=1358&amp;height=1288&amp;face=0_0_1358_1288"><a href="https://iskull-dev.tistory.com/200?category=906431" target="_blank" rel="noopener" data-source-url="https://iskull-dev.tistory.com/200?category=906431">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/dYyM9f/hyMa5UNXo6/JQKUunkv6SN9h1Bcfko3Ak/img.png?width=361&amp;height=170&amp;face=0_0_361_170,https://scrap.kakaocdn.net/dn/AIwLD/hyMa1EQm0d/t950AlyOfJ0l6pQQjWSJd1/img.png?width=361&amp;height=170&amp;face=0_0_361_170,https://scrap.kakaocdn.net/dn/cNHWRn/hyMa0MI4mV/juZ1eRSYERlddBS82OwxVK/img.png?width=1358&amp;height=1288&amp;face=0_0_1358_1288');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">HTTPS</p>
<p class="og-desc" data-ke-size="size16">기존 HTTP는 클라이언트, 서버 사이의 요청, 응답을 평문으로 전송하기 때문에 중간에 이런 데이터들을 가로채서 볼 수 있었다(와이어샤크 등을 통해). 이런 문제를 해결하기 위해 클라리언트, 서</p>
<p class="og-host" data-ke-size="size16">iskull-dev.tistory.com</p>
</div>
</a></figure>
<p data-ke-size="size16"><a href="https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71" target="_blank" rel="noopener">https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71</a></p>
<figure id="og_1635751524360" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="Nginx and Let’s Encrypt with Docker in Less Than 5 Minutes" data-og-description="Getting Nginx to run with Let’s Encrypt in a docker-compose environment is more tricky than you’d think&nbsp;…" data-og-host="pentacent.medium.com" data-og-source-url="https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71" data-og-url="https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71" data-og-image="https://scrap.kakaocdn.net/dn/1Zn2A/hyMa758Xk7/O6JwwKa0qiy0foh33YDGj1/img.jpg?width=1200&amp;height=675&amp;face=0_0_1200_675,https://scrap.kakaocdn.net/dn/ss7hU/hyMa7ZmTZL/FLv7RbRFys2ssMakr94rO1/img.jpg?width=2000&amp;height=1125&amp;face=0_0_2000_1125"><a href="https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71" target="_blank" rel="noopener" data-source-url="https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/1Zn2A/hyMa758Xk7/O6JwwKa0qiy0foh33YDGj1/img.jpg?width=1200&amp;height=675&amp;face=0_0_1200_675,https://scrap.kakaocdn.net/dn/ss7hU/hyMa7ZmTZL/FLv7RbRFys2ssMakr94rO1/img.jpg?width=2000&amp;height=1125&amp;face=0_0_2000_1125');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">Nginx and Let’s Encrypt with Docker in Less Than 5 Minutes</p>
<p class="og-desc" data-ke-size="size16">Getting Nginx to run with Let’s Encrypt in a docker-compose environment is more tricky than you’d think&nbsp;…</p>
<p class="og-host" data-ke-size="size16">pentacent.medium.com</p>
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