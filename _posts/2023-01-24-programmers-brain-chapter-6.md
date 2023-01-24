---
layout:       post
title:        "Chapter 6. 코딩 문제 해결을 더 잘하려면"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프로그래머의 뇌
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 문제에 대해 다양한 해결책을 고려할 때, 각각 저마다의 장점을 가지고 있기에 해결책을 결정하기 어렵다. 여러 소프트웨어 설계에 관한 결정을 할 때 도움이 되는 두 가지 프레임워크에 대해 다뤄보자.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 먼저 문제 해결과 프로그래밍 작업 도중 두뇌가 생성하는 심적 표상(mental representation)을 살펴보자. 이를 알면 더 많은 종류의 문제를 풀 수 있고, 코드에 대해 유추할 수 있으며, 문제를 더 효과적으로 풀 수 있다. 두 번째로, 문제를 풀 때 어떻게 컴퓨터에 대해 생각하는지 살펴보자. 프로그래밍 시, 컴퓨터에 관한 모든 방면을 고려하지 않아도 된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>모델을 사용해서 코드에 대해 생각해 보기</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>모델의 유익함</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 모델은 실제를 간단하게 표현한 것이다. 따라서 모델을 프로그래밍에 이용하면 복잡한 프로그램에 대한 정보를 다른 사람과 공유할 때 유용하다. 또 한, 문제를 풀 때 인지 부하를 줄여줘서 문제 풀이에 도움이 된다. 예컨대 변수 상태를 기록한 상태표는 루프 로직 파악에 유용하다. 모델은 LTM이 관련된 기억을 찾는 데 도움이 되기 때문에 문제 해결에 유용하다. 모델에는 제약이 있기 때문에 이 제약으로 인해 특정 부분에 해당하는 해결책만 생각할 수 있게 해 준다.&nbsp;</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>모든 모델이 동일하게 유용한 것은 아니다</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 문제에 대해 생각하기 위해 사용하는 모든 모델이 동일하지는 않다. 예를 들어 문제 해결을 위해 스택을 사용해야 한다 해보자. 여기서 스택이 구현된 있지 않은 언어를 문제 해결의 모델로 사용한다면, 스택 구현을 위해 많은 시간을 사용해야 한다. 하지만, 라이브러리로 이미 스택이 구현된 언어를 사용한다면, 문제를 좀 더 쉽게 해결할 수 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>정신 모델</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 언급한 모델은 두뇌 외부에서 생성되는 모델로, 다른 사람과 의사소통이나 문제에 대해 깊은 생각을 힐 때 유용하다. 만약 문제에 대해 오로지 생각을 해야 한다면 정신 모델(mental model)을 사용할 수 있다).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 정신 모델은 풀어야 할 문제에 대해 추론하기 위해 사용할 수 있는 작업 기억 공간 내의 추상화다. 개발자는 코드를 사용할 때 정신 모델을 사용한다. 예를 들어, 디버깅 시 개발자는 특정 라인이 실행되고 있다고 생각한다. 하지만, 실제로는 이진 코드가 실행되고 있다. 또 한, 자료구조 역시 그저 메모리에 존재하는 데이터에 불과하지만, 개발자는 특정 구조를 가지고 있다고 상상한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>정신 모델 자세힐 살펴보기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>정신 모델의 중요 특징과 프로그래밍 예시는 다음과 같다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%; text-align: center;"><span style="font-family: 'Noto Serif KR';">특징</span></td>
<td style="width: 50%; text-align: center;"><span style="font-family: 'Noto Serif KR';">예</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">정신 모델은 나타나고자 하는 원래의 시스템에 대한 완전한 모델일필요 없다.</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">변수를 값이 들어가는 박스로 생각하는 것이 재할당에 대해 적절히 설명해 주지 못한다.</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">정신 모델은 같은 상태를 계속 유지할 필요 없다.</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">프로그래밍을 배울 때 안에 값을 가지고 있는 박스로 생각하면 도움이 된다. 하지만 어느 정도 시간이 흐르면 변수는 한 가지 이상의 값을 동시에 가질 수 없다.</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">여러 개의 모델이 공존할 수 있다.</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">변수를 값을 가지는 박스 또는 이름표로 생각할 수 있다.</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">정신 모델은 종종 미신처럼 느껴진다. 사람들은 말도 안되는 것을 믿는다.</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">문제가 너무 안풀릴 때 컴퓨터에게 "제발 작동해 줘"라고 말하는 사람이 있다. 이는 정신 모델에 따라 컴퓨터가 사람 말에 반응하는 개체라 생각하기 때문이다</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">사람들은 가급적 정신 모델을 사용하지 않으려 한다. 두뇌는 많은 양의 에너지를 필요로 하기에 과부화를 줄일려 한다.</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">버그 발견 시, 디버깅을 하기 보다 코드를 살짝 고쳐보는 것이 이에 해당한다.</span></td>
</tr>
</tbody>
</table>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>새로운 정신 모델 배우기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 한 사람이 가진 특정 지식에 대한 모델은 더 깊이 배우고 나면 오래되고 잘못된 정신 모델이 제거되고 새로운 정신 모델로 대체된다고 생각할 수 있다. 하지만, 그러한 정보가 LTM에서 사라질 가능성은 지극히 낮다. 즉, 언제나 부정확한 정신 모델을 사용할 위험이 존재한다. 특히, 인지 부하가 높은 상황에서 말이다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>소스코드에 대한 정신 모델을 작업 기억 공간에 생성하기</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 정신 모델이 정확하고 구체적이면 복잡한 시스템에 대해 생각할 때 도움이 된다. 코드가 복잡할 경우 정확한 정신 모델을 만드는 대 많은 노력이 필요하다. 다음 과정을 거치면 복잡한 코드에 대한 정신 모델을 좀 더 편하게 만들 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>1. 일부 코드베이스만 나타내는 국지적 모델을 만든다.</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>2. 코드에 관련된 모든 객체 간의 관계를 나열한다.</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>3. 시스템에 대한 질문을 만들고 이 질문을 사용해 모델을 개선하라.</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>현재 사용 중인 시스템에 따라 올바른 질문이 다를 수 있지만, 다음과 같은 일반적인 질문이 가능하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 시스템에서 가장 중요한 요소는 무엇이고 그들이 모델에 포함되었나?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 이 중요한 요소들 사이의 관계는 무엇인가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 프로그램의 주요 목표는 무엇인가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 목표가 핵심 요소 및 그 관계와 어떻게 관련되어 있는가?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 일반적인 사용 사례는 무엇인가?</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>LTM의 정신 모델</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 언급한 정신 모델은 작업 기억 공간 속에 자리 잡고 있다고 설명한다. 하지만, 정신 모델이 LTM에 위치한다고 주장하는 의견도 존재한다. 이들은 일반적인 정신 모델이 LTM에 저장되고 필요할 때 기억해 낼 수 있다고 주장한다. 예를 들어 생소한 프로그래밍 언어로 구현된 트리를 봤을 때, 이전에 저장한 정신 모델에 존재하는 트리 모양을 이용하는 식이다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>LTM에 소스 코드에 대한 정신 모델 생성</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 정신 모델을 더 잘 활용하기 위해선 잠재적 정신 모델의 어휘를 많이 쌓아야 한다. LTM에 저장된 지식을 확장하는 좋은 방법으로 3장에서 플래시 카드 사용을 언급했다. 플래시 카드 한쪽에 정신 모델의 이름, 다른 쪽에는 정신 모델의 간략한 설명 또는 시작화된 정보를 적어 사용하면 좋다. 이렇게 이용할 수 있는 정신 모델로는 자료구조, 디자인 패턴 등이 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>개념적 기계</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 정신 모델은 일반적이며 모든 영역에서 찾아볼 수 있다. 정신 모델을 프로그래밍에 한정지은, 즉 컴퓨터가 코드를 실행하는 방법에 대해 추론할 때 상요하는 개념적 기계(notional machine)라는 것이 존재한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그램이 어떻게 작동하는지 이해하고자 할 때, 대부분 컴퓨터가 물리적으로 어떻게 동장 하는지 세부 사항에는 관심이 없다. 프로그래밍 언어를 통해 더 높은 개념적 수준에서 일어나는 효과에 관심이 많다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 개념적 기계는 불완전할지는 몰라도 프로그래밍 언어의 실행에 대해 일관되고 정확하게 추상화한 것이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>개념적 기계의 층위</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 개념적 기계는 프로그래밍 언어 수준에서 작동하며 기저에 있는 시스템의 모든 세부 사항은 추상화한다. 코드에 대해 추론할 때 자신이 어떤 세부 사항을 무시하는지 아는 것이 중요하다. 때로는 코드에 관련된 세부사항 까지도 추상화해서 이해를 더 어렵게 만들기 때문이다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>개념적 기계와 언어</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 기계의 작동 방식에 대해 추론할 때뿐만 아니라 코드에 대해 말을 할 때도 개념적 기계를 사용하곤 한다. 예를 들어 파일 열림, 닫힘은 사실 파 읽을 읽거나 읽을 수 없는 상태를 말한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>개념적 기계의 확장</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하나의 기계적 개념은 다른 기계적 개념을 구성하는 대 사용된다. 예를 들어 변수를 하나의 박스라 생각했을 때, 이들을 쌓으면 스택이 된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>여러 개념적 기계는 서로 충돌하는 정신 모델을 만들 수 있다</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>위에서 언급했듯 하나의 기계적 개념은 다른 기계적 개념을 구성하는 대 도움을 줄 때도 있지만, 개념적 기계가 만들어 내는 정신 모델이 서로 충돌할 수도 있다. 예를 들어 변수를 상자로 설명하는 개념적 기계와 변수를 이름표로 보는 개념적 기계는 하나의 정신 모델로 합칠 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 어떤 정신 모델을 사용하냐에 따라서 이해하는 부분이 다르다는 결과도 존재한다. 한&nbsp;<a href="https://dl.acm.org/doi/10.1145/3265757.3265765" target="_blank" rel="noopener">연구</a>에서 프로그래밍 언어를 가르칠 때 한 그룹에겐 변 후를 '라벨'이라는 정신 모델로 가르쳤고, 다른 한 그룹에는 변수를 '상자'라는 정신 모델로 가르쳤다. 그 후 (1). 하나의 변수에 관한 간단한 문제와 (2) 변수에 값을 두 번 할당하는 문제를 출제했다. 그 결과 변수를 '상자'로 이해한 그룹이 1번 문제를 더 잘 풀었다. 하지만 변수가 두 가지 값을 가질 수 있다고 오해하는 '상자'그룹 인원 역시 많았다. 이는 프로그래밍 개념과 그에 상응하는 컴퓨터의 동작을 설명할 때 현실 세계의 객체와 동작을 이용하는 것은 신중히 이루어져야 한다는 것을 시사한다. 비유는 때로는 유용하지만 때로는 혼란을 초래한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 프로그래머의 뇌</span></p></div>