---
layout:       post
title:        "Event Storming"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- eventstorming
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
                            <h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>왜 DDD를 사용하나?</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. DDD를 사용하면 실제 비즈니스 도메인을 아키텍처에 투영해 도메인을 정의하고 이 도메인을 바탕으로 커뮤니케이션 할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 도메인 전문가와 개발자들이 공통된 언어를 사용할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같은 이점들로 인해 DDD는 현재 널리 사용되고 있는 설계 방식이다. 그리고 DDD를 하기 위한 가장 쉬운 방법 중 하나가 Event Storming이다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Event Storming</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>사전 준비:</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 다양한 색의 포스트잇, 마커</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 포스트잇을 붙일 수 있는 큰 공간(모두가 볼 수 있어야 한다)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 각 포스트잇 색이 의미하는 바를 명시해 놓은 공간(모두가 볼 수 있어야 한다)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 좌석은 없이, 서서 진행한다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. 개발자 뿐만아니라 해당 소프트웨어를 제작하는데 필요한 모든 인원들이 함께 참석한다</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Event Storming의 장점</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>1. 간단한 방식으로 진행되기 때문에 이해가 쉽다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 개발과 비즈니스가 생각을 맞춰볼 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. MSA를 디자인할 때 도메인과 서브도메인을 가를 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Event Storming 결과</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>Event Storming의 최종 결과의 예시는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Event Storming의 최종 결과는 큰 바운더리를 여러개 가지며 하나의 바운더리 안에 여러개의 포스트잇이 존재한다. 각 포스트잇들은 위와 같이 연관된 것들 끼리 붙임으로서 상관 관계를 나타낸다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>각 포스트잇의 의미</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 "Event Sotrming 결과"에서 나온 각 포스트잇의 의미는 다음과 같다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Domain Event</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>이벤트를 도출할 때 사용한다. 사용자에게 발생하는 이벤트들을 서술하며 과거형 또는 수동형으로 서술한다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Command</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp; </b>커맨드는&nbsp;이벤트들을 발생시키는 행위다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>External System</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>이벤트 발생에 필요한 외부 시스템.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Aggregate</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>서로 관련있는 도메인 모델들의 집합이다. 한 개 이상의 entity 또는 value로 이뤄져 있다. 각 aggregate는 aggregate라는 루트 도메인을 가진다. 이 루트는 aggregate 내에 속한 객체의 변경을 책임지고, 도메인 규칙에 따라 내부에 존재하는 도메인 모델들의 일관성을 유지한다. aggregate의 예시는 다음과 같다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">@entity</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;Item&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #066de2;">String</span>&nbsp;name;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;quantity;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;PorductId&nbsp;productId;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Aggregate 끼리는 각자의 id를 통해 서로 참조해야 한다. 이를 통해 결합도를 낮춘다. Aggreate 끼리 직접 참조를 하면 다음과 같은 문제가 발생한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 1. 다른 aggregate를 수정하기 쉬워지기 때문에 우발적인 수정이 발생할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 2. 확장이 어렵다. 모든 aggreagate를 모두 같은 곳에 저장해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; command, aggregate, event는 command가 aggregate에게 영향을 주고 최종적으로 event가 발생되는 식으로 관계가 맺어져 있다. 예시는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 예시에서 볼 수 있듯이 aggregate와 event는 원자성을 가진다. 즉, 어떤 이벤트가 발생했을 때 aggregate의 상태에 변화가 발생한다.&nbsp;</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Event Storming 실행 절차</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이벤트를 붙일 때는 왼쪽에서 오른쪽으로 시간 순으로 붙인다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img_2.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; command는 event와 짝으로 발생한하며 각 event 왼편에 위치한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img_3.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 command와 event와 관련된 aggregate를 붙인다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img_4.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; command는 aggregate에 영향을 미쳐서 aggregate의 상태가 바뀌고, 그로 인해 event가 발생한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Boris diagram</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>Event diagram을 통해 나온 상관관계들을 aggregate 단위로 봤을 때 어떤 상호작용을 할지 볼 수 있는 다이어그램이다. 아래 예시에서 노란색은 aggregate를 나타내며 분홍색은 external system을 나타낸다.</span></p>
<p></p><figure class="imageblock alignCenter" width="670" height="313">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img_5.png" width="670" height="313">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Snap E</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>위 과정을 통해 도출한 서비스 중 일부를 필요하다면 좀 더 상세하게 적을 수 있다. 여기에는 해당 서비스가 사용하는 API, data, user story 등이 포함된다. 이를 통해 해당 서비스와 연관된 모든 것들을 한 눈에 파악할 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/RXZlbnQgU3Rvcm1pbmc=/img_6.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
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