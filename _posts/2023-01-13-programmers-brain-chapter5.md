---
layout:       post
title:        "Chpater 5. 코드를 더 깊이 있게 이해하기"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프로그래머의 뇌
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이전 장에서 문법을 알고 변수들의 관계를 이해하는 것이 코드를 읽는 대 도움이 된다는 것을 서술했다. 하지만 코드를 생각하는 데 큰 역할을 하는 더 깊은 주제가 있다. 코드에 대해 깊이 이해하는 법을 논의해 보자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>'변수 역할' 프레임워크</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>변수가 어떤 역할을 하는지 알아내는 것이 코드 추론에서 중요한 역할을 한다. 그 때문에 적절한 변수명은 표식(beacon)으로 사용될 수 있으며 해당 코드를 깊이 이해하는 데도 도움이 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이스턴 핀란드 대학교의 료르마 사야니에미(Jorma Sajanieimi) 교수에 따르면, 변수를 이해하기 어려운 이유는 대부분의 프로그래머가 변수를 연관 지을 좋은 스키마를 LTM에 가지고 있지 않기 때문이다. 또 한, 사람은 'studentInformation'이나 'numberOfCustomer' 같이 너무 포괄적이거나 너무 구체적인 청크를 사용하는 경향이 있다. 그 중간이 가장 적절하다. 가장 적절한 이름을 지을 수 있게 도와주는 변수 역할(rolw of variables)이라는 프레임워크를 살펴보자.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>변수는 각자 다른 일을 한다</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다음 코드를 살펴보자.&nbsp;</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">upperbound&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">int</span>(input(<span style="color: #63a35c;">'Upper&nbsp;bound?'</span>))</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">max_prime_factors&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">for</span>&nbsp;counter&nbsp;<span style="color: #a71d5d;">in</span>&nbsp;<span style="color: #066de2;">range</span>(upperbound):</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;factors&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;prime_factors(counter)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;factors&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;max_prime_factors:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;max_prime_factors&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;factors</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 코드에서 upperbound와 factors는 입력한 값을 갖거나 가장 최근 값으로 갱신되는 최근값 보유자 역할을 한다. counter는 루프를 돌면서 순차적으로 값이 면하는 스테퍼 역할을 한다. max_prime_factors는 달성하고자 하는 값을 보유하고 있는 목적값 보유자이다. 이처럼 변수 역할 프레임워크에서 변수는 여려 역할로 나눠져 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>11가지 역할&nbsp;</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 변수 역할 프레임워크에서 변수를 다음과 같은 11가지 역할로 나눈다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>고정값(fixed value)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 초기화를 통해 값이 할당된 이후 값이 변하지 않는 변수다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>스테퍼(stepper)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>루프를 반복할 때 값이 단계적으로 변하는 변수다(ex - for (int i = 0;...)에서 i).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>플래그(flag)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>무엇인가 발생했거나 어떤 경우에 해당하는지를 나타내는 변수.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>워커(walker)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>스테퍼와 유사하게 자료구조를 순회한다. 스테퍼는 정해진 값을 따라 루프를 순회한다. 하지만 워커는 루프가 시작되기 전에 어떤 값을 가지는지 알 수 없다. 스택 순회 등이 그 예시다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>최근값 보유자(most recent holder)<br></b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>어떤 값이 변해갈 때 가장 최근에 변경된 값을 갖는 변수. 파일을 읽을 때 가장 마지막에 읽은 라인 등이 그 예시다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>목적값 보유자(most wanted holder)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>어떤 값에 대해 반복할 때 그 목적이 어떤 특정한 값을 찾는 것이라면, 찾고자 하는 값 또는 현재까지 발견된 값 중에서 찾고자 하는 조건에 부합하는 값을 갖는 변수를 의미한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>모집자(gather)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>모집자는 데이터를 모으거나 모은 데이터에 대해 어떤 연산을 수행하여 얻은 값을 저장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>컨테이너(container)<br></b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>값을 새로 추가하거나 삭제할 수 있는 자료구조</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>추적자(follwer)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>이전 값 또는 다음 값을 추적하는 변수다. 리스트에서 이전 값에 대한 포인터가 그 예시다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>조직자(organizer)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>추가적인 처리를 위해 변수의 값을 변환해 저장하는 변수를 의미한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>임시(temporary)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;</b> 임시로 사용하기 위한 변수. 데이터를 바꾸는 등의 간단한 행위에 일지적으로 필요한 변수를 일컫는다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>역할과 패러다임</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 언급한 변수의 역할은 프로그래밍 패러다임에 관련 없이 모두 적용할 수 있다. 객체지향의 경우 다음과 같이 역할을 나눌 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;Dog&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;string&nbsp;name;&nbsp;<span style="color: #999999;">//&nbsp;초기화&nbsp;이후&nbsp;변하지&nbsp;않기에&nbsp;고정값&nbsp;역할</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;age;&nbsp;<span style="color: #999999;">//&nbsp;birthday를&nbsp;호출하면&nbsp;0에서&nbsp;시작해&nbsp;순차적으로&nbsp;증가하기에&nbsp;스테퍼&nbsp;역할</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;Dog(string&nbsp;n)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;n;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;age&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;birthday()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;age<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>;</span></div>
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
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 변수 역할 프레임워크를 새로운 개념이 아닌 변수에 대해 논의할 때 사용할 수 있는 새로운 용어를 제공해 주는 정도로 생각하면 된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>헝가리안 표기법</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>strName과 같이 변수 타입을 이름에 나타내는 방식을 헝가리안 표기법이라 한다. 이는 타입 시스템이 없는 언어에서 비롯되었다. IDE가 없던 시절 변수에는 변수 타입을 알기 어려웠기에 이에 대한 정보를 변수에 추가해 사용했다. 하지만 이 방식은 변수 이름을 길게 만들어 어떤 면에서 코드 가독성을 떨어트리거나 타입변경 시 많은 변수에 영향을 미친다. 따라서 현재에는 이 방식이 권장되지 않는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 헝가리안 표기법은 두 가지로 나뉜다. 변수명에 타입을 나타낸다면 이는 시스템 헝가리안 표기법(Systems Hungarian notaiton)이다. 타입이 아닌 특정 의미를 나타내는 접두어가 붙는다면 이는 앱 헝가리안 표기법(Apps Hungarian notatino)이다(배열의 길이를 나타낼 때 접두어로 l을 붙이는 등). 헝가리안 표기법에 대해 더 알고 싶다면 "Meta-Programming: A Software Porduction Method"를 참고하자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로그램에 대해 깊이 있는 지식을 얻으려면</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 콜로라도 대학교 심리학과 교수 낸시 페닝턴(Nancy Pennington)은 프로그래머가 소스 코드를 이해하는 두 개의 서로 다른 층위가 존재하며 이를 텍스트 구조 지식(text structure knowledge)과 계획 지식(plan knowledge)으로 나눴다. 텍스트 구조 지식은 변수 역할 같이 표면적인 이해와 관련 있다. 계획 지식은 프로그래머가 코드를 작성함으로써 이루고자 했던 목표와 계획에 연관돼 있다. 계획 지식은 코드의 구조를 살펴볼 때 명확해진다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>프로그램 이해의 여러 단계</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그램에 대한 계획 지식을 갖는다는 것은 코드의 각 부분이 다른 부분들과 어떤 방식으로 관련되어 있는지 이해하는 것을 의미한다. 브리검영 대학교 조너선 실리토(Jonathan Sillito) 교수의 연구에 선 코드를 이해하는 단계를 다음과 같이 정의했다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 원하는 목적을 달성하기 위한 코드의 초점(시작점)을 찾는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 초점으로부터 지식을 확장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 관련된 개체로부터 개념을 이해한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 여러 개체에 걸쳐 있는 개념을 이해한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>텍스트를 읽는 것과 코드를 읽는 것은 유사하다</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>코드가 두뇌에 하는 일</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>브로드만 영역은 두뇌를 서로 다른 52개의 위치로 나눈 것이다. 독일 컴퓨터 과학 교수 야네트 지그문트(Janet Siegmund)가 실시한 연구에서 실험자들은 잘 아려진 알고리즘을 구현한 코드를 읽었다. 이 코드에서 변수는 알아보기 어려준 이름으로 대치돼서 참자가 들은 프로그램 흐름을 파악해야 했다. 이 실험에서 총 5개의 브로드만 영역이 활성화된 것을 확인했다. 그중 두 개는 작업 기억 공관과 주의를 기울이는 정신 활동과 관련 있다. 나머지 세 개는 인간 언어 이해와 관련 있었다. 이해하기 어려운 변수를 읽고 추측할 때 이 세 개 영역을 사용했는 대, 이는 인간의 언어로 된 텍스트를 읽을 때 하는 일이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>프랑스어를 배울 수 있다면 파이썬도 배울 수 있다</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그래밍에서 어떤 인지 능력이 중요한 역할을 하는지에 대한 <a href="https://www.nature.com/articles/s41598-020-60661-8?awc=26427_1673597099_63f4beecf37e5e5a1ae21c195096160c&amp;utm_medium=affiliate&amp;utm_source=awin&amp;utm_campaign=CONR_PF018_ECOM_DE_PHSS_ALWYS_DEEPLINK&amp;utm_content=textlink&amp;utm_term=!!!affid" target="_blank" rel="noopener">연구</a> 결과를 살펴보자. 이 연구에서 계산 능력, 즉 수학적 능력은 그다지 중요하지 않다는 결과가 나왔다. 그보다는 듣고, 보고, 이해하는 언어 능력과 일반적인 인지 능력이 더 중요하다는 결론을 내렸다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>사람들은 어떻게 코드를 읽는가?</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 우와노 히데타게 교수의 연구에 따르면 프로그래머들은 코드를 검토하는 데 사용한 시간의 처음 30% 동안 코드의 70%를 훑어본다. 이런 스캔은 자연어로 된 텍스트의 구조를 전체적으로 파악할 때 일어난다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 초급 프로그래머는 코드를 읽을 때 순차적으로 읽는 반면 숙련된 프로그래머는 콜 스택을 좇아 읽는다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>코드 읽기에 적용해 볼 수 있는 텍스트 이해 전략</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 살펴봤듯 코드를 읽을 때 사용하는 인지적 능력은 자연어를 읽을 때 사용하는 것과 유사하다. 이는 자연어 텍스트 이해에 대한 통찰을 코드 독해에 적용할 수 있다는 의미다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 텍스트 이해에 대한 전략은 다음과 같이 7개의 범주로 나뉜다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 활성화: 관련된 것들을 적극적으로 생각해 이미 가지고 있는 지식을 활성화하는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 모니터링: 텍스트를 읽으면서 자신이 이해한 것을 관찰하고 기록하는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 중요도 결정: 텍스트에서 어느 부분이 중요한지 결정하는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 추론: 텍스트에서 명시적으로 주어지지 않은 사실을 유추하는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 시각화: 깊이 있는 이해를 위해 텍스트에 대한 도표를 만드는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 질문: 텍스트에 대해 질문하는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 요약: 텍스트를 짧게 요약하는 것</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 코드를 이해하는 관점에서 위 전력을 살펴보자</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>기존 지식의 활성화</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그래머는 코드를 읽을 때 자세히 읽기 전에 스캔을 먼저 하면서 코드 내에 존재하는 개념과 문법적 요소들에 대한 일차적 이해를 한다. 두뇌는 생각을 할 때 작업 기억 공간이 LTM에서 그와 관련된 지식을 검색한다. 코드를 스캔하는 과정에서 이런 검색이 발생한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>모니터링</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>코드를 읽을 때 현재 무엇을 읽고 있는지, 이해를 하고 있는지 계속 추적하는 것이 중요하다. 이해되는 것뿐만 아니라 이해되지 않는 것도 머릿속에 기억해야 한다. 이를 위해 이해되지 않는 라인이나 변수 역할을 표시하는 것이 좋다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>코드에서 중요한 라인을 결정하기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>코드를 읽을 때 어떤 라인이 중요한지를 파악하는 것은 유용하다. 이는 의도적 연습을 통해 할 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>변수명의 의미를 추론하기</b><b></b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그램의 의미가 코드의 구조 자체에 담겨있을 수 있다. 변수 등 프로그램 구성 요소의 이름에서 의미를 추론할 수 있다. 변수 이름은 중요한 표식이므로 코드를 읽을 때 의식적으로 변수에 주목하는 것이 좋다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>질문하기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 코드를 읽을 때 스스로에게 질문하는 것은 코드의 목적과 기능에 대해 이해하는 대 도움이 된다. 예를 들어 코드 작성자가 어떤 기술을 왜 사용했는지를 스스로 질문해 보는 식이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>코드 요약</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>읽은 코드를 사람이 사용하는 언어로 요약하는 것은 코드가 하는 일을 깊이 이해하는 데 도움이 된다. 이런 요약을 통해 개인적 목적의 문서를 만들 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 프로그래머의 뇌</span></p></div>