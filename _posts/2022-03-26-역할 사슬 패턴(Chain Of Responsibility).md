---
layout:       post
title:        "역할 사슬 패턴(Chain Of Responsibility)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- 디자인패턴
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 요청에 대한 처리를 어느 객체가 수행할 수 있는지 모를 때 사용한다. 요청이 들어오면, 이를 수신하는 객체가 해당 요청을 처리할 수 없는 경우 다음 객체에게 요청을 넘긴다. 요청을 처리할 수 있는 객체가 요청을 받으면 이를 처리한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 예제는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7Jet7ZWgIOyCrOyKrCDtjKjthLQoQ2hhaW4gT2YgUmVzcG9uc2liaWxpdHkp/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">5</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">6</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">7</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">8</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">9</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">10</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">11</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">12</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">16</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">17</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">23</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">24</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">25</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">26</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">27</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">28</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">29</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">30</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">31</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">32</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">33</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">34</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">35</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">36</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">37</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">38</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">39</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">40</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">41</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">42</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">43</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">44</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">45</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">46</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">47</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">48</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">49</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">50</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">51</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">52</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">53</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">54</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">55</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">56</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">57</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">58</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">59</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">60</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">61</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">62</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">63</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">64</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">65</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">66</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">67</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">68</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">69</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">70</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">71</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">72</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">73</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">74</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">75</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">76</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">77</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">78</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">79</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">80</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">81</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">82</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">83</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">84</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">85</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">abstract</span>&nbsp;calss&nbsp;AbstractLogger&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;INFO&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;DEBUG&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">2</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;ERROR&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">3</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;level;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;AbstractLogger&nbsp;nextLogger;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;setNextLogger(AbstractLogger&nbsp;nextLogger)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">this</span>.nextLogger&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;nextLogger;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;logMessage(<span style="color: #066de2;">int</span>&nbsp;level,&nbsp;<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(<span style="color: #a71d5d;">this</span>.level&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;level)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;write(message);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(nextLogger&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">!</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #066de2;">null</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nextLogger.logMessage(level,&nbsp;message);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">abstract</span>&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;write(<span style="color: #066de2;">String</span>&nbsp;message);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;ConsoleLogger&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;AbstractLogger&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;ConsoleLogger(<span style="color: #066de2;">int</span>&nbsp;leve)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">this</span>.level&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;level;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;@Override</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;write(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Standard&nbsp;Console::Logger:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;message);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;ErrorLogger&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;AbstractLogger&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;ErrorLogger(<span style="color: #066de2;">int</span>&nbsp;level)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">this</span>.level&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;level;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;@Override</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;write(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Error&nbsp;Console::Logger:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;message);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;FileLogger&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;AbstractLogger&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;FileLogger(<span style="color: #066de2;">int</span>&nbsp;level)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">this</span>.level&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;level;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;@Override</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;write(<span style="color: #066de2;">String</span>&nbsp;message)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"Fie::Logger:&nbsp;"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;message);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;ChainPatternDemo&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;AbstractLogger&nbsp;getChainOfLoggers()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AbstractLogger&nbsp;errorLogger&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ErrorLogger(AbstractLogger.ERROR);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AbstractLogger&nbsp;fileLogger&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;FileLogger(AbstractLogger.DEBUG);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AbstractLogger&nbsp;consoleLogger&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #a71d5d;">new</span>&nbsp;ConsoleLogger(AbstractLogger.INFO);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;errorLogger.setNextLogger(fileLogger);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fileLogger.setNextLogger(consoleLogger);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;errorLogger;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">static</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;main(<span style="color: #066de2;">String</span>[]&nbsp;args)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AbstractLogger&nbsp;loggerChain&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;getChainOfLoggers();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loggerChain.logMessage(AbstractLogger.INFO,&nbsp;<span style="color: #63a35c;">"This&nbsp;is&nbsp;an&nbsp;information."</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loggerChain.logMessage(AbstractLogger.DEBUG,&nbsp;<span style="color: #63a35c;">"This&nbsp;is&nbsp;an&nbsp;debug&nbsp;level&nbsp;information."</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;loggerChain.logMessage(AbstractLogger.ERROR,&nbsp;<span style="color: #63a35c;">"This&nbsp;is&nbsp;an&nbsp;error&nbsp;information."</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
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