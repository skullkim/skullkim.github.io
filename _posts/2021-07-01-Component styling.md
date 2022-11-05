---
layout:       post
title:        "Component styling"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- react
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
                            <p data-ke-size="size16"><b>일반 css</b></p>
<p data-ke-size="size16">&nbsp;그냥 디폴트로 들어 있는 css이다. 사용법은 가장 초기의 src/App.js, App.css를 보면 된다.</p>
<p data-ke-size="size16">&nbsp;Css를 사용할때 가장 중요한것은 css클래스를 중복되지 않게 만드는 거다. 이는 다음과 같은 두개의 방식으로 실천할 수 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. 규칙있는 이름</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; src/App.js초기 로직을 보면 className이 컴포넌트이름-클래스(ex.App-header)형태로 되어 있다. 또 한 BEM naming같은 것을 사용하는 것도 방법이다.</p>
<p data-ke-size="size16"><a href="http://getbem.com/naming/" target="_blank" rel="noopener">http://getbem.com/naming/</a></p>
<figure id="og_1625143060250" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="BEM — Block Element Modifier" data-og-description="BEM is a highly useful, powerful, and simple naming convention that makes your front-end code easier to read and understand, easier to work with, easier to scale, more robust and explicit, and a lot more strict." data-og-host="getbem.com" data-og-source-url="http://getbem.com/naming/" data-og-url="http://getbem.com/" data-og-image="https://scrap.kakaocdn.net/dn/ITDAP/hyKLlJ8NT1/RsKvPi6rxZWZAkwaWKKcOk/img.png?width=400&amp;height=400&amp;face=0_0_400_400,https://scrap.kakaocdn.net/dn/5LEjT/hyKKMCAEhZ/bbquceXDsq1JDJVfmBoj00/img.png?width=1280&amp;height=470&amp;face=0_0_1280_470,https://scrap.kakaocdn.net/dn/g0wkg/hyKLjZRp90/5rSxgDuAPrsp1Tn0RMgewK/img.png?width=600&amp;height=211&amp;face=0_0_600_211"><a href="http://getbem.com/naming/" target="_blank" rel="noopener" data-source-url="http://getbem.com/naming/">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/ITDAP/hyKLlJ8NT1/RsKvPi6rxZWZAkwaWKKcOk/img.png?width=400&amp;height=400&amp;face=0_0_400_400,https://scrap.kakaocdn.net/dn/5LEjT/hyKKMCAEhZ/bbquceXDsq1JDJVfmBoj00/img.png?width=1280&amp;height=470&amp;face=0_0_1280_470,https://scrap.kakaocdn.net/dn/g0wkg/hyKLjZRp90/5rSxgDuAPrsp1Tn0RMgewK/img.png?width=600&amp;height=211&amp;face=0_0_600_211');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">BEM — Block Element Modifier</p>
<p class="og-desc" data-ke-size="size16">BEM is a highly useful, powerful, and simple naming convention that makes your front-end code easier to read and understand, easier to work with, easier to scale, more robust and explicit, and a lot more strict.</p>
<p class="og-host" data-ke-size="size16">getbem.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; 2. Css selector</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; &nbsp; css에서 클래스네임 앞에 .컴포넌트이름을 넣으면 된다</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">.App&nbsp;.logo</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;height</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;10px</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Sass(Syntactically Awesome Style Sheets)</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>문법적으로 매우 멋진 스타일시트란다. 참 이름이 어메이징하다. 아무튼 sass는 css전처리기로 복잡한 작업을 쉽게 할 수 있도록 해주고, 스타일 코드의 재활용성을 높여 줄 뿐만 아니라 가독성을 높여 유지 보수를 쉽게 해준다.</p>
<p data-ke-size="size16">&nbsp; Sass는 .scss, .sass 두가지 확장자를 제공한다. .scss는 세미콜론과, {}를 사용하는 반면 .sass는 사용하지 않는다. 또 한 .scss가 기존 css와 문법이 유사하다</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">//.sass</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">$font-stack</span><span style="color: #4da51b;">:&nbsp;Helvetica</span><span style="color: #ff3399;"></span>,<span style="color: #ff3399;">&nbsp;sans-serif</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">body</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;font</span><span style="color: #4da51b;">:&nbsp;100%&nbsp;$font-stack</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">//.scss</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$font-stack:&nbsp;Helvetica</span><span style="color: #ff3399;"></span>,<span style="color: #ff3399;">&nbsp;sans-serif</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">body&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;font</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;100%&nbsp;$font-stack</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; Sass를 사용하려면 node-sass를 설치해야 한다.&nbsp;</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
<div style="line-height: 130%;">35</div>
<div style="line-height: 130%;">36</div>
<div style="line-height: 130%;">37</div>
<div style="line-height: 130%;">38</div>
<div style="line-height: 130%;">39</div>
<div style="line-height: 130%;">40</div>
<div style="line-height: 130%;">41</div>
<div style="line-height: 130%;">42</div>
<div style="line-height: 130%;">43</div>
<div style="line-height: 130%;">44</div>
<div style="line-height: 130%;">45</div>
<div style="line-height: 130%;">46</div>
<div style="line-height: 130%;">47</div>
<div style="line-height: 130%;">48</div>
<div style="line-height: 130%;">49</div>
<div style="line-height: 130%;">50</div>
<div style="line-height: 130%;">51</div>
<div style="line-height: 130%;">52</div>
<div style="line-height: 130%;">53</div>
<div style="line-height: 130%;">54</div>
<div style="line-height: 130%;">55</div>
<div style="line-height: 130%;">56</div>
<div style="line-height: 130%;">57</div>
<div style="line-height: 130%;">58</div>
<div style="line-height: 130%;">59</div>
<div style="line-height: 130%;">60</div>
<div style="line-height: 130%;">61</div>
<div style="line-height: 130%;">62</div>
<div style="line-height: 130%;">63</div>
<div style="line-height: 130%;">64</div>
<div style="line-height: 130%;">65</div>
<div style="line-height: 130%;">66</div>
<div style="line-height: 130%;">67</div>
<div style="line-height: 130%;">68</div>
<div style="line-height: 130%;">69</div>
<div style="line-height: 130%;">70</div>
<div style="line-height: 130%;">71</div>
<div style="line-height: 130%;">72</div>
<div style="line-height: 130%;">73</div>
<div style="line-height: 130%;">74</div>
<div style="line-height: 130%;">75</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">//sass-component.scss</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">$red</span><span style="color: #4da51b;">:&nbsp;#fa5252;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$orange:&nbsp;#fd7e14;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$yellow:&nbsp;#fcc419;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$green:&nbsp;#40c057;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$blue:&nbsp;#339af0;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$indigo:&nbsp;#5c7cfa;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$violet:&nbsp;#7950f2;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">//믹스인-재사용되는&nbsp;스타일&nbsp;블록을&nbsp;함수처럼&nbsp;사용&nbsp;가능</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">@mixin&nbsp;square($size)&nbsp;</span><span style="color: #ff3399;"></span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;$calculated</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;32px&nbsp;*&nbsp;$size</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;width</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$calculated</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;height</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$calculated</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">.SassComponent&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;display</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;flex</span><span style="color: #ff3399;">;</span><span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;.box&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;red</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;cursor</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;pointer</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;transition</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;all&nbsp;0.3s&nbsp;ease-in</span><span style="color: #ff3399;">;</span><span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.red&nbsp;</span>{<span style="color: #0099cc;">&nbsp;//red&nbsp;class가&nbsp;box와&nbsp;같이&nbsp;사용되었을때</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$red</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(1)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.orange&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$orange</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(2)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.yellow&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$yellow</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(3)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.green&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$green</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(4)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.blue&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$blue</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(5)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.indigo&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$indigo</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(6)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.violet&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$violet</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@include&nbsp;square(7)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&amp;.hover&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;black</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;</span>}<span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">//sass-component.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">import&nbsp;React&nbsp;from&nbsp;'react';</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">import&nbsp;'./sass-component.scss';</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">const&nbsp;SassComponent&nbsp;=&nbsp;</span>(<span style="color: #4da51b;"></span>)<span style="color: #ff3399;">&nbsp;=</span><span style="color: #4da51b;">&gt;</span><span style="color: #ff3399;">&nbsp;</span>{<span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;(</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="SassComponent"&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;red"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;orange"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;yellow"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;green"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;blue"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;indigo"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;div&nbsp;className="box&nbsp;violet"/&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;/div&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;)</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">export&nbsp;default&nbsp;SassComponent;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>utils 함수 분리하기</b></p>
<p data-ke-size="size16">&nbsp; 여러 파일에서 사용 가능한 변수와 믹스인은 별도의 파일로 분리하여 작성하고 필요할때 불러오면 편하다.&nbsp;</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">//utils.scss</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">$red</span><span style="color: #4da51b;">:&nbsp;#fa5252;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$orange:&nbsp;#fd7e14;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$yellow:&nbsp;#fcc419;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$green:&nbsp;#40c057;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$blue:&nbsp;#339af0;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$indigo:&nbsp;#5c7cfa;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">$violet:&nbsp;#7950f2;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">//믹스인-재사용되는&nbsp;스타일&nbsp;블록을&nbsp;함수처럼&nbsp;사용&nbsp;가능</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #4da51b;">@mixin&nbsp;square($size)&nbsp;</span><span style="color: #ff3399;"></span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;$calculated</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;32px&nbsp;*&nbsp;$size</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;width</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$calculated</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;height</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;$calculated</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">//sass-component.scss</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">@import&nbsp;'./utils';</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">//...</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>sass-loader 설정 커스터 마이징</b></p>
<p data-ke-size="size16">&nbsp; 프로젝트 디렉터리가 많아서 구조가 복잡하다면 상대 경로로 파일을 불러오는 것은 좋은 생각이 아니다. 이는 Sass를 처리하는 sass-loader의 설정을 커스터마이징하여 해결할 수 있다. 리액트 앱을 처음 만든 후 프로젝트는 구조의 복잡도를 낮추기 위해 세부 설정을 숨긴다. 이를 커스터 마이징 할려면 yarn eject 또는 npm run eject를 통해 세부 설정을 밖으로 꺼내야 한다. 또 한 이 명령어를 실행하기 전에 모든 파일들이 깃에 커밋되어 있어야 한다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;npm run eject를 실행하면 config라는 디렉터리가 생긴다. config/webpack.config.js에서 sassRegex라는 키워드를 찾자.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;test:&nbsp;sassRegex,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;exclude:&nbsp;sassModuleRegex,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;use:&nbsp;getStyleLoaders(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;importLoaders:&nbsp;<span style="color: #0099cc;">3</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sourceMap:&nbsp;isEnvProduction</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;?&nbsp;shouldUseSourceMap</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;isEnvDevelopment,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">'sass-loader'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;sideEffects:ture,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">},</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">위 부분을 다음과 같이 수정하자</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;test:&nbsp;sassRegex,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;exclude:&nbsp;sassModuleRegex,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;use:&nbsp;getStyleLoaders(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;importLoaders:&nbsp;<span style="color: #0099cc;">3</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sourceMap:&nbsp;isEnvProduction</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;?&nbsp;shouldUseSourceMap</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;isEnvDevelopment,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}).concat({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loader:&nbsp;require.resolve(<span style="color: #63a35c;">'sass-loader'</span>),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;options:&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sassOptions:&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;includePaths:&nbsp;[path.appSrc&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #63a35c;">'/style'</span>]</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sourceMap:&nbsp;isEnvDevelopment&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;shouldUseSourceMap,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;Don't&nbsp;consider&nbsp;CSS&nbsp;imports&nbsp;dead&nbsp;code&nbsp;even&nbsp;if&nbsp;the</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;containing&nbsp;package&nbsp;claims&nbsp;to&nbsp;have&nbsp;no&nbsp;side&nbsp;effects.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;Remove&nbsp;this&nbsp;when&nbsp;webpack&nbsp;adds&nbsp;a&nbsp;warning&nbsp;or&nbsp;an&nbsp;error&nbsp;for&nbsp;this.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;See&nbsp;https://github.com/webpack/webpack/issues/6571</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;sideEffects:&nbsp;<span style="color: #a71d5d;">true</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">},</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">위와 같이 설정하게 되면 scss파일의 경로가 어디에 있더라고 styles 디렉터리 기준 절대 경로로 작동하게 된다. 만약 특정 파일을 디폴트로 넣어주고 싶다면 위 코드에서 sourceMap아래 줄에 다음과 같은 코드를 넣으면 된다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">prependData:&nbsp;`@<span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'utils'</span>;`;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 만약 다음과 같은 에러가 발생한다면 이는 sass-loader의 버전차이로 인해 발생한 오류이니 prependData대신 additionalData를 사용하면 된다&nbsp;</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Error:&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//options&nbsp;has&nbsp;an&nbsp;unknown&nbsp;property&nbsp;'prependData'.&nbsp;These&nbsp;properties&nbsp;are&nbsp;valid:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//&nbsp;&nbsp;&nbsp;object&nbsp;{&nbsp;implementation?,&nbsp;sassOptions?,&nbsp;additionalData?,&nbsp;sourceMap?,&nbsp;webpackImporter?&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//solution:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">additionalData:&nbsp;`@<span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'utils'</span>;`;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>node_modules에서 라이브러리 불러오기 </b></p>
<p data-ke-size="size16">&nbsp; Sass는 라이브러리를 쉽게 불러와 사용할 수 있다. 또 한 node_modules에서 라이브러리를 불러올때는 맨 앞에 '~'를 추가하는 것으로 바로 node_modules에 접근할 수 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 반응형 디자인을 쉽게 만들어 주는 include-media, open-color를 npm으로 설치한 후 다음과 같이 하면 된다. 아래의 코드는 화면 크기가 768px보다 작아지면 배경 색을 바꾼다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//utils.css</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">@<span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'~include-media/dist/include-media'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">@<span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'~open-color/open-color'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//sass-component.scss</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">.SassComponent&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;display:&nbsp;flex;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;background:&nbsp;$oc<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>gray<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">2</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;@include&nbsp;media(<span style="color: #63a35c;">'&lt;768px'</span>)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;$oc<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>gray<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">9</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;.box&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//..</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>CSS module</b><b></b></p>
<p data-ke-size="size16">&nbsp;CSS module은 css를 불러와서 사용할 때 이름을 고유값 [파일 이름]_[클래스 이름]_[해시값]형태로 자동으로 만들어서 컴포넌트 스타일 클래스 이름이 중첩되는 현상을 방지해준다. 따라서 흔한 이름을 사용한다고 해도 문제가 되지 않는다. 해당 클래스는 방금 만든 스타일을 직접 불러온 컴포넌트 내부에서만 작동 된다. '.module.css'라는 확장자를 사용하면 css module을 사용할 수 있다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//css_module.module.css</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">.wrapper&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;black;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;padding:&nbsp;1rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;font<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>size:&nbsp;2rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">/*global&nbsp;css*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">:global&nbsp;.something&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;font<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>weight:&nbsp;<span style="color: #0099cc;">800</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;aqua;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//css_module.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;styles&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'./css_module.module.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CssModule&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{styles.wrapper}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hi,&nbsp;I&nbsp;am&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>span&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"something"</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>CSS&nbsp;module<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>span<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;CssModule;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//CSS&nbsp;Module을&nbsp;사용한&nbsp;클래스&nbsp;이름을&nbsp;두개&nbsp;이상&nbsp;적용시</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div&nbsp;className<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{`${styles.wrapper}&nbsp;${styles.inverted}`}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; scss를 사용할 때는 '.modules.css'대신에 '.modules.scss'를 사용하면 scss를 css module로 사용할 수 있다.</p>
</div>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">/*css_module_scss_module.scss*/<br>.wrapper&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;black</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;padding</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;1rem</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;color</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;white</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;font-size</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;2rem</span><span style="color: #ff3399;">;</span><span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&amp;.inverted&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;color</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;black</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;background</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;white</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;border</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;1px&nbsp;solid&nbsp;black</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;</span>}<span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #4da51b;">:global&nbsp;</span><span style="color: #ff3399;"></span>{<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;.something&nbsp;</span>{<span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;font-weight</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;800</span><span style="color: #ff3399;">;</span><span style="color: #0099cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0099cc;">&nbsp;&nbsp;&nbsp;&nbsp;color</span><span style="color: #ff3399;">:</span><span style="color: #0066cc;">&nbsp;aqua</span><span style="color: #ff3399;">;</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;</span>}<span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; 모듈이 아닌 일반 css, scss파일에서도 :local을 사용해 css module을 정의할 수 있다.</p>
</div>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #4da51b;">:local&nbsp;.wrapper&nbsp;</span><span style="color: #ff3399;"></span>{<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: #999999;">/*style*/</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;"></span><span style="color: #4da51b;">:local&nbsp;</span><span style="color: #ff3399;"></span>{<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;.wrapper&nbsp;</span>{<span style="color: #ff3399;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #ff3399;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: #999999;">/*style*/</span><span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;">&nbsp;&nbsp;&nbsp;&nbsp;</span>}<span style="color: #0066cc;"></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #0066cc;"></span>}</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Styled-components</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>컴포넌트 스타일링은 js 파일 안에서도 할 수 있다. 이를 CSS-in-JS라고 한다. 이를 위한 라이브러리 중 styled-components라는 라이브러리를 가장 많이 사용한다.</p>
<p data-ke-size="size16">&nbsp; CSS-in-JS를 사용하게 되면 별도의 스타일 관련 파일을 만들지 않아도 되기 때문에 큰 이점이 생긴다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
<div style="line-height: 130%;">35</div>
<div style="line-height: 130%;">36</div>
<div style="line-height: 130%;">37</div>
<div style="line-height: 130%;">38</div>
<div style="line-height: 130%;">39</div>
<div style="line-height: 130%;">40</div>
<div style="line-height: 130%;">41</div>
<div style="line-height: 130%;">42</div>
<div style="line-height: 130%;">43</div>
<div style="line-height: 130%;">44</div>
<div style="line-height: 130%;">45</div>
<div style="line-height: 130%;">46</div>
<div style="line-height: 130%;">47</div>
<div style="line-height: 130%;">48</div>
<div style="line-height: 130%;">49</div>
<div style="line-height: 130%;">50</div>
<div style="line-height: 130%;">51</div>
<div style="line-height: 130%;">52</div>
<div style="line-height: 130%;">53</div>
<div style="line-height: 130%;">54</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;"><span style="background-color: #fafafa; color: #999999;">//styled_component.js</span><br>import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;styled,&nbsp;{css}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'styled-components'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><br><span style="background-color: #fafafa; color: #999999;">//div에 스타일링을 해서 Box라는 엘리먼트로 사용한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;Box&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;styled.div&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//props로&nbsp;넣은&nbsp;값을&nbsp;직접&nbsp;전달&nbsp;할&nbsp;수&nbsp;있다<br>//여기에서의 props.color는 아래 Box태그의 color이다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;background:&nbsp;${props&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;props.color&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">|</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">|</span>&nbsp;<span style="color: #63a35c;">'blue'</span>}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;padding:&nbsp;1rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;display:&nbsp;flex;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">`;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;Button&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;styled.button`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;background:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;color:&nbsp;black;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;border<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>radius:&nbsp;4px;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;padding:&nbsp;<span style="color: #0099cc;">0.</span>5rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;display:&nbsp;flex;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;align<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>items:&nbsp;center;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;justify<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #066de2;">content</span>:&nbsp;center;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;box<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>sizing:&nbsp;border<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>box;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;font<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>size:&nbsp;1rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;font<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>weight:&nbsp;<span style="color: #0099cc;">600</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//&amp;를&nbsp;사용해&nbsp;sass처럼&nbsp;자기&nbsp;자신&nbsp;선택&nbsp;가능</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>:hover&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;rgba(<span style="color: #0099cc;">255</span>,&nbsp;<span style="color: #0099cc;">255</span>,&nbsp;<span style="color: #0099cc;">255</span>,&nbsp;<span style="color: #0099cc;">0.</span><span style="color: #0099cc;">9</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//inverted값이&nbsp;참일때&nbsp;특정&nbsp;스타일을&nbsp;부여한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;${(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;<br><span style="background-color: #fafafa; color: #999999;">//styled-components를 사용하면 조건부 스타일링을 <br>//간단하게 props로 처리할 수 있다.</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;props.inverted&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;css&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;none;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;border:&nbsp;2px&nbsp;solid&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>:hover&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;black;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;button&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;margin<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>left:&nbsp;1rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">`;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;StyledComponent&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;(<br><span style="background-color: #fafafa; color: #999999;"> //위에서 스타일링을 한 div</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Box&nbsp;color<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{<span style="color: #63a35c;">"black"</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>Hello<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>Button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Button&nbsp;inverted<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{<span style="color: #0099cc;">false</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>테두리만<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>Button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>Box<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;StyledComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">&nbsp;</div>
</div>
</td>
<td style="padding: 6px 0px; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;"><span style="background-color: #fafafa; color: #999999;">&nbsp;</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0px 2px 4px 0px;"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">&nbsp;</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; 위 코드 중 아래의 코드의 경우 css가 아닌 문자열로 주어도 동작은 가능 하다. 하지만 문자열로 처리를 할 경우 vs code확장 프로그램에서 syntax highlighting이 제대로 안된다. 또 한 함수를 받아와 사용하지 못해서 해당 부분에서는 props값을 사용하지 못한다.</p>
</div>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">${(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//styled-components를&nbsp;사용하면&nbsp;조건부&nbsp;스타일링을&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//간단하게&nbsp;props로&nbsp;처리할&nbsp;수&nbsp;있다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;props.inverted&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;css&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;none;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;border:&nbsp;2px&nbsp;solid&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>:hover&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;black;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//위&nbsp;코드&nbsp;대신</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">${(props)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//styled-components를&nbsp;사용하면&nbsp;조건부&nbsp;스타일링을&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//간단하게&nbsp;props로&nbsp;처리할&nbsp;수&nbsp;있다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;props.inverted&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;none;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;border:&nbsp;2px&nbsp;solid&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>:hover&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;white;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;black;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="color: #010101;"><span>&nbsp;</span>스타일링된 엘리먼트는 위의 Box와 같은 방법으로 만들어가 아래에 있는 방식으로 만들 수 있다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//태그의&nbsp;타입을&nbsp;styled&nbsp;함수의&nbsp;인자로&nbsp;전달한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;MyInput&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;styled(<span style="color: #63a35c;">'input'</span>)`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;background:&nbsp;gray;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//아예&nbsp;컴포넌트&nbsp;형식의&nbsp;값을&nbsp;넣어&nbsp;준다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;StyledLink&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;styled(Link)`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;color:&nbsp;blue;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>반응형 디자인</b></p>
<p data-ke-size="size16">&nbsp; styled-components에서 반응형 디자인을 하기 위해서는 media 쿼리를 사용하면 된다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//위&nbsp;코드의&nbsp;Box부분을&nbsp;다음과&nbsp;같이&nbsp;바꾼다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;Box&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;styled.div&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//props로&nbsp;넣은&nbsp;값을&nbsp;직접&nbsp;전달&nbsp;할&nbsp;수&nbsp;있다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;background:&nbsp;${props&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;props.color&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">|</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">|</span>&nbsp;<span style="color: #63a35c;">'blue'</span>};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;padding:&nbsp;1rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;display:&nbsp;flex;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;width:&nbsp;1024px;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;margin:&nbsp;<span style="color: #0099cc;">0</span>&nbsp;auto;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;@media&nbsp;(max<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>width:&nbsp;1024px)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;width:&nbsp;768px;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;@media&nbsp;(max<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>width:&nbsp;768px)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;width:&nbsp;<span style="color: #0099cc;">100</span>%;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">`;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 하지만 이와 같은 방식은 여러 컴포넌트가 있을때 귀찮을 수 있다. 이때는 다음과 같이 styled-components에서 제공하는 유틸함수를 사용하면 media 쿼리가 자동으로 만들어 진다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;styled,&nbsp;{css}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'styled-components'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;sizes&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;desktop:&nbsp;<span style="color: #0099cc;">1024</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;tablet:&nbsp;<span style="color: #0099cc;">768</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//위에&nbsp;있는&nbsp;size객체에&nbsp;따라&nbsp;자동으로&nbsp;media&nbsp;query&nbsp;함수를&nbsp;만들어&nbsp;준다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;media&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">Object</span>.keys(sizes).reduce((acc,&nbsp;label)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;acc[label]&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(...args)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;css&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@media&nbsp;(max<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>width:&nbsp;${sizes[label]&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>&nbsp;<span style="color: #0099cc;">16</span>}em)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$(css(...args));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;`;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;acc;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">},&nbsp;{});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;Box&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;styled.div&nbsp;`</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//props로&nbsp;넣은&nbsp;값을&nbsp;직접&nbsp;전달&nbsp;할&nbsp;수&nbsp;있다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;background:&nbsp;${props&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;props.color&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">|</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">|</span>&nbsp;<span style="color: #63a35c;">'blue'</span>};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;padding:&nbsp;1rem;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;display:&nbsp;flex;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;width:&nbsp;1024px;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;margin:&nbsp;<span style="color: #0099cc;">0</span>&nbsp;auto;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;${media.desktop`width:&nbsp;768px;`};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;${media.tablet`width:&nbsp;<span style="color: #0099cc;">100</span>%;`};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">`;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;<span style="color: #999999;">//...</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;StyledComponent;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><a href="https://styled-components.com/docs/advanced#media-templates" target="_blank" rel="noopener">https://styled-components.com/docs/advanced#media-templates</a></p>
<figure id="og_1625291684379" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="styled-components: Advanced Usage" data-og-description="Theming, refs, Security, Existing CSS, Tagged Template Literals, Server-Side Rendering and Style Objects" data-og-host="styled-components.com" data-og-source-url="https://styled-components.com/docs/advanced#media-templates" data-og-url="https://styled-components.com/docs/advanced#media-templates" data-og-image="https://scrap.kakaocdn.net/dn/uweNY/hyKLw0xzTl/ku9kljRZTR1A8Ipc7CSMW1/img.png?width=652&amp;height=652&amp;face=0_0_652_652,https://scrap.kakaocdn.net/dn/VgSfM/hyKLqF0JLe/Sl4T6ny26RLToh3bUME2c0/img.png?width=652&amp;height=652&amp;face=0_0_652_652"><a href="https://styled-components.com/docs/advanced#media-templates" target="_blank" rel="noopener" data-source-url="https://styled-components.com/docs/advanced#media-templates">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/uweNY/hyKLw0xzTl/ku9kljRZTR1A8Ipc7CSMW1/img.png?width=652&amp;height=652&amp;face=0_0_652_652,https://scrap.kakaocdn.net/dn/VgSfM/hyKLqF0JLe/Sl4T6ny26RLToh3bUME2c0/img.png?width=652&amp;height=652&amp;face=0_0_652_652');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">styled-components: Advanced Usage</p>
<p class="og-desc" data-ke-size="size16">Theming, refs, Security, Existing CSS, Tagged Template Literals, Server-Side Rendering and Style Objects</p>
<p class="og-host" data-ke-size="size16">styled-components.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp;</p>
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