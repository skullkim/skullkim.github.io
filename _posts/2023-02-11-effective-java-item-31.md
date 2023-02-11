---
layout:       post
title:        "Item 31. 한정적 와일드카드를 사용해 API 유연성을 높이라"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- java
- 이펙티브자바
- 도서
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16">&nbsp; 매개변수화 타입은 불공변(invariant)이다. 즉, 서로 다른 타입 Type1과 Type2가 있을 때 List &lt;Type1&gt;과 List &lt;Type2&gt;는 서로의 상위 타입도 하위 타입도 아니다. 예컨대 List &lt;String&gt;은 List &lt;Object&gt;의 하위 타입이 아니다. 이는 List &lt;String&gt;이 List &lt;Object&gt;가 하는 일을 제대로 수행하지 못하는 어쩌면 당연한 일이다.</p>
<p data-ke-size="size16">&nbsp; 하지만 때로는 불공변보다 유연한 방식이 필요하다. 예를 들어 다음과 같은 코드르 보자.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;Stack<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;Stack();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;push(E&nbsp;e);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;E&nbsp;pop();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #066de2;">boolean</span>&nbsp;isEmpty();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;pushAll(Interable<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;src);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위 코드에서 pushAll() 메서드는 완벽하지 않다. 예를 들어 Stack&lt;Number&gt;에서 int 타입을 pushAll()의 파라미터로 넘긴다 해보자. 그러면 매개변수화 타입은 불공변이므로 에러가 발생한다.</p>
<p data-ke-size="size16">&nbsp; 위 같은 문제를 해결하기 위해 한정적 와일드카드 타입이라는 매개변수화 타입을 지원한다. 한정적 와일드카드 타입은 상한(&lt;? extends E&gt;), 하한(&lt;? super E&gt;)으로 구분된다. 상한은 E의 하위 타입 요소를 모두 받는다. 하한은 반대로 E의 상위 타입 요소를 모두 받는다. 따라서 pushAll()의 선언을 다음과 같이 수정하면 int 타입도 받을 수 있게 된다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">void</span>&nbsp;pushAll(Interable<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>?&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;src);</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 모든 원소를 pop하는 메서드의 경우 다음과 같이 정의할 수 있다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">void</span>&nbsp;popAll(Coolection<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>?&nbsp;<span style="color: #a71d5d;">super</span>&nbsp;E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;dst)</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 유연성을 극대화하려면 원소의 생산자나 소비자용 입력 매개변수에 와일드카드 타입을 사용하라. 만약 입력 매개변수가 동시에 소비자와 생산자의 역할을 한다면, 이는 타입을 정확히 지정해야 하는 상황이므로 와일드카드를 사용하지 말라.</p>
<p data-ke-size="size16">&nbsp; 와일드카드 타입을 고를 때 PECS(producer-extends, consumer-super) 공식을 기억하면 도움이 된다. 이 공식으로 위 예시를 보면, pushAll은 Stack이 사용할 E 인스턴스를 생성 하기에 extends가, popAll은 Stack으로부터 E 인스턴스를 소비하기에 super가 적절하다.</p>
<p data-ke-size="size16">&nbsp; 반환 타입에는 한정적 와일드카드를 사용하지 않도록 주의하자. 반환값에 한정적 와일드카드를 사용한다면 유연성을 높여주지도 않고 클라이언트 코드에서도 와일드카드를 사용해야 한다. 클래스 사용자가 와일드카드 타입을 신경써야 한다면 그 API에 문제가 있을 가능성이 크다.</p>
<p data-ke-size="size16">&nbsp; 다음과 같은 코드가 존재한다 해보자.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;Set<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;union(Set<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;s1,&nbsp;Set<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>E<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;s2)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">set<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Number<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;numbers&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;union(integers,&nbsp;doubles);</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위 코드는 자바7 이하에서는 "incompatible types"라는 에러를 발생시킨다. 이는 <a href="https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#target-typing" target="_blank" rel="noopener">목표 타이핑(target typing)</a>을 java 8 부터 지원하기에 컴파일러가 올바른 타입 추론을 하지 못해 발생하는 에러다. 이를 해결하기 위해선 명시적 타입 인수(explicit type arguemnt)를 사용하면 된다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">set<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Number<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;numbers&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;Union.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Number<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>union(integers,&nbsp;doubles);</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p></div>