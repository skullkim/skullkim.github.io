---
layout:       post
title:        "teamproject1 후기"
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
                            <p data-ke-size="size16">&nbsp; 수업을 시작했더니 주제를 직접정하는 것이 아닌 지하철 노선도 서비스를 만드는 것으로 이미 정해져 있었다. 그때문에 모든 팀이 지하철 노선도 서비스를 만들게 되었다. 여느 학교 팀프로젝트와 같이 이 수업 역시 거의 혼자서 다 구현했다.</p>
<p data-ke-size="size16">&nbsp; 사용한 기술은 다음과 같다:</p>
<p data-ke-size="size16">&nbsp; &nbsp; 프론트: React, JS</p>
<p data-ke-size="size16">&nbsp; &nbsp; 백엔드: Express, TS, JWT</p>
<p data-ke-size="size16">&nbsp; &nbsp; Database: mysql, typeorm</p>
<p data-ke-size="size16">&nbsp; &nbsp; 인프라: Docker, nginx, HTTPS</p>
<p data-ke-size="size16">&nbsp; 이번 프로젝트를 하면서 타입스크립트를 처음 써봤고 덕분에 많이 해맸다. 타입을 지정해야 하는데 원하는대로 지정되지 않고 자꾸만 에러가 띄워져서 원인을 찾는대 많은 시간을 소비했다. Express로 여러 프로젝트를 진행하다 보니 처음 배울때 인강에서 알려준 디렉토리 구조를 그래로 사용했을때 코드에 대한 가독성이 떨어지는거 같아서 아래의 글을 참고해 디렉토리 구조를 싹다 바꾸어서 프로젝트를 진행했다.</p>
<p data-ke-size="size16"><a href="https://medium.com/codechef-vit/a-better-project-structure-with-express-and-node-js-c23abc2d736f" target="_blank" rel="noopener">https://medium.com/codechef-vit/a-better-project-structure-with-express-and-node-js-c23abc2d736f</a></p>
<figure id="og_1640586879526" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="article" data-og-title="A better project structure with Express and Node.Js" data-og-description="Learning how to structure your folder for other people to understand your code and further work on it easily is a great deal and shows how…" data-og-host="medium.com" data-og-source-url="https://medium.com/codechef-vit/a-better-project-structure-with-express-and-node-js-c23abc2d736f" data-og-url="https://medium.com/codechef-vit/a-better-project-structure-with-express-and-node-js-c23abc2d736f" data-og-image="https://scrap.kakaocdn.net/dn/mNPZe/hyMREaEr7G/Fhvossvwk0zuHCuOduA7M1/img.png?width=730&amp;height=453&amp;face=0_0_730_453,https://scrap.kakaocdn.net/dn/dKEhZ6/hyMRy2zVjU/kAW77qzCrQggn1DdsHGCzK/img.png?width=60&amp;height=37&amp;face=0_0_60_37"><a href="https://medium.com/codechef-vit/a-better-project-structure-with-express-and-node-js-c23abc2d736f" target="_blank" rel="noopener" data-source-url="https://medium.com/codechef-vit/a-better-project-structure-with-express-and-node-js-c23abc2d736f">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/mNPZe/hyMREaEr7G/Fhvossvwk0zuHCuOduA7M1/img.png?width=730&amp;height=453&amp;face=0_0_730_453,https://scrap.kakaocdn.net/dn/dKEhZ6/hyMRy2zVjU/kAW77qzCrQggn1DdsHGCzK/img.png?width=60&amp;height=37&amp;face=0_0_60_37');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">A better project structure with Express and Node.Js</p>
<p class="og-desc" data-ke-size="size16">Learning how to structure your folder for other people to understand your code and further work on it easily is a great deal and shows how…</p>
<p class="og-host" data-ke-size="size16">medium.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp; 기존에 진행했던 프로젝트인 유투브 클론코딩을 예로 들어 디렉토리 구조를 설명하면 다음과 같다.</p>
<p data-ke-size="size16"><a href="https://github.com/skullkim/Itube-simple-clone-of-youtube" target="_blank" rel="noopener">유투브 클론코딩 디렉토리 구조</a>:</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/dGVhbXByb2plY3QxIO2bhOq4sA==/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><a href="https://github.com/skullkim/metro-map-production/tree/main/backend" target="_blank" rel="noopener">지하철 노선도 서비스 디렉토리 구조:</a></p>
<p data-ke-size="size16">&nbsp;</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/dGVhbXByb2plY3QxIO2bhOq4sA==/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">이렇게 파일 구조를 바꾸고 보니 확실히 유지보수성이 높아진거 같다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">이번 프로젝트를 하면서 API문서를 처음 작성해 봤다. 노션으로 작성하고 markdown으로 export했는데 처음 작성하는 거라 제대로 작성을 한건지 의문이다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">typescript로 백엔드를 처음 하면서 sequelize대신 typeorm을 처음 사용했는데 typeorm이 sequelize보다 더 직관적이고 코드가 더 깔끔해 지는거 같다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">기존 프로젝트에서는 AWS를 사용하다가 프리티어 기간이 만료되서 집에서 운영하는 내 개인서버에 배포를 했다. 그런데 개인서버 사양때문인지 3명정도가 동시에 검색 여러번 하면 서버가 뻗는다.... 최적화를 해보고 싶은데 어떻게 해야 최적화를 할 수 있는지 감 조차 잡히지 않는다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">프론트엔드에서 지하철 노선도를 직접 그려서 역마다 모달의 띄우기 위해 노선도를 일일이 다 그렸다. react-d3-graph라는 라이브러리를 사용했는데 애초에 이런 노선도 그리라고 나온 라이브러리도 아닐 뿐더러 유지보수가 제대로 안되있는지 노선도에 커서를 두고 스크롤을 하면 콘솔창에 에러가 뜬다. 사용하는데는 문제가 없지만 참... 찝찝하네.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">production 레파지토리:</p>
<p data-ke-size="size16"><a href="https://github.com/skullkim/metro-map-production" target="_blank" rel="noopener">https://github.com/skullkim/metro-map-production</a></p>
<figure id="og_1640588461938" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/metro-map-production" data-og-description="Contribute to skullkim/metro-map-production development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/metro-map-production" data-og-url="https://github.com/skullkim/metro-map-production" data-og-image="https://scrap.kakaocdn.net/dn/DawAH/hyMRKopF3z/WPZ7NGAkvLWr5ySWOha8Tk/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/metro-map-production" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/metro-map-production">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/DawAH/hyMRKopF3z/WPZ7NGAkvLWr5ySWOha8Tk/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/metro-map-production</p>
<p class="og-desc" data-ke-size="size16">Contribute to skullkim/metro-map-production development by creating an account on GitHub.</p>
<p class="og-host" data-ke-size="size16">github.com</p>
</div>
</a></figure>
<p data-ke-size="size16">develop 레파지토리:</p>
<p data-ke-size="size16"><a href="https://github.com/skullkim/metro-map-front" target="_blank" rel="noopener">https://github.com/skullkim/metro-map-front</a></p>
<figure id="og_1640588497048" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/metro-map-front: team project1 front end" data-og-description="team project1 front end. Contribute to skullkim/metro-map-front development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/metro-map-front" data-og-url="https://github.com/skullkim/metro-map-front" data-og-image="https://scrap.kakaocdn.net/dn/xM39M/hyMRJwgMeQ/hvzZMPynkjfyM5AXrEyhGK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/metro-map-front" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/metro-map-front">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/xM39M/hyMRJwgMeQ/hvzZMPynkjfyM5AXrEyhGK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/metro-map-front: team project1 front end</p>
<p class="og-desc" data-ke-size="size16">team project1 front end. Contribute to skullkim/metro-map-front development by creating an account on GitHub.</p>
<p class="og-host" data-ke-size="size16">github.com</p>
</div>
</a></figure>
<p data-ke-size="size16"><a href="https://github.com/skullkim/metro-map-backend" target="_blank" rel="noopener">https://github.com/skullkim/metro-map-backend</a></p>
<figure id="og_1640588504590" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/metro-map-backend: team project1 backend" data-og-description="team project1 backend. Contribute to skullkim/metro-map-backend development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/metro-map-backend" data-og-url="https://github.com/skullkim/metro-map-backend" data-og-image="https://scrap.kakaocdn.net/dn/cwvfdn/hyMRKvcom7/KiEHFHuAiiGbotsd6cquzK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/metro-map-backend" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/metro-map-backend">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/cwvfdn/hyMRKvcom7/KiEHFHuAiiGbotsd6cquzK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/metro-map-backend: team project1 backend</p>
<p class="og-desc" data-ke-size="size16">team project1 backend. Contribute to skullkim/metro-map-backend development by creating an account on GitHub.</p>
<p class="og-host" data-ke-size="size16">github.com</p>
</div>
</a></figure>
<p data-ke-size="size16"><a href="https://github.com/skullkim/metro-map-docu" target="_blank" rel="noopener">https://github.com/skullkim/metro-map-docu</a></p>
<figure id="og_1640588511711" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/metro-map-docu: team project1 document" data-og-description="team project1 document. Contribute to skullkim/metro-map-docu development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/metro-map-docu" data-og-url="https://github.com/skullkim/metro-map-docu" data-og-image="https://scrap.kakaocdn.net/dn/R6sg3/hyMRv5TJWR/wDnMxKHaezYMZDKM4kZbn0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/metro-map-docu" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/metro-map-docu">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/R6sg3/hyMRv5TJWR/wDnMxKHaezYMZDKM4kZbn0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/metro-map-docu: team project1 document</p>
<p class="og-desc" data-ke-size="size16">team project1 document. Contribute to skullkim/metro-map-docu development by creating an account on GitHub.</p>
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