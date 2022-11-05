---
layout:       post
title:        "Web application"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- javascript
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
                            <p data-ke-size="size16"><b>History API</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>History API는 JS에서 브라우저의 URI나 이력 정보를 조작하기 위해한 API이다. 기존에는 애플리케이션 로직을 서버 사이드에서 담당하고 클라이언트 사이드는 단순히 정보를 표시하는 정도의 역할만 했었다. 하지만 최근에는 복잡한 상태의 이동을 클라이언트 사이드가 담당하게 되었고 Ajax로 콘텐츠가 클라이언트 사이드에서 갱신되면 URL이 바뀌지 않기 때문에 항상 페이지의 상태와 대응하게 js에서 URL을 관리해야 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 하지만 단순히 페이지의 URL을 바꾸는 것은 페이지의 이동을 발생시키고 JS의 상태도 초기화 돼버린다. 이때 사용하는 것이 History API이다. 이 API를 사용하면 페이지를 이동시키지 않고도 URL경로를 임의의 것을 바꿀 수 있다.</p>
<p data-ke-size="size16"><b>Hash fragment</b></p>
<p data-ke-size="size16">&nbsp; 원래 URL은 웹상의 콘텐츠를 식별하는데 사용된다. 하지만 AJAX를 사용하면 페이지 이동없이도 콘텐츠를 새롭게 표기할 수 있기 때문에 클라이언트 사이드에서 URL을 확실히 관리해야 한다. URL과 웹 애플리케이션은 분리가 불가능한 개념이다. URL이 웹상의 콘텐츠를 식별하는 역할을 제대로 수행하지 않으면 북마크, 외부 콘텐츠의 링크를 거는 일 등을 수행하지 못한다.</p>
<p data-ke-size="size16">&nbsp; 이 문제를 해결하기 위해 많은 Ajax 애플리케이션에서는 hash fragment를 사용하고 있다.&nbsp;</p>
<p data-ke-size="size16">Hash fragment와 크롤러</p>
<p data-ke-size="size16">&nbsp; Hash fragment를 위에서 서술한 용도로 사용한다면 검색 엔진 등의 크롤러와 상생하기 어려워 진다. 일반적인 크롤러는 애플리케이션에 포함된 JS를 해석하지 않는다. 따라서 페이지 로딩이 끝난 후 동적으로 가져온 콘텐츠를 크롤링할 수 없다. 그때문에 크롤러가 페이지의 콘텐츠를 수집하게 하려면 크롤러의 접근을 서버 사이드에서 판단하고, 크롤러에 대해 JS를 포함하지 않는 정적인 콘텐츠를 반환해야 한다.</p>
<p data-ke-size="size16">&nbsp; 하지만 URL의 hash fragment부분은 서버로 송신되지 않는 문제가 존재한다. 그때문에 크롤러는 본래 URL이 가리키는 콘텐츠를 정확히 구할 수 없다. 이를 해결하기 위해 구글에서는 다음과 같은 사양을 제시했다. 크롤러는 '#!'를 포함한 URL을 Ajax 애플리케이션이라 판단하고, '#!'fmf '?_escaped_fragment_'라는 파라미터로 치환해 서버로 접근하는 것이다. 예를 들어 <a href="http://www.example.com/#!/foo라는">http://www.example.com/#!/foo라는</a> URL이 있으면 이를 <a href="http://www.example.com/?_escaped_fragment_=/foo로">http://www.example.com/?_escaped_fragment_=/foo로</a> 치환한다. 따라서 서버에서는 _escaped_fragment_파라미터를 포함하는 요청을 크롤러로 판단하고 적절한 정적콘텐츠를 응답해야 한다.</p>
<p data-ke-size="size16"><b>인터페이스</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>History API에서는 주로 history 객체와 popstate 이벤트를 사용한다. history 객체는 window 객체의 프로퍼티로 이력 조작을 담당합니다.</p>
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