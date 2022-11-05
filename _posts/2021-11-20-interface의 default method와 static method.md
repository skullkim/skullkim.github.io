---
layout:       post
title:        "interface의 default method와 static method"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- java
- java8
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
                            <p data-ke-size="size16">&nbsp; Java8부터 interface에 default method와 static method를 사용할 수 있게 되었다. Default method와 static method는 해당 interface를 implements하는 모든 인스턴스가 같은 기능이 있었으면 좋겠다는 이유로 추가되었다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">interface</span>&nbsp;Foo&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;이름을&nbsp;출력하는&nbsp;추상&nbsp;메서드</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;printName();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;이름을&nbsp;대문자로&nbsp;출력하는&nbsp;메서드</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;printNameUpperCase()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(getName().toUpperCase());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;이름을&nbsp;가져오는&nbsp;메서드</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;@return&nbsp;String&nbsp;이름을&nbsp;반환</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">String</span>&nbsp;getName();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;DefaultFoo&nbsp;<span style="color: #a71d5d;">implements</span>&nbsp;Foo{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**이름을&nbsp;저장*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">String</span>&nbsp;name;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;DefaultFoo&nbsp;생성자</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;@param&nbsp;name&nbsp;이름을&nbsp;받는&nbsp;파라미터</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;DefaultFoo(<span style="color: #066de2;">String</span>&nbsp;name)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">this</span>.name&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;name;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;implements한&nbsp;Foo&nbsp;인터페이스의&nbsp;getName&nbsp;추상&nbsp;메서드&nbsp;구현체</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;@return&nbsp;String&nbsp;멤버&nbsp;변수&nbsp;name을&nbsp;반환</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;@Override</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #066de2;">String</span>&nbsp;getName()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #a71d5d;">this</span>.name;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;implements한&nbsp;Foo&nbsp;인터페이스의&nbsp;printName&nbsp;추상&nbsp;메서드&nbsp;구현체</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;@Override</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;printName()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #a71d5d;">this</span>.name);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;실습에&nbsp;필요한&nbsp;DefaultFoo의&nbsp;인스턴스를&nbsp;만들고&nbsp;결과를&nbsp;출력한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;@param&nbsp;args&nbsp;Unused</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Foo&nbsp;foo&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;DefaultFoo(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foo.printName();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;foo.printNameUpperCase();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; Default method를 사용하게 되면 해당 인터페이스를 implements한 모든 객체에서 사용 가능하지만 이 기능을 제대로 동작할 것이라는 보장이 없다. 왜냐면 getName()의 구현체에서 어떤 값이 실제로 반환될지 모르기 때문이다. 따라서 이를 방지하기 위해 문서화를 철저히 해야한다. 이때 java8에서 추가된 @impleSpec을 사용한다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;*&nbsp;@implSpec</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;*&nbsp;이름을&nbsp;대문자로&nbsp;출력하는&nbsp;메서드</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">default</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;printNameUpperCase()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(getName().toUpperCase());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 만약 이런 식으로 문서화를 했음에도 문제가 된다면 override를 하면 된다.</p>
<p data-ke-size="size16">&nbsp; Object에서 제공하는 메서드들은 default method로 재정의할 수 없다(추상 메서드는 가능).</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//Default&nbsp;method&nbsp;'toString'&nbsp;overrides&nbsp;a&nbsp;member&nbsp;of&nbsp;'java.lang.Object'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">default</span>&nbsp;<span style="color: #066de2;">String</span>&nbsp;<span style="color: #066de2;">toString</span>()&nbsp;{}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 만약 인터페이스가 제공하는 default method를 사용하고 싶지 않다면 다른 인터페이스를 만들고 해당 인터페이스를 extends 한뒤 defualt method를 추상 메서드로 만들면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">interface</span>&nbsp;Bar&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;Foo{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;printNameUpperCase();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 만약 Foo interface, Bar interface가 둘 다 같은&nbsp; default method를 가지고 있다면 두가지를 동시에 implements할 수 없다. 해야 한다면 implements를 한 클래스에서 override를 해야 한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>static method</b></p>
<p data-ke-size="size16">해당 인터페이스를 implements하는 객체가 helper mthod(메서드의 작업을 도와주는, 반복적으로 사용되는 짧은 메서드)나 유틸리티가 필요할 경우 사용된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;printAnyThing()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Foo"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Foo&nbsp;foo&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;DefaultFoo(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;foo.printName();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;foo.printNameUpperCase();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Foo.printAnyThing();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>java 8에서 추가된 default method</b></p>
<p data-ke-size="size16">&nbsp; <i><b>Iterable의 default method</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; forEach(): js의 forEach처럼 리스트를 순회한다. forEach는 Consumer를 인자로 받는다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;names&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ArrayList<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"skull"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"keesun"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"toby"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.forEach(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; spliterator(): forEach같이 순회를 할 수도 있고 리스트를 여러개로 쪼갤 수 도 있다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;names&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ArrayList<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"skull"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"keesun"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"toby"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Spliterator<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;spliterator&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;names.spliterator();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Spliterator<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;spliterator1&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;spliterator.trySplit();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//tryAdvance역시&nbsp;Consumer를&nbsp;인자로&nbsp;받는다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">while</span>(spliterator.tryAdvance(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>));&nbsp;<span style="color: #999999;">//keesun,&nbsp;toby</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"======="</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">while</span>(spliterator1.tryAdvance(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>));&nbsp;<span style="color: #999999;">//yunki,&nbsp;skull</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp; <i><b>Collection의 default method</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; stream() / parallelStream() : Collection의 모든 하위 인터페이스들은 stream을 가지고 있다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; &nbsp; stream은 내부적으로 spliterator를 사용한다. stream은 리스트 내부의 엘리먼트들을 스트림으로 만들어서 functional하게 처리를 할 수 있다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;names&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ArrayList<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"skull"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"keesun"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"toby"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;Set<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;streamResult&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;names.stream()</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.map(<span style="color: #066de2;">String</span>::toUpperCase)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.filter(s&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;s.startsWith(<span style="color: #63a35c;">"K"</span>))</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.collect(Collectors.toSet());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;streamResult.forEach(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; &nbsp; removeIf(Predicate): 조건에 만족하는 엘리먼트를 제거한다. 인가로 Predicate를 받는다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;java8&nbsp;공식&nbsp;API에서&nbsp;추가된&nbsp;default&nbsp;method&nbsp;실습</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;@param&nbsp;args&nbsp;Unused</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;names&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ArrayList<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"skull"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"keesun"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"toby"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.removeIf(name&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;name.startsWith(<span style="color: #63a35c;">"k"</span>));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.forEach(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; <i><b>Comparator의 default method, static method</b></i></p>
<p data-ke-size="size16">&nbsp; &nbsp; reversed(): 내림차순으로 엘리먼트를 비교한다</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;App&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">/**</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;java8&nbsp;공식&nbsp;API에서&nbsp;추가된&nbsp;default&nbsp;method&nbsp;실습</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*&nbsp;@param&nbsp;args&nbsp;Unused</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;List<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;names&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ArrayList<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"yunki"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"skull"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"keesun"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.<span style="color: #066de2;">add</span>(<span style="color: #63a35c;">"toby"</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//오름차순&nbsp;정렬</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.sort(<span style="color: #066de2;">String</span>::compareToIgnoreCase);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.forEach(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"=========="</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//내림차순&nbsp;정렬</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Comparator<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #066de2;">String</span><span style="color: #a71d5d;">&gt;</span>&nbsp;compareToIgnoreCase&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">String</span>::compareToIgnoreCase;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.sort(compareToIgnoreCase.reversed());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;names.forEach(<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>::<span style="color: #066de2;">println</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp; &nbsp; thenComparing(): 기본적인 비교를 한 뒤 또 다른 조건으로 비교를 하고 싶을때 사용한다</p>
<p data-ke-size="size16">&nbsp; &nbsp; static reverseOrder() / naturalOrder()</p>
<p data-ke-size="size16">&nbsp; &nbsp; static nullsFirst() / nullLast(): null이 우선순위를 가진다 / null의 우선순위가 가장 뒤이다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; static comparing()</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b>Default method가 java api에 가져온 변화</b></p>
<p data-ke-size="size16">&nbsp; 하나의 인터페이스가 있다고 해보자. java8이전에는 서로 다른 객체가 이 인터페이스를 조금 더 편리하게 상요하기 위해 아래 그림과 같이 인터페이스를 implements하는 추상 클래스를 만들고 이 추상클래스를 상속받아 사용했다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/aW50ZXJmYWNl7J2YIGRlZmF1bHQgbWV0aG9k7JmAIHN0YXRpYyBtZXRob2Q=/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; 이런방식을 사용하면 굳이 구현이 필요없는 추상 메서드의 구현체를 구현할 필요가 없어진다. 하지만 자바에서는 오직 하나의 객체만을 상속받을 수 있기 때문에 상속을 더이상 받을 수 없는 문제가 발생하게 된다.</p>
<p data-ke-size="size16">&nbsp; java 8이상을 사용하게 되면 default method를 이용이 이 문제를 해결할 수 있다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/aW50ZXJmYWNl7J2YIGRlZmF1bHQgbWV0aG9k7JmAIHN0YXRpYyBtZXRob2Q=/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
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