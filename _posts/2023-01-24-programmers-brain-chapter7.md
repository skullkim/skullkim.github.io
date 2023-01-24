---
layout:       post
title:        "Chapter 7. 생각의 버그"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프로그래머의 뇌
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16">&nbsp; 버그는 오타와 같이 일을 엉성하게 처리했을 때 발생하기도 하지만, 많은 경우 생각의 착오로 인해 발생한다.</p>
<h2 data-ke-size="size26"><b>왜 두 번째 프로그래밍 언어가 첫 번째보다 쉬울까?</b></h2>
<p data-ke-size="size16">&nbsp; 이미 배운 지식은 다른 영역에서도 유용하다. 이를 전이(transfer)라 한다. 지식 전달은 이미 알고 있는 정보가 새로운 것에 도움이 될 때 일어난다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; LTM에 저장된 프로그래밍 정보는 새로운 프로그래밍 지식을 배울 떄 다음과 같은 두 가지 방식으로 도움이 된다.</p>
<p data-ke-size="size16">&nbsp; 첫 번째는 프로그래밍에 대해 이미 많이 알고 있다면 더 깊이 배우는 것이 쉬워진다. LTM에 저장된 정보를 이용해 새로운 내용을 쉽게 배우는 과정을 학습 도중 전이(transfer during learning)라 한다.</p>
<p data-ke-size="size16">&nbsp; 두 번째 방식은 학습 전이(transfer of learning)다. 이는 완전히 낯선 상황에 이미 알고 있는 내용을 적용할 때 일어난다. 새로운 언어를 배울 때 기존 언어에 존재하는 개념을 떠올리는 식이다.</p>
<h3 data-ke-size="size23"><b>기존 프로그래밍 지식을 활용한 가능성을 높이는 방법</b></h3>
<p data-ke-size="size16">&nbsp; 한 작업에서 다른 작업으로 전이할 수 있는 학습의 양은 다음과 같은 요인으로 좌우된다.</p>
<p data-ke-size="size16">- 숙달: LTM에 이미 저장 된 지식과 관련한 작업을 얼마나 잘 숙달했는지</p>
<p data-ke-size="size16">- 유사성: 두 작업 간의 공통점</p>
<p data-ke-size="size16">- 배경: 환경이 얼마나 비슷한가. 같은 IDE를 사용하고 있는가, 자신과 비슷한 사람과 있는가 등</p>
<p data-ke-size="size16">- 중요 특성: 어떤 지식이 효과적인지를 알고 있는가</p>
<p data-ke-size="size16">- 연관: 두 작업이 얼마나 비슷하다고 느끼는가</p>
<p data-ke-size="size16">- 감정: 해당 작업에 대해 어떤 감정을 가지고 있는가&nbsp;</p>
<h3 data-ke-size="size23"><b>전이의 다른 형태</b></h3>
<p data-ke-size="size16">&nbsp; 전이에 대해 몇 가지 다른 관점이 존재한다. 이 관점들을 알고 아면 프로그래밍 언어 간에 이루어지는 전이를 보다 현실적으로 바라볼 수 있다.</p>
<h4 data-ke-size="size20"><b>고도 전이와 저도 전이</b></h4>
<p data-ke-size="size16">&nbsp; 자동화된 기술을 이전하는 것을 저도 전이(low-road transfer), 복잡한 작업이 전이되는 것을 고도 전이(high0 road transfer)라 한다. 저도 전이는 코드 복사-붙여 넣기와 같이 하는 행위에 대한 명확한 이해가 없는 것을 의미한다. 고도 전이는 상황을 명확히 이해하고 있는 것을 의미한다.</p>
<h4 data-ke-size="size20"><b>근거리 전이와 원거리 전이</b></h4>
<p data-ke-size="size16">&nbsp; 유사성에 따라 유사성이 높은 영역 사이에 지식 전이를 근거리 전이(near transfer), 서로 먼 영역 간의 전이를 원거리 전이(far transfer)라 한다.</p>
<h3 data-ke-size="size23"><b>이미 알고 있다는 것은 저주인가 축복인가?</b></h3>
<p data-ke-size="size16">&nbsp; 위에서 서술했던, 무언가를 알기 때문에 새로운 것을 할 때 도움이 되는 전이는 긍정적 전이(positive transfer)다. 긍정적 전이는 LTM에 저장된 다른 영역에 대한 정신 모델을 바탕으로 새로운 상황에 대한 정신 모델을 형성하기 때문에 더 빠르게 학습을 할 수 있다. 그에 반해 기존 지식이 새로 배우는 것을 방해하는 부정적 전이(negative transfer)도 존재한다. 이는 보통 기존의 지식을 바탕으로 잘못된 가정을 함으로써 발생한다. 자바에 checked exception이 있으므로 새로 배우는 언어에 무조건 checked exception이 존재할 것이라는 잘못된 가정이 그 예시다.</p>
<h3 data-ke-size="size23"><b>전이의 어려움</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>연구에 의하면 전이는 일어나기 어렵고, 대부분의 사람들에게 전이는 자동으로 이뤄나지 않는다. 텔아비브 대학의 가브리엘 살로몬(Garvriel Salomon)이 실행한 <a href="https://journals.sagepub.com/doi/abs/10.2190/6F4Q-7861-QWA5-8PL1?journalCode=jeca" target="_blank" rel="noopener">연구</a>에 따르면 성공적으로 특정 프로그래밍 기술을 습득한 사람들 중 대부분이 그 기술을 다른 인지 영역으로 전이하지 못했다.</p>
<p data-ke-size="size16">&nbsp; 전이를 활성화 시키기 위해선 새로운 언어를 배울 때, 기존 언어와 유사성이 낮은 언어를 선택하는 것이 좋다. 공통점과 차이점에 의식적으로 주의를 기울이며 새로운 언어를 배우는 것이 좋다.</p>
<h2 data-ke-size="size26"><b>오개념: 생각의 버그</b></h2>
<p data-ke-size="size16">&nbsp; 코드에 대해 잘못된 가정을 할 때 오개념이 발생한다. 오개념은 강한 확신 속에 있는 잘못된 사고방식으로 확신이 강하기 때문에 교정하기 어렵다. 잘못된 생각을 바꾸려면 잘못된 사고방식을 새로운 사고방식으로 바꿀 필요가 있다. 따라서 새로운 프로그래밍 언어를 배울 때는 이전 프로그래밍 언어에 대한 기존 지식을 떨쳐내기 위해 많은 에너지를 소비해야 한다.</p>
<h3 data-ke-size="size23"><b>새로운 프로그래밍 언어를 배울 때 오개념 방지하기</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>새로운 프로그래밍 언어나 기타 기술을 배울 때, 다음과 같은 방식을 이용해 오개념을 방지할 수있다.</p>
<p data-ke-size="size16">&nbsp; - 자신이 틀릴 수도 있다는 사실을 인지하고 열린 마음을 유지하라.</p>
<p data-ke-size="size16">&nbsp; - 흔히 발생하는 오개념에 대해 의도적으로 연구하고, 그런 오개념에 빠지는 것을 방지한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">출처 - 프로그래머의 뇌</p></div>