---
layout:       post
title:        "Digital building block"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- 하드웨어
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
                            <p><b>연산회로</b></p>
<p><b><i>1. 가산(adder)</i></b></p>
<p>&nbsp;&nbsp;<i>Half Adder</i></p>
<p><i>&nbsp; &nbsp;</i></p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="172" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img.png" data-origin-width="0" data-origin-height="0" width="172" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; 두개의 입력(A, B)와 두개의 출력(S, Cout)로 구성되 있다. S는 A, B의 SUM이며 만약 A, B가 모두 1이라면 1비트로 표현할 수 없으므로 Carry out인 Cout으로 나타낸다. Half adder는 XOR과 AND 게이트로 구성할 수 있다. Multi-bit adder에서 Cout은 다음 비트의 MSB에 더해지거나 carried in(Cin)된다. 하지만 Half adder의 경우 Cout을 받을 수 있는 Cin이 존재하지 않는다.&nbsp;</p>
<p><i>Full adder</i></p>
<p>&nbsp; &nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="211" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_1.png" data-origin-width="0" data-origin-height="0" width="211" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp;full adder는 Cin으로 carry in을 받는다 .</p>
<p><i>&nbsp; CPA(Carry Propagate Adder)</i></p>
<p>&nbsp; N-bit adder는 두개의 N-bit 입력 A, B와 Cin을 받고 N-bit result인 S와 Cout을 생산한다. 이를 CPA라 부른다, 왜냐면 한 비트의 carry out이 다음 비트를 propagate(유전)시키기 때문이다.</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="255" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_2.png" data-origin-width="0" data-origin-height="0" width="255" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp;CPA는 다음 세가지 종류로 사용될 수 있다.</p>
<p>&nbsp; &nbsp; &nbsp;1. ripple-carry adders(slow)</p>
<p>&nbsp; &nbsp; &nbsp;2. Carry-lookahead adders(fast)</p>
<p>&nbsp; &nbsp; &nbsp;3. Prefix adders(faster)</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp;Carry-lookahead와 prefix adders는 큰 연산에 대해 빠르게 동작하지만 더 많은 하드웨어를 필요로한다.</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp;Ripple-carry adders</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; 가장 단순한 방식으로 N-bit carry propagate를 만드는 방식으로서 N개의 full adder를 연결시킨형태이다. 이는 Cn이 cn-1에 의존하&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;므로 큰 수의 연산시 속도가 느리다. 이러한 지연은 비트의 개수에 직접적인 영향을 받는다. 이러한 지연을t(ripple)이라 하고 t(FA)는&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 모든 adder의 총 지연시간이다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_3.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="611" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_4.png" data-origin-width="0" data-origin-height="0" width="611" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p><i><b>2. 감산(subtracter)</b></i></p>
<p>&nbsp; 감산은 두번째 숫자의 부호를 반대로 하고 더하는 것이다. 2의 보수를 사용한다.</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="354" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_5.png" data-origin-width="0" data-origin-height="0" width="354" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp;&nbsp;<i><b>3. 비교연산(Comparator)</b></i></p>
<p><i></i>&nbsp; &nbsp;&nbsp;<i>Equality</i></p>
<p><i>&nbsp; &nbsp;&nbsp;</i>&nbsp; Equality는 A, B가 동일한지를 나타내는 하나의 출력을 생산한다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="371" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_6.png" data-origin-width="0" data-origin-height="0" width="371" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp; <i>Less than</i></p>
<p><i>&nbsp; &nbsp; &nbsp;&nbsp;</i>'&lt;'연산은 A - B의 MSB를 보고 판단을 한다. 만약 결과가 음수면 A &lt; B이고 아니면 A &gt;= B이다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="162" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_7.png" data-origin-width="0" data-origin-height="0" width="162" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp;<i><b>4. ALU(Arithmetic/Logical Unit)</b></i></p>
<p>&nbsp; &nbsp; &nbsp;ALU는 다양한 수학적, 논리적 연산을 하나의 유닛으로 만든것이다. ALU는 가감승제, AND, OR등을 수행할 수 있다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="400" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_8.png" data-origin-width="0" data-origin-height="0" width="400" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="310" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_9.png" data-origin-width="0" data-origin-height="0" width="310" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp;<i><b>5. Shifter, Rotator</b></i></p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="562" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_10.png" data-origin-width="0" data-origin-height="0" width="562" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="493" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_11.png" data-origin-width="0" data-origin-height="0" width="493" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="591" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_12.png" data-origin-width="0" data-origin-height="0" width="591" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp;<i><b>6. Multipliers</b></i></p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="507" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_13.png" data-origin-width="0" data-origin-height="0" width="507" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="510" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_14.png" data-origin-width="0" data-origin-height="0" width="510" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p><b>Counter</b></p>
<p>&nbsp; N-bit binary counter는 클럭, 리셋입력돠 N-bit 출력인 Q를 가지는 순차 산술 회로(sequential arithmetic circuit)이다. 리셋은 출력을 0으로 초기화 한다. 카운터는 가능한 모든 2^N개의 출력을 이진순서로 진행해 클럭의 상승 엣지에서 증가시킨다.</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="398" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_15.png" data-origin-width="0" data-origin-height="0" width="398" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p><b>Memory Arrays</b></p>
<p>&nbsp; 위에서는 산술과 순차회로에 대해 다루었다. 디지털 시스템은 이러한 회로들에 의해 나타내어지고, 사용되는 데이터를 저장하기 위해 메모리를 필요로 한다. Flip-flops로 만들어진 레지스터들역시 일종의 메모리로 적은 양의 데이터를 담는다. Memory arrays는 효과적으로 큰 양의 데이터를 저장할 수 있다.</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="253" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_16.png" data-origin-width="0" data-origin-height="0" width="253" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; 위 그림은 전형적인 memory array의 symbol을 보여준다. 이 메모리는 memory cell의 2차원 배열로 조직되어 있다. 이 메모리는 배열의 행 중 한 행의 내용에 대해 일기, 쓰기를 한다. 이 행들은 주솟값(address)에 의해 특정된다. 읽고 쓰여지는 값들은 데이터라 부른다. N-bit주소값과 M-bit데이터를 가지고 있는 배열은 2^N개의 행과 M개의 열을 가지고 있다. 각 행에 있는 데이터를 word라 부르기에 배열은 2^N개의 M-bit word들을 가지고 있다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="391" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_17.png" data-origin-width="0" data-origin-height="0" width="391" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; 여기서 width또는 word size는 배열의 열 갯수, depth는 배열의 행 갯수, 배열의 size는 width * depth이다</p>
<p><b>Bit cells</b></p>
<p>&nbsp; Memory arrays는 bit cell들의 배열로 만들어져 있다. 각 bit cell은 1비트의 데이터를 담고 있다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="320" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_18.png" data-origin-width="0" data-origin-height="0" width="320" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; 위 그림에서 볼수있듯이 각 bit cell은 하나의 wordline과 하나의 bitline에 연결되 있다. 따라서 wordline이 1이면 저장된 비트가 bitline으로 욺겨진다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" width="455" height="NaN" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RGlnaXRhbCBidWlsZGluZyBibG9jaw==/img_19.png" data-origin-width="0" data-origin-height="0" width="455" height="NaN" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>&nbsp; &nbsp; wordline은 메모리에 있는 하나의 행이 한번에 읽혀지고 쓰여지게 한다. 각 wordline은 유니크한 주소값에 대응된다. 한번에 하나의 wordline만 high일 수 있다.</p>
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