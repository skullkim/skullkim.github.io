---
layout:       post
title:        "Component - intro, props"
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
                            <p data-ke-size="size16">&nbsp; 컴포넌트의 기능은 단순한 템플릿 이상이다. 데이터가 주어 지면 이에 맞추어 UI를 만들로 라이프 사이클 API를 이용해 컴포넌트가 화면에 나타날때, 사라질때, 변화가 일어날때 주어진 작업들을 처리할 수 있으며, 임의 메서드를 만들어 특별한 기능을 붙여줄 수 있다.</p>
<p data-ke-size="size16">&nbsp; 컴포넌트는 함수형 컴포넌트, 클래스형 컴포넌트 두가지로 나뉘어져 있다. 이 둘의 차이점은 클래스형컴포넌트는 state 기능, 라이프 사이클 기능을 사용할 수 있다는 것과 임의 메서드를 정의할 수 있다는 것이다.</p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//함수형&nbsp;컴포넌트</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;App()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;<span style="color: #066de2;">name</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">"react"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"react"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>{<span style="color: #066de2;">name</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//클래스형&nbsp;컴포넌트</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{Component}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"react/cjs/react.production.min"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;Component&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;render()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;<span style="color: #066de2;">name</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"react"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>{<span style="color: #066de2;">name</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">함수형 컴포넌트의</p>
<p data-ke-size="size16">&nbsp; 장점</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 클래스형 컴포넌트 보다 선언하기 쉽다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 메모리 자원을 클래스형 컴포넌트에 비해 덜 먹는다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 배포할때 클래스형 컴포넌트 보다 파일 크기가 작다</p>
<p data-ke-size="size16">&nbsp; 단점</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. state, 라이프 사이클 API사용이 불가하다 -&gt; v16.8이후 Hooks 도입으로 인해 해결됬다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>첫 컴포넌트 생성</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>/src에서</p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//MyComponent.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>first&nbsp;component<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//App.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./App.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;MyComponent&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./MyComponent"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>MyComponent<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;App;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>props</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>props는 properties의 줄임말로서 컴포넌트 속성을 설정할 때 사용하는 요소이다. props값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정할 수 있다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>JSX내부에서 props렌더링</b></i></p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//MyComponent.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Hello&nbsp;{props.<span style="color: #066de2;">name</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//App.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./App.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;MyComponent&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./MyComponent"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>MyComponent&nbsp;<span style="color: #066de2;">name</span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"world"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;App;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//output:&nbsp;Hello&nbsp;world</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;&nbsp;<b>Default props</b></p>
<p data-ke-size="size16"><b>&nbsp; &nbsp;&nbsp;</b>위 코드에서 App.js의 name="world"부분을 지우면 출력은 hello가 된다. props를 따로 지정하지 않아도 기본값을 다음과 같이 지정할 수 있다.</p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//MyComponent.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Hello&nbsp;{props.<span style="color: #066de2;">name</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.defaultProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">'default&nbsp;props'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//App.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./App.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;MyComponent&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./MyComponent"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>MyComponent<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;App;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//output:&nbsp;hello&nbsp;default&nbsp;props</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>&nbsp; children</b></p>
<p data-ke-size="size16"><b>&nbsp; &nbsp;&nbsp;</b>리엑트에서 컴포넌트를 사용할 때 태그 사이의 값을 props.children을 통해 볼 접근할 수 있다.</p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//MyComponent.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hello&nbsp;{props.<span style="color: #066de2;">name</span>}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>br<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;children:&nbsp;{props.children}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.defaultProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">'default&nbsp;props'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//App.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./App.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;MyComponent&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./MyComponent"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>MyComponent<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>react<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>MyComponent<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;App;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//output:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Hello&nbsp;default&nbsp;props</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//children:&nbsp;react</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>비구조화 할당(destructing assignment)를 사용한 props내부 값 추출</b></i></p>
<p data-ke-size="size16">&nbsp;</p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;{<span style="color: #066de2;">name</span>,&nbsp;children}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;props;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hello&nbsp;{<span style="color: #066de2;">name</span>}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>br<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;children:&nbsp;{children}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.defaultProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">'default&nbsp;props'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//or</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({<span style="color: #066de2;">name</span>,&nbsp;children})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{}</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>propTypes를 통한 props 타입 지정</b></i></p>
<p data-ke-size="size16"><i><b></b></i>&nbsp; 컴포넌트의 필수 props를 지정하거나 props의 타입을 지정할 때는 propTypes를 사용하면 된다.</p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
<div style="line-height: 130%;">35</div>
<div style="line-height: 130%;">36</div>
<div style="line-height: 130%;">37</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//MyComponent.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;PropTypes&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'prop-types'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({<span style="color: #066de2;">name</span>,&nbsp;children})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;const&nbsp;{name,&nbsp;children}&nbsp;=&nbsp;props;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hello&nbsp;{<span style="color: #066de2;">name</span>}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>br<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;children:&nbsp;{children}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.defaultProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">'default&nbsp;props'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.propTypes&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;PropTypes.string,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//App.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./App.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;MyComponent&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./MyComponent"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>MyComponent&nbsp;<span style="color: #066de2;">name</span><span style="color: #a71d5d;">=</span>{<span style="color: #0099cc;">1</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>react<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>MyComponent<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;App;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//name이&nbsp;string이&nbsp;아닌&nbsp;number이므로&nbsp;다음과&nbsp;같은&nbsp;경고&nbsp;출력:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Warning:&nbsp;Failed&nbsp;prop&nbsp;type:&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Invalid&nbsp;prop&nbsp;`name`&nbsp;of&nbsp;type&nbsp;`number`&nbsp;supplied&nbsp;to&nbsp;`MyComponent`,&nbsp;expected&nbsp;`string`.</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;&nbsp;<b>isRequired를 통한 필수 props지정</b></p>
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
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
<div style="line-height: 130%;">35</div>
<div style="line-height: 130%;">36</div>
<div style="line-height: 130%;">37</div>
<div style="line-height: 130%;">38</div>
<div style="line-height: 130%;">39</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//MyComponent.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;PropTypes&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'prop-types'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({<span style="color: #066de2;">name</span>,&nbsp;favorite_number,&nbsp;children})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;const&nbsp;{name,&nbsp;children}&nbsp;=&nbsp;props;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hello&nbsp;{<span style="color: #066de2;">name</span>}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>br<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;children:&nbsp;{children}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>br<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;my&nbsp;favorite&nbsp;number:&nbsp;{favorite_number}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.defaultProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">'default&nbsp;props'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyComponent.propTypes&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">name</span>:&nbsp;PropTypes.string,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;favorite_number:&nbsp;PropTypes.number.isRequired,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;MyComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//App.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./App.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;MyComponent&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./MyComponent"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>MyComponent&nbsp;<span style="color: #066de2;">name</span><span style="color: #a71d5d;">=</span>{<span style="color: #63a35c;">"skullkim"</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>react<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>MyComponent<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;App;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//favorite_number를&nbsp;지정하지&nbsp;않았으므로&nbsp;다음과&nbsp;같은&nbsp;에러&nbsp;출력:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Warning:&nbsp;Failed&nbsp;prop&nbsp;type:&nbsp;The&nbsp;prop&nbsp;`favorite_number`&nbsp;is&nbsp;marked&nbsp;as&nbsp;required&nbsp;in&nbsp;`MyComponent`,&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//but&nbsp;its&nbsp;value&nbsp;is&nbsp;`undefined`.</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>&nbsp; prop-types type 종류</b></p>
<p data-ke-size="size16">kinddescription</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td>any</td>
<td>아무 종류</td>
</tr>
<tr>
<td>array</td>
<td>배열</td>
</tr>
<tr>
<td>bool</td>
<td>true/false</td>
</tr>
<tr>
<td>func</td>
<td>함수</td>
</tr>
<tr>
<td>number</td>
<td>숫자</td>
</tr>
<tr>
<td>object</td>
<td>객체</td>
</tr>
<tr>
<td>string</td>
<td>문자열</td>
</tr>
<tr>
<td>symbol</td>
<td>심벌 개체(ES6)</td>
</tr>
<tr>
<td>node</td>
<td>렌더링 가능한 모든것(number, string, element, 또는 그것들이 포함된 array/fragment)</td>
</tr>
<tr>
<td>element</td>
<td>React element</td>
</tr>
<tr>
<td>instanceOf(ClassName)</td>
<td>JS에서 instanceof로 정의 가능한 클래스 인스턴스</td>
</tr>
<tr>
<td>oneOf([…Value])</td>
<td>포함된 값들중 하나.(ex: oneOf([‘남자’,’여자’]))</td>
</tr>
<tr>
<td>oneOfType([…PropTypes])</td>
<td>포함된 PropTypes들중 하나. (ex: oneOfType([PropTypes.string, PropTypes.instanceOf(MyClass)]))</td>
</tr>
<tr>
<td>arrayOf(PropTypes)</td>
<td>해당 PropTypes으로 구성된 배열</td>
</tr>
<tr>
<td>objectOf(PropTypes)</td>
<td>주어진 종류의 값을 가진 객체</td>
</tr>
<tr>
<td>shape({key:PropTypes})</td>
<td>해당 스키마를 가진 객체.(ex:shape({name:PropTypes.string,age:PropTypes.number}))</td>
</tr>
<tr>
<td>exact({key:PropTypes})</td>
<td>명확하게 해당 스키마만 존재해야함.</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;&nbsp;<b>클래스형 컴포넌트에서 props사용</b></p>
<p data-ke-size="size16">&nbsp; &nbsp; 함수형 컴포넌트와 사용법은 같으나 props대신 this.props를 사용한다.또 한 static을 사용해서 defualtProps와 propsTypes를 클래스 내부에서 지정할 수 있다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">More about prop-types: <a href="https://github.com/facebook/prop-types" target="_blank" rel="noopener">https://github.com/facebook/prop-types</a></p>
<figure id="og_1624090696176" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="facebook/prop-types" data-og-description="Runtime type checking for React props and similar objects - facebook/prop-types" data-og-host="github.com" data-og-source-url="https://github.com/facebook/prop-types" data-og-url="https://github.com/facebook/prop-types" data-og-image="https://scrap.kakaocdn.net/dn/iJhSe/hyKByLwzpW/HsTn8kIhd9ZeQi5TRq0wv0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/facebook/prop-types" target="_blank" rel="noopener" data-source-url="https://github.com/facebook/prop-types">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/iJhSe/hyKByLwzpW/HsTn8kIhd9ZeQi5TRq0wv0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">facebook/prop-types</p>
<p class="og-desc" data-ke-size="size16">Runtime type checking for React props and similar objects - facebook/prop-types</p>
<p class="og-host" data-ke-size="size16">github.com</p>
</div>
</a></figure>
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