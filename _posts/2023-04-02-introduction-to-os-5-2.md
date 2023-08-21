---
layout:       post
title:        "Chapter5-2. 공유 자원과 임계구역"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
- ComputerScience
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여러 프로세스가 한정된 자원을 가지고 공동 작업을 하면 여러 문제가 발생할 수 있습니다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>공유 자원의 접근</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 공유 자원은 여러 프로세스가 공동으로 이용하는 변수, 메모리, 파일 등을 말한다. 공유 자원은 공동으로 이용되기 때문에 racing condition이 발생할 수 있다. 이런 racing condition이 발생할 수 있는 프로그램의 영역을 임계구역(critical section)이라 한다. 임계구역에서는 프로세스들이 동시에 작업하면 안 된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>생산자-소비자 문제(producer-consumer problem)</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>생산자-소비자 문제에서 생산자 프로세스와 소비자 프로세스는 서로 독립적으로 작업한다. 생산자는 데이터를 생산해 버퍼에 넣는다. 소비자는 버퍼에스 데이터를 사용한다. 버퍼를 계속 사용하기 위해 원형 버퍼(circular buffer)를 사용한다. 버퍼가 가득 찼는지를 확인하기 위해 sum이라는 전역 변수를 사용한다. sum에는 현재 버퍼가 얼마나 차있는지가 기록돼 있다. 이 과정을 sudo code로 간단히 표현하면 다음과 같다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">producer()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;input(buf);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;sum&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">consumer()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;output(buf);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;sum&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 코드는 생성자 코드와 소비자 코드가 동시에 실행될 때 다음과 같은 문제가 발생한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- 생산자가 데이터 하나를 buf 4에 저장했다. sum(현재 sum은 3)을 바꿔야 하지만 바꾸지 못했다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- 소비자가 데이터 하나를 소비했다. sum을 2로 바꿔야 하나 바꾸지 못했다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- 이 상태에서 "sum += 1"과 "sum -= 1"이 거의 동시에 실행되면 실행 순서에 따라 sum 값이 달라진다. 생산자와 소비자는 서로 독립적이라 상대방이 sum을 바꾸는 것을 모른다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- "sum += 1" -&gt; "sum -=1" 순서로 진행하면 sum = 2가 된다, 반대로 진행하면 sum = 4가 된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>임계구역 해결 조건</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 임계구역 문제를 해결하기 위해선 다음 세 가지 조건을 만족해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>상호 배제(mutual exclusion)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>한 프로세스가 임계구역에 들어가면 다른 프로세스는 임계구역에 들어갈 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>한정 대기(bounded waiting)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 어떤 프로세스도 무한 대기(inifite postpone) 하지 않아야 한다. 즉, 특정 프로세스가 임계구역에 진입하지 못하면 안 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>진행의 융통성(progress flexibility)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>한 프로세스가 다른 프로세스의 진행을 방해해선 안된다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p>
<p data-ke-size="size16">&nbsp;</p></div>