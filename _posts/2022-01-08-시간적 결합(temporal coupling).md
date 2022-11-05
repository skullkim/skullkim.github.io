---
layout:       post
title:        "시간적 결합(temporal coupling)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- 시간적결합
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;결합도는 소프트웨어의 유연성을 해친다. 시간적 결합은 coupling의 한 종류이며 어떤 방식으로 인해 코드가 시점에 의존하는 것을 의미한다. 시간적 결합이 있는 코드는 그 코드가 정확이 무엇을 하는지를 알지 못하는 한 사이드 이팩트를 야기한다. </span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다음은 시간적 결합의 종류와 예시이다.</span></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Sequencing</span></b></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">하나의 일이 어떤 일이 완료된 후 실행되야 하는 경우이다. 아래의 코드가 그 예시이다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">var&nbsp;circle&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Circle();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">circle.setRadius(<span style="color: #0099cc;">10</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">circle.getCircumference();&nbsp;<span style="color: #999999;">//&nbsp;throws&nbsp;if&nbsp;you&nbsp;haven't&nbsp;called&nbsp;setRadius()&nbsp;first!</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이런식으로 정해진 순서대로 코드를 작성해야 하는 것은 프로그래머가 요구되는 실행 순서를 알아야 하는 것을 강제한다. 만약 프로그래머가 강제되는 순서를 알지 못한다면 예상하지 못한 예외를 발생시킨다. 심지어는 처리가 완료되지 않은 데이터를 다운스트림으로 보낼 수 도 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 예제의 경우 radius를 미리 정하게 함으로써 시간적 결합을 해결할 수 있다. setRadius를 하는 대신 생성자의 파라미터로 raidus값을 넘기면 getCircumference 메서드를 호출하기 전에 setRadius 메서드를 호출할 필요가 없다. 또 한 생성자 파라미터를 넘기지 않으면 컴파일 단계에서 애러가 발생되기 때문에 사이드 이펙트를 방지할 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Waiting</span></b></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;쿼리나 API 호출 같이 일이 끝나기 까지 기다려야 하는 경우이다. 이는 소프트웨어에서 빈번히 발행하며 통상적으로 유저가 소프트웨어 사용을 위해 얼만큼의 시간을 기다려야 하는지를 고려한다. 유저는 소프트웨어 사용을 위해 기다리는 것을 싫어한다. 하지만 개발자는 머신이 다른 머신을 기다리는 시간이 얼마인지도 고려해야 한다. 이는 시스템의 설계와 프로그래밍의 난이도에 영향을 미친다. </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Waiting 문제는 순서의 문제와 종종 결합된다. 다음 작업을 위해 API 응답을 기다려야 하는 것이 그 예시다. 기다리는 시간이 길수록 실패의 확률도 올라간다. 기다리는 시간이 길면 머신이 time out을 발생시키거나 사람이 포기하게 된다. 분산 시스템에서 out of band healing이 지연과 순서에 해결책이 될 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 실질적으로 waiting을 없애는 것을 불가능 하다. 하지만 더 빠른 네티워크 커넥션과 더 빠른 머신을 사용해 waiting을 줄일 수 있다. 또 한 로딩 바 같은 것을 사용해 사용자가 기다려야 하는 시간을 명시하는 것도 하나의 방법이다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 비동기를 사용하는 것 역시 하나의 방법이다. 하나의 일이 끝나기를 기다리고 일이 끝나면 그 값을 전달하는 대신 값을 점진적으로 전달하면 된다. 처음 웹 페이지를 방문하면 최소한의 데이터만 렌더링 된 후 AJAX를 통해 더 많은 데이터를 로딩하는 것이 그 예시다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Circumstance(상황)</span></b></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위키 피디아의 시간적 결합 정의는 다음과 같다. "두 개의 일이 동시에 발생한다는 이유 만으로 하나의 모듈에 존재하는 것."</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 따라서 circumstance는 높은 응집도를 고려하지 않아 발생한 부산물이다. </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 개념적으로 분리된 것들이 합쳐져서 코드 유지보수를 더 어렵게 만든다. 만약 두 개의 일이 완전히 다른 일 이라면 문제를 쉽게 파악할 수 있고 정정할 수 있다. 하지만 만약 두 개의 일이 연결되 있는거 같은 느낌이 든다면 두 개의 연결점을 찾기 어려워 진다. 가장 복잡한 경우는 대규모 데이터셋을 반복하는 경우와 같이 성능 최적화의 일부로 결합이 발행하는 경우다. 이 경우 SOLID를 적용하고 올바른 리팩토링을 통해 결합도를 낮춰야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Circumstance의 경우 배포 후의 실질 문제를 만들지는 않을 거다. 하지만 이에 대해 무지하다면 더러워진 코드로 인해 개발 효율이 낮아진다. 만약 이로 인한 문제가 발생한다면 이를 해결하기 위해 수 많은 리소스가 투입된다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Loosen temporal coupling</span></b></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">시간적 결합을 온전히 없애는 것은 불가능 하다. 하지만 이를 최대한 없애지 않는 다면 코드의 변경이 어려워진다. 시간적 결합을 줄이기 위해서는 적절한 패턴을 활용해야 한다.</span></p>
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