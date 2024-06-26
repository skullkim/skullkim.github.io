---
layout:       post
title:        "Chapter 1. 프롬프트 엔지니어링은 질문을 잘하는 것이 아니다."
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 프롬프트 엔지니어링
- AI
---

# 1. 프롬프트란 무엇인가?

- 프롬프트란 컴퓨터가 사람에게 보여주기 위해 화면에 띄워 두는 글자를 의미한다.

# 2. 프롬프트 엔지니어링에 대한 저자의 정의

- 통상적으로 프롬프트 엔지니어링이라 하면 질문을 잘하는 방법을 떠올리지만 이것은 오해이다. 질문을 하는 방법 외에도 다양한 기법이 존재하기 때문이다.
- “프롬프트는 컴퓨터가 사용자에게 보여주는 문구다”라는 정의에서 출발해서 LLM 과의 대화를 바라보면 LLM의 응답이 프롬프트라는 것을 알 수 있다. 이 관점에서 프롬프트 엔지니어링을 바라보면 프롬프트 엔지니어링이란 AI의 응답을 사용자가 원하는 방향으로 수정하는 것이다. 원하는 답을 얻기 위한 여러 기법들은 그저 수단에 불과하다.

![prompt](/img/2023-12-23-prompt-engineering-1/img.png)
- 이런 관점은 AI를 기존 프로그램과 다르지 않는 도구로 바라보게 한다. 따라서 AI라는 도구를 활용해 좋은 결과를 만들어 내는 것이 중요하지 과정은 중요하지 않다.

# 3. 프롬프트 엔지니어링에 대한 업계의 통설적 정의

- 업계에서는 저자와 반대로 프롬프트를 사람이 AI에게 제공하는 입력 문구로 정의하고 있다. 이는 GPT-2 논문 영향이 큰데, 해당 논문은 한 번 만들어 둔 언어 모델에게 여러 명령을 바꿔 제공하는 것만으로도 성능과 기능이 달라질 수 있음을 보였다. 여기서 AI에게 지시하는 과정을 설명하면서 프롬프트라는 용어를 사용했다. 그 후 자연어 처리 학계에서 프롬프트라는 단어가 등장하는 빈도가 증가했다.
- 이 관점에서 바라보면 프롬프트 엔지니어링은 AI에 입력하면 좋은 결과를 뽑아낼 수 있는 문구를 설계하는 방법을 고민하고 사례를 기록하고, 실험을 통해 검증하는 과정이다. 이는 AI를 잘 제어하는 명령어를 설계하는 과정과 원리에 더 관심을 둔다는 의미다.

# 모로 가도 서울만 가면 된다

- 어느 정의를 따르던지 프롬프트 엔지니어링은 다음과 같은 프로세스를 따른다.
    - AI에 제공할 명령어를 설계한다
    - 이를 토대로 AI로부터 더 유용한 반응(답변)을 유도한다
    - 더 좋은 방법론을 탐구하고 체계적으로 정리한다

출처 - [프롬프트 엔지니어링](https://product.kyobobook.co.kr/detail/S000209512470)