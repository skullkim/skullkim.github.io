---
layout:       post
title:        "TDD(Test Driven Dvelopment)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- TDD
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
                            <p data-ke-size="size16">TDD는 테스트케이스를 작성한 후 실제 코드를 개발해 리펙토링을 한다.&nbsp;</p>
<p data-ke-size="size16">기존 방식:</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/VEREKFRlc3QgRHJpdmVuIER2ZWxvcG1lbnQp/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">TDD:</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/VEREKFRlc3QgRHJpdmVuIER2ZWxvcG1lbnQp/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; 애자일에서는 불확실성이 높을 때 피드백과 협력이 중요하다고 한다. TDD역시 이런 이유로 반복적인 피드백과, 협력을 중요시 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 만약 특정 기능을 하는 코드를 반복적으로 작성한 경험이 있거나 결과가 명백하다면 TDD를 하지 않아도 된다. 하지만 다음과 같은 경우에서는 TDD를 하는 것이 적절하다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 처음해보는 프로그램 주제 - 나에 대한 불확실성이 높을 경우</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 고객 요구사항이 지속적으로 바뀔경우 - 외부적인 불확실성이 높을 경우</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 개발 중에 코드를 많이 바꾸어야 하는 경우</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4.&nbsp; 누가 유지보수를 할지 모르는 경우</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Test의 명사화</b></p>
<p data-ke-size="size16">&nbsp; TDD에서 test는 동사가 아닌 명사이다. 즉, 동사처럼 그 순간에만 어떤 대상을 위해 존재하는 것이 아닌 명사처럼 이후에도 소유할 수 있다. 따라서 test는 하고 패스하는 것이 아닌 남들이 봐야하는, 남들이 실행시켜봐야 하는 것이다.</p>
<p data-ke-size="size16">&nbsp; 이것이 TDD가 협력을 증진시키는 이유이다. 다른 사람의 코드를 쉽게 접근할 수 있고 이해가 빨라진다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Red, Green, Refactor</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>Red, Green, Refactor는 TDD를 수행하는 하나의 프래임워크이다. 개발자는 이 프레임워크를 사용해 테스트 케이스를 만들고, 코드를 작성하고, 코드를 최적화 할 수 있다.</p>
<p data-ke-size="size16">&nbsp; Red - 개발을 해야할 대상에 대해 생각한다.</p>
<p data-ke-size="size16">&nbsp; Green - 어떻게 테스트케이스를 통과할지를 고민한다.</p>
<p data-ke-size="size16">&nbsp; Refactor - 현재 존재하는 코드를 어떻게 최적화할지를 고민한다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/VEREKFRlc3QgRHJpdmVuIER2ZWxvcG1lbnQp/img_2.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Red</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; Red는 Red, Green, Refactor사이클 중에서 시작점이다. 이 단계에서는 기능 구현을 알리는 테스트를 작성하게 된다. 이 테스트는 테스트의 예상 결과가 나왔을 때 패스된다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Green</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>Green은 코드를 실제로 작성해 Red에서 작성했던 테스트 케이스를 통과하도록 하는 과정이다. 이 단계에서는 코드 최적화와는 관련없이 그저 테스트 케이스가 통과될 정도의 코드만 작성하면 된다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Refactor</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp;&nbsp;</b></i>아직&nbsp;Green에 있는 단계이다. 이 단계에서는 코드를 어떻게 더 효율적으로 작성할지를 고민하면 된다. 이 단계에서 test suite(test case의 집합)를 리팩토링 한다면 좋은 테스트의 성질인 MC-FIRE에 대해 고민해야 한다. 코드를 리팩토링 하고 싶다면 어떻게 하면 동일한 output을 내보내되 더 명시적이고 빠른 코드를 작성할 수 있을지를 고민하면 된다.</p>
<p data-ke-size="size16">&nbsp; Refactor단계는 필수가 아니다. 하지만 Green단계에서 다시 Red단계로 넘어가기 전에 다음과 같은 질문을 하고 리팩토링을 고민하는 것이 좋다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1.&nbsp; 현재의 test suite를 더 명시적으로 만들 수 있나?</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 현재의 test suite가 믿을만한 피드백을 제공하고 있나?</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 현재의 코드와 test suite에서 중복된 케이스가 존재한가?</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. 현재의 코드를 더 명시적으로 바꿀 수 있나?</p>
<p data-ke-size="size16">&nbsp; &nbsp; 5. 좀 더 효율적인 방법이 있나?</p>
<p data-ke-size="size16">&nbsp; &nbsp; 6. 나의 테스트가 독립적인가?</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>좋은 테스트의 조건</b></p>
<p data-ke-size="size16">&nbsp; TDD에서는 수 많은 유닛 테스트가 요구된다. 따라서 어떤 테스트가 좋은 테스트인지 알 필요가 있다.</p>
<p data-ke-size="size16">&nbsp; Test suite를 사용하는 이유는 테스트들을 이용해 배포 전에 에러를 캐치하기 위함이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 좋은 테스트는 실행 시간이 길지 않으며 테스트가 통과되면 소프트웨어가 예상된 동작을 한다는 신뢰성을 주어야 한다. 만약 테스트가 버그를 발견한다면 이 테스트는 개발자가 버그의 원인을 찾을 수 있는 피드백을 주어야 한다.</p>
<p data-ke-size="size16">&nbsp; 좋은 테스트의 좋건은 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. Fast</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. Complete</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. Reliable</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. Isolated</p>
<p data-ke-size="size16">&nbsp; &nbsp; 5. Maintainable</p>
<p data-ke-size="size16">&nbsp; &nbsp; 6. Expressive</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Fast</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; Full-stack 웹 애플리케이션에 대한 테스트는 크게 유닛 테스트, 통합 테스트(integration tests)로 나뉘어져 있다. 유닛 테스트는 빠르고, 통합 테스트는 유닛 테스트에 비해 느리다. 만약 하나의 test suite가 다량의 통합 테스트를 포함하고 있다면 수 분, 심하면 몇시간을 기다려야 할 수도 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 빠른 test suite는 피드백을 더 빨리 주지 때문에 개발 프로세스가 느린 test suite에 비해 더 효율적이다. 만약 임의의 test suite A가 5분이 걸리고 test suite B가 30초가 걸린다고 해보자. A, B가 같은 코드에 대한 테스트라 했때 A, B를 5번 실행시키면 B는 A에 비해 약 22분을 절약할 수 있다.</p>
<p data-ke-size="size16">&nbsp; <i><b>Complete</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 하나의 애플리케이션에 해당하는 코드를 test suite가 전부 커버할 수 있다면 코드의 변경, 추가에 대한 어떠한 에러도 잡아낼 수 있다. 이런 온전한 test suite는 소프트웨어가 예상한 대로 동작한다는 신뢰성을 준다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Reliable</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp; &nbsp;&nbsp;</b></i>신뢰성 있는 테스트는 해당 테스트 스포트 밖의 변화와는 관련없이 지속적인 피드백을 주어야 한다. 신뢰성이 없는 테스트는 간헐적으로 실패를 하고 개발자가 애플리케이션에 가한 수정에 대한 피드백을 주지 않는다. 만약 테스트가 신뢰성이 없다면 온전히 같은 상황에서 버그 수정여부 확인을 위해 여러번의 테스트를 돌렸을 때 어떤것을 실패하고 어떤것은 성공할 것이다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;<b>Isolated</b></p>
<p data-ke-size="size16"><b>&nbsp; &nbsp; &nbsp;&nbsp;</b>하나의 test suite는 다른 테스트들과 충돌이 나지 않아야 한다. 따라서 일부 상황에서는 테스트를 진행한 후 기존 데이터를 정리해야 할 수도 있다.</p>
<p data-ke-size="size16">&nbsp;&nbsp;<i><b>Maintainable</b></i></p>
<p data-ke-size="size16"><i><b>&nbsp; &nbsp; &nbsp;&nbsp;</b></i>test suite는 조작이 간단해야 한다. 쉽게 추가하고, 바꾸고, 지울수 있어야 한다. 만약 새로운 기능에 대해 테스트를 추가할 수 없다면 해당 test suite는 비효율 적이고, 온전하지 않게 된다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; test suite를 유지, 관리할 수 있는 방법은 코딩 모범 사례를 따르며 사용자와 팀에 적합한 일관된 프로세스로 개발을 하는 것이다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;&nbsp;<i><b>Expressive</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 읽기 쉬운 test suite는 좋은 문서이다. 코드를 작성할때는 항상 테스의 대상이 되는 기능을 잘 서술해야 한다. test suite를 만들때는 다른 개발자들이 충분히 알아볼 수 있을 정도로 서술해아 하며 해당 웹 애플리케이션의 목적을 이해되게 해야 한다. 또 한 test suite는 소프트웨어의 한 부분이기 때문에 README나 문서들 보다도 더 빠르게 최신 버전을 유지해야 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp;&nbsp;</p>
<p data-ke-size="size16"><b>TDD 개발 방식의 장점</b></p>
<p data-ke-size="size16">&nbsp; 1. 낮은 의존성</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;TDD는 코드의 재사용 보장을 명시하고 TDD를 통한 SW 개발은 철저한 모듈화가 이뤄진다. 이는 종속성과 의존성이 낮은 모듈로 조합된 SW 개발을 가능하게 하고 필요에 따라 모듈을 추가하고 제거해도 SW전체 구조에 영향을 미치지 않는다.</p>
<p data-ke-size="size16">&nbsp; 2. 재설계 시간 단축</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 테스트코드 작성을 통해 현재 어떤 것이 필요한지를 명확히 할 수 있다. 따라서 중간에 설계를 변경하는 일이 줄어든다.</p>
<p data-ke-size="size16">&nbsp; 3. 디버깅 시간의 단축.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 유닛테스트를 통해 버그가 발생했을 때 어느 부분에서 문제가 발생한건지를 명확히 할수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;4. 테스트 문서의 대체 가능</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp;SI에서는 어떤 요소들이 테스트 되었는지 테스트 정의서를 만든다. 이는 단순한 통함 테스트 문서이다. 하지만 TDD의 경우 테스팅을 자동화 하고 보다 정확한 테스트 근거를 산출할 수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 5. 추가 구현의 용이</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; 기존 SW에 어떤 기능을 추가할때 추가한 코드가 기존 코드에 어떤 영향을 미칠지 모른다는 문제가 발생한다. 하지만 TDD를 사용하면 유닛 테스팅을 통해 테스트 기간을 단축시킬 수 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>TDD 개발 방식의 단점</b></p>
<p data-ke-size="size16">&nbsp; &nbsp; 처음 부터 2개의 코드를 짜야하기 때문에 일반적인 개발 방식에 비해 10~30%정도 개발 시간이 늘어난다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>AAA pattern(Arrage, Act, Assert)</b></p>
<p data-ke-size="size16">&nbsp; 테스트 코드를 작성할 때 AAA 패턴을 사용하면 가독성이 향상되고 다른 사람의 코드를 이해하는데 도움이 된다.</p>
<p data-ke-size="size16">&nbsp; AAA패턴은 테스트 코드를 3단계로 나누어 작성한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; Arrange(준비): 테스트를 실행하기 전에 필요한 것들을 준비한다. 객체 생성, 테스트 전에 호출할 API 호출 등.</p>
<p data-ke-size="size16">&nbsp; &nbsp; Act(실행): 테스트 코드를 실행한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; Assert(단언): 실행한 코드가 예상대로 작동했는지를 확인한다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//하나의&nbsp;유닛&nbsp;테스트는&nbsp;test()메서드에서&nbsp;이루어&nbsp;진다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//test()의&nbsp;첫번쨰&nbsp;인자는&nbsp;스트링이며&nbsp;어떤&nbsp;테스트인지를&nbsp;서술한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//두번째&nbsp;인자는&nbsp;콜백이며&nbsp;여기서&nbsp;실제&nbsp;테스트가&nbsp;실행된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//세번째&nbsp;인자는&nbsp;밀리세컨드&nbsp;단위의&nbsp;시간을&nbsp;넣을&nbsp;수&nbsp;있고</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//이는&nbsp;테스트를&nbsp;진행할&nbsp;시간을&nbsp;의미한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//만약&nbsp;1000을&nbsp;명시했는데&nbsp;해당&nbsp;테스트가&nbsp;1초안에&nbsp;끝나지&nbsp;않았다면</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//테스트는&nbsp;실패한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">test(<span style="color: #63a35c;">"convert&nbsp;array&nbsp;of&nbsp;country&nbsp;data&nbsp;objects&nbsp;to&nbsp;array&nbsp;of&nbsp;countries"</span>,&nbsp;()<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//AAA패턴&nbsp;사용</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//arrange</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;inputObject&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;[</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">"Argentina"</span>,&nbsp;capital:&nbsp;<span style="color: #63a35c;">"Buenos&nbsp;Aires"</span>},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">"Belize"</span>,&nbsp;capital:&nbsp;<span style="color: #63a35c;">"Belmopan"</span>},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<span style="color: #066de2;">name</span>:&nbsp;<span style="color: #63a35c;">"Bolivia"</span>,&nbsp;capital:&nbsp;<span style="color: #63a35c;">"Sucre"</span>}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;expectedValue&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;[<span style="color: #63a35c;">"Argentina"</span>,<span style="color: #63a35c;">"Belize"</span>,<span style="color: #63a35c;">"Bolivia"</span>]</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//act</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;actualValue&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;countryExtractor(inputObject)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//assertions</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;expect(actualValue).toEqual(expectedValue);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//toEqual()은&nbsp;깊은&nbsp;비교를&nbsp;하고&nbsp;tobe()는&nbsp;얕은&nbsp;비교를&nbsp;한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>jest를 사용해 assertion 단계에서 결과 검증하기</b></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">expect(actualValue).toEqual(expectedValue)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">expect(actualValue[<span style="color: #0099cc;">0</span>]).toBe(<span style="color: #63a35c;">"Argentina"</span>)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">expect(actualValue).toContain(<span style="color: #63a35c;">"Belize"</span>);<span style="color: #999999;">//actualValue가&nbsp;"Belize"를&nbsp;포함하고&nbsp;있나</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">expect(actualValue[<span style="color: #0099cc;">2</span>]&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">"Bolivia"</span>).toBeTruthy();<span style="color: #999999;">//expect()의&nbsp;조건이&nbsp;참인가</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//not은&nbsp;!과&nbsp;같다.&nbsp;toBeDefined()는&nbsp;undefined여부&nbsp;검증</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">expect(actualValue[<span style="color: #0099cc;">3</span>]).not.toBeDefined();<span style="color: #999999;">//actualValue의&nbsp;길이가&nbsp;3인가.&nbsp;만약&nbsp;3이면&nbsp;[3]은&nbsp;undefined</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
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