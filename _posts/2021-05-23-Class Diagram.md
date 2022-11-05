---
layout:       post
title:        "Class Diagram"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- 소프트웨어공학
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
                            <p data-ke-size="size16">-클래스, 인터페이스, 이들의 연관 관계를 표현하며 정적 객체 모델링에 사용된다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="1548" data-origin-height="1276" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img.png" data-origin-width="1548" data-origin-height="1276" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">위그림에서 가장 큰 사각형같은 모양으로 클래스를 표시한다. 3개의 작은 사각형으로 나뉘어져있고 첫번째 사각형에는 클래스의 이름, 두번째에는 속성, 세번째에는 메서드가 들어간다. 클래스, 인터페이스, 유스케이스, 액터를 이를 통해 표현한다</p>
<p data-ke-size="size16">&nbsp; 클래스가 추상 클래스인 경우 이탈릭체 또는 {abstract}라는 표기로 표기한다.</p>
<p data-ke-size="size16">&nbsp; 패키지를 표기할 경우 ::를 사용하거나 자바 프로그래밍 시에 사용하는 방식을 사용한다.ex). java.awt.font, java.awt::font</p>
<p data-ke-size="size16">&nbsp; 각 메서드, 속성의 앞에 특정 기호로 접근 권한을 표기한다(-private, +public, #protected, ~default)</p>
<p data-ke-size="size16">&nbsp; 속성의 맨 뒤에 타입을 기술한다&nbsp;</p>
<p data-ke-size="size16">&nbsp; 속성의 맨 앞에 /가 있을 경우 다른 값으로 부터 유도되는 값임을 의미한다</p>
<p data-ke-size="size16">&nbsp; static의 경우 믿줄로 표기한다</p>
<p data-ke-size="size16">&nbsp; 매개변수가 있을 경우 (매개변수 이름 : 타입)으로 표기한다</p>
<p data-ke-size="size16">&nbsp; 리턴 타입이 있으면 메서드 맨 뒤에 표기한다 ex)+ func(a: int) : int</p>
<p data-ke-size="size16">&nbsp; final method는 메서드 뒤에 {leaf}를 추가한다</p>
<p data-ke-size="size16">&nbsp; 추상 메서드의 경우 메서드 뒤에 {abtract}로 표기한다&nbsp;</p>
<p data-ke-size="size16">&nbsp; 생략: ...으로 표시</p>
<p data-ke-size="size16">&nbsp; 없음 또는 미정: 빈칸</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>클래스 간의 관계</b></p>
<p data-ke-size="size16">&nbsp; 상속: 속이 빈 삼각형, 실선</p>
<p data-ke-size="size16">&nbsp; 인터페이스: &lt;&lt;interface&gt;&gt;로 표시, 속이 빈 삼각형, 점선</p>
<p data-ke-size="size16">&nbsp; 의존관계(약한 의존관계): 점선, 열린 삼각형</p>
<p data-ke-size="size16">&nbsp; association: 실선, 열린 삼각형</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>속성 표기법:</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>텍스트 이용:</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp;데이터 타입, 데이터 자체를 표시하는 객체에 이용</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="1706" data-origin-height="326" width="671" height="128" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_1.png" data-origin-width="1706" data-origin-height="326" width="671" height="128" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption>&nbsp; 이름, 타입 명시&nbsp;</figcaption>
</figure><p></p>
<p data-ke-size="size16">선 이용:</p>
<p data-ke-size="size16">&nbsp; &nbsp; 객체에 이용</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="620" data-origin-height="229" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_2.png" data-origin-width="620" data-origin-height="229" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter" data-origin-width="1768" data-origin-height="380" width="651" height="140" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_3.png" data-origin-width="1768" data-origin-height="380" width="651" height="140" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption>&nbsp; &nbsp;Register가 갖는 Sale의 이름을 직선 아래에 명시</figcaption>
</figure><p></p>
<p data-ke-size="size16">둘 다 이용:&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="1652" data-origin-height="264" width="617" height="99" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_4.png" data-origin-width="1652" data-origin-height="264" width="617" height="99" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">속성 텍스트 표기법의 완전 형식: 가시성 속성이름:</p>
<p data-ke-size="size16">&nbsp; &nbsp; 타입 [다중성]=초기값 {프로퍼티 문자열}, ex) - func: String [*] = null {readonly}</p>
<p data-ke-size="size16">다중성 표기법:</p>
<p data-ke-size="size16">&nbsp; 다중성: 하나의 객체와 연관을 맺는 객체의 수</p>
<p data-ke-size="size16">&nbsp; &nbsp; [1]: 1개</p>
<p data-ke-size="size16">&nbsp; &nbsp; [N]: N개</p>
<p data-ke-size="size16">&nbsp; &nbsp; [0...*]: 0개 이상</p>
<p data-ke-size="size16">&nbsp; &nbsp; [0...1]: 0아니면 1</p>
<p data-ke-size="size16">프로퍼티:</p>
<p data-ke-size="size16">&nbsp; 한 요소의 특징을 표시하는 명명된 값이다</p>
<p data-ke-size="size16">&nbsp; {ordered}: 정렬이 되있다</p>
<p data-ke-size="size16">&nbsp; {List}: 리스트를 사용</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>노트 기호:</b></p>
<p></p><figure class="imageblock alignCenter" data-origin-width="166" data-origin-height="183" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_5.png" data-origin-width="166" data-origin-height="183" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; -UML메모나 주석</p>
<p data-ke-size="size16">&nbsp; -설명하고자 하는 대상과 노트 기호는 점선으로 연결</p>
<p data-ke-size="size16">&nbsp; -UML 제약 사항 {...} ex) {size &gt; 0}</p>
<p data-ke-size="size16">&nbsp; -메서드 몸체: UML오퍼레이션의 구현을 표기</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">UML의 오퍼레이션 형식:</p>
<p data-ke-size="size16">&nbsp; 가시성 이름(매개변수-리스트): 반환타입{프로퍼티-문자열}</p>
<p data-ke-size="size16">클래스 다이어그램에서 메서드를 표현하는 방식</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="2140" data-origin-height="438" width="611" height="125" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_6.png" data-origin-width="2140" data-origin-height="438" width="611" height="125" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><b>의존관계:</b></p>
<p data-ke-size="size16">&nbsp; 점선에 열린, 휘어진 화살표로 표시</p>
<p data-ke-size="size16">&nbsp; 클라이언트 요소(클래스, 패키지, 등)가 다른 공급자 요소에 대한 정보(지식)을 가지고 있어서 공급자의 변화가 클라이언트에게도 영향을 주는 관계 -참조를 의미</p>
<p data-ke-size="size16">&nbsp; 클라이언트에서 공급자에게로 점선 화살표를 연결(좁은 의미에서의 의존관계)</p>
<p data-ke-size="size16">&nbsp; 의존관계는 결합도의 한 상태</p>
<p data-ke-size="size16">넓은 범위의 의존관계:</p>
<p data-ke-size="size16">&nbsp; 클래스 다이어그램의 주요 의존관계:</p>
<p data-ke-size="size16">&nbsp; &nbsp; -공급자 타입(supplier type)을 속성으로 가지는 경우</p>
<p data-ke-size="size16">&nbsp; &nbsp; -공급자에게 메시지를 보내는 경우(연관)</p>
<p data-ke-size="size16">&nbsp; &nbsp;</p>
<p data-ke-size="size16">인터페이스 표기법:</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="2146" data-origin-height="1318" width="669" height="411" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_7.png" data-origin-width="2146" data-origin-height="1318" width="669" height="411" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Composition관계</b></p>
<p data-ke-size="size16">&nbsp; -하나의 클래스가 다른 클래스를 필드로 포함하는 관계</p>
<p data-ke-size="size16">&nbsp; -클래스 내에서 포함할 클래스의 객체를 인스턴스화하고 해당 클래스가 제공하는 기능들을 사용</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="434" data-origin-height="658" width="208" height="315" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_8.png" data-origin-width="434" data-origin-height="658" width="208" height="315" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; aggregation은 마름모가 비어있다</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>association관계</b></p>
<p data-ke-size="size16">&nbsp; -특정 클래스가 다른 클래스의 참조 정보 필드를 이용, 다른 클래스의 기능 사용</p>
<p data-ke-size="size16">&nbsp; -클래스 내부에서 다른 클래스의 인스턴스를 생성하지는 않는다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="456" data-origin-height="636" width="168" height="234" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_9.png" data-origin-width="456" data-origin-height="636" width="168" height="234" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption>B가 A에 의존한다</figcaption>
</figure><p></p>
<p data-ke-size="size16"><b>dependency 관계</b></p>
<p data-ke-size="size16">&nbsp; -특정 클래스가 다른 클래스의 참조 정보를 일시적으로 사용해 다른 클래스의 기능을 사용</p>
<p data-ke-size="size16">&nbsp; -한 클래스의 메서드가 다른 클래스이 객체를 인자로 받아 그 메서드를 사용하는 경우가 가장 일반적&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="434" data-origin-height="618" width="229" height="326" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xhc3MgRGlhZ3JhbQ==/img_10.png" data-origin-width="434" data-origin-height="618" width="229" height="326" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<pre id="code_1621774833879" class="java" data-ke-language="java" data-ke-type="codeblock"><code>//A-B: composition
//A-C:aggregation
//A-D:association
//A-E:dependency
class A{
 B b;
 C c;
 D d;
 public A(){
 	b = new B();
 }
 public A(C c){
 	this.c = c;
 }
 public void setValue(D d){
 	this.d = d;
 }
 public E isDependency(E e){
 	return e.isDependency();
 }
}</code></pre>
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