---
layout:       post
title:        "java bean vs spring bean"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- java
- spring
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
                            <h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>POJO(Plain Old Java Object)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; POJO 는 EJB 처럼 복잡하지 않고, 단순히 객체 만을 이용해 비즈니스 로직을 구현하는 것이다. POJO는 OOP에 충실하면서 환경, 기술에 종속되지 않고, 필요에 따라 재사용할 수 있는 방식으로 설계된 객체이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Java bean</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">자바 빈은 스윙에서 독립적인 GUI 컴포넌트의 개발을 용이하게 하기 위해 고안되었다. 자바 빈은 하나의 객체 내에 여러 객체들이 존재하는 형태이며, 다음과 같은 조건을 만족한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. Serializable를 implements 하고 있어야 한다. 즉, 직렬화할 수 있어야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 디폴트 생성자가 존재해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 자바 빈에 존재하는 모든 프로퍼티(멤버 변수)들은 private 이여야 하며 각 getter와 setter가 public 이어야 한다. </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 즉, getter와 setter를 통해 접근해야 한다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Java bean의 장단점</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 자바 빈의 사용은 다음과 같은 장단점을 가지고 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">장점:</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 프로퍼티, 이벤트, 메서드들을 재사용할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 이벤트 등록</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. HDD와 같은 persistent storage에 저장할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">단점:</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 디폴트 생성자은 올바른 초기화를 보장하지 못한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 자바 빈은 multable이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. getter와 setter 같은 보일러 플레이트가 존재한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Spring Bean</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>스프링 빈은 스프링 IOC 컨테이너가 관리하는 객체이며 BeanDefinition에 의해 생성된다. BeanDefinition은 빈의 프로퍼티들을 나타내며 다음과 같은 메타 데이터를 포함한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 클래스 이름</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 빈의 동작 구성: 스코프, 라이프 사이클 콜백, 등</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 빈이 협력하는 객체, 의존성</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 기타 설정</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>BeanDefinition properties</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. class</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. name</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. scope</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. constructor arguments</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. properties</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 6. autowiring mode</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 7. lazy-initialization mode</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 8. initialization method</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 9. desctruction method</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 자세한 설명은 아래 <a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/config/BeanDefinition.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Java Bean vs Spring bean</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">1. 스프링 빈은 스프링 IoC 컨테이너에 의해 관리되지만 자바 빈은 그렇지 않다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">2. 자바 빈은 반드시 직렬화를 지원해야 하지만, 스프링 빈은 반드시 지원하지 않아도 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">3. 스프링 빈은 디폴트 생성자가 없어도 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">4. 자바 객체는 동시에 자바 빈 이며 POJO이고, 스프링 빈이 될 수 있다.</span></p>
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