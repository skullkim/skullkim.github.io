---
layout:       post
title:        "Client-side Javascript"
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
                            <p data-ke-size="size16"><b>JS의 역할</b></p>
<p data-ke-size="size16">&nbsp; JS의 역할 중 하나는 좋은 UX를 제공하는 것이다. 하지만 다음과 같은 이유로 JS만으로 모든 기능을 실현할 수 없다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 많은 브라우저에서 JS를 실행하지 않게 설정할 수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 사용자가 직접 JS를 추가실행하는 기능을 제공하는 브라우저가 있다.</p>
<p data-ke-size="size16">&nbsp; 즉, 웹 사이트를 제공하는 쪽이 의도한 대로 JS를 실행할 수 없는 경우가 발생한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>HTML과 JS</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>웹브라우저가 웹 페이지를 표시할때는 다음과 같은 과정을 거친다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. HTML을 파싱</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 외부 JS파일, CSS파일 로드</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. JS가 전달돈 시점에 실행</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. DOM트리 구축완료</p>
<p data-ke-size="size16">&nbsp; &nbsp; 5. 이미지 파일 등 외부 리소스 로드</p>
<p data-ke-size="size16">&nbsp; &nbsp; 6. 완료</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>JS 작성 방법과 실행 타이밍</b></p>
<p data-ke-size="size16">&nbsp; HTML문서안에 JS를 작성할 수 있는 방식은 여러가지이며 방식마다 실행 시점이 다르다.</p>
<p data-ke-size="size16">&nbsp; 1. &lt;script&gt;</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &lt;script&gt;태그를 사용한 경우 이 태그가 해석된 직후에 실행된다. 여기서 주의해야할 점은 &lt;script&gt;태그 이후의 DOM요소는 아직 구축되지 않았기 때문에 &lt;script&gt;내부에 있는 JS는 &lt;/script&gt;이후의 DOM요소를 조작할 수 없다는 것이다. 이를 피하기 위해서는 &lt;/body&gt;바로 위에 &lt;script&gt;를 사용하면 된다. 하지만 이 경우에도 &lt;body&gt;태그는 완전히 닫히지 않았기 때문에 &lt;body&gt;태그에 대한 조작은 피해야 한다.</p>
<p data-ke-size="size16">&nbsp; 2. 외부 JS파일 읽기</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &lt;script&gt;태그의 src attribute를 사용해 외부 JS파일을 읽어올 수 있다. 파일을 읽는 타이밍은 &lt;script&gt;태그가 해석된 직후로 파일 안의 JS가 실행되는 것은 파일을 다 읽은 직후이다. 이 방식 같은 경우는 defer attribute와 async attribute를 사용할 수 있는 defer를 사용하면 나머지 해당 &lt;script&gt;태그에 대한 평가를 다른 &lt;script&gt;태그의 평가각 끝날때 까지 미룰 수 있다. async의 경우 비동기로 외부 파일을 읽고, 읽기가 끝난 후 순자적으로 실행한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 이런 외부파일을 사용했을 때의 이점은 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 1. JS파일을 브라우저에서 캐시할 수 있다. JS파일의 내용 변경이 많지 않다면 한번 내려받은 JS파일을 캐시해 두고 두 번째 접근&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 이&nbsp; 후로는 불필요한 다운로드를 피할 수 있어 성능이 향상된다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 2.&nbsp; 파일이 나뉘어 지기 때문에 팀 단위 작업이 쉬워진다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. onload event</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp;&lt;body onload=""&gt;를 사용하는 것으로 페이지의 읽기 처리과 완료된 후에 실행할 수 있다. 페이지가 전부 로딩된 후에 처리되므로 모든 DOM요소를 조작할 수 있다. 하지만 이러한 이유로 인해 페이지 내의 모든 이미지 파일을 읽은 후 실행된다는 것을 인지해야 한다. 만약 용량이 큰 이미지가 존재하고 JS에서 이미지를 조작하지 않는다면 JS를 실행하기 위해 필요 이상의 대기 시간이 필요하다. 또 한 이미지를 읽으는 것을 기다리면서 동시에 JS코드를 실행하는 것이 체감상 더 빠르다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. DOMContentLoaded</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; onload event의 단점을 해결한 것이 DOMContentLoaded이다. 이는 HTML의 해석이 끝난 직후 발생하는 이벤트이다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">document</span>.<span style="color: #066de2;">addEventListener</span>(<span style="color: #63a35c;">"DOMContentLoaded"</span>,<span style="color: #a71d5d;">function</span>&nbsp;()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">alert</span>(<span style="color: #63a35c;">"hello"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">},<span style="color: #0099cc;">false</span>);</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 5. 동적 로드</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; JS에서 script요소를 생성해 동적으로 JS파일을 로드할 수 있다. 이 방식으로 사용하면 파일의 다운로드 부터 실행이 개시될 때까지는 그 밖의 처리를 블록하지 않는다. 페이지 안에 script 요소가 직접 작성돼 이쓴 경우 해당 JS파일을 내려받는 사이 그 밖의 이미지 파일이나 CSS파일의 다운로드를 블록한다.&nbsp;</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;script&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">document</span>.createElement(<span style="color: #63a35c;">'script'</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">script.src&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'myJsFile.js'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">document</span>.getElementsByName(<span style="color: #63a35c;">'head'</span>)[<span style="color: #0099cc;">0</span>].appendChild(script);</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>onerror</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>JS에서 에러가 발생하면 Window 객체의 onerror 프로퍼티에 저장돼 있는 함수가 실행된다. 이 함수에는 세개의 인자가 전달된다. 에러 메시지, 에러가 발생한 JS가 포함된 문서의 URL, 에러가 발생한 행 번호.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>크로스 브라우징 지원</b></p>
<p data-ke-size="size16">&nbsp; 웹브라우저는 HTML 렌더링 엔진과 JS 엔진으로 구성되 있다. HTML 렌더링 엔진은 HTML이나 CSS를 해석해 그 결과를 적절한 형태로 표현한 것이다. 그리고 JS엔진은 JS를 해석해 그 결과를 적절한 형태로 표현한 것이다. 여기서 문제는 브라우저 마다 사용하고 있는 HTML 렌더링 엔진과 JS엔진이 다르다는 것이다. 이때문에 같은 웹사이트에 접속해도 UI가 조금씩 다르거나 다른 동작을 하는 문제가 발생한다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 33.3333%;">웹브라우저</td>
<td style="width: 33.3333%;">렌더링 엔진</td>
<td style="width: 33.3333%;">JS엔진</td>
</tr>
<tr>
<td style="width: 33.3333%;">IE</td>
<td style="width: 33.3333%;">Trident</td>
<td style="width: 33.3333%;">Jscript</td>
</tr>
<tr>
<td style="width: 33.3333%;">fireFox</td>
<td style="width: 33.3333%;">Gecko</td>
<td style="width: 33.3333%;">SpiderMonkey</td>
</tr>
<tr>
<td style="width: 33.3333%;">chrome</td>
<td style="width: 33.3333%;">Webkit, blink(V28 이후)</td>
<td style="width: 33.3333%;">V8</td>
</tr>
<tr>
<td style="width: 33.3333%;">safari</td>
<td style="width: 33.3333%;">Webkit</td>
<td style="width: 33.3333%;">JavaScriptCore</td>
</tr>
<tr>
<td style="width: 33.3333%;">opera</td>
<td style="width: 33.3333%;">Presto</td>
<td style="width: 33.3333%;">charakan</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>지원해야할 브라우저</b></i></p>
<p data-ke-size="size16"><i></i>&nbsp; &nbsp; 세상에는 다양한 웹브라우저가 존재하고 모든 브라우저를 지원하는 것은 비용 대비 효과를 생각하면 의미가 없다. 지원해야할 웹 브라우저 중 가장 문제가 되는 것이 IE이다. IE는 ECMA-262에는 기술되 있지 않은 독자 구형 요사가 많다. 따라서 단순히 동일 기능만 하게 구현한다면 크게 문제가 되지 않는다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 하지만 여기서 JS로 복잡한 동작을 구현할 때를 주의해야 한다. IE6는 최신 브라우저와 비교해 JS의 처리 속도가 압도적으로 느리다. 따라서 JS로 복잡한 동작을 구현해야 한다면 아예 IE6를 지원하지 않는다고 명시하는 것이 좋다. IE9부터는 웹 표준으로 처리한 구현을 궍장하기 때문에 최신 브라우저만들 대상으로 삼을 경우 크로스 브라우징 이슈는 거의 없다고 보아도 된다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;&nbsp;<i><b>구현방법</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;</b></i>크로스 브라우징 지원은 다음과 같은 두 가지 방식을 사용해 지원할 수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;1. user agent로 판단</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; user agent는 클라이언트 애플리케이션을 식별하기 위한 문자열이다. user agent는 Navigator객체의 userAgent프로퍼티로 구할 수 있다. 이 값은 브라우저의 종류, 버전, 운영체제의 종류, 버전으로 결정된다. 그러므로 이 값을 기준으로 처리를 나누면 된다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;2. 기능 유무로 판단</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;user agent로 판단을 할려면 user agent가 어떤 기능을 가지고 있는지 알아야 한다. 또 한 개발 중인 브라우저에서 user agent를 통한 크로스 브라우징 이슈 해결을 할 경우 기능이 업데이트 될 때 마다 코드를 업데이트 해야 한다. 또 한 일부 브라우저의 경우 agent를 자유롭게 설정할 수 있고 agent를 자유롭게 설정하는 것과 기능 지원은 별개이기 때문에 user agent로 판단하는 것은 크로스 브라우징 이슈를 제대로 해결할 수 없다. 따라서 기능 유무로 판단하는 것이 훨씬 좋은 선택이다. 하지만 특정 브라우저 버전에 대한 처리만을 바꾸고 싶다면 user agent를 사용해야 한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Window 객체</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>Client-side JS에서는 Window객체가 전역객체이다. Window 객체는 브라우저에 의해 표시되고 있는 윈도우 자체에 대응하는 객체이다. Window 프로퍼티가 참조하는 객체가 JS안에서의 전역 객체가 된다. Window 객체는 JS로 다룰 수 있는 최상위 객체이며 다음과 같은 프로퍼티를 가진다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. navigator</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. location</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. history</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. screen</p>
<p data-ke-size="size16">&nbsp; &nbsp; 5. frames</p>
<p data-ke-size="size16">&nbsp; &nbsp; 6. document</p>
<p data-ke-size="size16">&nbsp; &nbsp; 7. parent, top, self</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Navigator 객체</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>navigator프로퍼티는 Navigator객체이다. Navigator 객체는 브라우저 버전, 이용 가능한 플러그인, 사용 언어 등 브라우저에 대한 각종 정보를 담고있다. Navigator객체의 userAgent프로퍼티를 사용하여 크로스브라우징 이슈를 해결할 수 있다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Location 객체</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; Window 객체의 location property는 Location 객체이다. 현재 표시된 URL에 대한 정보를 담고 있다. Location 객체는 다음과 같은 프로퍼티들을 가지고 있다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 28.0232%;">프로퍼티명</td>
<td style="width: 46.9768%;">설명</td>
<td style="width: 25%;">예</td>
</tr>
<tr>
<td style="width: 28.0232%;">protocol</td>
<td style="width: 46.9768%;">protocol</td>
<td style="width: 25%;">http:</td>
</tr>
<tr>
<td style="width: 28.0232%;">host, hostname</td>
<td style="width: 46.9768%;">host name</td>
<td style="width: 25%;">example.com</td>
</tr>
<tr>
<td style="width: 28.0232%;">port</td>
<td style="width: 46.9768%;">port&nbsp;</td>
<td style="width: 25%;">80</td>
</tr>
<tr>
<td style="width: 28.0232%;">pathname</td>
<td style="width: 46.9768%;">path</td>
<td style="width: 25%;">/path</td>
</tr>
<tr>
<td style="width: 28.0232%;">search</td>
<td style="width: 46.9768%;">query</td>
<td style="width: 25%;">?q=foo</td>
</tr>
<tr>
<td style="width: 28.0232%;">hash</td>
<td style="width: 46.9768%;">fragement</td>
<td style="width: 25%;">#bar</td>
</tr>
<tr>
<td style="width: 28.0232%;">href</td>
<td style="width: 46.9768%;">현재 표시하고 있는 페이의 완전한 URL을 나타낸다. URL을 대입하게 되면 해당 URL로 이동한다.</td>
<td style="width: 25%;">location.href='http://example.com'</td>
</tr>
<tr>
<td style="width: 28.0232%;">assign()</td>
<td style="width: 46.9768%;">href()와 같은 동작을 한다</td>
<td style="width: 25%;">location.assign('http://example.com')</td>
</tr>
<tr>
<td style="width: 28.0232%;">replace()</td>
<td style="width: 46.9768%;">인자로 넘긴 URL로 이동한다. replace()는 hreft와 같이 다른 URL로 이동하지만 브라우저 이력(검색기록)에 남지 않는다. 따라서 뒤로가기가 동작하지 않는다.</td>
<td style="width: 25%;">location.replace('http://example.com')</td>
</tr>
<tr>
<td style="width: 28.0232%;">reload()</td>
<td style="width: 46.9768%;">현재 페이지를 리로드한다. 인자로 true을 주면 브라우저 캐시를 무시하고 강제 리로드를 하고 false또는 아무것도 전달하지 않으면 브라우저 캐시를 이용해 리로드한다.</td>
<td style="width: 25%;">location.reload(true);</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>History 객체</b></i></p>
<p data-ke-size="size16"><i></i>&nbsp; &nbsp; Window 객체의 history 프로퍼티는 History 객체이다. History객체의 back(), forward()를 사용해 브라우저 이력을 뒤로 또는 앞으로 전환할 수 있다. go()를 활용하면 인자로 넘기는 정수 만큼 페이지를 이동할 수 있다. 양수를 넘기면 앞으로, 음수를 넘기면 뒤로 간다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Screen 객체</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; 화면의 크기 등의 정보를 저장하고 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>frames 프로퍼티</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>윈도우 안에 여러 개의 프레임이 존재 할 떄 frames프로퍼티에 해당 프레임에 대한 참조가 저장된다. 없다면 빈 배열이 저장된다. 프레임은 &lt;frameset&gt;, &lt;frame&gt;, &lt;iframe&gt;을 사용해 만들 수 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp; 프레임 자신도 Window 객체가 되므로 window.frames[1].fram[2]처럼 프레인 안의 서브 프레임에 대한 참조를 얻을 수 있다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>self프로퍼티&nbsp;</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; 자기 자신의 Window객체를 참조한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;<i><b>parent프로퍼티</b></i></p>
<p data-ke-size="size16"><i></i>&nbsp; &nbsp; &nbsp;서브 프레임에서 부모 프레임으로의 참조를 구할 수 있다. 부모 프레임이 존재하지 않는다면 parent 프로퍼티는 자기 자신의 Window 객체를 참조한다.</p>
<p data-ke-size="size16">&nbsp; <i><b>top프로퍼티</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 프레임이 중첨되 있을 때 최상위 프레임을 참조한다. 자신이 최상위 프레임이면 top프로퍼티는 자신의 Window 객체를 가리킨다.&nbsp;</p>
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