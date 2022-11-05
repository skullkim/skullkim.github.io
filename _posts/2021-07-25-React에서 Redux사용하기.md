---
layout:       post
title:        "React에서 Redux사용하기"
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
                            <p data-ke-size="size16">&nbsp; 리액트 애플리케이션에서 리덕스를 사용하면, 상태 업데이트에 대한 로직을 모듈로 따로 분리 해서 컴포넌트 파일과 별개로 관리할 수 있기 떄문에 코드 유지보수에 도움이 된다. 여러 컴포넌트에서 동일한 상태를 공유 할 때 유용하고, 실제 업데이트가 필요한 컴포넌트만 리렌더링 되게 쉽게 최적화 할 수 있다.</p>
<p data-ke-size="size16">&nbsp; 바닐라에서 리덕스를 사용할 거면, dispatch, subscribe를 사용해야 했지만, 리액트에서 리덕스를 사용할 때에는 react-redux라는 라이브러리에서 제공하는 유틸 함수(connect)와 컴포넌트(Provider)를 사용해 리덕스 관련 작업을 한다.</p>
<p data-ke-size="size16">&nbsp; 리액트에서 리덕스를 사용할 때에는 통상적으로 presentational component와 container component를 분리하여 사용한다. Presentational component는 props를 받아와 보여주기만 하는 컴포넌트이고 container component는 리덕스와 연동되어 있는 컴포넌트로, 리덕스로 부터 상태를 받아 오거나 스토어에 액션을 디스패치 한다. 따라서 다음과 같은 패턴을 사용한다</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="378" data-origin-height="239" data-ke-mobilestyle="widthOrigin">
    <span data-lightbox="lightbox">
        <img src="/img/UmVhY3Tsl5DshJwgUmVkdXjsgqzsmqntlZjquLA=/img.png" data-origin-width="378" data-origin-height="239" data-ke-mobilestyle="widthOrigin">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><b>파일 구조</b></p>
