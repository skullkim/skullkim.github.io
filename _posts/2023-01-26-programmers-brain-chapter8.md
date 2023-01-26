---
layout:       post
title:        "Chapter 8. 명명을 잘 하는 방법"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프로그래머의 뇌
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16">&nbsp; 좋은 이름을 사용하면 LTM을 활성화하여 코드 도메인에 대해 이미 알고 있는 관련 정보를 찾을 수 있다. 반면, 나쁜 이름은 코드에 대한 잘못된 추측을 하게 하고 오개념을 유발한다.</p>
<h2 data-ke-size="size26"><b>이름이 중요한 이유</b></h2>
<p data-ke-size="size16">&nbsp; 클래스나 자료구조가 수행하는 모든 작업을 모호하지 않은 하나의 단어로 표현하는 것은 쉽지 않은 일이다. 예루살렘 히브리 대학의 전산학과 교수 드로 페이텔슨(Dror Feitelson)의 <a href="https://ieeexplore.ieee.org/document/9018121" target="_blank" rel="noopener">실험</a>에 따르면 두 개발자가 같은 이름을 선택할 확률도 7%에 불과하다. 이름을 짓는 일은 어렵지만, 코드에서 추론하는 객체에 맞는 이름을 고르는 것은 매우 중요하다.</p>
<h3 data-ke-size="size23"><b>명명이 중요한 이유</b></h3>
<p data-ke-size="size16">- 이름은 코드베이스의 상당 부분을 차지한다</p>
<p data-ke-size="size16">- 코드 리뷰 시 이름의 역할</p>
<p data-ke-size="size16">&nbsp; 이름은 코드 내에 존재하지만, 프로그래머들은 코드 리뷰 등 환경에서 이름에 관해 많은 언급을 한다</p>
<p data-ke-size="size16">- 이름은 문서화의 가장 쉬운 형태다</p>
<p data-ke-size="size16">&nbsp;공식 문서가 코드보다 더 많은 정보를 제공하지만, 이름은 코드 베이스 내에서 바로 사용할 수 있기 때문에 일종의 중요한 문서로 가능하다.</p>
<p data-ke-size="size16">- 이름의 표식 역할을 할 수 있음</p>
<p data-ke-size="size16">&nbsp; 변수 이름은 주석문 외에도 코드를 이해하는 데 도움이 되는 중요한 표식이다.</p>
<h3 data-ke-size="size23"><b>명명에 대한 다양한 관점</b></h3>
<p data-ke-size="size16">&nbsp; 어떤 명명법이 좋은가에 대해선 저마다 다른 관점을 가지고 있다. 이 중 몇가지를 살펴보자.</p>
<h4 data-ke-size="size20"><b>좋은 이름은 문법적으로 정의할 수 있다</b></h4>
<p data-ke-size="size16">&nbsp; 좋은 이름은 문법에 기초한 몇 가지 규칙을 지켜야 한다는 관점이다. 영국 오픈 대학교 강사 사이먼 버틀러(Simon Butler)는 변수 이름과 관련해 다음과 같은 이슈 목록을 만들었다.</p>
<p data-ke-size="size16"><b>버틀러의 명명 규약</b></p>
<p data-ke-size="size16">- 비정상적인 대문자 사용 금지, 대문자와 소문자를 표준적이지 않은 방식으로 섞어 쓰지 않는다.</p>
<p data-ke-size="size16">- 연속된 두 개의 밑줄 금지</p>
<p data-ke-size="size16">- 사전 등재 단어 사용</p>
<p data-ke-size="size16">- 단어 수는 4개를 초과하지 않는다</p>
<p data-ke-size="size16">- 의미없이 짧은 단어를 사용하지 않는다</p>
<p data-ke-size="size16">- 열거형 식별자는 알파벳 순서로 선언한다</p>
<p data-ke-size="size16">- 식별자의 시작과 끝에는 밑줄을 사용하지 않는다</p>
<p data-ke-size="size16">- 헝가리언 표기법 등으로 식별자 이름에 타입 정보를 나타내면 안 된다.</p>
<p data-ke-size="size16">- 식별자는 숫자만 나타내는 단어만 사용해선 안된다.</p>
<h4 data-ke-size="size20"><b>이름은 코드베이스 내에서 일관성이 있어야 한다</b></h4>
<p data-ke-size="size16">&nbsp; 좋은 이름은 일관성이 있어야 한다는 주장이다. 유사한 객체에 동일 단어를 사용하면 LTM에 저장된 정보를 더 쉽게 찾을 수 있기에 이 역시 의미 있는 주장이다.</p>
<h3 data-ke-size="size23"><b>초기 명명 관행은 지속적인 영향을 미친다.</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>존슨 홉킨스 대학의 수석연구원 돈 로리(Dawn Lawrie)가 진행한 명명 동향 <a href="https://link.springer.com/article/10.1007/s10664-006-9032-2?awc=26429_1674647161_fbfc2048d075e97ba4e961b9910cb710&amp;utm_medium=affiliate&amp;utm_source=awin&amp;utm_campaign=CONR_BOOKS_ECOM_DE_PHSS_ALWYS_DEEPLINK&amp;utm_content=textlink&amp;utm_term=101248" target="_blank" rel="noopener">조사</a>에서는 다음과 같은 결론이 나왔다.</p>
<p data-ke-size="size16">- 최신 코드는 명명 지침을 더 잘 따른다.</p>
<p data-ke-size="size16">- 하지만 동일한 코드베이스 내에서 명명 관행을 일정하게 유지된다.</p>
<p data-ke-size="size16">- 명명 관행 면에서 작은 코드 베이스와 큰 코드베이스 사이에 차이는 없다.</p>
<p data-ke-size="size16">- 프로그램 개발 초기에 만들어진 식별자의 품질은 계속 유지된다.</p>
<p data-ke-size="size16">&nbsp; 위 결론을 통해 프로젝트 초기 단계에서 사용한 이름을 만드는 방식이 이후로도 계속 사용될 가능성이 높다는 결론이 나왔다.</p>
<p data-ke-size="size16">&nbsp; 깃허브 테스트 사용 현황에 대해서도 비슷한 결론이 지어졌다. 레파지토리에 새로 참여한 사람들은 프로젝트 지침을 읽기보다는 기존 테스트를 보고 수정하는 경우가 많았다. 저장소에 테스트가 있을 때는 새로운 참여자도 테스트를 추가해야 하는 부담을 느끼고 프로젝트가 구성되는 방식을 준수한다.&nbsp;</p>
<h2 data-ke-size="size26"><b>명명의 인지적 측면</b></h2>
<p data-ke-size="size16">&nbsp; 위에서 언급한 좋은 명명에 대한 다양한 관점은 다음과 같이 인지적으로 합당한 이유를 갖는다.</p>
<p data-ke-size="size16">- 문법적으로 비슷한 이름 사용: 이름을 처리할 때 인지 부하가 낮음</p>
<p data-ke-size="size16">- 코드베이스 내에서의 일관성: 청킹을 지원</p>
<h3 data-ke-size="size23"><b>명확한 이름이 LTM에 도움이 된다</b></h3>
<p data-ke-size="size16">&nbsp; 이름을 짓는 다은 것은 올바른 단어 선택 그 이상의 일이다. 인지적 관점에서 선택한 단어는 매우 중요한 역할을 한다. 변수 이름은 다음과 같은 과정을 통해 처리된다.</p>
<p data-ke-size="size16">1. 변수 이름이 감각 기억에 의해 처리되고 STM으로 전송된다.</p>
<p data-ke-size="size16">2. STM은 크기 제한이 있어서 변수 이름을 단어로 구분하려 한다. 이 때, 이름이 체계적일수록 변수명의 각 부분을 식별하기 쉽다.</p>
<p data-ke-size="size16">3. LTM도 관련 사실을 검색한 후 검색된 정보를 작업 기억 공간으로 보낸다. 이때, 올 마른 도메인 이름을 사용하면 코드의 독자가 LTM에서 관련 정보를 찾는 데 도움이 된다.</p>
<h3 data-ke-size="size23"><b>변수 이름은 이해에 도움이 되는 다양한 유형의 정보를 포함할 수 있다</b></h3>
<p data-ke-size="size16">&nbsp; 식별자는 다음과 같은 정보를 표현할 수 있다.</p>
<p data-ke-size="size16">- 코드의 도메인에 대해 생각할 때 이름이 도움이 된다.</p>
<p data-ke-size="size16">- 프로그래밍에 대해 생각할 때도 이름이 도움이 된다. 특정 자료구조 같은 프로그래밍 개념도 LTM에서 정볼르 가져오는 데 일조한다.</p>
<p data-ke-size="size16">- 경우에 따라 변수에 LTM이 이미 알고 있는 규약에 대한 정보가 포함될 수도 있다. 예를 들어 temp라는 변수 이름은 임시 변수를 가리키는데 종종 사용된다.</p>
<h3 data-ke-size="size23"><b>이름의 품질 평가 시기</b></h3>
<p data-ke-size="size16">&nbsp; 문제 해결에 몰두해 있을 때는 높은 인지 부하로 인해 좋은 이름을 짓기 어렵다. 따라서 코딩 이외의 시간에 이름의 품질을 숙고하는 것이 바람직하다. 예컨대 코드 리뷰 중 이름 품질을 검토할 수 있다.</p>
<h2 data-ke-size="size26"><b>어떤 종류의 이름이 더 이해하기 쉬운가?</b></h2>
<h3 data-ke-size="size23"><b>축약할 것인가, 하지 않을 것인가</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>독일 파사우 대학 연구원 요하네스 호프마이스터 연구에 따르면 코드를 이해하고 버그를 쉽게 찾기 위해선 명확한 의미의 단어를 사용해야 하는 반면, 기억을 잘하기 위해선 간결한 약자를 사용해야 한다. 따라서 명확한 의미의 단어와 간결한 단어 사이에서 균형을 잘 잡아야 한다.</p>
<h3 data-ke-size="size23"><b>스네이크 케이스냐, 캐멀 케이스냐?</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>로욜라 대학 메릴랜드의 컴퓨터 과학 교수 데이브 빙클리(Dave Binkley)는 캐멀 케이스 변수와 스네이크 케이스 변수가 프로그램에 적응하는 속도와 정확도에 어떤 영향을 주는지 <a href="http://www.cs.loyola.edu/~binkley/papers/icpc09-clouds.pdf" target="_blank" rel="noopener">조사</a>했다. 그 결과 프로그래머와 일반인 모두 캐멀케이스에서 더 높은 정확도를 보여주었다. 하지만 답을 선택하는 대 더 오랜 시간이 들었다. 또 한, 훈련된 프로그래머는 대부분 캐멀 케이스를 사용했으며, 하나의 식별자 명시 방식만 사용한 사람은 다른 방식으로 된 변수를 볼 때 더 오랜 시간을 소모하는 것으로 나타났다. 따라서 굳이 기존 코드를 바꿀 필요는 없지만 새로 명영 규약을 정한다면 캐멀 케이스가 더 좋은 방식이다.</p>
<h2 data-ke-size="size26"><b>더 나은 변수명에 대한 페이텔슨의 3단계 모델</b></h2>
<p data-ke-size="size16">&nbsp; 페이텔슨은 개발자들이 더 나은 이름을 선택하는 데 도움이 되는 3단계 모델을 설계했다.</p>
<p data-ke-size="size16"><b>1. 이름에 포함할 개념을 선택한다.</b></p>
<p data-ke-size="size16">&nbsp; 이름의 의도를 고려해 포함할 개념을 선택해야 한다. 의도는 개체가 보유한 정보를 서술하고 사용되는 목적을 나타내야 한다.</p>
<p data-ke-size="size16"><b>2. 각 개념을 나타낼 단어를 선택한다.</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>중요한 정의가 기록되 있고 동의어가 등재된 프로젝트 어휘 사전을 만들어 프로그래머가 일관된 이름을 선택하는 데 도움이 되게 한다.</p>
<p data-ke-size="size16"><b>3. 이 단어들을 상용해 이름을 구성한다.</b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">출처 - 프로그래머의 뇌</p>
<p data-ke-size="size16">&nbsp;&nbsp;</p></div>