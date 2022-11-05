---
layout:       post
title:        "Singleton"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- 디자인패턴
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
                            <p>싱클톤은 오직 하나의 인스턴스만을 생성가능하고 getter 메서드 사나로만 생성, 접근이 가능하다.&nbsp;</p>
<p>싱글톤은 인스턴스가 오직 하나만 존재해야 하므로 생성자가 외부에 드러나 있으면 안되고 클래스 변수를 사용한다.</p>
<p>singleton은 Eager Initialization, lazy Initialization with syncronized를 사용해 구현할 수 있다.</p>
<p><b>Eager</b> <b>Initialization</b></p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/U2luZ2xldG9u/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>Earger Initialization</figcaption>
</figure><p></p>
<p>클래스 변수로 싱글톤 객체를 선언해 클래스 로더에 의해 클래스가 로딩될때 static binding으로 인스턴스가 생성되게 한다. 이때 객체가 생성되기 때문에 thread-safe하다. 싱글턴에서는 thread-safe가 반드시 보장되야 한다.</p>
<p><b>Lazy Initialization with synchronized(동기화 블럭)</b></p>
<p>&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/U2luZ2xldG9u/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>Lazy Initialization wiht Synchronized</figcaption>
</figure><p></p>
<p>메서드에 동기화 블럭을 지정해 thread safe를 지정한다. 이는 인스턴스를 필요한 시점에 요청해 dynamic binding을 통해 인스턴스를 생성한다. 이 방법에 단점은 synchronized에 있다 인스턴스가 생성이 되었든 아니든 일단 getInstance()를 거치는데 synchronized를 사용하면 속도 저하가 생긴다.&nbsp;</p>
<p><b>Double Checking Locking</b></p>
<p><span style="color: #333333;">속도 저하를 줄이기 위해선 인스턴스가 생성될때만 동기화를 하게 하면 된다.</span></p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/U2luZ2xldG9u/img_2.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p><b>장점:</b></p>
<p><b>&nbsp;&nbsp;</b>인스턴스를 하나만 생성하기때문에 메모리에 공간을 덜 차지한다</p>
<p>&nbsp; 인스턴스를 호출할때 두번째 부터는 객체 로딩 시간이 줄어든다</p>
<p>&nbsp; 전역으로 전선되므로 다른 인스턴스와 데이터를 쉽게 공유할 수 있다.</p>
<p><b>단점:</b></p>
<p><b>&nbsp;&nbsp;</b>싱글톤으로 생성된 인스턴스가 다른 클래스의 인스턴스와 많은 데이터를 공유하면 Open-Closed-Principle를 어기게 된다.</p>
<p>Open-Closed-Principle은 개체(클래스, 모듈, 함수 등)는 확장에 대해 열려있어야 하고 수정에 대해 닫혀있어야 한다는 프로그래밍 원칙이다.</p>
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