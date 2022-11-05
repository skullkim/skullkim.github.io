---
layout:       post
title:        "Event driven"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- event-driven
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
                            <p data-ke-size="size16">&nbsp; &nbsp;Event Driven Architecture(EDA)는 분리되어 있는 애플리케이션들이 event broker를 통해 비동기적으로 이벤트들을 구독하고 실행할 수 있는 소프트웨어 디자인패턴이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; EDA는 비즈니스 전반에 걸쳐 이벤트가 발생했을 때 애플리케이션, microservice, 연결된 디바이스 간에 실시간으로 정보가 오고가게 할 수 있도록 지원하는 IT 엔터프라이즈 시스템이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>EDA에서의 event</b></p>
<p data-ke-size="size16">&nbsp; 하나의 서비스에서 발생하능한 모든 일은 이벤트이다. 소비자의 요청, 품목 업데이트, 센서 감지 등. 주어진 이벤트에 대해 대응을 할때 그의 가치는 시간이 지남에 따라 감소한다. 따라서 더 빠르게 필요한 이벤트에 대한 정보를 얻을수록, 기업은 고객만족, 생산전환 등의 기회에 효율적으로 대응할 수 있다. 그때문에 이벤트가 발생 했을 때 정보를 제공하는 EDA는 대부분의 기업이 사용하고 있는 주기적으로 업데이트를 pooling하는 것을 기다리는 API 주도 접근 방식보다 더 나은 접근 방식이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; EDA는 이벤트가 발생했을 때 해당 이벤트에 대한 정보가 필요한 시스템과 사람들에서 전달되는 것을 보증한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; EDA는&nbsp; event broker로 알려진 중간 관리자를 사용해 애플리케이션 간의 loose coupling을 구현한다. 즉, 애플리케이션과 디바이스가 정보를 보내는 곳이나 그들이 사용하는 정보의 출처를 모른다. loose coupling은 문제점이 존재하긴 하나 시스템의 퍼포먼스와 확장성을 크게 향상시킨다. EDA의 이벤트는 이벤트 브로커로 부터 선택적으로 수신을 하는 것을 제외하면 응답방식에 대한 규격을 고려하지 않고 정송한다. 이는 수신자와 송신자 사이의 의존성이 없다는 것을 의미한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Event broker</b></p>
<p data-ke-size="size16">&nbsp; Event broker는 미들웨어이다. Event broker는 publish-subscribe messaging pattern을 사용해 시스템 간의 이벤트들을 라우팅한다. 송신자로부터 이벤트들을 받아서 그 이벤트들을 받을 수 있게 구독된 모든 시스템들에게 전달하는 모든 애플리케이션들은 이벤트 브로커와 연결되 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; publish-subscribe는 애플리케이션들의 decoupling으로 정의된 커뮤티케이션 패턴이다. 애플리케이션들은 직접적으로 소비자들과커뮤니케이션을 하는 것이 아닌 중간에 있는 브로커에게 메시지를 publish한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp; EDA는 시시각각 발생하는 이벤트의 생성, 감지, 반응을 중심으로 구축되기 때문에 현존하는 최고 수준의 복잡성과 역동성에 가장 효율적으로 대응할 수 있는 모델로 평가된다.&nbsp;</p>
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