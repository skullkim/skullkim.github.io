---
layout:       post
title:        "DOM(Document Object Model)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- DOM
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
                            <p data-ke-size="size16">&nbsp; 웹 페이지의 내용을 js로 다룰때는 단순히 내용을 문자열로 다루는 것 보다 어떠한 덩어리로 조작하는 것이 더 쉽다. 이를 위한 것이 DOM이다.</p>
<p data-ke-size="size16">&nbsp; DOM은 HTML, XML문서를 프로그램에서 이용하기 위한 API이며 트리 구조를 사용한다. 이때 이 트리를 DOM트리라 한다. 구조 자체가 트리인 만큼 DOM트리 안에서 각 객체를 노드라 하며 어떤 노드와 다른 노드와의 관계는 트리에서 사용하는 관계와 같다(부모, 자식 등).</p>
<p data-ke-size="size16">&nbsp; DOM 사양은 W3C에 의해 Level1~3으로 정의되 있다.</p>
<p data-ke-size="size16"><b>DOM Level 1 </b><b></b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>DOM Level1은 Core, HTML이 두 가지 모듈로 구성되 있다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">모듈</td>
<td style="width: 50%;">설명</td>
</tr>
<tr>
<td style="width: 50%;">Core</td>
<td style="width: 50%;">HTML에 한정되지 않은 일반적인 DOM 조작에 대한 사양<br>&nbsp; getElementsByTagName - 태그명을 지정해 요소를 구한다<br>&nbsp; createElement - 요소를 작성한다<br>&nbsp; appendChild - 요소를 삽입한다</td>
</tr>
<tr>
<td style="width: 50%;">HTML</td>
<td style="width: 50%;">HTML 문서 특유의 메서드에 대한 사용</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><b>DOM Level 2</b></p>
<p data-ke-size="size16">&nbsp;DOM Level2는 Level1의 모듈을 가지면서 이벤트 처리에 관한 Events 모듈이 들어 있다. CSS 또 한 여기에 정의되 있다. IE8이하는 Level2를 따르지 않고 파이어폭스, 크롬은 Level2를 거의 완벽하게 지원한다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">모듈</td>
<td style="width: 50%;">설명</td>
</tr>
<tr>
<td style="width: 50%;">Core</td>
<td style="width: 50%;">Level1 Core의 확장</td>
</tr>
<tr>
<td style="width: 50%;">HTML</td>
<td style="width: 50%;">Level1 HTML의 확장</td>
</tr>
<tr>
<td style="width: 50%;">Views</td>
<td style="width: 50%;">문서의 표시 상태에 대한 사양</td>
</tr>
<tr>
<td style="width: 50%;">Events</td>
<td style="width: 50%;">캡처링, 버블링, 이벤트 취고 등의 이벤트 시스템의 사양</td>
</tr>
<tr>
<td style="width: 50%;">Style</td>
<td style="width: 50%;">stylesheet에 대한 사양</td>
</tr>
<tr>
<td style="width: 50%;">Traversal and Range</td>
<td style="width: 50%;">DOM트리를 따라가는 방법이나 범위 지정에 대한 사양</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><b>DOM Level3</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>DOM Level3은 아직 권고 단계에 있지 않다. 하지만 최신 브라우저 에서는 Events 모듈에 정의된 내용이 구현되 있다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">모듈</td>
<td style="width: 50%;">설명</td>
</tr>
<tr>
<td style="width: 50%;">Core</td>
<td style="width: 50%;">Level2 Core의 확장</td>
</tr>
<tr>
<td style="width: 50%;">Load and Save</td>
<td style="width: 50%;">문서 구조 읽고 쓰기에 대한 사양</td>
</tr>
<tr>
<td style="width: 50%;">Validation</td>
<td style="width: 50%;">문서 구조가 타당한지를 검증하기 위한 사양</td>
</tr>
<tr>
<td style="width: 50%;">XPath</td>
<td style="width: 50%;">XPath에 대한 사양</td>
</tr>
<tr>
<td style="width: 50%;">Events</td>
<td style="width: 50%;">Level2 Events의 확장, 키보드 이벤트 지원</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>요소, 노드</b></p>
<p data-ke-size="size16">&nbsp; 요소와 노드는 상속 관계에 있고, 노드가 상위 타입이다. 노드에는 nodeType이라는 속성이 존재하는데 이 값이 ELEMENT_NODE(1)인것이 요소이다. 다음은 HTML문서에서 주로 사용되는 노드이다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 25%;">노드</td>
<td style="width: 25%;">노드 타입 상수</td>
<td style="width: 25%;">노드 타입의 값</td>
<td style="width: 25%;">인터페이스</td>
</tr>
<tr>
<td style="width: 25%;">요소 노드</td>
<td style="width: 25%;">ELEMENT_NODE</td>
<td style="width: 25%;">1</td>
<td style="width: 25%;">Element</td>
</tr>
<tr>
<td style="width: 25%;">속성 노드</td>
<td style="width: 25%;">ATTRIBUTE_NODE</td>
<td style="width: 25%;">2</td>
<td style="width: 25%;">Attr</td>
</tr>
<tr>
<td style="width: 25%;">텍스트 노드</td>
<td style="width: 25%;">TEXT_NODE</td>
<td style="width: 25%;">3</td>
<td style="width: 25%;">Text</td>
</tr>
<tr>
<td style="width: 25%;">코멘트 노드</td>
<td style="width: 25%;">COMMENT_NODE</td>
<td style="width: 25%;">8</td>
<td style="width: 25%;">Comment</td>
</tr>
<tr>
<td style="width: 25%;">문서 노드</td>
<td style="width: 25%;">DOCUMENT_NODE</td>
<td style="width: 25%;">9</td>
<td style="width: 25%;">Document</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Document 객체</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>Document 객체는 DOM 트리에서 루트 노드 이다. Document객체는 documentElement property or body property에 대응하지만 특정 태그에 대응되지는 않는다. Document객체를 해당 HTML문서 전체를 표현한다.</p>
<p data-ke-size="size16">&nbsp; Document객체는 js안에서 document 전역 변수로 접근할 수 있으며 document는 window 객체의 프로퍼티로 존재 한다. 하지만 window 객체는 전역 객체 이므로 해당 프로퍼티에 접근할 때에는 window를 생략해도 된다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>getElementsByTagName()</b></p>
<p data-ke-size="size16">&nbsp; getElementsByTagName은 Document.getElemetById()와는 다르게 Document객체와 Element객체 양쪽의 메서드이다. getElementById()는 Document 객체에만 존재한다. 따라서 특정 Element 객체에 대해 getElementsByTagName()을 실행하면 해당 Element 객체의 자손 노드 가운데 특정 태그 명을 지닌 요소를 구한다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>라이브 객체(또는 Live Collection)</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; getElementsByTagName()을 사용 시 주의할 점이 있다. 이를 사용하면 NodeList객체가 구해 진다는 점이다. NodeList는 유사 배열, 즉 배열의 형태를 띄고 있지만 배열이 아닌 객체이다. 여기서 NodeList는 라이브 객체이며 라이브 객체는 DOM 트리에 대한 참조를 가지고 있기 때문에 DOM의 변경 사항을 실시간으로 반영 한다. Element.childNodes또한 라이브 객체를 반환 한다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;id<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"foo"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>span<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>first<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>span<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>span<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>second<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>span<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>script<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;elems&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">document</span>.getElementsByTagName(<span style="color: #63a35c;">'span'</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(elems.<span style="color: #066de2;">length</span>);<span style="color: #999999;">//2</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;newSpan&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">document</span>.createElement(<span style="color: #63a35c;">'span'</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;newSpan.appendChild(<span style="color: #066de2;">document</span>.createTextNode(<span style="color: #63a35c;">'third'</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;foo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">document</span>.<span style="color: #066de2;">getElementById</span>(<span style="color: #63a35c;">'foo'</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;foo.appendChild(newSpan);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(elems.<span style="color: #066de2;">length</span>);<span style="color: #999999;">//3</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>script<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 라이브객체는 다음과 같이 반복문을 실행할 때 문제가 생긴다. 아래와 같이 코드를 작성하면 라이브 객체의 특성 때문에 무한루프를 돌게 된다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;divs&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">document</span>.getElementsByTagName(<span style="color: #63a35c;">'div'</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">let</span>&nbsp;newDiv;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">for</span>(<span style="color: #a71d5d;">let</span>&nbsp;i&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;i&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;divs.<span style="color: #066de2;">length</span>;&nbsp;i<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;newDiv&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">document</span>.createElement(<span style="color: #63a35c;">'div'</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;newDiv.appendChild(<span style="color: #066de2;">document</span>.createTextNode(<span style="color: #63a35c;">'new&nbsp;div'</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;divs[i].appendChild(newDiv);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;&nbsp;<i>라이브 객체의 성능</i></p>
<p data-ke-size="size16"><i>&nbsp; &nbsp; &nbsp; &nbsp;</i>라이브 객체를 성능상으로 좋지 않다. 따라서 라이브 객체를 한번 slice()를 사용해 Array로 변환 후 사용하는 편이 성능상 뛰어 나다. 라이브 객체는 성능 면에서 문제가 있으므로 라이브러리에서는 Array로 변환하고 나서 반환하는 것도 있다</p>
<p data-ke-size="size16">&nbsp; &nbsp; NodeList외에도 HTMLCollection은 라이브 객체이다. DOM Level 1에 정의되 있는 HTMLCollection은 다음과 같다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">HTMLCollection</td>
<td style="width: 50%;">설명</td>
</tr>
<tr>
<td style="width: 50%;">document.images</td>
<td style="width: 50%;">문서 안의 img 요소 목록</td>
</tr>
<tr>
<td style="width: 50%;">document.apples</td>
<td style="width: 50%;">문서 안의 자바 애플릿 객체 목록</td>
</tr>
<tr>
<td style="width: 50%;">document.links</td>
<td style="width: 50%;">문서 안의 링크 요소(&lt;a href&gt;)목록</td>
</tr>
<tr>
<td style="width: 50%;">document.forms</td>
<td style="width: 50%;">문서 안의 form요소 목록</td>
</tr>
<tr>
<td style="width: 50%;">document.anchors</td>
<td style="width: 50%;">문서 안의 앵커 요소 (a 태그 안에 name 속성이 설정되 있는거) 목록</td>
</tr>
<tr>
<td style="width: 50%;">form.elements</td>
<td style="width: 50%;">폼 안에 input 요소 목록</td>
</tr>
<tr>
<td style="width: 50%;">map.areas</td>
<td style="width: 50%;">이미지 맵 안의 area목록</td>
</tr>
<tr>
<td style="width: 50%;">table.rows</td>
<td style="width: 50%;">테이블 안의 tr목록</td>
</tr>
<tr>
<td style="width: 50%;">table.tBodies</td>
<td style="width: 50%;">테이블 안의 tbody목록</td>
</tr>
<tr>
<td style="width: 50%;">tableSection.rows</td>
<td style="width: 50%;">테이블 세션(thead 요소, tfoot 요소)안의 tr 요소 목록</td>
</tr>
<tr>
<td style="width: 50%;">row.cells</td>
<td style="width: 50%;">테이블의 행 안의 td요소와 th요소 목록</td>
</tr>
</tbody>
</table>
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