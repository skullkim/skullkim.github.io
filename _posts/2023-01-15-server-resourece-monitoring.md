---
layout:       post
title:        "서버 리소스 사용량 관측하기"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 프로젝트
- kilomter
- OS
- linux
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로젝트를 하던 도중 세부적인 CPU 사용량과 context switching에 소모되는 리소스를 관측해야 하는 일이 생겨 이를 도와줄 수 있는 툴에 대해 찾아보게 되었다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>vmstat</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 메모리, 시스템 프로세스, 페이징, 인터럽트, I/O, CPU 스케줄링에 대한 정보를 수집해 전체 호스트 수준에서 보여주는 툴이다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Bprocs&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>memory<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>swap<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>io<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>system<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;r&nbsp;&nbsp;b&nbsp;&nbsp;&nbsp;swpd&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;buff&nbsp;&nbsp;cache&nbsp;&nbsp;&nbsp;si&nbsp;&nbsp;&nbsp;so&nbsp;&nbsp;&nbsp;&nbsp;bi&nbsp;&nbsp;&nbsp;&nbsp;bo&nbsp;&nbsp;&nbsp;in&nbsp;&nbsp;&nbsp;cs&nbsp;us&nbsp;sy&nbsp;id&nbsp;wa&nbsp;st</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1216236</span>&nbsp;&nbsp;<span style="color: #0099cc;">76632</span>&nbsp;<span style="color: #0099cc;">12827516</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">5</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같은 정보를 확인할 수 있으며, 이 중 in(interrupt), cs(Context Switching)이 Context Switching 비용과 관련 있다. CPU 사용량 단위는 ‘%’이고 메모리 사용 단위는 ‘KB’이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Vmstat가 제공한는 각 지표의 의미는 다음과 같다</span></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">process</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">r: 실행 가능한 프로세스</span></li>
<li><span style="font-family: 'Noto Serif KR';">b: 블로킹된 프로세스</span></li>
</ul>
</li>
<li><span style="font-family: 'Noto Serif KR';">memory</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">swpd: 스왑 메모리</span></li>
<li><span style="font-family: 'Noto Serif KR';">free: 미사용 메모리</span></li>
<li><span style="font-family: 'Noto Serif KR';">buff: 버퍼로 사용한 메모리</span></li>
<li><span style="font-family: 'Noto Serif KR';">cache: 캐로 사용한 메모리</span></li>
</ul>
</li>
<li><span style="font-family: 'Noto Serif KR';">swap</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">si: 디스크로 교체된 들어간 메모리(swap-in)</span></li>
<li><span style="font-family: 'Noto Serif KR';">so: 디스크에서 교체되 빠져나온 메모리(swap-out)</span></li>
</ul>
</li>
<li><span style="font-family: 'Noto Serif KR';">io</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">bi(block-in): input 장치에서 받은 512 바이트 블록 개수</span></li>
<li><span style="font-family: 'Noto Serif KR';">bo(block-out): output 장치로 보낸 512 바이트 블록 개수</span></li>
</ul>
</li>
<li><span style="font-family: 'Noto Serif KR';">system</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">in: interrupt 횟수</span></li>
<li><span style="font-family: 'Noto Serif KR';">cs: context switching 횟수</span></li>
</ul>
</li>
<li><span style="font-family: 'Noto Serif KR';">cpu(단위: %)</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><span style="font-family: 'Noto Serif KR';">us: 유저 시간</span></li>
<li><span style="font-family: 'Noto Serif KR';">sy: 커널 시간(system time)</span></li>
<li><span style="font-family: 'Noto Serif KR';">id: 유휴 시간</span></li>
<li><span style="font-family: 'Noto Serif KR';">wa: 대기 시간</span></li>
<li><span style="font-family: 'Noto Serif KR';">st: 도둑 맞은 시간(가상 머신에 할애된 시간)</span></li>
</ul>
</li>
</ul>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">특정 기간을 두고 특정 횟수만큼 측정을 하고 싶다면 다음과 같이 vmstat를 사용하면 된다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">vmstat&nbsp;<span style="color: #0099cc;">5</span>&nbsp;<span style="color: #0099cc;">10</span>&nbsp;<span style="color: #999999;">#&nbsp;5초의&nbsp;간격을&nbsp;두고&nbsp;10번&nbsp;캡쳐한다</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">1초에 한번 관측되는 수치 변화를 계속 보고 싶다면 다음과 같이 사용하면 된다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">주의해야 할</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;">&nbsp;</td>
</tr>
</tbody>
</table>
</div>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b> 지표</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">만약 위 지표 중 cpu의 us(유저 모드에서 CPU 사용률)가 100% 근처에 도달하지 못했는데 어떤 프로세스에서 콘텍스트 스위칭 비율(system 지표에서 cs)이 높게 나왔다면, 이는 I/O에서 블로킹이 발생했서나 스레드 락 경합(thread lock contention) 상황이 발생했을 확률이 크다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>cperf</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">복합적인 시스템 퍼포먼스 통계를 내주는 툴이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>설치:</b></span></h3>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">sudo&nbsp;apt<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>get&nbsp;install&nbsp;linux<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>tools<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>common&nbsp;linux<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>tools<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>generic</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">sudo&nbsp;apt&nbsp;install&nbsp;linux<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>tools<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">5.</span><span style="color: #0099cc;">15.</span><span style="color: #0099cc;">0</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">52</span><span style="color: #a71d5d;">-</span>generic&nbsp;linux<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cloud<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>tools<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">5.</span><span style="color: #0099cc;">15.</span><span style="color: #0099cc;">0</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">52</span><span style="color: #a71d5d;">-</span>generic</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">다음과 같이 임의의 시간 동안 데이터를 수집해 통계를 낼 수 있다</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">sudo&nbsp;perf&nbsp;stat&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>a&nbsp;sleep&nbsp;<span style="color: #0099cc;">20</span>&nbsp;<span style="color: #999999;">#&nbsp;20초&nbsp;동안&nbsp;데이터를&nbsp;수집한다</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">통계 결과:</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Performance&nbsp;counter&nbsp;stats&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;<span style="color: #63a35c;">'system&nbsp;wide'</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">80</span>,<span style="color: #0099cc;">007.</span><span style="color: #0099cc;">09</span>&nbsp;msec&nbsp;cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>clock&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;4.000&nbsp;CPUs&nbsp;utilized</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">9</span>,<span style="color: #0099cc;">832</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;context<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>switches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;122.889&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">202</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>migrations&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;2.525&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2</span>,<span style="color: #0099cc;">393</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;page<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>faults&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;29.910&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>,<span style="color: #0099cc;">338</span>,<span style="color: #0099cc;">969</span>,<span style="color: #0099cc;">186</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cycles&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;0.042&nbsp;GHz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.32%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>,<span style="color: #0099cc;">830</span>,<span style="color: #0099cc;">939</span>,<span style="color: #0099cc;">977</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stalled<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cycles<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>frontend&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;114.73%&nbsp;frontend&nbsp;cycles&nbsp;idle&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.32%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>,<span style="color: #0099cc;">454</span>,<span style="color: #0099cc;">468</span>,<span style="color: #0099cc;">148</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stalled<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cycles<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>backend&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;103.46%&nbsp;backend&nbsp;cycles&nbsp;idle&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(66.69%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">482</span>,<span style="color: #0099cc;">245</span>,<span style="color: #0099cc;">519</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;instructions&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;0.14&nbsp;&nbsp;insn&nbsp;per&nbsp;cycle</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;7.94&nbsp;&nbsp;stalled&nbsp;cycles&nbsp;per&nbsp;insn&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">98</span>,<span style="color: #0099cc;">889</span>,<span style="color: #0099cc;">967</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;1.236&nbsp;M/sec&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">14</span>,<span style="color: #0099cc;">826</span>,<span style="color: #0099cc;">643</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branch<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>misses&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;14.99%&nbsp;of&nbsp;all&nbsp;branches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.33%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20.</span><span style="color: #0099cc;">001630108</span>&nbsp;seconds&nbsp;time&nbsp;elapsed</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">특정 프로세스의 동작을 특정 시간동안 확인하고 싶다면, 다음과 같은 명령어를 사용하면 된다</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">sudo&nbsp;perf&nbsp;record&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>F&nbsp;<span style="color: #0099cc;">99</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>p&nbsp;PID&nbsp;sleep&nbsp;<span style="color: #0099cc;">10</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이렇게 수집된 특정 프로세스의 데이터는 .data 확장자를 가진 바이너리 파일로 저장된다. 이 파일 수치를 확인하기 위해선 다음과 같은 명령어를 사용하면 된다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">sudo&nbsp;perf&nbsp;report</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1940" data-origin-height="1653"><span data-url="https://blog.kakaocdn.net/dn/cWEnNt/btrWjkgYvbv/OOd2dBwugGFHk42RlUitB1/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-server-resource-monitoring/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcWEnNt%2FbtrWjkgYvbv%2FOOd2dBwugGFHk42RlUitB1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1940" data-origin-height="1653"></span></figure>
<p></p>
<h1><span style="font-family: 'Noto Serif KR';"><b>Context Switching 테스트</b></span></h1>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">위에서 소개한 툴들의 정상 동작 여부를 확인하기 위해 일부러 콘텍스트 스위칭을 많이 발생시키는 코드를 만들고 돌려보자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">time.csv:</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">past_date,future_date&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2006</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">12</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">28</span>,<span style="color: #0099cc;">2030</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">03</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">23</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2001</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">11</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">20</span>,<span style="color: #0099cc;">2026</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">10</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">30</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2006</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">12</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">28</span>,<span style="color: #0099cc;">2035</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">03</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">23</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2004</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">11</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">20</span>,<span style="color: #0099cc;">2024</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">01</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">30</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2003</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">12</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">28</span>,<span style="color: #0099cc;">2035</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">03</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">23</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2002</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">11</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">20</span>,<span style="color: #0099cc;">2024</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">08</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">30</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2005</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">12</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">28</span>,<span style="color: #0099cc;">2033</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">03</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">23</span>&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2005</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">07</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">20</span>,<span style="color: #0099cc;">2051</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">01</span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">30</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">contextSwitch.go:</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">23</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">24</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">25</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">26</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">27</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">28</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">29</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">30</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">31</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">32</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">33</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">34</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">35</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">36</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">37</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">38</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">39</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">40</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">41</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">42</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">43</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">44</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">45</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">46</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">47</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">48</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">49</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">50</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">51</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">52</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">53</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">54</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">gpackage&nbsp;main&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">import</span>&nbsp;(</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"encoding/csv"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"fmt"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"log"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"os"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"sync"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"time"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">func&nbsp;f(from&nbsp;<span style="color: #a71d5d;">string</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;wg&nbsp;sync.WaitGroup</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;sliceLength&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1000000</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;wg.Add(sliceLength)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;i&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>;&nbsp;i&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;sliceLength;&nbsp;i<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;records&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;readCsvFile(<span style="color: #63a35c;">"time.csv"</span>)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;go&nbsp;func(i&nbsp;<span style="color: #a71d5d;">int</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;defer&nbsp;wg.Done()</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;_,&nbsp;record&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;range&nbsp;records&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;layout&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">"2006-01-02"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;past_date,&nbsp;_&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;time.Parse(layout,&nbsp;record[<span style="color: #0099cc;">0</span>])</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;future_date,&nbsp;_&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;time.Parse(layout,&nbsp;record[<span style="color: #0099cc;">1</span>])</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;past_date.Date()</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;future_date.Date()</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}(i)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;wg.Wait()</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">func&nbsp;readCsvFile(filePath&nbsp;<span style="color: #a71d5d;">string</span>)&nbsp;[][]<span style="color: #a71d5d;">string</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;f,&nbsp;err&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;os.Open(filePath)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;err&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">!</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;nil&nbsp;{&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log.Fatal(<span style="color: #63a35c;">"Unable&nbsp;to&nbsp;read&nbsp;input&nbsp;file&nbsp;"</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>filePath,&nbsp;err)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;defer&nbsp;f.Close()&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;csvReader&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;csv.NewReader(f)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;records,&nbsp;err&nbsp;:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;csvReader.ReadAll()&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;err&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">!</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;nil&nbsp;{&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log.Fatal(<span style="color: #63a35c;">"Unable&nbsp;to&nbsp;parse&nbsp;file&nbsp;as&nbsp;CSV&nbsp;for&nbsp;"</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>filePath,&nbsp;err)&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;records&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">func&nbsp;main()&nbsp;{&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;f(<span style="color: #63a35c;">"direct"</span>)&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;fmt.Println(<span style="color: #63a35c;">"done"</span>)&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이제 위 코드를 구동시켜보자</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">go&nbsp;run&nbsp;contextSwitch.go</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이제 vmstat와 pref를 이용해 위 코드가 구동되는 사이의 수치를 관측하면 된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>vmstat 결과 (사용 명령어: vmstat 1)</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">콘텍스트 스위칭 발생 시 system에 속하는 in(interrupt)와 cs(context switching) 수치가 월등히 높아진 것을 확인할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">contextSwitch.go를 실행한 상태:</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">procs&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>memory<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>swap<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>io<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>system<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;r&nbsp;&nbsp;b&nbsp;&nbsp;&nbsp;swpd&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;buff&nbsp;&nbsp;cache&nbsp;&nbsp;&nbsp;si&nbsp;&nbsp;&nbsp;so&nbsp;&nbsp;&nbsp;&nbsp;bi&nbsp;&nbsp;&nbsp;&nbsp;bo&nbsp;&nbsp;&nbsp;in&nbsp;&nbsp;&nbsp;cs&nbsp;us&nbsp;sy&nbsp;id&nbsp;wa&nbsp;st</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1189036</span>&nbsp;&nbsp;<span style="color: #0099cc;">93012</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">5</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1188004</span>&nbsp;&nbsp;<span style="color: #0099cc;">93012</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">12955</span>&nbsp;<span style="color: #0099cc;">127689</span>&nbsp;<span style="color: #0099cc;">38</span>&nbsp;<span style="color: #0099cc;">13</span>&nbsp;<span style="color: #0099cc;">49</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1187104</span>&nbsp;&nbsp;<span style="color: #0099cc;">93012</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13228</span>&nbsp;<span style="color: #0099cc;">125807</span>&nbsp;<span style="color: #0099cc;">35</span>&nbsp;<span style="color: #0099cc;">16</span>&nbsp;<span style="color: #0099cc;">48</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">2</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1185200</span>&nbsp;&nbsp;<span style="color: #0099cc;">93012</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13595</span>&nbsp;<span style="color: #0099cc;">123887</span>&nbsp;<span style="color: #0099cc;">37</span>&nbsp;<span style="color: #0099cc;">14</span>&nbsp;<span style="color: #0099cc;">49</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">3</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1184500</span>&nbsp;&nbsp;<span style="color: #0099cc;">93012</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13349</span>&nbsp;<span style="color: #0099cc;">126304</span>&nbsp;<span style="color: #0099cc;">35</span>&nbsp;<span style="color: #0099cc;">14</span>&nbsp;<span style="color: #0099cc;">50</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1184500</span>&nbsp;&nbsp;<span style="color: #0099cc;">93020</span>&nbsp;<span style="color: #0099cc;">12857328</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">92</span>&nbsp;<span style="color: #0099cc;">13183</span>&nbsp;<span style="color: #0099cc;">128388</span>&nbsp;<span style="color: #0099cc;">34</span>&nbsp;<span style="color: #0099cc;">16</span>&nbsp;<span style="color: #0099cc;">49</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">2</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1182736</span>&nbsp;&nbsp;<span style="color: #0099cc;">93020</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13236</span>&nbsp;<span style="color: #0099cc;">126502</span>&nbsp;<span style="color: #0099cc;">35</span>&nbsp;<span style="color: #0099cc;">16</span>&nbsp;<span style="color: #0099cc;">49</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1182876</span>&nbsp;&nbsp;<span style="color: #0099cc;">93020</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">13284</span>&nbsp;<span style="color: #0099cc;">125777</span>&nbsp;<span style="color: #0099cc;">35</span>&nbsp;<span style="color: #0099cc;">16</span>&nbsp;<span style="color: #0099cc;">48</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">4</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1181980</span>&nbsp;&nbsp;<span style="color: #0099cc;">93020</span>&nbsp;<span style="color: #0099cc;">12857336</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">14028</span>&nbsp;<span style="color: #0099cc;">121666</span>&nbsp;<span style="color: #0099cc;">35</span>&nbsp;<span style="color: #0099cc;">15</span>&nbsp;<span style="color: #0099cc;">50</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">일반 상황:</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">procs&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>memory<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>swap<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>io<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>system<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;r&nbsp;&nbsp;b&nbsp;&nbsp;&nbsp;swpd&nbsp;&nbsp;&nbsp;free&nbsp;&nbsp;&nbsp;buff&nbsp;&nbsp;cache&nbsp;&nbsp;&nbsp;si&nbsp;&nbsp;&nbsp;so&nbsp;&nbsp;&nbsp;&nbsp;bi&nbsp;&nbsp;&nbsp;&nbsp;bo&nbsp;&nbsp;&nbsp;in&nbsp;&nbsp;&nbsp;cs&nbsp;us&nbsp;sy&nbsp;id&nbsp;wa&nbsp;st</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1175292</span>&nbsp;&nbsp;<span style="color: #0099cc;">93216</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">5</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1175180</span>&nbsp;&nbsp;<span style="color: #0099cc;">93216</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">295</span>&nbsp;&nbsp;<span style="color: #0099cc;">477</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">100</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174704</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">44</span>&nbsp;&nbsp;<span style="color: #0099cc;">284</span>&nbsp;&nbsp;<span style="color: #0099cc;">491</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1175208</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">277</span>&nbsp;&nbsp;<span style="color: #0099cc;">486</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174956</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">258</span>&nbsp;&nbsp;<span style="color: #0099cc;">472</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">100</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174792</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">299</span>&nbsp;&nbsp;<span style="color: #0099cc;">516</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174452</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">284</span>&nbsp;&nbsp;<span style="color: #0099cc;">484</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174928</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">259</span>&nbsp;&nbsp;<span style="color: #0099cc;">458</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">100</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174452</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">84</span>&nbsp;&nbsp;<span style="color: #0099cc;">300</span>&nbsp;&nbsp;<span style="color: #0099cc;">497</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174956</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">290</span>&nbsp;&nbsp;<span style="color: #0099cc;">488</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">100</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1174452</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">297</span>&nbsp;&nbsp;<span style="color: #0099cc;">510</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">4608</span>&nbsp;<span style="color: #0099cc;">1175208</span>&nbsp;&nbsp;<span style="color: #0099cc;">93224</span>&nbsp;<span style="color: #0099cc;">12856044</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">290</span>&nbsp;&nbsp;<span style="color: #0099cc;">520</span>&nbsp;&nbsp;<span style="color: #0099cc;">1</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #0099cc;">99</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span>&nbsp;&nbsp;<span style="color: #0099cc;">0</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>perf 결과 (사용 명령어: sudo perf stat -a sleep 20)</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">contextSwitch.go를 실행한 상태:</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Performance&nbsp;counter&nbsp;stats&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;<span style="color: #63a35c;">'system&nbsp;wide'</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">80</span>,<span style="color: #0099cc;">011.</span><span style="color: #0099cc;">25</span>&nbsp;msec&nbsp;cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>clock&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;4.000&nbsp;CPUs&nbsp;utilized</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2</span>,<span style="color: #0099cc;">279</span>,<span style="color: #0099cc;">586</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;context<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>switches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;28.491&nbsp;K/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">13</span>,<span style="color: #0099cc;">291</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>migrations&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;166.114&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">123</span>,<span style="color: #0099cc;">884</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;page<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>faults&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;1.548&nbsp;K/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">114</span>,<span style="color: #0099cc;">869</span>,<span style="color: #0099cc;">775</span>,<span style="color: #0099cc;">771</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cycles&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;1.436&nbsp;GHz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.32%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">122</span>,<span style="color: #0099cc;">889</span>,<span style="color: #0099cc;">824</span>,<span style="color: #0099cc;">804</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stalled<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cycles<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>frontend&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;106.98%&nbsp;frontend&nbsp;cycles&nbsp;idle&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.32%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">103</span>,<span style="color: #0099cc;">631</span>,<span style="color: #0099cc;">665</span>,<span style="color: #0099cc;">515</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stalled<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cycles<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>backend&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;90.22%&nbsp;backend&nbsp;cycles&nbsp;idle&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(66.68%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">92</span>,<span style="color: #0099cc;">521</span>,<span style="color: #0099cc;">223</span>,<span style="color: #0099cc;">777</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;instructions&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;0.81&nbsp;&nbsp;insn&nbsp;per&nbsp;cycle</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;1.33&nbsp;&nbsp;stalled&nbsp;cycles&nbsp;per&nbsp;insn&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">19</span>,<span style="color: #0099cc;">027</span>,<span style="color: #0099cc;">317</span>,<span style="color: #0099cc;">534</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;237.808&nbsp;M/sec&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">170</span>,<span style="color: #0099cc;">918</span>,<span style="color: #0099cc;">900</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branch<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>misses&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;0.90%&nbsp;of&nbsp;all&nbsp;branches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.33%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20.</span><span style="color: #0099cc;">002279774</span>&nbsp;seconds&nbsp;time&nbsp;elapsed</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">일반 상황:</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Performance&nbsp;counter&nbsp;stats&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;<span style="color: #63a35c;">'system&nbsp;wide'</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">80</span>,<span style="color: #0099cc;">007.</span><span style="color: #0099cc;">03</span>&nbsp;msec&nbsp;cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>clock&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;4.000&nbsp;CPUs&nbsp;utilized</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">9</span>,<span style="color: #0099cc;">509</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;context<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>switches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;118.852&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">202</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cpu<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>migrations&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;2.525&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">2</span>,<span style="color: #0099cc;">329</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;page<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>faults&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;29.110&nbsp;/sec</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>,<span style="color: #0099cc;">287</span>,<span style="color: #0099cc;">813</span>,<span style="color: #0099cc;">081</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cycles&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;0.041&nbsp;GHz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.32%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>,<span style="color: #0099cc;">728</span>,<span style="color: #0099cc;">859</span>,<span style="color: #0099cc;">681</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stalled<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cycles<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>frontend&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;113.41%&nbsp;frontend&nbsp;cycles&nbsp;idle&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.32%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">3</span>,<span style="color: #0099cc;">400</span>,<span style="color: #0099cc;">931</span>,<span style="color: #0099cc;">749</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;stalled<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>cycles<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>backend&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;103.44%&nbsp;backend&nbsp;cycles&nbsp;idle&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(66.69%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">472</span>,<span style="color: #0099cc;">904</span>,<span style="color: #0099cc;">185</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;instructions&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;0.14&nbsp;&nbsp;insn&nbsp;per&nbsp;cycle</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;7.89&nbsp;&nbsp;stalled&nbsp;cycles&nbsp;per&nbsp;insn&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">96</span>,<span style="color: #0099cc;">356</span>,<span style="color: #0099cc;">371</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;&nbsp;1.204&nbsp;M/sec&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">14</span>,<span style="color: #0099cc;">636</span>,<span style="color: #0099cc;">573</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;branch<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>misses&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#&nbsp;&nbsp;&nbsp;15.19%&nbsp;of&nbsp;all&nbsp;branches&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(83.34%)</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">20.</span><span style="color: #0099cc;">001863836</span>&nbsp;seconds&nbsp;time&nbsp;elapsed</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">참고 자료:</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://www.hanbit.co.kr/store/books/look.php?p_code=B7707787549" target="_blank" rel="noopener">OREILLY 자바 최적화</a></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://www.site24x7.com/learn/linux/context-switching.html" target="_blank" rel="noopener">High context switch and interrupt rates: How to diagnose and fix in linux</a></span></p></div>