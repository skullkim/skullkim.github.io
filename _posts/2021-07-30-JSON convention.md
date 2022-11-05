---
layout:       post
title:        "JSON convention"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- JSON
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
                            <p data-ke-size="size16"><b>Client</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>클라이언트가 json 문서와 함께 요청을 할때는 다른 Content-Type을 명시 없이 Content-Type: application/vnd.api_json을 명시해야 한다. 클라이언트가 Accept 헤더에 JSON:API media type을 포함한다면 반드시 다른 미디어 타입이 없는 채로 해당 미디어 타입을 적어도 한번 명시해야 한다. 클라이언트는 반드시 응답 문서의 Content-Type 헤더에 수신된 application/vnd.api+json미디어 유형에 대한 파라미터를 무시해야 한다.</p>
<p data-ke-size="size16"><b>Server</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>서버는 반드시 다른 Content-Type의 명시 없이 Content-Type: application/vnd.api+json을 명시해서 JSON을 응답해야 한다. 만약 클라이언트가 Content-Type에 application/vnd.api+json과 함께 다른 타입을 명시했다면 415 Unsupported Media Type을 전송해야 한다.</p>
<p data-ke-size="size16"><b>JSON 구조</b></p>
<p data-ke-size="size16">&nbsp; 하나의 JSON객체는 반드시 모든 JSON:API 요청, 응답의 루트에 위치에 있어야 한다. 이 객체는 하나의 문서의 top level을 결정한다.</p>
<p data-ke-size="size16">&nbsp; 1. 문서는 다음 중 최소 한개의 top-level 멤버를 반드시 가지고 있어야 한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 1. data: 해당 문서의 "primary data"</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 2. errors: error 객체 배열</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 3. meta: 비표준적인 메타 정보를 담고 있는 메타 객체</p>
<p data-ke-size="size16">&nbsp; &nbsp; data와 errors는 한개의 문서에 공존해서는 안된다</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;&nbsp;<i>error object:</i></p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 하나의 연산을 실행 할때 발생한 에러에 대한 추가적인 정보를 담고 있다. Error object는 반드시 errors를 키로 하는 배열을 통해&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; top-level에서 반환되어야 한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 하나의 에러 객체는 다음과 같은 멤버들을 가질 수 있다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>&nbsp;id: a unique identifier for this particular occurrence of the problem.</li>
<li>links: a<span>&nbsp;</span><a href="https://jsonapi.org/format/#document-links">links object</a><span>&nbsp;</span>containing the following members:
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>about: a<span>&nbsp;</span><a href="https://jsonapi.org/format/#document-links">link</a><span>&nbsp;</span>that leads to further details about this particular occurrence of the problem.</li>
</ul>
</li>
<li>status: the HTTP status code applicable to this problem, expressed as a string value.</li>
<li>code: an application-specific error code, expressed as a string value.</li>
<li>title: a short, human-readable summary of the problem that<span>&nbsp;</span><b>SHOULD NOT</b><span>&nbsp;</span>change from occurrence to occurrence of the problem, except for purposes of localization.</li>
<li>detail: a human-readable explanation specific to this occurrence of the problem. Like<span>&nbsp;</span>title, this field’s value can be localized.</li>
<li>source: an object containing references to the source of the error, optionally including any of the following members:
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>pointer: a JSON Pointer [<a href="https://tools.ietf.org/html/rfc6901">RFC6901</a>] to the associated entity in the request document [e.g.<span>&nbsp;</span>"/data"<span>&nbsp;</span>for a primary data object, or<span>&nbsp;</span>"/data/attributes/title"<span>&nbsp;</span>for a specific attribute].</li>
<li>parameter: a string indicating which URI query parameter caused the error.</li>
</ul>
</li>
<li>meta: a<span>&nbsp;</span><a href="https://jsonapi.org/format/#document-meta">meta object</a><span>&nbsp;</span>containing non-standard meta-information about the error.</li>
</ul>
<p data-ke-size="size16">&nbsp; 2. 하나의 문서는 다음 top-level 멤버들을 가질 수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 1. jsonapi: 서버 구현을 서술하는 객체</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 2. links: primary data와 관련된 링크</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 3. included: primary data와 연관된 resource object들의 배열</p>
<p data-ke-size="size16">&nbsp; &nbsp; 만약 문서가 data를 가지고 있지 않다면 include를 사용해서는 안된다.</p>
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