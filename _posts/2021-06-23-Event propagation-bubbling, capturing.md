---
layout:       post
title:        "Event propagation-bubbling, capturing"
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
                            <pre id="code_1624455892179" class="html xml" data-ke-language="html" data-ke-type="codeblock"><code>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;style&gt;
        html{border: 5px solid red; padding: 30px}
        body{border: 5px solid green; padding: 30px}
        fieldset{border: 5px solid blue; padding: 30px}
        input{border: 5px solid black; padding: 30px}
    &lt;/style&gt;
    &lt;title&gt;Title&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;fieldset&gt;
        &lt;legend&gt;event propagation&lt;/legend&gt;
        &lt;input type="button" id="target" value="target"&gt;
    &lt;/fieldset&gt;
    &lt;script&gt;
    	 function handler(event) {
            const phases = ['capturing', 'target', 'bubbling'];
            console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase - 1]);
        }
        document.getElementById('target').addEventListener('click', handler, true);
        document.querySelector('fieldset').addEventListener('click', handler, true);
        document.querySelector('body').addEventListener('click', handler, true);
        document.querySelector('html').addEventListener('click', handler, true);
    &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<p data-ke-size="size16">&nbsp; 위와 같은 코드가 있다고 하자. 태그는 부모, 자식 관계를 가진다. 이때 html, body, fieldset, input태그에 각각 이벤트를 장착했다고 하자. 그 후 버튼을 클릭했을때 html은 body를 감싸고 있고, body는 filedset을, filedset은 input을 감싸고 있기 때문에 어떤 순서고 이벤트가 발생할 것인가를 event propagation이라 한다.</p>
<p data-ke-size="size16">&nbsp; event propagation은 두 종류가 있다. (1). bubbling-자식 이벤트 부터 부모 이벤트, (2). capturing-부모 이벤트 부터 자식 이벤트.</p>
<p data-ke-size="size16">&nbsp; 위 코드를 실행시키면 다음과 같은 결과가 나온다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="932" data-origin-height="158" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgcHJvcGFnYXRpb24tYnViYmxpbmcsIGNhcHR1cmluZw==/img.png" data-origin-width="932" data-origin-height="158" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption>capturing</figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; bubbling을 실행하기 위해서는 이벤트 리스너의 3번째 인자를 false 또는 없애면 된다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="938" data-origin-height="154" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgcHJvcGFnYXRpb24tYnViYmxpbmcsIGNhcHR1cmluZw==/img_1.png" data-origin-width="938" data-origin-height="154" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption>bubbling</figcaption>
</figure><p></p>
<p data-ke-size="size16">*위 코드에서 event.eventPhase는&nbsp;</p>
<p data-ke-size="size16">&nbsp; 1. capturing일때는 1</p>
<p data-ke-size="size16">&nbsp; 2. 가장 아래의 이벤트 일때는 2</p>
<p data-ke-size="size16">&nbsp; 3. bubbling일때는 3</p>
<p data-ke-size="size16">을 반환한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>stopPropagation()</b></p>
<p data-ke-size="size16">위 코드에 다음과 같은 함수 하나를 추가하자</p>
<pre id="code_1624457836205" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code> function stopHandler(event){
 	const phases = ['capturing', 'target', 'bubbling'];
 	console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase - 1]);
 	event.stopPropagation();
}</code></pre>
<p data-ke-size="size16">그 후 body tag의 콜백을 stopHandler로 바꾸자. 그러면 다음과 같은 결과가 나온다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="944" data-origin-height="126" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgcHJvcGFnYXRpb24tYnViYmxpbmcsIGNhcHR1cmluZw==/img_2.png" data-origin-width="944" data-origin-height="126" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">따라서 이벤트 전파를 멈추기 위해서는 stopPropagation()을 사용하면 되는것을 알 수 있다.</p>
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