---
layout:       post
title:        "temporal dead zone"
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
                            <p data-ke-size="size16"><b>TDZ(Temporal Dead Zone)</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>다음과 같은 코드가 있다고 해보자</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;a&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">a;<span style="color: #999999;">//1</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">a<span style="color: #999999;">//throws&nbsp;'Reference&nbsp;error'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;a&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">a;<span style="color: #999999;">//1</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">첫번째 예시에서는 제대로 된 결과가 나오고 두번째 예시에서는 reference error가 뜬다. 두번째 예시에서 1줄이 TDZ이다.</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="614" data-origin-height="726" width="302" height="357" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/dGVtcG9yYWwgZGVhZCB6b25l/img.png" data-origin-width="614" data-origin-height="726" width="302" height="357" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">TDZ는 변수를 선언하기 이전에 변수를 엑세스 하는 것을 금한다.</p>
<p data-ke-size="size16">다음과 같은 statement는 TDZ의 영향을 받는다.</p>
<p data-ke-size="size16">&nbsp; 1. const, let</p>
<p data-ke-size="size16">&nbsp; 2. class statement, construcotr() 내부에 있는 super()</p>
<p data-ke-size="size16">&nbsp; 3. Default function parameters</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">다음은 hoisting으로 인해 영향을 받지 않는 것들이다</p>
<p data-ke-size="size16">&nbsp; 1. var</p>
<p data-ke-size="size16">&nbsp; 2. function&nbsp;</p>
<p data-ke-size="size16">&nbsp; 3. import modules</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>typeof와 TDZ</b></p>
<p data-ke-size="size16">&nbsp; 만약 정의되지 않은 변수를 typeof하면 undefined가 출력된다. 하지만 TDZ에서 typeof를 하게 되면 ReferenceError가 뜬다. 이 이유는 변수가 아래에 정의되 있기 때문이다</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">typeof</span>&nbsp;val;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">let</span>&nbsp;val;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>TDZ와 scope</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>TDZ는 선언문이 존재하는 스코프 범위 에서만 변수에 영향을 준다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;func(){</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;cont&nbsp;b&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">typeof</span>&nbsp;a;<span style="color: #999999;">//undefined,&nbsp;function&nbsp;scope</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>(b&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>){<span style="color: #999999;">//inner&nbsp;scope</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">typeof</span>&nbsp;a;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">let</span>&nbsp;a;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
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