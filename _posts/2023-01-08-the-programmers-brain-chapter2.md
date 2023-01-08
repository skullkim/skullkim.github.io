---
layout:       post
title:        "Chapter 2. 신속한 코드 분석"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프로그래머의 뇌
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 코드를 읽는 행위에 대해 살펴보자. <a href="https://ieeexplore.ieee.org/document/7997917" target="_blank" rel="noopener">연구</a>(Measuring Program Comprehension)에 의하면 프로그래머는 프로그래밍 시간 중 60%를 코드 이해에 사용한다. 따라서 정확도를 유지하면서 코드를 빨리 읽어야 효율이 증가한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>코드를 신속하게 읽기</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 코드를 읽을 때 대부분의 프로그래머는 그 코드에 존재하는 특정 정보를 찾는다. 따라서 관련 정보를 신속하게 찾는 능력의 향상은 곧 효율의 향상이다. 다음과 같은 코드가 존재하고 이 코드를 이해해야 한다고 해보자.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">5</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">6</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">7</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">8</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">9</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">10</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">11</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">12</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">16</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">17</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;InsertionShort&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>[]&nbsp;array&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;{<span style="color: #0099cc;">2</span>,&nbsp;<span style="color: #0099cc;">4</span>,&nbsp;<span style="color: #0099cc;">1</span>,&nbsp;<span style="color: #0099cc;">10</span>,&nbsp;<span style="color: #0099cc;">20</span>,&nbsp;<span style="color: #0099cc;">14</span>};</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;temp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(<span style="color: #066de2;">int</span>&nbsp;i&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;i&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;array.<span style="color: #066de2;">length</span>;&nbsp;i<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(<span style="color: #066de2;">int</span>&nbsp;j&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;i;&nbsp;j&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;j<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(array[j]&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;array[j&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">1</span>])&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;temp&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;array[j];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;array[j]&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;array[j&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">1</span>];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;array[j&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">1</span>]&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;temp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(<span style="color: #066de2;">int</span>&nbsp;i&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;i&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;array.<span style="color: #066de2;">length</span>;&nbsp;i<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(array[i]);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 코드를 읽을 때 클래스 이름이 InsertionShort 이므로 삽입 정렬을 구현한 코드라는 것을 알 짐작할 수 있다. 따라서 이 코드를 읽을 때 LTM에 저장된 삽입 정렬에 대한 지식과 STM에 저장된 변수 이름 등을 복합적으로 사용하게 된다. 이제 다음과 같은 코드를 보자</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">5</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">6</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">7</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">8</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">9</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">10</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">11</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">12</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;execute(<span style="color: #066de2;">int</span>&nbsp;x[])&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;b&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;x.<span style="color: #066de2;">length</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(<span style="color: #066de2;">int</span>&nbsp;v&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;b&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">1</span>;&nbsp;v&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;v<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;func(x,&nbsp;b,&nbsp;v);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(<span style="color: #066de2;">int</span>&nbsp;l&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;b&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">1</span>;&nbsp;l&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;l<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;temp&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;x[<span style="color: #0099cc;">0</span>];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x[<span style="color: #0099cc;">0</span>]&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;x[l];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x[l]&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;temp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;func(x,&nbsp;l,&nbsp;<span style="color: #0099cc;">0</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 코드는 메서드 이름이나 변수 이름을 통해 LTM에 저장된 프로그래밍 지식을 이끌어낼 수 없다. 따라서 대부분의 경우 STM에 의존하기 때문에 코드를 일기 위해 더 많은 리소스가 필요하다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>생소한 코드를 읽는 것은 왜 어려운가</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>STM의 기억력은 30초를 넘지 않고 용량 또한 2~6개 사이로&nbsp;극히 적다. 이것이 STM에 많이 의존해야 하는, 생소한 코드를 읽기 어려운 이유다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>기억의 크기 제한을 극복하기</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;위 이론대로 라면 STM을 사용하기 때문에 코드에서 6개 넘는 문자를 기억할 수 없다. 하지만 실상은 더 많은 것을 기억한다. 그 이유는 LTM을 사용해 단위(chunk)로 정보를 묶기 때문이다. 예컨대 위 코드에서 코드 여러 줄을 InsertionShort라는 단위로 묶는 것이다. InsertionShort라는 청크로 위 코드를 묶을 때 LTM에 존재하는 삽입 정렬에 대한 지식을 사용하게 된다. 따라서 LTM에 존재하는 프로그래밍 지식이 많은 전문가가 초보자 보다 더 많은 코드를 기억한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>읽는 것보다 보는 것이 더 많다</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; STM에 정보가 도달하기 전에 정보는 감각 기억 공간(Sensory Memory)이라는 영역을 통과한다. 이 영역은 각 감각에 대한 정보를 임시 저장하는 버퍼 같은 역할을 한다. 여러 종류의 감각 기억 공간 중 프로그래밍과 관련된 영상 기억 공간(Iconic Memory)이라는 시각 관련 기억 공간을 살펴보자.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>영상 기억 공간</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>정보가 감각 기관을 통해 들어오면 감각 기억 공간에 임시 저장돼었다가 STM으로 전달된다. 하지만 "T<a href="https://psycnet.apa.org/record/2011-17733-001" target="_blank" rel="noopener">he Inoframtion Available in Brief Visual Presentation</a>"에 의하면 감각 기억 공간에 임시 저장된 지식이 모두 STM으로 전달되지 않는다. STM의 저장 공간은 감각 기억 공간의 절반 정도다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>영상 정보와 코드</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 언급했 듯 모든 영상 기억 공간에 저장된 정보를 STM으로 이전할 수 없기에 무의식적으로 코드를 읽을 때 처리할 수 있는 부분을 선택한다. 따라서 무의식 적으로 중요한 부분을 놓치기도 한다. 이는 코드에 대해 STM이 처리할 수 있는 것보다 더 많은 정보를 저장하는 것이 이론적으로는 가능하다는 것을 의미한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>기억하는 대상이 중요한 것이 아니고 기억하는 방식이 중요하다</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>알골 언어 키워드를 21개 주고 초급, 중급, 고급 프로그래머들에게 이 키워드를 기억하게 하는 실험이 있었다. 이 실험에서 고급 프로그래머들은 키워드들을 이미 가지고 있는 지식을 이용해 묶어 기억했다. 예를 들어 TRUE와 FALSE를 묶고, IF, THEN, ELSE를 묶는 식이다. 이를 통해 일상적이고 예상 가능한 상황은 청크로 묶는 것을 쉽게 한다는 것을 알 수 있다. 따라서 그룹을 나누기 쉬운 코드가 읽기 쉬운 코드라 추측할 수 있고 이에 대한 연구 역시 진행되었다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>디자인 패턴의 사용</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>그룹을 묶기 쉬운 코드로 작성하기 위해선 디자인 패턴을 사용하면 된다. 현직 개발자를 대상으로 한 <a href="https://link.springer.com/article/10.1023/B:EMSE.0000027778.69251.1f" target="_blank" rel="noopener">실험</a>에서 디자인 패턴을 알고 난 후 이를 사용해 코드를 수정할 때 소요되는 시간이 패턴을 사용하지 않았을 경우 보다 더 적게 소요된다는 결론을 얻었다. 즉, 디자인 패턴이라는 지식을 사용해 여러 정보를 청킹 했다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>주석문 쓰기</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; <a href="https://ieeexplore.ieee.org/document/48797" target="_blank" rel="noopener">연구</a> 결과에 의하면 개발자는 주석문을 포함한 코드를 읽을 때 주석문을 포함하지 않는 코드보다 더 많은 시간을 사용한다. 따라서 주석문을 사용하면 개발자는 주석들을 읽는다는 의미다. 따라서 복잡한 로직을 간단히 서술하는 주석(ex - XXX 알고리즘을 사용한다.)은 개발자가 코드를 읽을 때 청킹을 도와줘서 읽기에 도움이 된다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>표식 (beacon) 남기기</b><b></b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 표식은 개발자가 코드를 읽을 때 그 코드가 어떤 역할을 하는지 알려주는 역할을 한다. 표식은 코드를 일고 이해하는 과정에서 소스 코드에 대해 개발자가 갖는 가정의 오류 여부를 확인시켜 주기에 중요한 역할을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 표식에는 단순 표식(simple beacon)과 복합 표식(compound beacon)이 존재한다. 단순 표식은 의미 있는 변수명 같은 코드의 문법을 통해 의미가 저명한 표식이다. 언어 자체에서 지원하는 키워드도 단순 표식에 해당된다. 복합 표식은 여러 단순 표식으로 이루어진 더 큰 단위를 의미한다. 인스턴스의 메서드를 호출할 경우 '인스턴스.메서드(..)'와 같은 모양을 갖는대 이런 것이 복합 표식이다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 표식은 청크와 관련 있지만 대부분의 연구자들은 이 둘을 다른 개념으로 보고 있다. 표식은 보통 청크보다는 작은 코드의 일부분으로 받아들여진다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>청킹 연습</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 경험이 쌓이면 프로그래밍 지식이 늘어나면서 코드에 대한 청킹 능력이 늘긴 하지만, 코드 청킹을 의도적 연습(deliberate practice - 기술 향상을 위해 조금씩 연습하는 것)을 통해 훈련하는 것도 좋다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 코드 청킹을 연습하는 방법은 다음과 같다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 50줄이 넘지 않는 코드를 준비한다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 최대 2분이 넘지 않는 시간 동안 코드를 파악한다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 종이나 IDE에 파익 했던 코드를 기억해 내면서 작성해 본다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 원래 코드와 스스로 작성한 코드를 비교하면서 회고한다. 회고 시 다음과 같은 질문을 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 어느 부분을 쉽게 기억했는가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 부분적으로 기억한 코드가 있는가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 전체를 다 기억하지 못한 코드가 있는가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; -&nbsp; 기억하지 못한 라인들이 있다면 그 이유가 무엇일까?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 기억하지 못한 라인에 본인이 익숙하지 않은 프로그래밍 개념이 들어 있지는 않은가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 기억하지 못한 라인에 본인이 익숙하지 않은 도메인 지식이 있지는 않은가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 같이 연습할 사람이 있다면 서로의 코드를 비교해 본다(생략 가능).</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 프로그래머의 뇌</span></p>
<p data-ke-size="size16">&nbsp;</p></div>