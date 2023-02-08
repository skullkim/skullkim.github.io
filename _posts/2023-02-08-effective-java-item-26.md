---
layout:       post
title:        "Item 26. 로 타입은 사용하지 말라"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- java
- 이펙티브자바
- 도서
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 클래스와 인터페이스 선언에 타입 매개변수(type parameter)를 쓰면, 이를 각가 제네릭 클래스와 제네릭 인터페이스라 한다. 이 둘을 통틀어 제네릭 타입(generic type)이라 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 각 제네릭 타입은 매개변수화 타입(parameterized type)을 정의한다. 예컨대 List &lt;String&gt;은 원소 타입이 String인 리스트를 의미하는 매개변수화 타입이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 제네릭 타입을 정의하면 로 타입(raw type)도 함께 정의된다. 로 타입은 매개변수를 전혀 사용하지 않을 때를 의미한다.로 타입은 정보가 전부 지워진 것처럼 동작하는데 이는 제네릭이 java5에서 출시되기 전의 코드와 호환되게 하기 위한 궁여지책이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 로 타입 컬렉션을 사용하면 다음과 같은 문제가 발생한다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;Stamp&nbsp;인스턴스만&nbsp;취급한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">private</span>&nbsp;finla&nbsp;Collection&nbsp;stamps&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;...;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;실수로&nbsp;다른&nbsp;타입의&nbsp;인스턴스를&nbsp;넣어도&nbsp;문제가&nbsp;없다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">stamps.<span style="color: #066de2;">add</span>(<span style="color: #a71d5d;">new</span>&nbsp;Coin(...));</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">// 이 컬렉션에서 잘못 할당한 인스턴스를 꺼내야 에러가 발생한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">for</span>&nbsp;(Iterator&nbsp;i&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;stamps.iterator();&nbsp;i.hasNext();)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;Stamp&nbsp;stamp&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;(Stamp)&nbsp;i.next();&nbsp;<span style="color: #999999;">//ClassCastException&nbsp;발생</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;stamp.cancel();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 같이 인스턴스를 꺼내야 에러가 발생한다면 문제가 되는 코드와 에러가 발생한 곳이 물리적으로 멀리 떨어져 있을 가능성이 크다. 따라서 코드 전체를 훑어봐야 하는 불상사가 발생한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 제네릭을 사용하면 컴파일러가 인스턴스 타입을 인지하게 되서 의도한 동작을 보장할 수 있다. 컴파일러는 컬렉션에서 원소를 꺼내는 모든 곳에 보이지 않는 형변환을 추가해서 실패하지 않음을 보장한다. 그에 반해 로 타입을 사용하면 제네릭이 안겨주는 안전성과 표현력을 모두 잃게 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 많은 단점에도 불구하고 로 타입이 나온 이유는 자바가 나온 후 10년 뒤에야 제네릭이 추가되었기 때문이다. 제네릭 이전의 코드와 새로운 코드가 호환되게 하기 위해 로 타입을 도입했다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 로 타입 대시신 List&lt;Object&gt; 같이 임의 객체를 허용하는 매개변수화 타입은 괜찮다. 이는 모든 타입을 허용한다는 것을 컴파일러에 명확히 전달하기 때문이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 제네릭 타입을 쓰고 싶지만, 실제 타입 매개변수 타입을 신경 쓰고 싶지 않다면 비한정적 와일드카드 타입(unbounded wildcard type, ex - Set &lt;?&gt;)을 사용하는 게 좋다. 로타입 컬렉션은 아무 원소나 넣을 수 있기에 타입 불변식을 훼손할 여지가 있다. 그에 반해 비한정적 와일드카드 타입은 어떤 원소도 넣을 수 없고 컬렉션에서 꺼낼 수 있는 객체의 타입도 알 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 로 타입을 사용해도 되는 예외가 몇 가지 있다. class 리터럴에는 로 타입을 사용해야 한다. 자바 명세에서는 List.class같이 로 타입 사용은 허용하지만 List&lt;String&gt;.class 같은 매개변수화 타입은 허용하지 않는다. 또 다른 경우는 instanceof 연산자다. 런타임에선 제네릭 타입 정보가 지워지기 때문에 instanceof 연산자는 비한정적 와일드카드 타입 이외의 매개변수화 타입에는 적용할 수 없다. 또 한, instanceof는 로 타입과 비한정적 와일드카드 타입 여부와 관련 없이 똑같이 동작한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 이펙트브 자바</span></p></div>