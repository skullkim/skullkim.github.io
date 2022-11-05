---
layout:       post
title:        "소유권(Ownership)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- rust
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 소유권은 러스트가 gc없이 메모리 안정성 보장을 하게 해준다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;러스트에서 메모리는 컴파일 타임에 컴파일러가 체크할 규칙들로 구성된 소유권 시스템을 통해 관리된다. 소유권 기능들은 런타임 비용이 발생하지 않는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 애플리케이션 실행 시 힙에 저장된 데이터에 접근하는 것은 스택에 저장된 데이터에 접근하는 것 보다 느리다. 스택 메모리는 top에 접근하면 되는 반면에 힙은 포인터가 가리키는 곳을 따라가야 하기 때문이다. 코드의 어느 부분이 힙의 어떤 데이터를 사용하는지 추적하는 것, 힙의 중복된 데이터의 양을 최소화 하는 것, 힙 내에 사용하지 않는 데이터를 제거하는 것이 소유권과 관련된 문제이다. 따라서 힙 데이터를 관리하는 것이 소유권 존재의 이유이다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>소유권 규칙</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 소유권은 다음과 같은 규칙을 가지고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 1. 러스트의 각각의 값은 해당값의 오너(owner)라 불리는 변수를 가지고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 2. 한번에 딱 하나의 오너만 존재할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 3. 오너가 스코프 밖으로 벗어나면 값은 버려진다(dropped).</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>String 타입</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 소유권을 설명하기 위해 우선 String타입을 보자.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 문자열 타입은 불변이기 때문에 스트링 리터럴을 사용하는 것은 일부 경우에 부적절할 수 있다. 이를 위해 러스트는 String이라는 타입을 제공한다. 이 타입은 힙에 할당되며 길이가 정해져 있지 않는 문자열을 저장할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;::은&nbsp;타입&nbsp;아래&nbsp;함수를&nbsp;특정짓는&nbsp;네임스페이스&nbsp;연산자</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;<span style="color: #0086b3;">mut</span>&nbsp;str&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;str.push_str(<span style="color: #63a35c;">",&nbsp;world"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;println<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span>(<span style="color: #63a35c;">"{}"</span>,&nbsp;str);&nbsp;<span style="color: #999999;">//&nbsp;hello&nbsp;world</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 예제에서 볼 수 있듯이 String타입은 변할 수 있지만 스트링 리터럴은 변할 수 없다. 이 차이는 두 타입이 메모리를 사용하는 방식의 차이에서 비롯된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>스트링 리터럴과 String 타입의 차이</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i></i>&nbsp; &nbsp; 스트링 리터럴의 경우 문자열이 변경되지 않을 것을 전제로 한다. 따라서 내용물을 컴파일 타임에 알 수 있고 텍스트가 최종 파일에 직접 하드코딩 되어 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; String 타입은 변경 가능하고 커질 수 있는 텍스트를 지원하기 위해 만들어졌다. 이는 힙에서 컴파일 타임에는 알 수 없는 크기의 메모리&nbsp; &nbsp; 공간을 할당받아 내용물을 저장한다. 즉, 다음과 같은 기능이 필요하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 1. 런타임에 운영체제로부터 메모리가 요청되어야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 2. String의 사용이 끝났을 때 OS에게 메모리를 반납할 방법이 필요하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 첫번째 기능의 경우 String::from을 호출해 구현 부분에서 필요한 만큼의 메모리를 요청하면 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 하지만 두번째 기능의 경우 러스트는 GC도 없고, 직접 메모리를 해제하지도 않는다. 즉, 러스트는 다른 방식으로 이 문제를 해결한다. 러스트는 변수가 소속된 스코프 밖으로 벗어나는 순간 자동으로 반납된다. 이를 위해 러스트는 drop이라는 함수를 '}'가 나올때 자동으로 호&nbsp; &nbsp; 출한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>변수와 데이터가 상호작용 하는 방법: move.</b></i></span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">5</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;y&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 위의 코드는 y에 x를 value로 복사한다. 그리고 5라는 값들이 스택에 push된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 하지만 아래의 예시처럼 런타임때 메모리를 할당받는 경우는 동작 방식이 다르다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;s1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;s2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;s1;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 이 코드에서 첫번째 줄은 다음과 같은 구조를 가지고 있다.(String은 메모리의 포인터, 길이, 용량 총 3개의 부분으로 이루어져 있다.)</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7IaM7Jyg6raMKE93bmVyc2hpcCk=/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 두 번째 줄이 실행되면 String 데이터가 복사된다. 여기서 복사는 스택에 존재하는 ptr, len, capacity가 복사된다는 의미이다. 따라서 다음과 같은 구조가 된다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7IaM7Jyg6raMKE93bmVyc2hpcCk=/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 이제 러스트의 메모리 해제 방식을 다시 떠올려 보자. 러스트는 변수가 스코프 밖으로 벗어나면 자동으로 drop 함수를 호출해 메모리를 해재한다. 따라서 위와 같이 s1과 s2가 같은 값을 가리키고 있을 경우 s1, s2가 스코프 밖으로 벗어나면 메모리가 두번 해제(double free) 오류가 발생한다. 이는 메모리 손상(memory corruption)의 원인이며 보안 취약성이 발생할 가능성이 존재한다. 이 문제를 해결 하기 위해 러스트는 할당된 메모리를 복사하는 대신 s1을 더이상 유효하지 않다고 간주한다. 이러면 s1이 스코프 밖으로 벗어나도 해제할 필요가 없어진다. 이는 새로운 변수가 같은 값을 가리킬때 기존 변수를 유효하지 않다고 간주한다는 점에서 얕은 복사와 차이가 발생한다. 따라서 러스트는 이를 이동(move)이라 한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7IaM7Jyg6raMKE93bmVyc2hpcCk=/img_2.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>변수와 데이터가 상호작용하는 방법: 클론</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i></i>&nbsp; &nbsp; 만약 데이터를 위와 같이 이동을 통해 스택 데이터만 복사하는 것이 아닌 힙 데이터까지 깊은 복사를 하고 싶다면 clone을 사용하면 된다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;s1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;s2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;s1.clone();</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;&nbsp;<i><b>변수와 데이터가 상호작용하는 방법: 복사</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i></i>&nbsp; &nbsp; &nbsp; 러스트는 정수형과 같이 스택에 저장할 수 있는 타입에 대해 달수 있는 Copy 트레잇이라 불리는 특별한 어노테이션을 가지고 있다. 만약 어떤 타입이 Copy 트레잇을 가지고 있으면 대입 과정 후에도 예전 변수를 계속 사용할 수 있다. 이런 Copy가 가능한 타입으로는 스칼라 타입과 스칼라 타입들의 묶음(스칼라들로만 이루어진 튜플)이 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>소유권과 함수</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i><b>&nbsp; &nbsp;&nbsp;</b></i>함수에게 변수를 넘기는 것은 이동을 사용한다. 따라서 인자로 변수를 넘기면 그 인자의 소유권은 호출한 함수로 이동한다. 함수가 값을 반환하면 그 값의 소유권은 반환값을 받는 함수로 이동한다. 복사가 되는 변수의 경우 '변수와 데이터가 상호작용하는 방법: 복사'에서 설명한 것과 같이 사용된다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>참조자(references)와 빌림(borrowing)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>만약 함수에게 값을 사용할 수 있도록 하되 소유권은 갖지 않도록 하고 싶다면 참조자를 사용하면 된다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;s1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;&amp;가&nbsp;참조자</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;len&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;calculate_length(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s1);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;println<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span>(<span style="color: #63a35c;">"{}"</span>,&nbsp;len);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;calculate_length(s:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>String)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #066de2;">usize</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;s.len()</span></div>
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
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 코드는 다음과 같은 구조를 가지고 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7IaM7Jyg6raMKE93bmVyc2hpcCk=/img_3.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 즉, 참조자는 소유권에 대한 참조만을 한다. 변수 s가 유효한 스코프의 범위는 일반 함수 파라미터의 스코프와 동일하지만 소유권을 갖고 있지 않기 때문에 참조자가 스코프 밖으로 벗어나도 참조자가 가리키는 값을 버리지 않는다. 또 한 실제 값 대신 참조자를 파라미터로 갖고 있는 함수는 소유권을 갖고 있지 않기 때문에 소유권을 되돌려주기 위해 값을 다시 반환할 필요도 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 빌린 것을 수정하려 한다면 에러가 발생한다. 이는 참조자 역시 불변이기 때문이다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;s1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;&amp;가&nbsp;참조자</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;change(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s1);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;change(s:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>String)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;error:&nbsp;cannot&nbsp;borrow&nbsp;immytable&nbsp;borrewed&nbsp;content&nbsp;`*s`&nbsp;as&nbsp;mutable</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;s.push_str(<span style="color: #63a35c;">",&nbsp;world"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>가변 참조자(mutable references)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>만약 참조자를 사용해 값을 바꾸고 싶다면 가변 참조자를 사용하면 된다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;<span style="color: #0086b3;">mut</span>&nbsp;s1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;&amp;가&nbsp;참조자</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;change(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #0086b3;">mut</span>&nbsp;s1);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;change(s:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #0086b3;">mut</span>&nbsp;String)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;error:&nbsp;cannot&nbsp;borrow&nbsp;immytable&nbsp;borrewed&nbsp;content&nbsp;`*s`&nbsp;as&nbsp;mutable</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;s.push_str(<span style="color: #63a35c;">",&nbsp;world"</span>);</span></div>
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
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하지만 가변 참조자는 특정 스코프 내에서 특정한 데이터 조각에 대해 가변 참조자를 오직 한번만 사용할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;<span style="color: #0086b3;">mut</span>&nbsp;s&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;error[E0499]:&nbsp;cannot&nbsp;borrow&nbsp;`s`&nbsp;as&nbsp;mutable&nbsp;more&nbsp;than&nbsp;once&nbsp;at&nbsp;a&nbsp;time</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;sr1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #0086b3;">mut</span>&nbsp;s;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;sr2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #0086b3;">mut</span>&nbsp;s;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이런 제약 사항은 러스트가 컴파일 타임에 데이터 레이스(data race)를 방지하게 해준다. 데이터 레이스틑 다음과 같은 동작이 발생했을 때 나타나는 특정한 레이스 조건이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 1. 두 개 이상의 포인터가 동시에 같은 데이터에 접근한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 2. 그 중 적어도 하나의 포인터가 데이터를 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 3. 데이터에 접ㅈ근하는데 동기화를 하는 어떠한 매커니즘도 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 가변 참조자와 불변 참조자를 혼용할 경우도 위와 비슷한 규칙이 적용된다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;<span style="color: #0086b3;">mut</span>&nbsp;s&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;sr1&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;s;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;sr2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;s;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;error[E0502]:&nbsp;cannot&nbsp;borrow&nbsp;`s`&nbsp;as&nbsp;mutable&nbsp;because&nbsp;it&nbsp;is&nbsp;also&nbsp;borrowed&nbsp;as&nbsp;immutable</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;sr3&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #0086b3;">mut</span>&nbsp;s;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 불변 참조자를 사용중일 때는 가변 참조자를 사용할 수 없다. 대신 데이터를 읽기만 하는 것은 다른 것들이 그 데이터를 읽는데에 어떤 영향도 주지 않기 때문에 여러개의 불변 참조자는 만들 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>댕글링 참조자(Dangling references)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>댕글링 포인터는 어떤 메모리를 가리키는 포인터를 보존하는 동안, 그 메모리를 해제해서 다른 개체에게 사용하도록 줄지도 모르는 메모리를 참조하고 있는 포인터를 의미한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 러스트에서는 컴파일러가 모든 참조자가 댕글링 참조자가 되지 않도록 보장해 준다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;reference_to_nothing&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;dangle();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;error[E0106]:&nbsp;missing&nbsp;lifetime&nbsp;specifier</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;dangle()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>String&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;s&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>슬라이스(Slices)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>슬라이스는 참조처럼 소유권을 갖지 않는다. 슬라이스는 컬렉션 전체가 아닌 컬렉션의 연속된 일련의 요소들을 참조할 수 있게 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스트링을 입력받아 해당 스트링의 첫번째 단어를 반환해야 한다고 해보자. 그리고 이 문제를 다음과 같은 코드로 해결해 보자.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;<span style="color: #0086b3;">mut</span>&nbsp;s&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello&nbsp;world"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;word&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;get_first_world(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;s.clear();&nbsp;<span style="color: #999999;">//&nbsp;String을&nbsp;빈&nbsp;문자열로&nbsp;만든다</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;word는&nbsp;5라는&nbsp;값을&nbsp;가지고&nbsp;있지만&nbsp;이&nbsp;값을&nbsp;의미있게&nbsp;사용할</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;스트링이&nbsp;존재하지&nbsp;않는다.</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;word는&nbsp;s의&nbsp;상태와&nbsp;연결되&nbsp;있지&nbsp;않다.</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;get_first_world(s:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>String)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #066de2;">usize</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;반복문&nbsp;순회를&nbsp;위해&nbsp;바이트&nbsp;배열로&nbsp;변환</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;bytes&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;s.as_bytes();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;iter()는&nbsp;컬랙션의&nbsp;각&nbsp;요소를&nbsp;반환</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;enumerate()는&nbsp;iter의&nbsp;결과값을&nbsp;직접&nbsp;반환하는&nbsp;대신</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;이를&nbsp;감싸서&nbsp;튜플의&nbsp;일부로&nbsp;만들어&nbsp;반환</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;튜플의&nbsp;첫&nbsp;요소는&nbsp;인덱스,&nbsp;두번째는&nbsp;요소에&nbsp;대한&nbsp;참조값</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(i,&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>item)&nbsp;in&nbsp;bytes.iter().enumerate()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;바이트&nbsp;리터럴&nbsp;문법을&nbsp;활용해&nbsp;공백&nbsp;문자를&nbsp;찾는다.</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;item&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;b<span style="color: #63a35c;">'&nbsp;'</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;i;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;s.len()</span></div>
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
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 코드는 word와 s의 상태가 연결되 있지 않기 때문에 버그가 발생할 수 있다. 이 문제를 해결하기 위해서 스트링 슬라이스를 사용하면 된다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>스트링 슬라이스</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>스트링 슬라이스는 String의 일부분에 대한 참조자이다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;s2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello&nbsp;world"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;hello&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s[<span style="color: #0099cc;">0.</span>.<span style="color: #0099cc;">5</span>];&nbsp;<span style="color: #999999;">//&nbsp;"hello"</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 대괄호 내에는 [시작 인덱스..끝인덱스 + 1]를 통해 범위를 특정할 수 있다. 내부적으로는 시작 위치와 슬라이스의 길이를 저장한다. 따라서 let world = &amp;s[6..11]이면 다음과 같은 구조를 갖는다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7IaM7Jyg6raMKE93bmVyc2hpcCk=/img_4.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 시작을 문자열의 처음, 끝을 문자열의 마지막으로 정한다면 각각 처음과 끝의 인덱스를 생략할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;hello&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s[..<span style="color: #0099cc;">5</span>];&nbsp;<span style="color: #999999;">//&nbsp;처음부터</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;hello&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s[<span style="color: #0099cc;">2.</span>.];&nbsp;<span style="color: #999999;">//&nbsp;인덱스&nbsp;2부터&nbsp;끝까지</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이를 활용해 get_first_world의 코드를 수정하면 빌림 규칙으로 인해 에러가 발생하게 된다. 빌림 규칙때문에 불변 참조자를 만들면 가변 참조자를 만들지 못한다. clear 함수가 String을 수정할때 이 함수는 가변 참조자를 가지려 하고 실패하게 된다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;<span style="color: #0086b3;">mut</span>&nbsp;s&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;String::from(<span style="color: #63a35c;">"hello&nbsp;world"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;word&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;get_first_world(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;s.clear();&nbsp;<span style="color: #999999;">//&nbsp;Error</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;&amp;str은&nbsp;스트링&nbsp;슬라이스를&nbsp;나타내는&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">fn</span>&nbsp;get_first_world(s:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>String)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>str&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">let</span>&nbsp;bytes&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;s.as_bytes();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">for</span>&nbsp;(i,&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>item)&nbsp;in&nbsp;bytes.iter().enumerate()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;바이트&nbsp;리터럴&nbsp;문법을&nbsp;활용해&nbsp;공백&nbsp;문자를&nbsp;찾는다.</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;item&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;b<span style="color: #63a35c;">'&nbsp;'</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s[<span style="color: #0099cc;">0.</span>.i];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>s[..]</span></div>
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
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>스트링 리터럴은 슬라이스이다.</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>스트링 리터럴은 바이너리 안에 저장된다. 따라서 스트링 리터럴의 타입은 &amp;str이다. &amp;str은 불변 참조자 이므로 스트링 리터럴은 불변이다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>배열의 슬라이스</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 배열의 슬라이스 역시 스트링 슬라이스와 같이 동작한다. 아래의 예제의 경우 슬라이스는 &amp;[i32] 타입을 갖는다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;a&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;[<span style="color: #0099cc;">1</span>,&nbsp;<span style="color: #0099cc;">2</span>,&nbsp;<span style="color: #0099cc;">3</span>,&nbsp;<span style="color: #0099cc;">4</span>];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">let</span>&nbsp;slice&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>a[<span style="color: #0099cc;">1.</span>.<span style="color: #0099cc;">3</span>];</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
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