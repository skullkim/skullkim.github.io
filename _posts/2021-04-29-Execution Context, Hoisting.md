---
layout:       post
title:        "Execution Context, Hoisting"
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
                            <p><b>Execution Context</b></p>
<p>&nbsp;lexical environment는 어디서 어떻게 코드를 작성하는 지를 판단한다.&nbsp;</p>
<pre id="code_1619689408333" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>function doSomething(){
  var age = 7;
 }</code></pre>
<p>&nbsp; 위 코드에서 age는 어휘면에서(lexically) doSomething()이라는 함수 안에 존재한다. 통상적으로 코드에는 한개 이상의 lexical environment가 존재하지만 모든 lexical environment가 한번에 실행되지 않는다.</p>
<p>&nbsp; 코드가 실행되는 것을 도와주는 환경을 Execution Context라 한다. 이것은 현재 실행중인 코드와 그 코드가 실행되기 위해 도움을 주는 모든것들을 의미한다. Lexical environment는 여러개가 존재할 수 있지만 Execution Context는 오직 현재 실행중인 하나의 코드에만 신경을 쓴다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RXhlY3V0aW9uIENvbnRleHQsIEhvaXN0aW5n/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>Execution Context에서는 코드를 한 줄씩 실행가능한 바이트 코드로 파싱하고 메모리를 할당하고 실행한다.</p>
<p>다음 코드가 실행된다고 가정해 보자&nbsp;</p>
<pre id="code_1619690020756" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>var age = 7;</code></pre>
<p>위 코드는 다음과 같은 과정을 거쳐서 실행이 된다</p>
<p>1. Tokenizing:</p>
<p>&nbsp; 이 과정에서 코드는 의미를 가진 Tokens라는 조각으로 나눠진다. 위 코드의 경우 var, age, =, 7, ; 로 나눠진다.</p>
<p>2. Parsing:</p>
<p>&nbsp; 이 과정에서 위의 Tokens 배열은 해당 원소로 이뤄진, 언어의 문법으로 이해할 수 있는 트리로 변환되며 이 트리를 AST(Abstract Syntax Tree)라 한다.</p>
<p>3. Code Generation:</p>
<p>&nbsp; 위에서 만들어진 AST는 실행 가능한 바이트코드로 변환되며 이 실행가능한 바이트 코드는 JIT 컴파일러에 의해 최적화 된다.</p>
<p>따라서 Execution Context는 코드의 특정 부분이 실행되는 환경이다.</p>
<p>&nbsp;</p>
<p>Execution Context는 두개의 종류가 있다</p>
<p>&nbsp; 1. Global Execution Context(GEC)</p>
<p>&nbsp; 2. Function Execution Context(FEC)</p>
<p>그리고 위의 두 종류는 각각 다음과 같은 두개의 Phase를 가지고 있다</p>
<p>&nbsp; 1. Creation Phase</p>
<p>&nbsp; 2. Execution Phase</p>
<p>&nbsp;</p>
<p><b>GEC(Global Execution Context)</b></p>
<p>&nbsp; js코드를 실행할때면 js코드는 GEC를 생성한다.</p>
<p>&nbsp; 1. Creation Phase</p>
<p>&nbsp; &nbsp; Creation Phase에서는 두개의 유니크한 것이 생성된다.</p>
<p>&nbsp; &nbsp; &nbsp; -window object</p>
<p>&nbsp; &nbsp; &nbsp; -this</p>
<p>&nbsp; &nbsp; 변수: 변수가 존재 한다면 변수를 위해 메모리가 할당된다. 이 변수들은 undefined로 초기화 된다.</p>
<p>&nbsp; &nbsp; 함수: 함수가 존재한다면 메모리에 할당한다</p>
<p>&nbsp; 2. Execution Phase</p>
<p>&nbsp; &nbsp; &nbsp;여기서 코드의 실행이 시작된다. 전역 변수에 값이 할당된다.&nbsp;</p>
<p>예시:</p>
<p>&nbsp; HTML파일을 하나 만들고 그 파일에 빈 js파일을 import하자</p>
<p>그 후 개발자도구에서&nbsp;</p>
<p>window를 입력하면 다음과 같이 나온다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RXhlY3V0aW9uIENvbnRleHQsIEhvaXN0aW5n/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>this를 입력하면 다음과 같이 나온다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RXhlY3V0aW9uIENvbnRleHQsIEhvaXN0aW5n/img_2.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>window === this를 하면 True가 반환된다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RXhlY3V0aW9uIENvbnRleHQsIEhvaXN0aW5n/img_3.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>따라서 다음과 같은 결과를 얻을 수 있다.</p>
<p>&nbsp; 1. Glocal Execution Context는 js파일을 로딩할때 생성되면 js파일의 empty여부과 관련이 없다</p>
<p>&nbsp; 2. Creation phase에서 window객체와 this가 생성된다</p>
<p>&nbsp; 3. Global Execution Context에서는 window와 this가 같다</p>
<p>&nbsp; 4. js 파일이 비어있으므로 Execution phase에서는 아무일도 일어나지 않았다.</p>
<p>예시:</p>
<p>만약 위의 예시에서 생성된 js파일이 다음과 같은 코드를 갖는다면</p>
<pre id="code_1619691778846" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>var b = "a";
function log(){
    console.log(b);
}</code></pre>
<p>creation phase에서</p>
<p>&nbsp; 1. 전역 객체 window와 this가 생성된다</p>
<p>&nbsp; 2. 변수 b와 함수 log()를 메모리에 할당한다</p>
<p>&nbsp; 3. b에 undefined가 할당된다. log()함수가 메모리에 직접 배치된다.</p>
<p>&nbsp;에서</p>
<p>&nbsp; 1. b에 a가 할당된다</p>
<p>&nbsp; 2. 함수를 정의는 했지만 호출하지 않았으므로 function execution이 실행되지 않는다.</p>
<p>&nbsp;</p>
<p><b>FEC(function execution context)</b></p>
<p>&nbsp; 함수를 호출하면 FEC가 생성된다. FEC도 GEC와 마찬가지로 creation와 execution phase를 거친다.&nbsp;</p>
<p>&nbsp; FEC는 arguments라는 변수에 엑세스하는데 이 변수는 함수도 전달되는 인자들이다. 이때도 window객체와 this는 접근 가능하다. 만약 함수다 또 다른 함술 호출한다면 새로운 FEC를 생성한다. 하나의 함수는 하나의 FEC를 가지며 FEC는 각 함수에서 사용되는 변수들의 scope를 결정한다.</p>
<p>&nbsp;</p>
<p><b>Hoisting</b></p>
<p><i><b>Variable hostring</b></i></p>
<p>. 다음과 같은 코드가 있다고 해보자</p>
<pre id="code_1619798409923" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>console.log(name);
var name;</code></pre>
<p>이 코드의 출력은 undefined이다</p>
<p>만약 다른 언어로 위와 같은 코드를 작성했다면 에러가 발생하겠지만 js에서는 그렇지 않는다. 이러한 현상이 발생하는 이유는 execution context와 관련있다.</p>
<p>&nbsp; creation phase에서:</p>
<p>&nbsp; &nbsp; - name에 메모리가 할당된다</p>
<p>&nbsp; &nbsp; - name에 undefined가 할당된다</p>
<p>&nbsp; execution phase에서</p>
<p>&nbsp; &nbsp; - console.log(name)이 실행된다</p>
<p>&nbsp; 위 과정에서 변수에 메모리가 할당되고 undefined가 할당되는 creation phase에서의 메커니즘을 variable hosting이라 한다.</p>
<p>&nbsp; *undefined는 변수가 선언은 되었지만 값이 할당되지 않았음을 의미한다</p>
<p>&nbsp; 만약 다음과 같이 변수에 값을 할당했다면 execution phase에서 해당 값이 변수에 할당될것이다.</p>
<pre id="code_1619798872409" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>name = 'a';</code></pre>
<p><i><b>Function hoistring</b></i></p>
<p><i><b>&nbsp;&nbsp;</b></i>Function hoisting역시 variable hoisting과 같은 절차를 밟는다. Creation phase에서 함수의 선언을 메모리에 넣고 execution phase에서 실행한다.</p>
<pre id="code_1619799091294" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>funcA();

