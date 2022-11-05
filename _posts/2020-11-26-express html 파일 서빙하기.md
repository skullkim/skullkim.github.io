---
layout:       post
title:        "express html 파일 서빙하기"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- Express
- nodejs
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
                            <p>express로 html 파일을 서빙하기 위해서는 res.send()대신 res.sendFile()을 사용하면 된다</p>
<p></p><figure class="imageblock alignLeft" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/ZXhwcmVzcyBodG1sIO2MjOydvCDshJzruZntlZjquLA=/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>code</figcaption>
</figure><figure class="imageblock alignLeft" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/ZXhwcmVzcyBodG1sIO2MjOydvCDshJzruZntlZjquLA=/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>terminal</figcaption>
</figure><figure class="imageblock alignLeft" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/ZXhwcmVzcyBodG1sIO2MjOydvCDshJzruZntlZjquLA=/img_2.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>html code</figcaption>
</figure><figure class="imageblock alignLeft" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/ZXhwcmVzcyBodG1sIO2MjOydvCDshJzruZntlZjquLA=/img_3.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>browser</figcaption>
</figure><p></p>
<p>위 예제에서 파일을 서빙할때 path.join(__dirname, './public/index.html');을 사용했다.&nbsp;</p>
<p>path는 운영체제 별로 경로를 표시하는 방법이 다른 문제를 해결해 주는 모듈이다. path.join()은 상대경로를 합쳐 절대 경로로 바꾸어 준다.</p>
<p>__dirname은 현재의 경로를 의미하고 './public/index.html'은 원하는 파일의 경로이다.</p>
<figure data-ke-type="image" data-ke-style="alignLeft">
<figcaption style="display: none;"></figcaption>
</figure>
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