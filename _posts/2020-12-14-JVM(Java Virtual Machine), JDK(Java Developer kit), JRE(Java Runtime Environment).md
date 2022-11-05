---
layout:       post
title:        "JVM(Java Virtual Machine), JDK(Java Developer kit), JRE(Java Runtime Environment)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- java
- JVM
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
                            <p>JVM, JDK, JRE에 대해 설명하기 전에 우선 자바 파일이 어떻게 실행되는지를 먼저 보자</p>
<p>&nbsp; .java확장자를 가진 파일로 자바 코드를 작성한다</p>
<p>&nbsp; 프로그램은 바이트코드로 컴파일 되고 자바 컴파일러(javac)는 소스코드를 .class확장자를 가진 파일로 컴파일한다.</p>
<p>&nbsp; 이 클래스 파일은 JVM을 활용해 어느 플랫폼에서든 실행할 수 있다</p>
<p>&nbsp; JVM은 바이트 코드를 해당 플랫폼이 실행할 수 있는 native machine code로 변환한다.</p>
<p><b>JVM</b></p>
<p>&nbsp; Java Virtual Machine은 java bytecode를 실행하는 가상 머신이다. 이 bytecode는 .java파일을 .class파일로 컴파일링했을때 .class파일안에 내장되게 된다. 즉, JVM은 자바 바이트코드가 실행되는 런타임 환경을 제공하는 명세서이다.&nbsp;</p>
<p>&nbsp; JVM은 여러 발전된 기술을 사용해 자바 애플리케이션의 퍼포먼스를 최적화 하며 이를 위해 state-of-the-art memory모델, garbage collector, adaptive optimizer를 결합해 사용한다.&nbsp;</p>
<p>&nbsp; JVM은 client, server에 대해 조금 다름 작동 방식을 제공한다. Server VM의 경우 최대 연산 속도에 초점을 맞추었다. 빠른 시작 시간보단 빠른 연산이 필요한 long-running server apllication들의 실행에 초점이 맞춰져 있다. 개발자는 -client, -server를 명시함으로써 둘 중 하나를 선택할 수 있다.</p>
<p>&nbsp; JVM이 virtual이라 불리는 이유는 운영체제와 하드웨어 아키텍쳐에 의존하지 않는 machine interface를 제공하기 때문이다. 이는 자바자 가지고 있는 특징 중 하나인 write-once-run-anywhere에 대한 초석이다.</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SlZNKEphdmEgVmlydHVhbCBNYWNoaW5lKSwgSkRLKEphdmEgRGV2ZWxvcGVyIGtpdCksIEpSRShKYXZhIFJ1bnRpbWUgRW52aXJvbm1lbnQp/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>JVM Architecture</figcaption>
</figure><p></p>
<p>Class loader</p>
<p>&nbsp; class loader는 클래스 파일들을 로딩하는데 사용되는 서브시스템이다. 이는 세가지 함수로 이루어져있다</p>
<p>&nbsp; 1. Loading</p>
<p>&nbsp; &nbsp; JVM은 세가지 클래스 로더를 가지고있다. Bootstrap, extionsion, application</p>
<p>&nbsp; &nbsp; 클래스를 로딩할때 JVM은 일부 클래스들을 위한 의존성을 찾는다</p>
<p>&nbsp; &nbsp; bootstrap classloader는 클래스를 찾는다. 이는 JRE lib폴더에있는 rt.jar을 스캔한다</p>
<p>&nbsp; &nbsp;만일 클래스를 찾지 못했다면 extention classloader가 jre/lib/ext폴더에 있는 클래스를 검색한다</p>
<p>&nbsp; &nbsp;이때도 클래스를 찾지 못했다면 application classholder가 시스템의 CLASSPATH환경변수에 있는 모든 jar파일과 클래스들을 찾는다.</p>
<p>&nbsp; &nbsp;모든 로더가 클래스를 찾지 못했다면 클래스는 class loader에 의해 로드되거나 ClassNotFoundException을 throw한다.</p>
<p>&nbsp; 2. Linking</p>
<p>&nbsp; &nbsp; classloader에 의해 크래스가 로드된 후, linking을 시작한다. 여기에선 Bytecode verifier가 바이트코드가 적합한지를 판단하며 적합하지 않다면 verification error를 반한다. 또 한 클래스에서 찾은 클래스 변수와 메서드에 대해 메모리 할당을 한다.</p>
<p>3. Initialization</p>
<p>&nbsp; &nbsp; class loader의 마지막 과정이다. 여기서는 모든 클래스 변수가 original values로 할당되며 static block이 실행된다.</p>
<p>&nbsp;</p>
<p>JVM Memory area</p>
<p>&nbsp; JVm memory area는 각 파트가 특정 애플리케이션 데이터를 담기위해 여러 파트로 나뉘어져있다.</p>
<p>&nbsp; 1. Method Area</p>
<p>&nbsp; &nbsp; meta data, constant runtime pool, 메서드에 대한 코드같은 클래스구조들을 담는다</p>
<p>&nbsp; 2. Heap</p>
<p>&nbsp; &nbsp; 애플리캐이션 실행시에 만들어지는 모든 객체들을 담는다</p>
<p>&nbsp; 3. Stacks</p>
<p>&nbsp; &nbsp; 로컬변수, 중간 별과(intermediate results)를 담는다. 모든 값들은 그 값들이 만들어진 스레드에 위치한다. 각 그레드는 각자의 JVM stack을 가지고 있고 이는 스레드의 생성과 비슷한 과정으로 생성된다. 따라서 이런 모든 로컬 변수들을 thread-local variables라 부른다</p>
<p>&nbsp; 4. PC register</p>
<p>&nbsp; &nbsp; 현재 실행되는 각 statement의 물리적 주소를 저장한다. 자바에선 각 그레드가 그들만의 PC register를 가지고 있따.</p>
<p>&nbsp; 5. Native Method stacks</p>
<p>&nbsp; &nbsp; 자바는 low-level code인 C, C++같은 native코드를 지원한다. 이는 Native Method stack이 관리한다</p>
<p>JVM Execution Engine</p>
<p>&nbsp; JVM에 할당되는 모든 코드는 execution engine에 의해 실행된다. execution engine은 바이트 코드를 읽고 하나씩 실행한다. 이는 내부에 있는 두개의 interpreter와 JIT 컴파일러를 사용해 바이트 코드를 machine code로 변환하고 실행시킨다.&nbsp;</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SlZNKEphdmEgVmlydHVhbCBNYWNoaW5lKSwgSkRLKEphdmEgRGV2ZWxvcGVyIGtpdCksIEpSRShKYXZhIFJ1bnRpbWUgRW52aXJvbm1lbnQp/img_1.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>Plaform Dpecifics Interpreters</figcaption>
</figure><p></p>
<p>JVM에서 interpreter와 compiler는 모두 native code를 돌출하지만 어떠한 방식으로 native code를 돌출하는지, 얼마으 비용을 사용해 코드를 최적화 하는지에 차이점이 있다</p>
<p>&nbsp;</p>
<p>Interpreter</p>
<p>&nbsp; JVM interpreter는 machine instruction mapping으로 사전에 정의된 JVM-instruction을 사용해 각 byte-code instruction을 관련있는 native instruction으로 변환한다. 이는 직접적으로 바이트코드를 실행시키고 어떠한 최적화돋 하지 않는다.</p>
<p>JIT Compiler</p>
<p>&nbsp; 퍼포먼스 향샹을 위해 JIT 컴파일러는 런타임에서 JVM과 상호작용을 하고 적절한 바이트코드를 native machine code로 컴파일한다. 통상적으로 JIT컴파일러는 코드를 한 블럭씩(인터프리터 처럼 각 문을 한번에 가져오지 않는다) 가져와 최적화시키고 이를 최적화된 machine code로 변환한다</p>
<p>&nbsp; JIT 컴파일러는 디폴트로 활성화 되어있고 만약 자바 프로그램을 interpret하게 실행할 거면 이를 비활성화 시키면 된다. 만약 프로그램을 진단하거나 JIT compilation problem들을 면하고 싶으면 이를 비활성화 시키지 않는것이 좋다.</p>
<p>&nbsp;</p>
<p>JRE</p>
<p>&nbsp; Java Runtime Environment는 libraries(jars), JVM, 자바 애플리케이션을 실행하는데 필요한 다른 요소들을 포함하는 소프트웨어 패키지이다. JVM은 JRE의 한 부분이다.</p>
<p>&nbsp; JRE을 설치하는것은 모든 컴퓨터에서 자바 애플리케이션을 실행가능하게 하기위한 최소한의 요구사항이다.</p>
<p>&nbsp; JRE는 아래와 같은 요소를 포함하고있다</p>
<p>&nbsp; &nbsp; 1. java HotSpot Client Virtual Machine에 사용되는 DLL파일</p>
<p>&nbsp; &nbsp; 2. java HotSpot Server Virtual Machine에 사용되는 DLL파일</p>
<p>&nbsp; &nbsp; 3. java 런타임 환경에 사용되는 코드 라이브러리, 올바른 세팅, 리소스파일.(rt.jar, charsets.jar 등)</p>
<p>&nbsp; &nbsp; 4. java확장 파일(localedata.jar 등)</p>
<p>&nbsp; &nbsp; 5. 보안 관리에 사용되는 파일들. 이 파일들은 Security Policy(java.policy)와 Security properties(java.security)파일들을 포함한다.</p>
<p>&nbsp; &nbsp; 6. applet을 위한 서포트 클래스를 포함한 jar파일</p>
<p>&nbsp; &nbsp; 7. 플랫폼에서 사용되는 TrueType font file</p>
<p>&nbsp; JRE는 JDK의 한 부분으로 또는 개별적으로 다운로드할 수 있다.</p>
<p>&nbsp; JRE는 플랫폼에 의존적이기때문에 이를 사용할 기기의 운영체제와 아키텍쳐에 따라 적절한 JRE번들을 선택해 설치하고 적용해야한다.</p>
<p>&nbsp;</p>
<p>JDK</p>
<p>&nbsp; JRE의 결합체이다. JDK는 JRE가 가지고 있는 개발, 디버깅, 자바 애플리케이션 모니터링을 위한 개발 툴들을 포함하고있다. JDK는 자바 애플리케이션을 개발하기 위해 필수불가결하다.</p>
<p>&nbsp; 아래는 JDK가 포함하는 일부 중요한 요소들이다</p>
<p>&nbsp; &nbsp; 1. appletviewer: 웹브라우저없이 java applet을 디버깅하고 실행할 수 있다.</p>
<p>&nbsp; &nbsp; 2. apt: 어노테이션 프로세싱툴</p>
<p>&nbsp; &nbsp; 3. extcheck: jar파일들의 충돌을 찾아낸다</p>
<p>&nbsp; &nbsp; 4. javadoc: documentation generator이다. 자동적으로 소스코드 주석들에서 문서를 생성한다</p>
<p>&nbsp; &nbsp; 5. jar: 압축기이다. 패키지들에 연관된 클래스 라이브러리들을 하나의 jar파일로 파키징한다. 이 툴은 jar파일들을 관리하는데 사용된다.</p>
<p>&nbsp; &nbsp; 6. jarsinger: jar서명과 검증 툴</p>
<p>&nbsp; &nbsp; 7. javap: class file disassembler</p>
<p>&nbsp; &nbsp; 8. javaws: JNLP 애플리케이션들을 위한 java web start launcher</p>
<p>&nbsp; &nbsp; 9: Jconsole: 자바 모니터링, 관리툴</p>
<p>&nbsp; &nbsp; 10. jhat: 자바힙 관찰툴</p>
<p>&nbsp; &nbsp; 11. jrunscript: java command-line script shell</p>
<p>&nbsp; &nbsp; 12. jstack: 자바 스레드의 자바 스택 추적을 프린트하는 유틸리티</p>
<p>&nbsp; &nbsp; 13. keytool: 키저장소를 활용하기위한 툴</p>
<p>&nbsp; &nbsp; 14. policytool: 정책 생성과 관리를 위한 툴</p>
<p>&nbsp; &nbsp; 15. xjc: JAXB(Java API for XML Binding)의 일부 API, XML 스키마를 받고 자바 클래스들을 도출한다.</p>
<p>&nbsp;</p>
<p>&nbsp; JRE처럼 JDK역시 플랫폼에 의존적이다.</p>
<p>&nbsp;</p>
<p>JDK, JRE, JVM의 차이점</p>
<p>JRE = JVM + 자바 애플리케이션을 실행하기 위한 라이브러리들</p>
<p>JDK = JRE + 자바 애플리케이션을 개발하기위한 툴들</p>
<p></p><figure class="imageblock widthContent" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/SlZNKEphdmEgVmlydHVhbCBNYWNoaW5lKSwgSkRLKEphdmEgRGV2ZWxvcGVyIGtpdCksIEpSRShKYXZhIFJ1bnRpbWUgRW52aXJvbm1lbnQp/img_2.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption>JDK VS JRE VS JVM</figcaption>
</figure><p></p>
<p>&nbsp; 자바를 통한 개발을 하기 위해선 JDK를 설치해야하고 단지 JAVA 애플리케이션들을 실행하고싶다면 JRE만 설치하면 된다</p>
<p>&nbsp;</p>
<p>번외</p>
<p>1. 클래스로더가 어떻게 작동하는가</p>
<p>&nbsp; 클래스로더는 jar파일들과 클래스들에 대한 사전에 정의된 위치를 스캔한다. 이 경로에 있는 요청된 모든 클래스를 보고 스캔한다. 만약 찾았다면 클래스파일을 load, link, initilialize한다.</p>
<p>2. JRE와 JVM의 차이</p>
<p>&nbsp; JVM은 자바 애플리케이션드을 실행하는 런타임환경을 위한 명세서이다. Hotspot JVM이 이 명세서의 사용 예시다. 이는 클래스파일들을 로드하고 interpreter와 JIT 컴파일러로 바이트코드를 machine coded로 변환하고 실행한다.</p>
<p>3. interpreter와 JIT compiler의 차이</p>
<p>&nbsp; 인터프리터는 바이트코드의 라인 하나를 interpret하고 실행하기를 반복한다. 이의 퍼포먼스는 그닥 좋지않다. JIT compiler의 경우 바이트코드에 대해 코드를 블럭단위로 검사해 최적화를 시키고 이에 대해 더 많은 최적화된 machine code를 준비한다.&nbsp;</p>
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