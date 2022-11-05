---
layout:       post
title:        "컴포넌트의 합성(composition)과 상속(inheritance)"
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
                            <p data-ke-size="size16">&nbsp; 상속은 extends 키워드를 사용해 부모의 모든 속성과 메서드를 물려받는 방식이다. 상속은 부모와 자식간의 의존성이 강하게 결합되기 때문에 유연성이 부족하다. Facebook에서는 수천 개의 리액트 컴포넌트를 사용하지만 컴포넌트를 상속 계층 구조로 작성을 권장할 만한 사례가 등장하지 않았다.</p>
<p data-ke-size="size16"><b>합성</b></p>
<p data-ke-size="size16">&nbsp; <i>컴포넌트에서 다른 컴포넌트를 담기</i></p>
<p data-ke-size="size16">&nbsp; &nbsp; 하나의 컴포넌트에 어떤 자식 컴포넌트가 들어올지 알 수 없을때 children prop를 사용해 자식 엘리먼트를 출력에 그대로 전달해야 한다.&nbsp;&nbsp;</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//FacncyBorder내부의&nbsp;것들이&nbsp;props.children으로&nbsp;전달&nbsp;된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;WelcomeDialog()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>FancyBorder&nbsp;color<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"blue"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>h1&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"Dialog-title"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Welcome</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>h1<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>p&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"Dialog-message"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thank&nbsp;you&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;visiting&nbsp;our&nbsp;spacecraft<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>p<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>FancyBorder<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;FancyBorder(props)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{<span style="color: #63a35c;">'FancyBorder&nbsp;FancyBorder-'</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;props.color}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{props.children}</div>
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
<p data-ke-size="size16">&nbsp; &nbsp; 만약 여러개의 컴포넌트를 props로 전달해야 한다면 children대신 다음과 같은 방식을 상용하면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;SplitPane(props)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"SplitPane"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"SplitPane-left"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{props.left}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"SplitPane-right"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{props.right}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;App()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>SplitPane</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;left<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Contacts&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;right<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Chat&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
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
<p data-ke-size="size16"><b>특수화</b></p>
<p data-ke-size="size16">&nbsp; 어떤 컴포넌트가 특수한 경우인 경우. 즉, 일반적인 컴포넌트가 아닌 구체적은 컴포넌트가 필요한 경우 다음과 같이 일반적인 컴포너트를 렌더링 하고 props를 통해 내용을 전달하면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;Dialog(props)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>FancyBorder&nbsp;color<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"blue"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>h1&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"Dialog-title"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{props.title}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>h1<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>p&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"Dialog-message"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{props.message}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>p<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>FancyBorder<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;WelcomeDialog()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Dialog</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;title<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"Welcome"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;message<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"Thank&nbsp;you&nbsp;for&nbsp;visiting&nbsp;our&nbsp;spacecraft!"</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
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