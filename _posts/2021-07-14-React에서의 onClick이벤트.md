---
layout:       post
title:        "React에서의 onClick이벤트"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- react
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
                            <p data-ke-size="size16">&nbsp; 리엑트는 HTML/JS처럼 유저가 애플리케이션의 인터페이스와 상호작용을 할때 함수를 호출하고 그에대한 액션을 발동한다. 이러한 상호작용은 이벤트를 발생시킨다 .&nbsp;</p>
<p data-ke-size="size16">&nbsp; 클릭 이벤트는 하나의 엘리먼트가 클릭 되었을 때 발동되며 onClick으로 정의된다. 이는 유저의 액션에 대해 작용하고 싶은 엘리먼트의 attribute로 정의 된다.&nbsp;</p>
<p data-ke-size="size16"><b>Vanila와 React의 이벤트 헨들링 차이.</b></p>
<p data-ke-size="size16">&nbsp; 1. 바닐리와는 다르게 리엑트는 camelCase를 사용한다(js-onclick, react-onClick)</p>
<p data-ke-size="size16">&nbsp; 2. HTML의 요소가 클릭되어 이벤트 헨들러가 함수를 호출한다면 다음과 같이 호출된다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//vanila&nbsp;js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>button&nbsp;<span style="color: #066de2;">onclick</span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"doSomething()"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Do&nbsp;something<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//react</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>button&nbsp;onClick<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{doSomething}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Do&nbsp;something<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위의 두 코드는 단순 문법 차이로 보일 수 있지만 사실 아주 큰 차이가 존재한다. JSX에서 직접적으로 함수를 호출하는 것은 함수의 반환값이 onClick attribute에서 사용된다는 의미 이다. 따라서 버튼을 클릭했을때 호출되는 함수를 넘기는게 아니다. 이는 오직 리렌더링 될때 한번만 호출된다. 따라서 해당 버튼에 대한 반복적인 클릭은 함수의 결과를 호출한다. 그때문에 상호작용이나 액션이 일어나지 않는다.</p>
<p data-ke-size="size16">&nbsp; 3. 리엑트의 onClick은 오직 하나의 함수만 받을 수 있는 반면에 vanila는 여러개의 함수를 반을 수 있다.</p>
<p data-ke-size="size16">&nbsp; 4. 리엑트의 이벤트들은 모두 bubbling이 일어 난다. 그에 반해 vanila의 onchange같은 경우는 bubbling이 발생하지 않는다</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp;그때문에 엘리먼트나 컴포넌트가 컨테이너 안에 존재하고 컨테이너에 이벤트 헨들러를 달면 안에 존재하는 엘리먼트를 클릭했을 때&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;이벤트 버블링이 발생한다. 따라서 preventDefault()를 사용해야 한다.</p>
<p data-ke-size="size16"><b>Functional component에서의 event handler</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>함수형 프로그래밍에서 이벤트핸들러는 하나의 attribute로 엘리먼트 또는 컴포넌트에 전달 된다. 이 attritubte는 유저가 이 엘리먼트와 상호작용을 할때 어떤 일이 발생할지를 서술한 함수를 받는다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 다른 이벤트와 마찬가지로 유저가 여러면 엘리먼트를 클릭한다면 이 이벤트는 여러번 발동되고 함수도 여러번 호출된다.</p>
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
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"react"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">"./styles.css"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;<span style="color: #a71d5d;">function</span>&nbsp;App()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">function</span>&nbsp;greetUser()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #63a35c;">"Hi&nbsp;there,&nbsp;user!"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;onClick<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{greetUser()}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>p<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Click&nbsp;<span style="color: #066de2;">this</span>&nbsp;text&nbsp;to&nbsp;see&nbsp;the&nbsp;<span style="color: #066de2;">event</span>&nbsp;bubbling<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>p<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>button&nbsp;onClick<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{greetUser}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Click&nbsp;me<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위 코드를 실행하면 버튼을 클릭하지 않았음에도 "Hi there, user"라는 메시지가 콘솔에 찍힌다. 이 로그는 onClick={greetUser()}에서 찍힌 부분이다. 여기서 버튼을 한번 클릭한다면 버튼태그에 있는 greetUser가 호출된다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 10번째 줄에서 greetUser()를 greetUser로 바꾼 후 버튼을 클릭하면 이벤트 버블링이 발생한다.&nbsp;</p>
<p data-ke-size="size16"><b>onClick 이벤트 핸들러에 인자 사용하기</b></p>
<p data-ke-size="size16"><b>&nbsp;</b>화살표 함수를 사용하면 된다</p>
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
<div style="line-height: 130%;">14</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"react"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">"./styles.css"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;<span style="color: #a71d5d;">function</span>&nbsp;App()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">function</span>&nbsp;greetUser(<span style="color: #066de2;">name</span>)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(`Hi&nbsp;there,&nbsp;${<span style="color: #066de2;">name</span>}`);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>button&nbsp;onClick<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;greetUser(<span style="color: #63a35c;">"John"</span>)}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Click&nbsp;me<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;);</div>
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