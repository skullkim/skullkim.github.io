---
layout:       post
title:        "Chapter 4. 복잡한 코드 읽는 방법"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프로그래머의 뇌
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16">&nbsp; 2장에서 효과적으로 코드를 나누는 법, 3장에서는 LTM에 더 많은 문법을 저장하는 법을 배웠다. 이 둘을 이용하면 코드를 읽는 데에 도움이 되지만 너무 복잡한 코드를 이해하기에는 역부족일 때가 있다. 따라서 작업 기억 공간(working memory - 두뇌에서 처리하는 능력)의 기저에 있는 인지 과정을 살펴보고 복잡한 코드를 좀 더 쉽게 다루는 법을 살펴보자.</p>
<h2 data-ke-size="size26"><b>복잡한 코드를 이해하는 것이 왜 어려울까?</b></h2>
<p data-ke-size="size16">&nbsp; 작업 기억 공간은 두뇌가 생각하고 새로운 아이디어를 형성하고 문제를 해결하는 능력에 해당한다.</p>
<h3 data-ke-size="size23"><b>작업 기억 공간과 STM의 차이</b></h3>
<p data-ke-size="size16">&nbsp; 일부 사람들이 STM과 작업 기억 공간을 혼용한다. 하지만, STM은 정보를 일시적으로 기억하는 역할을 하고, 작업 기억 공간은 정보를 처리하는 역할을 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; STM과 마찬가지로 작업 기억 공간도 한 번에 2~6개 정보를 기억할 수 있다. 작업 기억 공간의 맥락에서 이를 인지 부하(cognitive load)라 부른다. 너무 많은 요소가 존재해 청크로 나누지 못하는 문제를 풀려하면 작업 공간은 과부하(overlaod) 상태가 된다.</p>
<h3 data-ke-size="size23"><b>프로그래밍과 관련한 인지 부하</b></h3>
<p data-ke-size="size16">&nbsp; 오스트레일리아의 존 스웰러(John Sweller) 교수가 제안한 인지 부하 이론에 따르면 다음과 같은 세 가지 인지 부하가 존재한다.</p>
<table style="border-collapse: collapse; width: 100%; height: 71px;" border="1" data-ke-align="alignLeft">
<tbody>
<tr style="height: 18px;">
<td style="width: 50%; height: 18px; text-align: center;">부하 종류</td>
<td style="width: 50%; height: 18px; text-align: center;">간략한 설명</td>
</tr>
<tr style="height: 17px;">
<td style="width: 50%; height: 17px; text-align: center;">내재적(intrinsic) 부하</td>
<td style="width: 50%; height: 17px; text-align: center;">문제 자체가 얼마나 복잡한지</td>
</tr>
<tr style="height: 18px;">
<td style="width: 50%; height: 18px; text-align: center;">외재적(extraneous) 부하</td>
<td style="width: 50%; height: 18px; text-align: center;">외부적 요인에 의해 문제에 추가된 것</td>
</tr>
<tr style="height: 18px;">
<td style="width: 50%; height: 18px; text-align: center;">본유적(germane) 부하</td>
<td style="width: 50%; height: 18px; text-align: center;">생각을 LTM에 저장하는 과정에서 일어나는 인지 부하</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; 여기서는 내재적 부하와 외재적 부하를 다루고 본유적 부하는 10장에서 다루겠다.</p>
<h4 data-ke-size="size20"><b>코드를 읽을 때 내재적 인지 부하( intrinsic cognitive load)</b></h4>
<p data-ke-size="size16">&nbsp; 문제 그 자체가 갖는 특성 때문에 발생하는 인지 부하다. 어떤 문제를 풀 때, 이 문제의 해법이 유일하고 더 이상 간소화할 수 없을 때 이 문제의 부하는 문제에 내재해 있다고 본다. 프로그래밍에서는 이런 문제의 내재적 측면을 내재적 복잡성(inherent complexity)이라 한다. 인지 과학에서는 문제 자체에 존재하는 특성이 내재적 인지 부하의 원인이라 한다.</p>
<h4 data-ke-size="size20"><b>코드를 읽을 때 외재적 인지 부하(extraneous cognitive load)</b></h4>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>어떤 문제가 두뇌에 일으키는 자연적이고 내재적인 부하에 더해 문제에 추가되는 인지 부하를 의미한다. 예를 들어 1*3의 답을 구하는 방식은 고유하며 더 단순화가 불가능 하기에 내재적 인지 부하를 일으킨다. 여기서 3을 임의의 자연수 a로 치환한다면 1*a가 된다. 이 식 역시 곱셈에 대한 지식을 요구하지만 a라는 변수에 임의의 자연수를 선택하고 연결시켜야 한다는 외재잭 인지 부하가 추가되었다. 즉, 여러 해법이 존재해 특정 해법을 찾아 연결시키는 과정에서 외재적 인지 부하가 발생한다. 이런 외재적 인지 부하를 프로그래밍에선 우발적 복잡성(accidental complexity)라 한다. 외재적 부하는 특정 개념을 많이 경험할수록 그것에 대한 인지 부하가 적아진다.</p>
<h2 data-ke-size="size26"><b>인지 부하를 줄이기 위한 기법</b></h2>
<p data-ke-size="size16">&nbsp; 이제 인지 부하를 줄이는 방법을 알아보자</p>
<h3 data-ke-size="size23"><b>리팩터링</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>유지보수하기 좋은 코드를 작성하는 대신 현 시점에서 가독성이 높은 코드를 작성하는 인지적 리팩터링(cognitive refactoring)은 인지 부하를 줄일 수 있다. 인지적 리팩터링을 하는 과정에서 역 리팩터링(reverse refactoring)을 수반할 수도 있다. 메서드를 인라인으로 바꾸는 등의 역 리팩터링은 메서드 이름이 모호할 때 이름의 의도를 알아내기 위해 소모하는 외재적 인지 부하를 줄여준다. 그 후 새로운 맥락에서 코드를 파악하면 더 적절한 메서드 이름을 지을 수 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 코드 내에서 메서드 위치를 바꾸는 것도 하나의 방법이다. 예를 들어 메서드가 최초로 호출되는 위치로부터 가까이 정의돼 있으면 코드의 가독성이 좋아진다.</p>
<p data-ke-size="size16">&nbsp; 사람마다 지식이 다르고 코드 이해도가 자르기에 인지적 리팩터링은 자신만을 위한 것이다. 따라서 인지적 리팩터링을 이용해 코드를 이해했다면 반드시 원상태로 돌려놓아야 한다.</p>
<h3 data-ke-size="size23"><b>생호한 언어 구성 요소를 다른 것으로 대치하기</b></h3>
<p data-ke-size="size16">&nbsp; 익숙하지 않은 언어 구성 요소는 작업 기억 공간에 외재적 인지 부하를 늘리기 때문에 잘 인지하고 있는 기본적인 문법으로 치환해 보는 것도 한 방법이다.&nbsp;</p>
<h3 data-ke-size="size23"><b>플래시카드에 코드 동의어 추가</b></h3>
<p data-ke-size="size16">&nbsp; 3장에서 언급한 플래시 카드를 이용해 익숙하지 않은 고급 개념을 익힐 수 있다. 앞면에 익숙하지 않은 개념을 사용한 코드를 적고 뒷면에 그에 해당하는 전통적인 방식의 코드를 적고 사용하면 된다.</p>
<h2 data-ke-size="size26"><b>작업 기억 공간에 부하가 오면 쓸 수 있는 기억 보조 수단</b></h2>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>위에서 언급한 방법을 사용해도 코드 구조가 여전히 복잡하다면 작업 기억 공간에 과부하를 줄 수 있다. 복잡한 코드 구조는 다음과 같은 방식으로 작업 기억 공간에 과부하를 유발한다.</p>
<p data-ke-size="size16">&nbsp; 1. 정확히 코드의 어떤 부분을 파악해야 할지 모르 때이다. 이는 필요 이상으로 많은 코드를 읽게 되고 작업 기억 공간이 처리할 수 있는 것보다 많은 양이 될 수 있다.</p>
<p data-ke-size="size16">&nbsp; 2. 코드가 서로 밀접하게 연결되 있는 경우 두뇌는 두 가지 작업을 동시에 수행한다. 1. 코드의 개별 라인을 이해하면서 2. 계속 읽어야 하는 부분을 판단하기 위해 코드 구조를 이해해야 한다.</p>
<p data-ke-size="size16">&nbsp; 위와 같은 상황에서 코드를 집중해서 읽는 데 도움이 되는 보조 수단은 다음과 같다.</p>
<h3 data-ke-size="size23"><b>의존 그래프 생성</b></h3>
<p data-ke-size="size16">&nbsp; 코드를 바탕으로 의존 그래프(dependency graph)를 만들면 흐름을 이해하고 논리적 흐름에 따라 코드를 읽는 데 도움이 된다. 이 방식을 사용하기 위해 코드를 pdf로 변환하거나 프린트하는 것을 추천한다. 의존 그래프를 그리는 방법은 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; 1. 모든 변수를 찾아 원으로 표시하고 동일 변수끼리 선으로 연결한다</p>
<p data-ke-size="size16">&nbsp; 2. 변수의 원과는 다른 색으로 메서드나 함수를 원으로 표시한다. 그 후 메서드 정의와 호출된 위치를 선으로 연결한다.</p>
<p data-ke-size="size16">&nbsp; 3. 또 다른 색으로 클래스의 모든 인스턴스를 원으로 표시한다. 그 후 클래스 정의와 인스턴스를 서로 연결한다.</p>
<p data-ke-size="size16">&nbsp; 이 방식은 패턴을 만들어 코드의 흐름을 보여준다. 따라서 코드 구조에 대한 정보를 가진 레퍼런스로 활용해 코드의 의미와 메서드 정의를 찾는 데 들이는 노력을 줄일 수 있다.</p>
<h3 data-ke-size="size23"><b>상태표 사용</b></h3>
<p data-ke-size="size16">&nbsp; 인지적 리팩터링을 하고 의존 그래프를 이용했음에도 코드를 이해하기 어렵다면, 이는 코드에서 수행하는 계산 로직이 어렵기 때문이다. 이렇게 계산이 많은 코드를 파악할 때 보조 수단으로 상태표(state table)를 사용할 수 있다. 상태표는 변수의 값 변동에 중점을 둔다. 테이블의 열은 변수를 나타내고 행은 해당 변수가 각 단계에서 갖는 값을 나타낸다.</p>
<p data-ke-size="size16">&nbsp; 상태 표는 다음과 같은 단계로 만들 수 있다.</p>
<p data-ke-size="size16">&nbsp; 1. 모든 변수를 나열한다</p>
<p data-ke-size="size16">&nbsp; 2. 테이블을 만들고 각 열에 하나의 변수를 기입한다</p>
<p data-ke-size="size16">&nbsp; 3. 코드의 실행 단계마다 행을 만든다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 여기서 각 실행 단계는 정하기 나름이다. 반복문 1회 반복, 조건 분기가 될 수도 있다.</p>
<p data-ke-size="size16">&nbsp; 4. 코드를 각 단계별로 실행하고 그 단계에서 변수들의 값을 해당하는 열과 행에 적는다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 이 과정에서 모든 변수를 생략 없이 꼼꼼히 적어야 코드를 이해하는 데 도움이 되고 작업 기억 공간에 과부하가 걸릴 때 코드 분석에 유용하다. 상태 표를 레퍼런스로 사용 시 일관성 있게 전체적 윤곽에 집중해 코드를 살펴봐야 한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">출처 - 프로그래머의 뇌</p></div>