---
layout:       post
title:        "MVC(Model-View-Controller)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- MVC
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
                            <p data-ke-size="size16">&nbsp;&nbsp;<span style="font-family: 'Nanum Gothic';">MVC는 애플리케이션을 3개의 논리적 컴포넌트로 분할하는 아키텍처 패턴이다. 이 3개의 컴포넌트는 각각 모델, 뷰, 컨트롤러이며 각 컴포넌트는 애플리케이션의 특정 부분을 담당한다. MVC는 확장가능한 프로젝트를 만들기 위해 가장 많이 사용되는 웹 개발 프레임워크다.</span></p>
<h3 data-ke-size="size23"><b><span style="font-family: 'Nanum Gothic';">Model</span></b></h3>
<p data-ke-size="size16"><b><span style="font-family: 'Nanum Gothic';">&nbsp; </span></b><span style="font-family: 'Nanum Gothic';">모델 컴포넌트는 유저가 작업하는 모든 데이터 관련 로직에 해당한다. 이 컴포넌트는 뷰와 컨트롤러 사이에 전송될 데이터 또는 다른 비즈니스 로직과 관련된 데이터를 나타낸다. 로직을 처리한 후 모델의 변경사항을 컨트롤러와 뷰에 전달한다. 예를 들어 Customer 객체는 DB에서 소비자 정보를 찾고, 조작하고 업데이트한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; 모델은 다음과 같은 규칙을 준수해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 1. 사용자가 원하는 편집하길 원하는 데이터를 가지고 있어야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 2. 뷰, 컨트롤러에 대해서는 알지 말아야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 3. 변경이 발생하면 변경 통지에 대한 처리방법을 구현해야 한다.</span><span style="font-family: 'Nanum Gothic';"></span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Nanum Gothic';"><b>View</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; 뷰 컴포넌트는 애플리케이션의 모든 UI 로직에 사용된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; 뷰는 다음과 같은 규칙을 준수해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 1. 모델이 가지고 있는 정보를 저장해선 안된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 2. 모델, 컨트롤러에 대해서는 알지 말아야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 3. 변경이 발생하면 변경 통지에 대한 처리방법을 구현해야 한다.</span><span style="font-family: 'Nanum Gothic';"></span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Nanum Gothic';"><b>Controller</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; 컨트롤러는 모델과 뷰 컴포넌트 사이에서 모든 비즈니스 로직과 요청을 처리하는 역할을 한다. 즉, 브릿지 역할을 한다. 모델을 사용해 데이터를 조작하고 뷰와 상호작용해 결과를 출력한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; 컨트롤러는 다음과 같은 규칙을 준수해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 1. 모델, 뷰에 대해 알고 있어야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Nanum Gothic';">&nbsp; &nbsp; 2. 모델, 뷰의 변경을 모니터링 해야 한다.</span></p>
<p></p><figure class="imageblock alignCenter" width="533" height="334">
    <span data-lightbox="lightbox">
        <img src="/img/TVZDKE1vZGVsLVZpZXctQ29udHJvbGxlcik=/img.png" width="533" height="334">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h3 data-ke-size="size23"><b>MVC를 사용하는 이유</b></h3>
<p data-ke-size="size16">&nbsp; 요구 사항은 항상 변한다. 따라서 유지보수의 편의를 위해서는 각 기능간의 결합도가 낮아야 한다. MVC 패턴의 경우 각 컴포넌트는 자신이 맡은 역할만 수행하고 다른 컴포넌트에 결과만 넘겨준다. 따라서 시스템 결합도가 낮아져서 변경이 용이해진다.</p>
<p data-ke-size="size16">&nbsp;</p>
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