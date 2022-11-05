---
layout:       post
title:        "JavaScript에서의 객체"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- javascript
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
                            <p data-ke-size="size16">&nbsp; js의 객체를 형식적으로 정의 하면 프로퍼티의 집합이다. 프로퍼티는 name: value쌍으로 나타내어진다. 프로퍼티의 값에는 어떤 타입이라도 정의가 가능하다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 객체지향 프로그래밍의 흐름은 특징의 공통성(타입)보다는 인스턴스 간의 협조에 초점을 맞춘다. 즉, 메시지를 주고받는 객체이다. 메시지를 받는 객체는 전달된 메시지에 반응한다. 메시지를 구현 차원으로 떨어뜨리면 메서드 호출로, 메시지에 대한 반응은 메서드 안에서 처리를 나누게 된다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; js에서의 객체지향에서는 객체간의 협조(메시지 전달)는 프로퍼티 접근이다. 객체간의 공통성은 같은 객체에서 성질을 계승하는 형태로 구현된다. js에서는 이를 프로토타입 기반으로 구현한다.</p>
<p data-ke-size="size16"><b>객체 리터럴</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>Js에서 객체 리터럴은 객체를 생성하는 한가지 방법이다. 객체 리터럴을 활용하는 것이 new연산 보다 좀 더 js다운 코드이다. 객체 리터럴을 사용하는 순간은 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 싱글턴 패턴</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 다중 데이터로서의 용도(함수 인자 또는 반환값)</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 객체 생성을 의도한 생성자를 대신하는 함수</p>
<p data-ke-size="size16"><b>생성자와 new식</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>new식의 평가는 다음과 같이 이루어 진다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 내부적으로 특별한 특징을 갖지 않는 빈 객체를 생성한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 다음으로 new 식으로 지정한 생성자를 호출한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 생성된 객체는 생성자 안의 this참조에서 참조된다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. 생성자를 실행하고 최종적으로 new식의 평가값으로 객체의 참조가 반환된다.</p>
<p data-ke-size="size16">&nbsp; 생성자를 사용하면 생성자는 암묵적으로 마지막에 return this;가 있는거 처럼 동작한다. 이때 명시적으로 return을 했을때 만약 객체를 반환한다면 생성한 객체와는 관련 없는 return문 뒤에 있는 객체가 반환된다. 만약 primitive value를 반환한다면 해당 return은 무시되며 return this;가 동작된다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Js에서는&nbsp;일반&nbsp;함수를&nbsp;생성자로&nbsp;사용할&nbsp;수&nbsp;있다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass1(x)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass2(x)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{y:&nbsp;<span style="color: #0099cc;">3</span>};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyCLass3(x)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #0099cc;">4</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyClass1(<span style="color: #0099cc;">1</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyClass2(<span style="color: #0099cc;">2</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj3&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyCLass3(<span style="color: #0099cc;">3</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj);&nbsp;<span style="color: #999999;">//MyClass1&nbsp;{x:&nbsp;1,&nbsp;constructor:&nbsp;Object}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj2);&nbsp;<span style="color: #999999;">//&nbsp;{y:&nbsp;3}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj3);&nbsp;<span style="color: #999999;">//MyClass3&nbsp;{x:&nbsp;3,&nbsp;constructor:&nbsp;Object}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 물론 ES6부터는 class를 통해 클래스를 정의할 수 있지만 다음과 같이 함수로도 가능하다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass&nbsp;(x)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//필드</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//메서드</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.print&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">function</span>()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #066de2;">this</span>.x);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 하지만 위와 같이 사용을 하면 다음과 같은 단점이 존재한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 모든 인스턴스가 같은 메서드 정의의 실체의 복사본을 가지므로 메모리 효율과 실행 효율이 좋지 않다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 프로퍼티 값의 접근 제어를 할 수 없다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>프로퍼티 접근</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>프로퍼티 접근은 '.'연산자 또는 '[]'연산자로 접근이 가능하다. 이때 '.'연산자를 통해 프로퍼티 명을 접근하면 프로퍼티 명을 식별자로 다루고, '[]'연산자를 사용하면 문자열 식으로 평가 된다. 또 한 프로퍼티 접근의 연산 대상은 변수가 아닌 객체 참조이다.</p>
<p data-ke-size="size16">&nbsp; 객체의 프로퍼티에 접근할 때 둘 중 어느연산자를 사용해야 된다는 것은 정해져 있지 않다. 하지만 점 연산자가 조금 더 간결하므로 점 연산자가 더 선호된다. 이때 점 연선자로 쓸 수 있는 패턴은 괄호 연산자로도 쓸 수 있지만 그 반대는 성립하지 않으므로 이럴 경우에는 괄요 연산자를 사용해야 한다.</p>
<p data-ke-size="size16">&nbsp; 다음은 반드시 괄호 연산자를 사용해야 하는 경우이다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 식별자로 사용할 수 없는 프로퍼티명을 사용하는 경우(숫자나 하이픈을 포함하는 문자열은 식별자로 사용할 수 없다.)</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 변수의 값을 프로퍼티명에 사용하는 경우</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 식의 평가 결과를 프로퍼티명에 사용하는 경우</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>연관 배열</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>배열의 키는 연속하는 숫자 이므로 순서가 있는 값의 모음이다. 숫자에 한정되 있지 않고 임의의 타입인 키를 허용해 키와 값의 모음을 다루는 데이터 구조를 연관 배열이라 한다. 연관 배열은 다른 언어에서 맵, 딕셔너리 등으로 불린다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 연관 배열의 주된 용도는 키로 값을 뽑아내는 것이다. js에서는 객체를 연관 배열로 사용하는 것이 정석이다.</p>
<p data-ke-size="size16">&nbsp; 연관 배열에서 프로퍼티 삭제</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;map&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{x:&nbsp;<span style="color: #0099cc;">3</span>,&nbsp;y:&nbsp;<span style="color: #0099cc;">4</span>};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(map.x);&nbsp;<span style="color: #999999;">//3</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">delete</span>&nbsp;map.x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(map.x);&nbsp;<span style="color: #999999;">//undefined</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 여기서 주의해야 할 것은 delete이다. Js에서의 delete는 C++의 delete와 같이 참조할 객체의 메모리를 해제를 의미하지 않는다. Js에서의 delete는 객체에서 프로퍼티를 제거하는 것뿐이다. 즉, 키를 제거해서 대응하는 값이 키와의 대응 관계가 끊기는거다. 그 결과 참조되지 않게된 객체가 gc로 인해 사라질 수 도 있지만 이는 delete연산의 직접적인 작용은 아니다.</p>
<p data-ke-size="size16">&nbsp; 존재하지 않는 요소에 접근했을 때 결과 타입은 undefined이다. 하지만 undefined는 명시적으로도 할당이 가능하기 때문에 키의 존재 여부를 확인할 때 undefined와 항등 연산을 하는 것은 적절하지 않다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>연관 배열로서의 객체와 관련된 주의점</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>연관 배열로서의 객체는 프로토타입 상속과 관련해 주의할 점이 존재한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 1. 프로토타입 상속한 프로퍼티는 delete할 수 없다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp;2. 객체를 연관 배열로 생성할 때 리터럴로 생성하는 것이 일반적이다. 이때 요소가 없는 연관 배열을 만들려고 빈 객체 리터럴을 사용&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;해&nbsp; 도 실제로는 Object클래스에서 프로퍼티를 프로토타입 상속하고 있기 때문에 주의해야 한다. 프로퍼티가 존재하는 지는 in연산&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 을 통해 확인할 수 있다. for in문을 사용하면 프로토타입 상속한 프로퍼티까지 검사하게 된다. 만약 상속받은 프로퍼티가 아닌 자신&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 만&nbsp; 의 프로퍼티인지를 검사하고 싶다면 hasOwnProperty()를 사용하면 된다.</p>
<p data-ke-size="size16"><b>프로퍼티의 속성</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>프로퍼티에는 속성(attribute)가 존재 한다. ECMAScript에서는 프로퍼티 값을 '값속성'이라는 속성 중 하나를 사용해 나타낸다. 따라서 프로퍼티는 이름(프로퍼티명)과 여러 속성의 모음이 된다.</p>
<p data-ke-size="size16">&nbsp; ES5기준 다음과 같은 프로퍼티의 속성이 존재 한다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">속성명</td>
<td style="width: 50%;">의미</td>
</tr>
<tr>
<td style="width: 50%;">writeable</td>
<td style="width: 50%;">프로퍼티 값의 덮어쓰기 기능</td>
</tr>
<tr>
<td style="width: 50%;">enumerable</td>
<td style="width: 50%;">for in 문에서 열거 가능</td>
</tr>
<tr>
<td style="width: 50%;">configurable</td>
<td style="width: 50%;">속성을 변경 가능, 프로퍼티의 제거 가능</td>
</tr>
<tr>
<td style="width: 50%;">get</td>
<td style="width: 50%;">프로퍼티 값의 접근자 함수를 지정 가능</td>
</tr>
<tr>
<td style="width: 50%;">set</td>
<td style="width: 50%;">프로퍼티 값의 설정자 함수를 지정 가능</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><b>메모리 누수</b></p>
<p data-ke-size="size16"><b>&nbsp;</b>js에서는 gc가 존재하기 때문에 일반적인 경우라면 메모리 누수가 발생하지 않지만 메모리 누수가 발생하는 경우도 존재 한다. 순환 참조에서 일어나는 메모리 누수가 그 예시이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>불변 객체</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>불변 객체를 사용하면 버그를 줄일 수 있다. 예를 들어 메서드 안에서 인자로 전달된 객체의 내용을 의도치 않게 바꿀때, 이 객체가 불변이면 버그가 발생할 확률이 줄어든다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>불변객체의 기법</b></i></p>
<p data-ke-size="size16"><i>&nbsp; &nbsp;</i>Js객체를 불변 객체로 만드는 방법은 다음과 같다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 프로퍼티(상태)를 숨기고,, 변경 조작 수단을 제공하지 않는다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. ES5에서 제공하는 일부 함수를 활용한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. Writeable 속성, Configurable속성, 설정자 함수, 접근자 함수를 활용한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; JS에서는 객체의 메서드 또는 상태를 명시적으로 숨길 수 있는 접근 제어자가 존재하지 않는다.</p>
<p data-ke-size="size16">&nbsp; 다음과 같은 함수를 사용해 불변 객체를 만들 수 있다</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 20%;">메서드명</td>
<td style="width: 20%;">프로퍼티 추가</td>
<td style="width: 20%;">프로퍼티 제거</td>
<td style="width: 20%;">프로퍼티 값 변경</td>
<td style="width: 10%;">확인 메서드</td>
<td style="width: 10%;">프로퍼티 속성</td>
</tr>
<tr>
<td style="width: 20%;">preventExtensions</td>
<td style="width: 20%;">X</td>
<td style="width: 20%;">O</td>
<td style="width: 20%;">O</td>
<td style="width: 10%;">Object.isExtensible</td>
<td style="width: 10%;">&nbsp;</td>
</tr>
<tr>
<td style="width: 20%;">seal</td>
<td style="width: 20%;">X</td>
<td style="width: 20%;">X</td>
<td style="width: 20%;">O</td>
<td style="width: 10%;">Object.isSealed</td>
<td style="width: 10%;">configurable: false</td>
</tr>
<tr>
<td style="width: 20%;">freeze</td>
<td style="width: 20%;">X</td>
<td style="width: 20%;">X</td>
<td style="width: 20%;">X</td>
<td style="width: 10%;">Object.isFrozen</td>
<td style="width: 10%;">writable: false</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 위 메서드를 사용할때는 다음과 같은 점을 주의해야 한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 1. 한번 변경하면 원래대로 돌아갈 수 없다</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;2. 프로토타입 상속원도 불변적으로 만들고 싶다면 상속원에 대해서도 명시적으로 지정할 필요가 있다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>메서드</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>JS언어 사양에서 메서드는 존재하지 않는다. 다만 편의상 프로퍼티에 함수를 설정한 것을 메서드라 부른다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>this참조 규칙</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>탑 레벨 코드에서는 this는 전역 객체를 참조한다. 하지만 함수 안에서는 어떤 방식으로 함수를 호출하냐에 따라 this의 참조할 객체가 달라 진다.</p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">함수 호출 방법</td>
<td style="width: 50%;">this 참조의 참조하는 객체</td>
</tr>
<tr>
<td style="width: 50%;">생성자 호출</td>
<td style="width: 50%;">생성한 객체</td>
</tr>
<tr>
<td style="width: 50%;">메서드 호출</td>
<td style="width: 50%;">리시버 객체<br>&nbsp; - 점 연산 또는 대괄호 연산에서 객체의 메서드를 호출했을 때 연산자의 좌변에 지정한 객체</td>
</tr>
<tr>
<td style="width: 50%;">apply 또는 call 호출</td>
<td style="width: 50%;">apply 또는 call의 인자로 지정한 객체</td>
</tr>
<tr>
<td style="width: 50%;">그 외의 호출</td>
<td style="width: 50%;">전역 객체</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; &nbsp; 자바같은 클래스 기반 언어에서는 메서드 안의 this가 참조하는 리시버 객체는 항상 해당 클래스의 인스턴스이다. 하지만 js에서는 그와 같은 동작을 보장하지 않는다. JS의 this참조가 참조할 곳은 메서드의 호출 방법에 따라 달라진다. 리시버 개체가 없거나 다른 리시버 객체를 통해 같은 함수를 호출하면 동작 방식이 바뀐다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;x:&nbsp;<span style="color: #0099cc;">3</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;doit:&nbsp;<span style="color: #a71d5d;">function</span>()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #63a35c;">'method&nbsp;is&nbsp;called'</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #066de2;">this</span>.x);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">obj.doit();<span style="color: #999999;">//method&nbsp;is&nbsp;called&nbsp;3</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//obj.doti이&nbsp;참조하는&nbsp;함수&nbsp;객체를&nbsp;전역&nbsp;함수&nbsp;fn에&nbsp;대입</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;fn&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;obj.doit;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//함수&nbsp;안의&nbsp;this참조는&nbsp;전역&nbsp;객체를&nbsp;참조</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">fn();<span style="color: #999999;">//method&nbsp;is&nbsp;called&nbsp;undefined</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//this&nbsp;참조가&nbsp;전역&nbsp;객체를&nbsp;참조하고&nbsp;있는지&nbsp;확인</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">5</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">fn();<span style="color: #999999;">//method&nbsp;is&nbsp;called&nbsp;5</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//다른&nbsp;객체&nbsp;obj2의&nbsp;프로퍼티에&nbsp;obj의&nbsp;메서드(함수&nbsp;객체의&nbsp;참조)를&nbsp;대압</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//메서드&nbsp;안의&nbsp;this&nbsp;참조는&nbsp;객체&nbsp;objs를&nbsp;참조</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;x:&nbsp;<span style="color: #0099cc;">4</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;doti2:&nbsp;fn</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">obj2.doti2();<span style="color: #999999;">//method&nbsp;is&nbsp;called&nbsp;4</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><i>&nbsp; 메서드 안에서 다른 메서드를 호출하는 경우&nbsp;</i></p>
<p data-ke-size="size16"><i>&nbsp; &nbsp;&nbsp;</i>자바나 C++에서는 메서드 안에서 다른 메서드를 호출할 떄 this를 생략한다. 하지만 js에서는 메서드 안에서 별도의 메서드를 호출하려면 this를 참조해야 한다. 만약 this를 사용하지 않으면, 함수가 중첩될 경우 바깥 쪽 스코프를 향해 이름을 찾는다.</p>
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
<div style="line-height: 130%;">13</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;x:&nbsp;<span style="color: #0099cc;">3</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;doit:&nbsp;<span style="color: #a71d5d;">function</span>()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #63a35c;">'doit&nbsp;'</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #066de2;">this</span>.x);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">this</span>.doit2();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;doit2:&nbsp;<span style="color: #a71d5d;">function</span>()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #63a35c;">'doit2&nbsp;'</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #066de2;">this</span>.x);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">obj.doit();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//doit&nbsp;3</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//doit2&nbsp;3</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp;&nbsp;<i>apply와 call</i></p>
<p data-ke-size="size16"><i>&nbsp; &nbsp; &nbsp;&nbsp;</i>함수 객체에는 apply와 call이라는 메서드가 존재 하고, 이것들을 이용하면 호출한 함수 안의 this참조를 지정한 임의의 객체를 참조해 사용할 수 있다. 즉, 리시버 객체를 명시적으로 지정할 수 있다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;f()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #066de2;">this</span>.x);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;x:&nbsp;<span style="color: #0099cc;">4</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">f.apply(obj);&nbsp;<span style="color: #999999;">//this는&nbsp;obj를&nbsp;참조</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">f.call(obj);&nbsp;<span style="color: #999999;">//this는&nbsp;obj를&nbsp;참조</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//둘&nbsp;다&nbsp;4&nbsp;출력</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;x:&nbsp;<span style="color: #0099cc;">3</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;doit:&nbsp;<span style="color: #a71d5d;">function</span>()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #63a35c;">'method&nbsp;is&nbsp;called&nbsp;'</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #066de2;">this</span>.x);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">var</span>&nbsp;obj2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;x:&nbsp;<span style="color: #0099cc;">4</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//메서드&nbsp;obj.doti을&nbsp;apply로&nbsp;호출한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//메서드&nbsp;안의&nbsp;this&nbsp;참조는&nbsp;객체&nbsp;obj2를&nbsp;참조한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">obj.doit.apply(obj2);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//method&nbsp;is&nbsp;called&nbsp;4</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; apply, call을 사용하면 모두 첫번쨰 인자에 전달한 객체를 this가 참조한다. apply와 call의 차이는 첫번쨰 인자 외에 인자를 전달하는 방식에 있다. apply는 남은 인자를 메서드에 배열로 넘기고 call은 인자 형식 그대로 넘긴다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>프로토타입 상속</b></p>
<p data-ke-size="size16">&nbsp; 프로토타입 상속을 이용하는 것과 이용하지 않는 것의 문법상 차이는 다음과 같다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//클래스&nbsp;정의</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass(x,&nbsp;y)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.y&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;y;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.show&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">function</span>()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #066de2;">this</span>.x,&nbsp;<span style="color: #066de2;">this</span>.y);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//프로토타입&nbsp;상속을&nbsp;이용한&nbsp;클래스&nbsp;정의</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass(x,&nbsp;y)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;x;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.y&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;y;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyClass.<span style="color: #066de2;">prototype</span>.show&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">function</span>(){</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">console</span>.log(<span style="color: #066de2;">this</span>.x,&nbsp;<span style="color: #066de2;">this</span>.y);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위 예제에서 두 클래스의 차이는 메서드 정의가 인스턴스 객체의 직접 프로퍼티냐 아니냐이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp;<i><b>프로토타입 기반 언어</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>JS는 프로토타입 기반 언어이다. 즉, 모든 객체들이 메서드와 속성들을 상속 받기 위한 템플릿으로 프로토타입 객체를 가진다. 프로토타입 객체는 또 다시 상위 프로토타입 객체에서 메서드와 속성을 상속받을 수 있다. 이를 프로토타입 체인이라 부른다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;&nbsp;<i><b>프로토타입 체인</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp; &nbsp;&nbsp;</b></i>프로토 타입 상속은 프로토타입 체인을 사용한다. 프로토타입 체인은 다른 객체에서 정의된 메서드와 속성을 한 객체에서 사용하게 하는 근간이다. 정확히 말하면 상속되는 속성과 메서드들은 각 객체가 아니라 객체의 생성자의 proptype이라는 속성에 정의되 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 객체의 prototype(Object.getPrototypeOf(obj) 또는 deprecated된 __proto__속성으로 접근가능한것)과 생성자의 prototype속성은 차이가 존재한다. 객체의 prototype은 개별 객체의 속성이고 생성자의 prototype은 생성자의 속성이다. 즉,Object.getPrototypeOf(new Foobar())의 반환값이 Foobar.prototype과 동일하다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;v&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;[<span style="color: #0099cc;">1</span>,&nbsp;<span style="color: #0099cc;">2</span>];</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//개별&nbsp;객체의&nbsp;속성</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(<span style="color: #066de2;">Object</span>.getPrototypeOf(v));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//생성자의&nbsp;속성</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(<span style="color: #066de2;">Array</span>.<span style="color: #066de2;">prototype</span>);</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 프로토타입 체인을 사용하는 전제는 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 1. 모든 함수(객체)는 prototype이라는 이름의 프로퍼티를 갖는다(prototype 프로퍼티를 참조하는 객체를 prototype 객체라 하자)</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 2.&nbsp; 모든 객체는 객체 생성에 사용한 생성자(함수 객체)의 prototype 객체로 연결되는 (숨은)링크를 갖는다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; ECMAScript 명세에서는 prototype 프로퍼티를 명시적인 프로토타입 프로퍼티(explicit prototype property), 숨은 링크를 암묵적인 프로토타입 링크(implicit prototype link)라 부른다. 여기서는 전자를 프로토타입 참조, 후자를 암묵적인 링크라고 하자.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 객체의 프로토타입 체인의 동작 방식은 다음과 같은 순서로 이루어 진다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 1. 객체 자신의 프로퍼티</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 2. 암묵적인 링크의 참조 객체(생성자의 protorype 객체)의 프로퍼티</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 3. 2의 객체의 암묵적인 링크에 대한 참조 객체의 프로퍼티</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 4. 3의 동작을 탐색이 끝날때 까지 반복 한다(끝은 Object.prototype객체)</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 프로토타입 체인 이라는 용어를 제외하면 결국에는 암묵적인 링크의 프로퍼티의 상속이다. 암묵적인 링크의 참조할 객체는 생성자의 prorotype 객체이므로 이 글의 프로토입 예제 중 맨 위에 있는 예제외 연결된다. 객체 리터럴로 생성한 객체의 암묵적인 링크는 Object.property를 참조한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;&nbsp;<i><b>객체 프로퍼티 쓰기</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;</b></i>객체프로퍼티의 쓰기는 오직 자신의 프로퍼티에 대해서만 가능하다. 만약 객체 프로퍼티 쓰기에서도 읽기와 같이 프로퍼티 체인이 있다고 가정해 보자. 만약 어떤 객체가 Object.toString()에 대해 쓰기를 한다면 모든 객체는 Object.property에 대한 암묵적 링크를 가지므로 다른 객체에 까지 영향을 주게 된다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;하지만 읽기에 경우 어떤 암묵적인 링크의 toString메서드를 덮어 쓰면 해당 객체를 프로토타입 상속 받은 객체도 그 구현을 사용할 수 있다. 이는 구현의 상속이라는 OOP개념에 적절하다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;암묵적인 링크의 참조할 객체를 프로토타입 객체라 한다. 즉, 프로퍼티를 읽을 때 프로토타입 객체의 프로퍼티를 상속한다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>프로토타입 체인의 예</b></i></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'x'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;myClass&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyClass();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(myClass.x);<span style="color: #999999;">//x</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(myClass.y);<span style="color: #999999;">//undefined</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyClass.<span style="color: #066de2;">prototype</span>.y&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'y'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(myClass.y);<span style="color: #999999;">//y</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;MyClass()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">this</span>.x&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">"x"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">MyClass.<span style="color: #066de2;">prototype</span>.y&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">"y"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyClass();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj.y);&nbsp;<span style="color: #999999;">//&nbsp;y</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">obj.y&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">"z"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj.y);&nbsp;<span style="color: #999999;">//z</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;obj2&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;MyClass();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//쓰기는&nbsp;프로토타입&nbsp;체인을&nbsp;따르지&nbsp;않는다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj2.y);&nbsp;<span style="color: #999999;">//y</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">delete</span>&nbsp;obj.y;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//직접&nbsp;프로퍼티가&nbsp;없어지면&nbsp;프로토타입&nbsp;체인을&nbsp;따른다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj.y);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(<span style="color: #a71d5d;">delete</span>&nbsp;obj.y);&nbsp;<span style="color: #999999;">//true</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj.y);&nbsp;<span style="color: #999999;">//프로토타입&nbsp;체인&nbsp;앞의&nbsp;프로퍼티는&nbsp;delete&nbsp;할&nbsp;수&nbsp;없다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><b>객체와 타입</b></p>
<p data-ke-size="size16">&nbsp; 클래스 기반의 언어의 경우 객체의 타입은 모형이 되는 클래스 또는 구현 인터페이스로 결정된다. 하지만 JS의 경우 클래스도, 인터페이스도 존재하지 않기 때문에 이 관점에서의 JS는 타입이 존재하지 않는다. 하지만 좀 더 본질에 다가가서 타임을 객체 특징의 공통성으로 바라본다면 JS의 타입에도 객체가 존재 한다.</p>
<p data-ke-size="size16">&nbsp; JS에서는 typeof 연산자를 통해 타입을 확인할 수 있는데 객체에다가 이것을 사용하면 'object'라는 문자열이 반환된다. 따라서 JS에서 객체를 더 세분화 하는 구조는 없다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>객체 타입 판정</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>1. contructor 프로퍼티: 객체의 생성자 확인</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 주의점: contructor 프로퍼티는 객체에 직접 포함된 프로퍼티가 아닌 프로토타입 체인에서 찾은 프로퍼티이다.&nbsp;</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;Foo()&nbsp;{}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;Bar()&nbsp;{}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">Foo.<span style="color: #066de2;">prototype</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Bar();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;obj&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;Foo();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">console</span>.log(obj.constructor);<span style="color: #999999;">//obj의&nbsp;contructor&nbsp;프로퍼티는&nbsp;Base를&nbsp;참조</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//출력:&nbsp;f&nbsp;Bar(){}&nbsp;</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 2. instanceof, isPortotypeOf</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 3. duck typing</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 클래스, 인스턴스와 객체는 정적인 관계이기 때문에 instanceof 연산으로도 객체의 타입을 완벽히 판정할 수 있다. 하지만 JS는 동적이기 때문에 마음대로 프로퍼티를 추가하거나 생성자 없이 객체를 생성할 수 있다. 이렇게 추가된 프로퍼티는 contructor나 instanceof로 판별할 수 없다. 이럴때는 해당 객체에 어떤 프로퍼티가 있는지를 판정해야 하는데 이때 사용하는 기법이 duck typing이다. duck typing으로 사용되는 것 중 하나는 in연산이다. in 좌변에는 프로퍼티명 스트링, 우변에는 객체 참조를 지정한다. 만약 해당 프로퍼티가 우변 참조객체에 있으면 참을 반환한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>전역 객체</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>객체에는 본질적으로 이름이 없다. Object 객체 역시 마찬가지다. 단지 Object라는 이름으로 접근이 가능할 뿐이다. 전역 객체의 경우, JS의 언어 사양으로는 정해진 이름이 없다. 따라서 window객체 역시 클라이언트 사이드에서 전역 객체를 참조하는 window라는 변수가 처음부터 존재한거다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>전역 객체와 전역 변수</b></i></p>
<p data-ke-size="size16"><i></i>&nbsp; &nbsp; 전역 변수와 전역 함수는 전역 객체의 프로퍼티이다. 따라서 Object 역시 전역 객체의 프로퍼티이다. js의 타입명은 전부 프로퍼티명으로 원래 타입명이라는 개념은 없다. 전역 객체가 어떤 프로퍼티를 가지는 지는 실행 환경에 따라 달라진다.</p>
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