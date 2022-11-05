---
layout:       post
title:        "Concurrent programming"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- java
- Java8
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
                            <p data-ke-size="size16">&nbsp; Concurrent software는 동시에 여러 작업을 할 수 있는 소프트웨어이다.</p>
<p data-ke-size="size16">&nbsp; 자바에서는 다음과 같은 concurrent programming을 지원한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. multi processing</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. multi thread</p>
<p data-ke-size="size16">&nbsp; &nbsp; 자바는 멀티쓰레딩을 설정하지 않는 한 기본적으로 main thread에서 동작한다.</p>
<p data-ke-size="size16">&nbsp; 자바에서 multi thread를 사용할려면 다음과 같은 방식을 사용하면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//클래스를&nbsp;만들어서&nbsp;사용하는&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MyThread&nbsp;myThread&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyThread();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;myThread.start();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;MyThread&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;Thread&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Override</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;run()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
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
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//runnable, 람다 사용</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread&nbsp;thread&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Thread(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;thread.start();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>thread 중지 시키기</b></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//클래스를&nbsp;만들어서&nbsp;사용하는&nbsp;방법</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread&nbsp;thread&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Thread(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">try</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//thread를&nbsp;인자로&nbsp;넘긴&nbsp;시간만큼&nbsp;중지된다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(1000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">catch</span>&nbsp;(InterruptedException&nbsp;e)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//sleep을&nbsp;하는&nbsp;도중&nbsp;thread를&nbsp;시작시키면&nbsp;에러&nbsp;발생</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.printStackTrace();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;thread.start();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">thread 재시작,thread 종료</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//클래스를&nbsp;만들어서&nbsp;사용하는&nbsp;방법</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread&nbsp;thread&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Thread(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">while</span>(<span style="color: #0099cc;">true</span>)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">try</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(1000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">catch</span>&nbsp;(InterruptedException&nbsp;err)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//thread를&nbsp;재시작&nbsp;시키면&nbsp;종료</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"interrupted"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;thread.start();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(3000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;sleep된&nbsp;thread를&nbsp;재시작시킨다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;thread.interrupt();&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">thread하나가 종료될때 까지 기다리기 (join)</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Thread&nbsp;thread&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Thread(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">try</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(3000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">catch</span>&nbsp;(InterruptedException&nbsp;err)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">throw</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;IllegalStateException(err);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;thread.start();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//위에서&nbsp;생성한&nbsp;thread가&nbsp;끝날때&nbsp;까지&nbsp;다른&nbsp;thread는&nbsp;동작을&nbsp;멈춘다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;thread.join();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//thread가&nbsp;끝나는&nbsp;3초뒤&nbsp;이&nbsp;라인이&nbsp;실행된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(thread&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #63a35c;">"&nbsp;is&nbsp;finished"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>Executors</b></p>
<p data-ke-size="size16">&nbsp; Thread를 관리하는 것을 위의 방식 보다는 좀 더 고수준 API에게 위임한다. Executor는 다음과 같은 일을 한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. Thread를 생성한다: 애플리케이션이 상요할 thread pool을 만들어 관리한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. Thread 관리: thread 생명주기를 관리한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 작업 처리, 실행: thread로 실행할 작업을 제공할 수 있는 API를 제공한다.</p>
<p data-ke-size="size16">&nbsp; Executor를 직접 사용해도 되지만 좀 더 다양한 작업을 제공하는 ExecutorService를 더 많이 사용한다. 또 한 ExecutorService를 상속받는 ScheduledExecutorService역시 존재한다. 이는 특정 주기로 어떤 작업을 실행하거나 또는 어떤 작업을 delay했다가 시작할때 사용된다.</p>
<p data-ke-size="size16">&nbsp; ExecutorService는 명시적으로 종료시킬때 까지 대기를 하기때문에 작업이 끝나면 반드시 종료를 해줘야 한다. 이는 ExecutorService.shutdown()이라는 메서드를 사용하고 이 메서드는 graceful shutdown을 한다(현재 진핸중인 작업을 완전히 끝내고 종료한다). 만약 graceful shutdown()을 하고싶지 않다면 ExecutorService.shutdoenNow()를 사용하면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newSingleThreadExecutor();&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.submit(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.shutdown();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 만약 thread의 갯수 보다 해야 하는 task의 갯수가 많을 경우 thread는 각자 task를 하나씩 가져가 처리한다. 이때 남는 task는 blocking queue에 저장된다. 그 후 thread하나가 task하나를 끝낼때 마다 blocking queue는 task를 작업을 끝낸 thread에 할당한다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//thread가&nbsp;2개인&nbsp;thread&nbsp;pool</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newFixedThreadPool(<span style="color: #0099cc;">2</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.submit(getRunnable(<span style="color: #63a35c;">"hello0"</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.submit(getRunnable(<span style="color: #63a35c;">"hello1"</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.submit(getRunnable(<span style="color: #63a35c;">"hello2"</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.submit(getRunnable(<span style="color: #63a35c;">"hello3"</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.submit(getRunnable(<span style="color: #63a35c;">"hello4"</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.shutdown();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;Runnable&nbsp;getRunnable(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(message&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><i><b>ScheduledExecutorService</b></i></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ScheduledExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newSingleThreadScheduledExecutor();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//3초를&nbsp;기다린&nbsp;후에&nbsp;실행</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.schedule(getRunnable(<span style="color: #63a35c;">"hello"</span>),&nbsp;<span style="color: #0099cc;">3</span>,&nbsp;TimeUnit.SECONDS);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.shutdown();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;Runnable&nbsp;getRunnable(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(message&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
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
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ScheduledExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newSingleThreadScheduledExecutor();&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//처음에는&nbsp;1초&nbsp;delay를&nbsp;하고&nbsp;그&nbsp;다음부터&nbsp;2초&nbsp;주기로&nbsp;실행</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.scheduleAtFixedRate(getRunnable(<span style="color: #63a35c;">"hello"</span>),&nbsp;<span style="color: #0099cc;">1</span>,&nbsp;<span style="color: #0099cc;">2</span>,&nbsp;&nbsp;TimeUnit.SECONDS);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;Runnable&nbsp;getRunnable(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(message&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i></p>
<p data-ke-size="size16"><b><i>Callable</i></b></p>
<p data-ke-size="size16">&nbsp; Runnable은 반환값이 void이다</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q29uY3VycmVudCBwcm9ncmFtbWluZw==/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><i>&nbsp;&nbsp;</i>따라서 thread에서 임의의 task를 수행한 후 결과를 반환해야 한다면 Runnable이 아닌 Callable을 사용해야 한다. Callable은 Runnable과 비슷하지만 값을 반환할 수 있다는 차이가 존재한다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q29uY3VycmVudCBwcm9ncmFtbWluZw==/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newSingleThreadScheduledExecutor();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Callable<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(2000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//Callable의&nbsp;반환값은&nbsp;Future를&nbsp;사용해&nbsp;가져온다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Future<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;submit&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;executorService.submit(hello);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//isDone()은&nbsp;현재&nbsp;thread의&nbsp;작업이&nbsp;끝났으면&nbsp;true,&nbsp;아니면&nbsp;false</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(submit.isDone());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Thread"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//cancel()을&nbsp;통해&nbsp;현재&nbsp;thread를&nbsp;interrupt하고&nbsp;종료한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//인자로&nbsp;true를&nbsp;주면&nbsp;곧바로&nbsp;종료시키고</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//인자로&nbsp;false를&nbsp;주면&nbsp;하던&nbsp;작업을&nbsp;마무리&nbsp;하고&nbsp;종료한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//하지만&nbsp;어떤식으로&nbsp;종료를&nbsp;하던&nbsp;강제로&nbsp;종료한&nbsp;것이기&nbsp;때문에&nbsp;반환값을&nbsp;가져올&nbsp;수&nbsp;없다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//cancel을&nbsp;하면&nbsp;isDone()은&nbsp;true가&nbsp;된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(submit.cancel(<span style="color: #0099cc;">true</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//get()이전까지는&nbsp;그냥&nbsp;실행되고</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//get()&nbsp;부터는&nbsp;thread가&nbsp;작업을&nbsp;끝나기를&nbsp;기다린다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;submit.get();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(submit.isDone());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.shutdown();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><i><b>Callable의 invokeAny, invokeAll 예제</b></i></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newFixedThreadPool(<span style="color: #0099cc;">4</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Callable<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(2000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Callable<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;java&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(3000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Java"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Callable<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;keesun&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread.sleep(1000L);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"keesun"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//incokeAll을&nbsp;사용해&nbsp;Future의&nbsp;리스트를&nbsp;만든다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//invokeAll은&nbsp;입력한&nbsp;Callable이&nbsp;모두&nbsp;종료될때&nbsp;까지&nbsp;기다린다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//따라서&nbsp;결과값이&nbsp;한번에&nbsp;나온다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Future<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;futures&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;&nbsp;executorService.invokeAll(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arrays.asList(hello,&nbsp;java,&nbsp;keesun)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;futures.forEach((future)&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">try</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">catch</span>&nbsp;(InterruptedException&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">|</span>&nbsp;ExecutionException&nbsp;e)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.printStackTrace();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//invokeAny는&nbsp;입력한&nbsp;Callable를&nbsp;수행하되&nbsp;하나만&nbsp;완료되면&nbsp;해당&nbsp;값만&nbsp;반환하고&nbsp;종료한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">String</span>&nbsp;s&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;executorService.invokeAny(Arrays.asList(hello,&nbsp;java,&nbsp;keesun));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(s);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;executorService.shutdown();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>CompletableFuture</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>위에서 다루었던 Futre는 예외처리를 할 수 없고 Future.get()을 하기 전까지는 아무런 작업을 할 수 없다.&nbsp; Future.get()은 blocking call이기 때문에 이 작업이 끝나야 결과값을 가지고 어떤 로직을 수행할 수 있다.</p>
<p data-ke-size="size16">&nbsp; CompletableFuture는 외부에서 complete를 시킬 수 있다.</p>
<p data-ke-size="size16">&nbsp; 반환값이 필요 없는 경우 예제</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.runAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;future.get();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 반환값이 있는 경우 예제</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; CompleteableFuture을 사용하면 callback을 사용할 수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 반환값이 있는 경우 예제</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}).thenApply((string)&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;string.toUpperCase();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;반환값이 없는 경우 예제:</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}).thenAccept((string)&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;반환값이 없고 결과 조차 참조를 안해도 되는 경우 예제:</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}).thenRun(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 위예제의 경우 thread pool을 만들지 않고도 다른 thread를 사용했다. 이게 가능한 이유는 ForkJoinPool때문이다. ForkJoinPool은 executor를 구현한 구현체의 한 종류이다. 이는 deque를 사용하고 thread가 task가 없으면 직접 이 deque에서 task를 가져와 수행한다. 만약 thread자신이 파생시킨 sub-task가 존재한다면 sub-task를 다른 thread에 분산시켜 작업을 하고 마지막에 join을 한다. 따라서 별도로 executor를 사용하지 않아도 ForkJoinPool내부에 있는 common pool을 사용한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp; Executor를 별도로 생성해 사용하는 방법은 다음과 같다</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;ExecutorService&nbsp;executorService&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Executors.newFixedThreadPool(<span style="color: #0099cc;">4</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},&nbsp;executorService).thenRun(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;CompletableFuture로 작업 조합</b></i></p>
<p data-ke-size="size16"><i></i>&nbsp; &nbsp; Future는 콜백이 없기 때문에 여러 작업을 연결할 수 없었다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;world&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"World&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"World"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(hello.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(world.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 위 예제 같이 Hello다음에 World를 출력하기 위해서는 helllo.get()을 한 뒤 그 다음에 world.get()을 해야 했다. 하지만 다음과 같이 thenCompose()를 사용해 작업을 compose할 수 있다. 이 방식은 두개의 future간에 의존성이 있을때 사용된다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;hello.thenCompose(App::getWorld);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;getWorld(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(message&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;message&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #63a35c;">"World"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 만약 두개의 future간에 의존성이 없다면 다음과 같은 방식을 사용할 수 있다. 이 방식은 thenCombine()을 사용한다. thenCombine()은 biFunction을 사용해 두 개의 task가 끝나면 이를 합쳐서 반환한다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;world&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"World&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"World"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;hello.thenCombine(world,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(helloResult,&nbsp;worldResult)&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;helloResult&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #63a35c;">"&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;worldResult</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 만약 두개 이상의 task가 모두 끝난다음에 수행해야할 로직이 있다면 allOf()를 사용하면 된다. 하지만 이를 통해서 특정 결과를 가져올 수 없다. 그 이유는 allOf()인자로 넘기는 모든 task의 결과가 모두 같은 type이라는 보장이 없기 때문이다. 또 한 에러가 발생했을 수 도 있다. 그렇기 때문에 null이 반환된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;world&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"World&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"World"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.allOf(hello,&nbsp;world)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.thenAccept(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);&nbsp;<span style="color: #999999;">//&nbsp;null</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(future.get());&nbsp;<span style="color: #999999;">//&nbsp;null&nbsp;&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp;따라서 두개 이상의 task를 수행해야 한다면 다음과 같은 방식을 사용해야 한다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;world&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"World&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"World"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;futures&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Arrays.asList(hello,&nbsp;world);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture[]&nbsp;futuresArray&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;futures.toArray(<span style="color: #a71d5d;">new</span>&nbsp;CompletableFuture[futures.size()]);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Object<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.allOf(futuresArray)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.thenApply(result&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;futures.stream()</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.map(CompletableFuture::join)&nbsp;<span style="color: #999999;">//&nbsp;Future에서&nbsp;반환하는&nbsp;최종&nbsp;결과값이&nbsp;나온다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.collect(Collectors.toList()));&nbsp;<span style="color: #999999;">//&nbsp;결과값을&nbsp;리스트로&nbsp;만든다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;future.get()</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.forEach(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 여러 task중 어느 하나가 끝나면 해당 값을 반환하는 방식은 다음과 같다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;world&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"World&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"World"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;future&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.anyOf(hello,&nbsp;world)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.thenAccept(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;future.get();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; <i><b>CompletableFuture에러 처리</b></i></p>
<p data-ke-size="size16"><i></i>&nbsp; CompletableFuture에서는 다음과 같은 방식을 사용해 에러처리를 한다</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">boolean</span>&nbsp;throwError&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">true</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>(throwError)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">throw</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;IllegalArgumentException();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}).exceptionally(ex&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(ex);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Error"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(hello.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; 또 한 handle()을 사용할 수 도 있다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;<span style="color: #a71d5d;">throws</span>&nbsp;ExecutionException,&nbsp;InterruptedException&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">boolean</span>&nbsp;throwError&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">true</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;CompletableFuture<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;hello&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;CompletableFuture.supplyAsync(()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>(throwError)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">throw</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;IllegalArgumentException();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Hello&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;Thread.currentThread().getName());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"hello"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}).handle((result,&nbsp;ex)&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>(ex&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">!</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">null</span>)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(ex);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #63a35c;">"Error"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;result;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(hello.get());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
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