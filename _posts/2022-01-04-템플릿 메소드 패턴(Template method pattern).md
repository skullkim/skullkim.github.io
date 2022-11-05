---
layout:       post
title:        "템플릿 메소드 패턴(Template method pattern)"
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 템플릿 메소드 패턴은 알고리즘의 구조를 메서드에 정의하고, 하위 클래스에서 알고리즘 구조의 변경없이 알고리즘을 재정의 하는 패턴이다. 알고리즘이 단계별로 나누어 지거나, 같은 역할을 하는 메서드이지만 여러곳에서 다른 형태로 사용이 필요한 경우 유용하다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>장점</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 코드 중복을 줄일 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 자식 클래스의 역할을 줄여 핵심 로직 관리가 용이하다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>단점</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 추상 메서드가 많아지면 클래스 관리가 복잡해 진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 클래스 간의 관계와 코드가 꼬일 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>예제</b></span></p>
<p data-ke-size="size16">&nbsp;</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7YWc7ZSM66a/IOuplOyGjOuTnCDtjKjthLQoVGVtcGxhdGUgbWV0aG9kIHBhdHRlcm4p/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">abstract</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;Work&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #066de2;">String</span>&nbsp;personName;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;Work(<span style="color: #066de2;">String</span>&nbsp;personName)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">this</span>.personName&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span>&nbsp;personName;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #066de2;">String</span>&nbsp;getPersonName()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;personName;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">private</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;finishWork()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(<span style="color: #63a35c;">"퇴근"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;work()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;startWork();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;finishWork();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">abstract</span>&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;startWork();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">class</span>&nbsp;Painter&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;Work&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;Painter(<span style="color: #066de2;">String</span>&nbsp;name)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">super</span>(name);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;@Override</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;startWork()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(getPersonName()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #63a35c;">"은&nbsp;그림을&nbsp;그린다."</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">class</span>&nbsp;Singer&nbsp;<span style="color: #a71d5d;">extends</span>&nbsp;Work&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;Singer(<span style="color: #066de2;">String</span>&nbsp;name)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">super</span>(name);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;@Override</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">protected</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;startWork()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">System</span>.<span style="color: #066de2;">out</span>.<span style="color: #066de2;">println</span>(getPersonName()&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #63a35c;">"은&nbsp;노래를&nbsp;부른다."</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
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