<p data-ke-size="size16">&nbsp; 리덕스를 사용할 때 강제되는 디렉터리 구조는 없지만 통상적으로 리덕스를 사용할 때 actions, constants, reducers라는 3개의 디렉터리를 만들어서 각각 액션 생성 함수, 액션 타입, 리듀서를 저장해 사용한다. 하지만 새로운 액션을 만들어야 할때 세 종류의 파일을 모두 수정해야 하기 때문에 불편하다. 이때 사용하는 패턴이 ducks이다. Ducks는 디렉터리를 기준으로 파일을 나누는 것이 아닌 위의 3종류를 각 하나의 파일에 몰아서 넣는 방식이다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; modules라는 디렉터리를 만들고 다음과 같은 코드들을 작성하자</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//modules/counter.js<br>//액션&nbsp;타입&nbsp;정의</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;타입은&nbsp;'모듈&nbsp;이름/액션&nbsp;이름'&nbsp;형식으로&nbsp;해서&nbsp;중복을&nbsp;피한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;INCREASE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'counter/INCREASE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;DECREASE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'counter/DECREASE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;생성&nbsp;함</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;increase&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({type:&nbsp;INCREASE});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;decrease&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({type:&nbsp;DECREASE});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//초기&nbsp;상태</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;initialState&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;number:&nbsp;<span style="color: #0099cc;">0</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//reducer&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;counter&nbsp;(state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;initialState,&nbsp;action)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">switch</span>&nbsp;(action.type)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;INCREASE:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;number:&nbsp;state.number&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #0099cc;">1</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;DECREASE:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;number:&nbsp;state.number&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>&nbsp;<span style="color: #0099cc;">1</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">default</span>:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;state;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;counter;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
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
<div style="line-height: 130%;">76</div>
<div style="line-height: 130%;">77</div>
<div style="line-height: 130%;">78</div>
<div style="line-height: 130%;">79</div>
<div style="line-height: 130%;">80</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//modules/todos.js<br>//액션&nbsp;타입&nbsp;지정</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CHANGE_INPUT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/CHNAGE_INPUT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;INSERT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/INSERT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TOGGLE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/TOGGLE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;REMOVE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/REMOVE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;생성&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;changeInput&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(input)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;CHANGE_INPUT,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;input</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">let</span>&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">3</span>;<span style="color: #999999;">//insert&nbsp;한번&nbsp;호출&nbsp;시&nbsp;+1</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;insert&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(text)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;INSERT,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;todo:&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;id<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;toggle&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(id)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;TOGGLE,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;id</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;remove&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(id)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;REMOVE,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;id</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//초기&nbsp;상태</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;initialState&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;input:&nbsp;<span style="color: #63a35c;">''</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;todos:&nbsp;[</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">1</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'learn&nbsp;basic&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #a71d5d;">true</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">2</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'use&nbsp;react&nbsp;and&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;],</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//reducer&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;todos(state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;initialState,&nbsp;action)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">switch</span>(action.type)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;CHANGE_INPUT:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;input:&nbsp;action.input</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;INSERT:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.concat(action.todo)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;TOGGLE:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.map(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;action.id&nbsp;?&nbsp;{...todo,&nbsp;done:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span>todo.done}&nbsp;:&nbsp;todo</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;REMOVE:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.filter(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;action.id)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">default</span>:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;state;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;todos;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위와 같이 리듀서를 여러개 만들어도 되지만, createStore함수를 사용해서 스토어를 만들때는 리듀서를 하나만 사용해야 한다. 따라서 기존에 만들었던 리듀서를 하나로 합쳐야 하는데, 이는 리덕스의 combineReducers()를 사용하면 된다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//modules/index.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{combineReducers}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;counter&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./counter"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;todos&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./todos"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;rootReducer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;combineReducers({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;counter,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;todos,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;rootReducer;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>스토어 생성</b></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//src/index.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;ReactDOM&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-dom'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{createStore}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{Provider}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//크롬&nbsp;확장&nbsp;개발자&nbsp;도구인&nbsp;Redux&nbsp;DevTools를&nbsp;사용하기&nbsp;위한&nbsp;세팅</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{composeWithDevTools}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"redux-devtools-extension"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;<span style="color: #63a35c;">'./index.css'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;App&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'./App'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;reportWebVitals&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'./reportWebVitals'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;rootReducer&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"./modules"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;store&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createStore(rootReducer,&nbsp;composeWithDevTools());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">ReactDOM.render(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">//리액트&nbsp;컴포넌트에서&nbsp;스토어를&nbsp;사용할&nbsp;수&nbsp;있게&nbsp;App컴포넌트를&nbsp;react-redux에서&nbsp;제공하는</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//Provider&nbsp;컴포넌트로&nbsp;감싼다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Provider&nbsp;store<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{store}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>App&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>Provider<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #066de2;">document</span>.<span style="color: #066de2;">getElementById</span>(<span style="color: #63a35c;">'root'</span>)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//&nbsp;If&nbsp;you&nbsp;want&nbsp;to&nbsp;start&nbsp;measuring&nbsp;performance&nbsp;in&nbsp;your&nbsp;app,&nbsp;pass&nbsp;a&nbsp;function</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//&nbsp;to&nbsp;log&nbsp;results&nbsp;(for&nbsp;example:&nbsp;reportWebVitals(console.log))</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//&nbsp;or&nbsp;send&nbsp;to&nbsp;an&nbsp;analytics&nbsp;endpoint.&nbsp;Learn&nbsp;more:&nbsp;https://bit.ly/CRA-vitals</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">reportWebVitals();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 이제 컴포넌트에서 리덕스 스토어에 접근해 원하는 상태를 받아오고, 액션 디스패치를 하자. 리덕스 스토어와 연동된 컴폰너트를 컨테이너 컴포넌트라 한다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//containers/CounterContainer.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{connect}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;Counter&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../components/Counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{increase,&nbsp;decrease}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../modules/counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CounterContainer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({number,&nbsp;increase,&nbsp;decrease})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Counter&nbsp;number<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{number}&nbsp;onIncrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{increase}&nbsp;onDecrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{decrease}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//아래&nbsp;두&nbsp;함수의&nbsp;반환&nbsp;객체&nbsp;내부&nbsp;값들은&nbsp;컴포넌트의&nbsp;props로&nbsp;전달&nbsp;된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//state를&nbsp;파라미터로&nbsp;받고,&nbsp;이&nbsp;값은&nbsp;현재&nbsp;스토어가&nbsp;지닌&nbsp;상태이다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;mapStateToProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;number:&nbsp;state.counter.number,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//스토어의&nbsp;내장&nbsp;함수&nbsp;dispatch를&nbsp;파라미터로&nbsp;받아&nbsp;온다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;mapDispatchToProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;dispatch&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;increase:&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dispatch(increase());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;decrease:&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dispatch(decrease());</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//컴포넌트를&nbsp;리덕스와&nbsp;연동하기&nbsp;위해&nbsp;react-redux에서&nbsp;제공하는&nbsp;connect()를&nbsp;사용해야&nbsp;한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//connect는&nbsp;첫&nbsp;인자로&nbsp;리덕스&nbsp;스토어&nbsp;안의&nbsp;상태를&nbsp;컴포넌트의&nbsp;props로&nbsp;넘겨주기&nbsp;위한&nbsp;설정&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//두&nbsp;번쨰&nbsp;인자로&nbsp;액션&nbsp;생성&nbsp;함수를&nbsp;컴포넌트의&nbsp;props로&nbsp;넘겨주기&nbsp;위한&nbsp;함수를&nbsp;사용한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;connect(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;mapStateToProps,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;mapDispatchToProps,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//connect는&nbsp;호출되면&nbsp;또&nbsp;다른&nbsp;함수를&nbsp;반환하는데,&nbsp;이&nbsp;함수의&nbsp;인자로</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//연동할&nbsp;컴포넌트를&nbsp;넣어&nbsp;주면&nbsp;된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">)(CounterContainer);&nbsp;<span style="color: #999999;">//연동할&nbsp;컴포넌</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 만약 위의 코드에서 액션을 디스패치하기 위해 액션 생성함수를 호출하고, dispatch로 감싸는 것을 하기 싫다면 bindActionCreators를 사용하면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//스토어의&nbsp;내장&nbsp;함수&nbsp;dispatch를&nbsp;파라미터로&nbsp;받아&nbsp;온다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;mapDispatchToProps&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;dispatch&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;bindActionCreators({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;increase,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;decrease,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},&nbsp;dispatch)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">);</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">또는 다음과 같은 방식을 사용하면 된다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//containers/CounterContainer.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{bindActionCreators}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{connect}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;Counter&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../components/Counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{increase,&nbsp;decrease}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../modules/counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CounterContainer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({number,&nbsp;increase,&nbsp;decrease})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Counter&nbsp;number<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{number}&nbsp;onIncrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{increase}&nbsp;onDecrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{decrease}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//컴포넌트를&nbsp;리덕스와&nbsp;연동하기&nbsp;위해&nbsp;react-redux에서&nbsp;제공하는&nbsp;connect()를&nbsp;사용해야&nbsp;한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//connect는&nbsp;첫&nbsp;인자로&nbsp;리덕스&nbsp;스토어&nbsp;안의&nbsp;상태를&nbsp;컴포넌트의&nbsp;props로&nbsp;넘겨주기&nbsp;위한&nbsp;설정&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//두&nbsp;번쨰&nbsp;인자로&nbsp;액션&nbsp;생성&nbsp;함수를&nbsp;컴포넌트의&nbsp;props로&nbsp;넘겨주기&nbsp;위한&nbsp;함수를&nbsp;사용한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;connect(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;number:&nbsp;state.counter.number,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//두번쨰&nbsp;인자로&nbsp;액션&nbsp;생성&nbsp;함수로&nbsp;이루어진&nbsp;객체&nbsp;형태를&nbsp;넣으면</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//connect함수가&nbsp;내부적으로&nbsp;bindActionCreators작업을&nbsp;한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;increase,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;decrease,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//connect는&nbsp;호출되면&nbsp;또&nbsp;다른&nbsp;함수를&nbsp;반환하는데,&nbsp;이&nbsp;함수의&nbsp;인자로</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//연동할&nbsp;컴포넌트를&nbsp;넣어&nbsp;주면&nbsp;된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">)(CounterContainer);&nbsp;<span style="color: #999999;">//연동할&nbsp;컴포넌</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>흐름 정리</b></p>
<p data-ke-size="size16">&nbsp; 다음 코드를 순차적으로 보면 흐름이 이해될 거다.</p>
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
<div style="line-height: 130%;">76</div>
<div style="line-height: 130%;">77</div>
<div style="line-height: 130%;">78</div>
<div style="line-height: 130%;">79</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//modules/todos.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;타입&nbsp;지정</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CHANGE_INPUT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/CHNAGE_INPUT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;INSERT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/INSERT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TOGGLE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/TOGGLE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;REMOVE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/REMOVE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;생성&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;changeInput&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(input)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;CHANGE_INPUT,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;input</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">let</span>&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">3</span>;<span style="color: #999999;">//insert&nbsp;한번&nbsp;호출&nbsp;시&nbsp;+1</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;insert&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(text)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;INSERT,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;todo:&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;id<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;toggle&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(id)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;TOGGLE,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;id</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;remove&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(id)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;type:&nbsp;REMOVE,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;id</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;initialState&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;input:&nbsp;<span style="color: #63a35c;">''</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;todos:&nbsp;[</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">1</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'learn&nbsp;basic&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #a71d5d;">true</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">2</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'use&nbsp;react&nbsp;and&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;],</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">function</span>&nbsp;todos(state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;initialState,&nbsp;action)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">switch</span>(action.type)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;CHANGE_INPUT:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;input:&nbsp;action.input</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;INSERT:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.concat(action.todo)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;TOGGLE:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.map(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;action.id&nbsp;?&nbsp;{...todo,&nbsp;done:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span>todo.done}&nbsp;:&nbsp;todo</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">case</span>&nbsp;REMOVE:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.filter(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;action.id)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">default</span>:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;state;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;todos;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//containers/TodosContainer.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{connect}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{changeInput,&nbsp;insert,&nbsp;toggle,&nbsp;remove}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../modules/todos'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;Todos&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../components/Todos'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TodosContainer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;input,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;todos,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;changeInput,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;insert,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;toggle,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;remove,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Todos</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;input<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{input}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{todos}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onChangeInput<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{changeInput}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onInsert<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{insert}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onToggle<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{toggle}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onRemove<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{remove}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;connect(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;({todos})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;input:&nbsp;todos.input,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;todos.todos,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;changeInput,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;insert,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;toggle,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;remove,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">)(TodosContainer);</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//components/Todos.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TodoItem&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({todo,&nbsp;onToggle,&nbsp;onRemove})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>input</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"checkbox"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onClick<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;onToggle(todo.id)}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;checked<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{todo.done}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;readOnly<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{<span style="color: #a71d5d;">true</span>}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>span&nbsp;style<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{{textDecoration:&nbsp;todo.done&nbsp;?&nbsp;<span style="color: #63a35c;">'line-through'</span>&nbsp;:&nbsp;<span style="color: #63a35c;">'none'</span>}}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{todo.text}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>span<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>button&nbsp;onClick<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;onRemove(todo.id)}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span><span style="color: #a71d5d;">delete</span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;Todos&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;input,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;todos,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;onChangeInput,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;onInsert,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;onToggle,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;onRemove,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;onSubmit&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(e)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.preventDefault();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onInsert(input);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onChangeInput(<span style="color: #63a35c;">''</span>);<span style="color: #999999;">//등록&nbsp;후&nbsp;인풋&nbsp;초기화</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;onChange&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;e&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;onChangeInput(e.target.value);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>form&nbsp;onSubmit<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onSubmit}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>input&nbsp;type<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #63a35c;">"text"</span>&nbsp;value<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{input}&nbsp;onChange<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onChange}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>button&nbsp;type<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{<span style="color: #63a35c;">"submit"</span>}<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>submit<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>button<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>form<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{todos.map(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>TodoItem</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todo<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{todo}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;key<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{todo.id}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onToggle<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onToggle}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onRemove<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onRemove}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;))}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span>div<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;Todos;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>리덕스 간략화</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>redux-action을 사용하면 보다 코드를 더 깔끔하게 쓸 수 있다.&nbsp;</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{createAction,&nbsp;handleActions}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux-actions'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;타입&nbsp;지정</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CHANGE_INPUT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/CHNAGE_INPUT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;INSERT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/INSERT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TOGGLE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/TOGGLE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;REMOVE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/REMOVE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;생성&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//createAction으로&nbsp;액션을&nbsp;만들면&nbsp;액션에&nbsp;필요한&nbsp;추가&nbsp;데이터는&nbsp;payload라는&nbsp;이름을&nbsp;사용한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//{type:&nbsp;CHANGE_INPUT,&nbsp;payload:&nbsp;input}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;changeInput&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(CHANGE_INPUT,&nbsp;input&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;input);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">let</span>&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">3</span>;<span style="color: #999999;">//insert&nbsp;한번&nbsp;호출&nbsp;시&nbsp;+1</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;insert&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(INSERT,&nbsp;text&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;id:&nbsp;id<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;text,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;toggle&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(TOGGLE,&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;id);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;remove&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(REMOVE,&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;id);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;initialState&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;input:&nbsp;<span style="color: #63a35c;">''</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;todos:&nbsp;[</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">1</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'learn&nbsp;basic&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #a71d5d;">true</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">2</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'use&nbsp;react&nbsp;and&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;],</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//createAction을&nbsp;사용했기&nbsp;때문에&nbsp;모든&nbsp;값은&nbsp;action.payload로&nbsp;조회&nbsp;한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;todos&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;handleActions({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[CHANGE_INPUT]:&nbsp;(state,&nbsp;action)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({...state,&nbsp;input:&nbsp;action.payload}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[INSERT]:&nbsp;(state,&nbsp;action)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.concat(action.payload),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//이와&nbsp;같이&nbsp;payload를&nbsp;사용하는&nbsp;대신&nbsp;비구조화&nbsp;할당을&nbsp;통해&nbsp;payload이름을&nbsp;새로&nbsp;설정할&nbsp;수&nbsp;있다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[TOGGLE]:&nbsp;(state,&nbsp;{payload:&nbsp;id})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.map(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;id&nbsp;?&nbsp;{...todo,&nbsp;done:&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span>todo.done}&nbsp;:&nbsp;todo,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[REMOVE]:&nbsp;(state,&nbsp;action)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;...state,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;state.todos.filter(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;action.payload),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">},&nbsp;initialState);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;todos;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;immer를 사용하면 복잡한 객체의 수정에 대한 코드를 줄일 수있다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{createAction,&nbsp;handleActions}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux-actions'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;produce&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">"immer"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;타입&nbsp;지정</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CHANGE_INPUT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/CHNAGE_INPUT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;INSERT&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/INSERT'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TOGGLE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/TOGGLE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;REMOVE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #63a35c;">'todos/REMOVE'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//액션&nbsp;생성&nbsp;함수</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//createAction으로&nbsp;액션을&nbsp;만들면&nbsp;액션에&nbsp;필요한&nbsp;추가&nbsp;데이터는&nbsp;payload라는&nbsp;이름을&nbsp;사용한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//{type:&nbsp;CHANGE_INPUT,&nbsp;payload:&nbsp;input}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;changeInput&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(CHANGE_INPUT,&nbsp;input&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;input);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">let</span>&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">3</span>;<span style="color: #999999;">//insert&nbsp;한번&nbsp;호출&nbsp;시&nbsp;+1</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;insert&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(INSERT,&nbsp;text&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;id:&nbsp;id<span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">+</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;text,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;toggle&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(TOGGLE,&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;id);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;remove&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;createAction(REMOVE,&nbsp;id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;id);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;initialState&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;input:&nbsp;<span style="color: #63a35c;">''</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;todos:&nbsp;[</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">1</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'learn&nbsp;basic&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #a71d5d;">true</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id:&nbsp;<span style="color: #0099cc;">2</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;text:&nbsp;<span style="color: #63a35c;">'use&nbsp;react&nbsp;and&nbsp;redux'</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done:&nbsp;<span style="color: #0099cc;">false</span>,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;],</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//createAction을&nbsp;사용했기&nbsp;때문에&nbsp;모든&nbsp;값은&nbsp;action.payload로&nbsp;조회&nbsp;한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;todos&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;handleActions({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[CHANGE_INPUT]:&nbsp;(state,&nbsp;{payload:&nbsp;input})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;produce(state,&nbsp;draft&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;draft.input&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;input;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[INSERT]:&nbsp;(state,&nbsp;{payload:&nbsp;todo})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;produce(state,&nbsp;draft&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;draft.todos.push(todo);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//이와&nbsp;같이&nbsp;payload를&nbsp;사용하는&nbsp;대신&nbsp;비구조화&nbsp;할당을&nbsp;통해&nbsp;payload이름을&nbsp;새로&nbsp;설정할&nbsp;수&nbsp;있다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[TOGGLE]:&nbsp;(state,&nbsp;{payload:&nbsp;id})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;produce(state,&nbsp;draft&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;draft.todos.find(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;id);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todo.done&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">!</span>todo.done;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;[REMOVE]:&nbsp;(state,&nbsp;{payload:&nbsp;id})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;produce(state,&nbsp;draft&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;index&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;draft.todos.findIndex(todo&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;todo.id&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;id);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;draft.todos.splice(index,&nbsp;<span style="color: #0099cc;">1</span>);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}),</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">},&nbsp;initialState);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;todos;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>Hooks를 사용해 컨테이너 컴포넌트 만들기</b></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5; width: 31.9886px;">
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
</div>
</td>
<td style="padding: 6px 0px; text-align: left; width: 571.989px;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;"><span style="background-color: #fafafa; color: #999999;">//containers/CounterContainer.js</span><br>import</span>&nbsp;React,&nbsp;{useCallback}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{bindActionCreators}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{useSelector,&nbsp;useDispatch}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;Counter&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../components/Counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{increase,&nbsp;decrease}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../modules/counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CounterContainer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//useSelect()의&nbsp;파라미터는&nbsp;connect()의&nbsp;첫&nbsp;파라미터인</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//mapStateToProps에&nbsp;해당한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;number&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useSelector(state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;state.counter.number);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//컴포넌트&nbsp;내부에서&nbsp;스토어의&nbsp;내장&nbsp;함수&nbsp;dispatch를&nbsp;사용할&nbsp;수&nbsp;있게&nbsp;해준다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;dispatch&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useDispatch();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Counter</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;number<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{number}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onIncrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span> dispatch(increase())}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onDecrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span> dispatch(decrease())}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;CounterContainer;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0px 2px 4px 0px; width: 15.9943px;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 위의 코드의 경우 컴포넌트가 리렌더링 되면 onIncrease와 onDecrease가 새롭게 만들어 진다. 따라서 성능 최적화를 위해서라면 useCallback으로 액션을 dispatch하는 함수를 감싸야 한다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">import React, {useCallback} <span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{bindActionCreators}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{useSelector,&nbsp;useDispatch}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;Counter&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../components/Counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{increase,&nbsp;decrease}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../modules/counter'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;CounterContainer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//useSelect()의&nbsp;파라미터는&nbsp;connect()의&nbsp;첫&nbsp;파라미터인</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//mapStateToProps에&nbsp;해당한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;number&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useSelector(state&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;state.counter.number);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//컴포넌트&nbsp;내부에서&nbsp;스토어의&nbsp;내장&nbsp;함수&nbsp;dispatch를&nbsp;사용할&nbsp;수&nbsp;있게&nbsp;해준다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;dispatch&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useDispatch();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;onIncrease&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useCallback(()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;dispatch(increase()),&nbsp;[dispatch]);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;onDecrease&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useCallback(()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;dispatch(decrease()),&nbsp;[decrease]);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Counter</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;number<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{number}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onIncrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onIncrease}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onDecrease<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onDecrease}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;CounterContainer;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//useSelector의&nbsp;경우&nbsp;다음과&nbsp;같이&nbsp;비구조화&nbsp;할당도&nbsp;할&nbsp;수&nbsp;있다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;{input,&nbsp;todos}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useSelector(({todos})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;input:&nbsp;todos.input,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;todos.todos,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}));</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><i>useSotre</i></p>
<p data-ke-size="size16">&nbsp; &nbsp;컴포넌트 내부에서 리덕스 스토어 객체를 사용할 수 있다. 정말 간혹 스토어에 직접 접근해야 할때만 사용한다.</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;store&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useStore();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">sotre.dispatch({type:&nbsp;<span style="color: #63a35c;">'a'</span>});</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">store.getState();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;&nbsp;<i>useActions</i></p>
<p data-ke-size="size16"><i>&nbsp; &nbsp;&nbsp;</i>useActions는 원래 redux-react에 내장될 계획이었으나 훅을 사용할때 개념적 오버헤드와 syntax상의 복잡을 야기한다는 의견으로 인해 제외 되었다. 하지만 다음 링크에서 코드를 복사해 useActions를 사용할 수 있다.</p>
<p data-ke-size="size16"><a href="https://react-redux.js.org/api/hooks#recipe-useactions" target="_blank" rel="noopener">https://react-redux.js.org/api/hooks#recipe-useactions</a></p>
<figure id="og_1627542186813" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="website" data-og-title="Hooks | React Redux" data-og-description="API > Hooks: the `useSelector` and `useDispatch` hooks`" data-og-host="react-redux.js.org" data-og-source-url="https://react-redux.js.org/api/hooks#recipe-useactions" data-og-url="https://react-redux.js.org/api/hooks" data-og-image="https://scrap.kakaocdn.net/dn/b30P12/hyK3CET0sw/IYUJJkofKMBd2xCw0SxsB0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600,https://scrap.kakaocdn.net/dn/NdjCU/hyK2ItaTN2/hSDsPomYaW2V1EDCRXbQuK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://react-redux.js.org/api/hooks#recipe-useactions" target="_blank" rel="noopener" data-source-url="https://react-redux.js.org/api/hooks#recipe-useactions">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/b30P12/hyK3CET0sw/IYUJJkofKMBd2xCw0SxsB0/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600,https://scrap.kakaocdn.net/dn/NdjCU/hyK2ItaTN2/hSDsPomYaW2V1EDCRXbQuK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">Hooks | React Redux</p>
<p class="og-desc" data-ke-size="size16">API &gt; Hooks: the `useSelector` and `useDispatch` hooks`</p>
<p class="og-host" data-ke-size="size16">react-redux.js.org</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp; &nbsp; useActions는 액션 생성 함수를 액션을 dispatch하는 함수로 변환해 준다. 액션 생성 함수를 사용해 액션 객체를 만들고, 이를 스토어에 디스패치하는 작업을 해 주는 함수를 자동으로 만들어 준다.</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//lib/useActions.js</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{&nbsp;bindActionCreators&nbsp;}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'redux'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{&nbsp;useDispatch&nbsp;}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{&nbsp;useMemo&nbsp;}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//actions-&gt;액션&nbsp;생성&nbsp;함수로&nbsp;이뤄진&nbsp;배열</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">//deps-&gt;이&nbsp;배열&nbsp;안에&nbsp;이쓴&nbsp;원소가&nbsp;바뀌면&nbsp;액션을&nbsp;디스패치&nbsp;하는&nbsp;함수를&nbsp;새로&nbsp;만든다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">function</span>&nbsp;useActions(actions,&nbsp;deps)&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;dispatch&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useDispatch()</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;useMemo(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(<span style="color: #066de2;">Array</span>.isArray(actions))&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;actions.map(a&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;bindActionCreators(a,&nbsp;dispatch))</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;bindActionCreators(actions,&nbsp;dispatch)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;deps&nbsp;?&nbsp;[dispatch,&nbsp;...deps]&nbsp;:&nbsp;[dispatch]</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
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
<p data-ke-size="size16">&nbsp; useActions는 다음과 같이 사용할 수 있다</p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;React,&nbsp;{useCallback}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{useSelector,&nbsp;useDispatch}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'react-redux'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;{changeInput,&nbsp;insert,&nbsp;toggle,&nbsp;remove}&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../modules/todos'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;Todos&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../components/Todos'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">import</span>&nbsp;useActions&nbsp;<span style="color: #a71d5d;">from</span>&nbsp;<span style="color: #63a35c;">'../lib/useActions'</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">const</span>&nbsp;TodosContainer&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;()&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;{input,&nbsp;todos}&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useSelector(({todos})&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;({</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;input:&nbsp;todos.input,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos:&nbsp;todos.todos,</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}));</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;[onChangeInput,&nbsp;onInsert,&nbsp;onToggle,&nbsp;onRemove]&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;useActions(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[changeInput,&nbsp;insert,&nbsp;toggle,&nbsp;remove],</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[]</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;);</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;(</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>Todos</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;input<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{input}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;todos<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{todos}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onChangeInput<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onChangeInput}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onInsert<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onInsert}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onToggle<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onToggle}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onRemove<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>{onRemove}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">/</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">};</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">export</span>&nbsp;<span style="color: #a71d5d;">default</span>&nbsp;TodosContainer;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><b>connect()와 훅의 차이</b></p>
<p data-ke-size="size16">&nbsp; connect()를 사용하면 해당 컨테이너 컴포넌트의 부모 컴포넌트가 리렌더링 될 때 해당 컨테이너 컴포넌트의 props가 바뀌지 않았다면 리렌더링이 자동으로 방지 된다. 반면, 훅은 이러한 최적화가 자동으로 이루어 지지 않기 때문에 React.memo를 컨테이어 컴포넌트에 사용해야 한다.</p>
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