function functionA(){
	console.log('Function A');
    functionB();
}

function functionB(){
	console.log('Function B');
}</code></pre>
<p>출력:</p>
<p>Function A</p>
<p>Function B</p>
<p>&nbsp;</p>
<p>위 코드는 다음과 같은 방식으로 동작한다:</p>
<p>1. execution context가 funcA()를 위한 메모리를 생성하고 함수의 선언을 메모리에 넣는다.</p>
<p>2. funcA()는 자신만의 execution context를 생성하고 이때문에 functionB()에도 비슷할 일이 발생한다</p>
<p>3. 각자 자신의 execution context에서 실행된다</p>
<p>따라서 함수 정의 전체를 creation phase에서 메모리의 맨 앞에 넣는 것을 function hoisting이라 한다.</p>
<p>&nbsp;</p>
<p>만약 함수를 변수에 할당한다고 해보자 사용한다고 해보자</p>
<pre id="code_1619799557947" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>log();

var log = function(){
	console.log("log");
}</code></pre>
<p>위와 같은 코드를 작성할 경우 에러가 발생하게 된다</p>
<p></p><figure class="imageblock alignCenter" data-filename="E280FCC5-0996-4A81-AC5F-0275620BD1D2.jpeg" data-origin-width="640" data-origin-height="120" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RXhlY3V0aW9uIENvbnRleHQsIEhvaXN0aW5n/img.jpg" data-filename="E280FCC5-0996-4A81-AC5F-0275620BD1D2.jpeg" data-origin-width="640" data-origin-height="120" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>이와 같은 에러가 발생하는 이유는 변수에 함수를 할당했기 때문이다</p>
<p>위 코드에서 log는 변수로 호이스팅되기 때문에 undefined를 creation phase에서 할당받게 된다 그런데 log()에서 함수를 호출하고 있으므로 에러가 발생한다</p>
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