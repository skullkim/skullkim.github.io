---
layout:       post
title:        "개략적인 컴퓨터 구조와 프로그램 동작 과정"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- OS
- 하드웨어
- ComputerScience
---

<div class="tt_article_useless_p_margin contents_style"><div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdio.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main(<span style="color: #a71d5d;">void</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"Hello&nbsp;world\n"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같이 "Hello world"를 출력하는 간단한 프로그램은 개발 공부를 처음 시작하는 사람이라면 누구나 한 번쯤은 작성해 봤을 겁니다. 이 프로그램을 실행해 보고는 더 많은 지식들을 얻기 위해 책을 다음 페이지로 넘깁니다. 하지만, 이 간단한 프로그램 동작과정에는 보이지 않는 지식들이 수도 없이 들어있습니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 글에서는 위 코드를 예시로 우선 소프트웨어 측면에서 위 프로그램이 실행되기 위한 소프트웨어적인 변환 과정을 설명합니다. 그 후, 하드웨어와 OS 관점에서 동작 과정을 설명하면서 개략적인 컴퓨터 구조를 설명합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 글은 인텔 x86 아키텍처를 기반으로 작성되었습니다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>hello.c 텍스트 파일을 오브젝트 파일로 만들기까지</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그래머가 소스 파일을 작성하는 것이 프로그램에게 생명을 불어넣는 첫 단계입니다. 작성한 소스 파일은 hello.c라는 이름의 텍스트 파일로 저장됩니다. 소스 파일은 비트들의 연속이고 단위는 8비트(1byte)입니다. 또 한, 대부분의 컴퓨터 시스템은 문자를 나타내기 위해 ASCII 표준을 사용합니다. 따라서 "#include &lt;stdio.h&gt;"를 연속된 바이트로 바꾸면 "35 105 110 99 108 117 100 101 32 60 115 116 100 105 111 46 104 62"가 됩니다. hello.c처럼 ASCII 문자로만 이루어진 파일들을 텍스트 파일, 나머지 유형 파일들을 바이너리 파일이라 합니다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; hello.c 소스 파일 작성에 사용한 C 프로그램은 인간이 이해하고 읽을 수 있지만 기계는 이해하지 못합니다. 따라서 hello.c 내에 있는 코드들은 저급 기계어 인스트럭션(2진 비트들로 구성돼 있다)들로 번역돼야 합니다. 번역된 인스트럭션들은 실행가능 목적프로그램이라는 형태로 합쳐져서 바이너리 디스크 파일로 저장됩니다. 이 과정을 도식화하면 다음과 같습니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1760" data-origin-height="250"><span data-url="https://blog.kakaocdn.net/dn/dhXXIl/btr4suCokHp/2o9fCN7w8LdDkch0grTbKk/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdhXXIl%2Fbtr4suCokHp%2F2o9fCN7w8LdDkch0grTbKk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1760" data-origin-height="250"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 이 단계들을 하나씩 간단히 살펴보겠습니다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Pre-prosessor(cpp)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>전처리기인 cpp는 C 프로그램을 # 문자로 시작하는 디렉티브(directive)에 따라 수정합니다. "#include"는 뒤에 따라오는 파일을 프로그램 문장에 삽입할 것을 지시합니다. 따라서 예제의 경우 "stdio.h" 헤더 파일이 삽입됩니다. hello.c 파일이 pre-processor 과정을 거쳐 hello.i 파일로 변환 결과를 보기 위해선 다음과 같은 명령어를 실행시키면 됩니다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">gcc&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>E&nbsp;hello.c&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>o&nbsp;hello.i</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 변환된 hello.i 파일은 내부는 다음과 같습니다.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">86</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">87</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">88</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #63a35c;">"hello.c"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #63a35c;">"&lt;built-in&gt;"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #63a35c;">"&lt;command-line&gt;"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdc-predef.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">0</span>&nbsp;<span style="color: #63a35c;">"&lt;command-line&gt;"</span>&nbsp;<span style="color: #0099cc;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"hello.c"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">27</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/libc-header-start.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">33</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/libc-header-start.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">392</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features-time64.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">20</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features-time64.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/wordsize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">21</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features-time64.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/timesize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">19</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/timesize.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/wordsize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">20</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/timesize.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">22</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features-time64.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">393</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">486</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/sys/cdefs.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">559</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/sys/cdefs.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/wordsize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">560</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/sys/cdefs.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/long-double.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">561</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/sys/cdefs.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">487</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">510</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/gnu/stubs.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">10</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/gnu/stubs.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/gnu/stubs-64.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">11</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/gnu/stubs.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">511</span>&nbsp;<span style="color: #63a35c;">"/usr/include/features.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">34</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/libc-header-start.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">28</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/lib/gcc/x86_64-linux-gnu/11/include/stddef.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">209</span>&nbsp;<span style="color: #63a35c;">"/usr/lib/gcc/x86_64-linux-gnu/11/include/stddef.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">209</span>&nbsp;<span style="color: #63a35c;">"/usr/lib/gcc/x86_64-linux-gnu/11/include/stddef.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">typedef</span>&nbsp;<span style="color: #066de2;">long</span>&nbsp;<span style="color: #a71d5d;">unsigned</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;size_t;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">34</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/lib/gcc/x86_64-linux-gnu/11/include/stdarg.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">40</span>&nbsp;<span style="color: #63a35c;">"/usr/lib/gcc/x86_64-linux-gnu/11/include/stdarg.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">typedef</span>&nbsp;__builtin_va_list&nbsp;__gnuc_va_list;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">37</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/types.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">27</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/types.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/wordsize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">28</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/types.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/timesize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">19</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/timesize.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/wordsize.h"</span>&nbsp;<span style="color: #0099cc;">1</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">20</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/timesize.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">29</span>&nbsp;<span style="color: #63a35c;">"/usr/include/x86_64-linux-gnu/bits/types.h"</span>&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">typedef</span>&nbsp;<span style="color: #a71d5d;">unsigned</span>&nbsp;<span style="color: #066de2;">char</span>&nbsp;__u_char;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">typedef</span>&nbsp;<span style="color: #a71d5d;">unsigned</span>&nbsp;<span style="color: #066de2;">short</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;__u_short;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">typedef</span>&nbsp;<span style="color: #a71d5d;">unsigned</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;__u_int;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">typedef</span>&nbsp;<span style="color: #a71d5d;">unsigned</span>&nbsp;<span style="color: #066de2;">long</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;__u_long;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;생략&nbsp;...</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">extern</span>&nbsp;<span style="color: #a71d5d;">void</span>&nbsp;funlockfile&nbsp;(FILE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>__stream)&nbsp;__attribute__&nbsp;((__nothrow__&nbsp;,&nbsp;__leaf__));</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">885</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">extern</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;__uflow&nbsp;(FILE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #a71d5d;">extern</span>&nbsp;<span style="color: #066de2;">int</span>&nbsp;__overflow&nbsp;(FILE&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>,&nbsp;<span style="color: #066de2;">int</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">902</span>&nbsp;<span style="color: #63a35c;">"/usr/include/stdio.h"</span>&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #0099cc;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">2</span>&nbsp;<span style="color: #63a35c;">"hello.c"</span>&nbsp;<span style="color: #0099cc;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #0099cc;">3</span>&nbsp;<span style="color: #63a35c;">"hello.c"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main(<span style="color: #a71d5d;">void</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"hello&nbsp;world"</span>);</span></div>
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
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Compiler(cc1)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>cc1이라는 컴파일러가 텍스트 파일 hello.i를 hello.s로 변환합니다. '. s'는 어셈블리 파일입니다. 어셈블리어는 상위 수준 언어들의 컴파일러들을 위한 공통 출력 언어를 제공합니다. hello.c 파일은 다음과 같은 명령어를 통해 어셈블리어로 변환할 수 있습니다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">gcc&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>S&nbsp;helloworld.c</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 변환된 hello.s 파일은 다음과 같습니다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.file&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"hello.c"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.text</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.section&nbsp;&nbsp;&nbsp;&nbsp;.rodata</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">.LC0:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">string</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"hello&nbsp;world"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.text</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.globl&nbsp;&nbsp;&nbsp;&nbsp;main</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.type&nbsp;&nbsp;&nbsp;&nbsp;main,&nbsp;@function</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">main:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">.LFB0:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.cfi_startproc</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;endbr64</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;pushq&nbsp;&nbsp;&nbsp;&nbsp;%rbp</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.cfi_def_cfa_offset&nbsp;<span style="color: #0099cc;">16</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.cfi_offset&nbsp;<span style="color: #0099cc;">6</span>,&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">16</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;movq&nbsp;&nbsp;&nbsp;&nbsp;%rsp,&nbsp;%rbp</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.cfi_def_cfa_register&nbsp;<span style="color: #0099cc;">6</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;leaq&nbsp;&nbsp;&nbsp;&nbsp;.LC0(%rip),&nbsp;%rax</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;movq&nbsp;&nbsp;&nbsp;&nbsp;%rax,&nbsp;%rdi</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;movl&nbsp;&nbsp;&nbsp;&nbsp;$0,&nbsp;%eax</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;call&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>@PLT</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;movl&nbsp;&nbsp;&nbsp;&nbsp;$0,&nbsp;%eax</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;popq&nbsp;&nbsp;&nbsp;&nbsp;%rbp</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.cfi_def_cfa&nbsp;<span style="color: #0099cc;">7</span>,&nbsp;<span style="color: #0099cc;">8</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;ret</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.cfi_endproc</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">.LFE0:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">size</span>&nbsp;&nbsp;&nbsp;&nbsp;main,&nbsp;.<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>main</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.ident&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"GCC:&nbsp;(Ubuntu&nbsp;11.3.0-1ubuntu1~22.04)&nbsp;11.3.0"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.section&nbsp;&nbsp;&nbsp;&nbsp;.note.GNU<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #066de2;">stack</span>,<span style="color: #63a35c;">""</span>,@progbits</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.section&nbsp;&nbsp;&nbsp;&nbsp;.note.gnu.property,<span style="color: #63a35c;">"a"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.align&nbsp;<span style="color: #0099cc;">8</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">long</span>&nbsp;&nbsp;&nbsp;&nbsp;1f&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>&nbsp;0f</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">long</span>&nbsp;&nbsp;&nbsp;&nbsp;4f&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>&nbsp;1f</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">long</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">5</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">0</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">string</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"GNU"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">1</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.align&nbsp;<span style="color: #0099cc;">8</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">long</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0xc0000002</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">long</span>&nbsp;&nbsp;&nbsp;&nbsp;3f&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>&nbsp;2f</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">2</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.<span style="color: #066de2;">long</span>&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0099cc;">0x3</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">3</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;.align&nbsp;<span style="color: #0099cc;">8</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0099cc;">4</span>:</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Assembler(as)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>이 단계에서는 어셈블러(as)가 hello.s를 기계어 인스트럭션으로 번역하고, 이들을 재배치(realocation) 가능 목적프로그램(오브젝트 코드) 형태로 묶습니다. 여기서 재배치란 목적프로그램을 원래 정의되었던 주소와 다른 주소에 적재될 수 있게 목적 프로그램을 변경하는 것입니다. 재배치 목적프로그램은 다른 재배치 가능 목적 프로그램과 결합하게 됩니다. hello.o는 바이너리 파일로 다음과 같은 명령어로 생성할 수 있습니다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">gcc&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span>c&nbsp;hello.c</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 변환된 hello.o 파일은 다음과 같습니다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">ELF<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span>`@@</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">óúUHåHHÇ¸è¸]Ãhello&nbsp;worldGCC:&nbsp;(Ubuntu&nbsp;<span style="color: #0099cc;">11.</span><span style="color: #0099cc;">3.</span><span style="color: #0099cc;">0</span><span style="color: #a71d5d;">-</span>1ubuntu1~<span style="color: #0099cc;">22.</span><span style="color: #0099cc;">04</span>)&nbsp;<span style="color: #0099cc;">11.</span><span style="color: #0099cc;">3.</span>0GNUÀzRx#EC</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Zñÿ&nbsp;&nbsp;&nbsp;&nbsp;#hello.cmainprintfüÿÿÿÿÿÿÿüÿÿÿÿÿÿÿ&nbsp;.symtab.strtab.shstrtab.rela.text.data.bss.rodata.comment.note.GNU<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #066de2;">stack</span>.note.gnu.property.rela.eh_frame&nbsp;@#@&nbsp;0<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&amp;</span>c,c1c90o,BR&nbsp;&nbsp;jÀ8e@Ð&nbsp;&nbsp;&nbsp;&nbsp;ø&nbsp;&nbsp;&nbsp;&nbsp;èt</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Linker(1d)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; hello.c에서 호출하는 printf 함수는 표준 C 라이브러리에 존재합니다. 위 과정에서 산출된 hello.o 파일은 hello.c 내부 코드만 바이너리로 변환했을 뿐, 표준 C 라이브러리가 제공하는 함수들이 포함돼 있지는 않습니다. 따라서 작성한 코드와 포함해야 하는 라이브러리들을 하나의 실행가능 목적 파일로 묶어줘야 하는데 링커가 이 일을 합니다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 'hello.c'에서 호출한 printf에 대한 목적 파일은 '/usr/bin' 디렉터리에 위치하는 것을 확인할 수 있습니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="852" data-origin-height="80"><span data-url="https://blog.kakaocdn.net/dn/dqf9Ek/btr4qzk5W9y/P1LgzkFdfa8JYqgL0FvUY0/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdqf9Ek%2Fbtr4qzk5W9y%2FP1LgzkFdfa8JYqgL0FvUY0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="852" data-origin-height="80"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 링커는 printf 목적파일과 hello.o파일을 결합시킵니다. 이로 인해 hello 파일은 실행가능 목적파일로 메모리에 적재된 시스템에 의해 실행됩니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1264" data-origin-height="126"><span data-url="https://blog.kakaocdn.net/dn/Uz1Re/btr4t6IG8FN/dUnQFlOGcnzUI6TpxWqiK0/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUz1Re%2Fbtr4t6IG8FN%2FdUnQFlOGcnzUI6TpxWqiK0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1264" data-origin-height="126"></span></figure>
<p></p>
<h2 style="color: #000000; text-align: start;" data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>컴퓨터 구조</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정을 통해 사용자가 작성한 소스 프로그램은 hello라는 실행가능한 목적 파일로 번역되어 디스크에 저장되었습니다. 이제 './hello'라는 명령어로 hello 목적파일을 실행시켰을 때 어떤 과정으로 프로그램이 동작하고 종료하는 지를 알아보기 위해 우선 현대 컴퓨터 구조부터 살펴보겠습니다.</span></p>
<h3 style="color: #000000; text-align: start;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>폰 노이만 구조</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>현대의 컴퓨터라고 하면 보통은 stored prgram computer를 의미합니다. Stored program computer는 애플리케이션이 컴퓨터 자체에 내장되어 있고 여러 태스크를 진행할 수 있도록 프로그래밍된 컴퓨터를 의미합니다. sotred computer program 컨셉을 다루었고, 현대에 모든 컴퓨터가 따르고 있는 구조가 폰 노이만 구조입니다. 폰 노이만 구조는 다음과 같습니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1204" data-origin-height="882"><span data-url="https://blog.kakaocdn.net/dn/bLaISj/btr4v9EJg1y/TfvQ52n9EwYdxBqlHJVVU1/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbLaISj%2Fbtr4v9EJg1y%2FTfvQ52n9EwYdxBqlHJVVU1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="538" height="394" data-origin-width="1204" data-origin-height="882"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 그림을 3가지 구성 요소로 요약하면 memory, CPU(processor), I/O device가 됩니다. 폰 노이만 구조를 좀 더 현대 컴퓨터 구조에 맞게 상세히 그리면 다음과 같은 모습을 가집니다.<b></b></span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1450" data-origin-height="1160"><span data-url="https://blog.kakaocdn.net/dn/dQjcXq/btr4uION04E/5ObvZ8B6tFtwkJ6qP75sIK/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdQjcXq%2Fbtr4uION04E%2F5ObvZ8B6tFtwkJ6qP75sIK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="633" height="506" data-origin-width="1450" data-origin-height="1160"></span></figure>
<p></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>프로세서(processor)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>메인 메모리에 저장된 인스트럭션들을 해독하는 엔진입니다. PC(Program Counter)가 존재해 인스트럭션을 가리킵니다. 전원이 들어오면 전원이 꺼질 때까지 프로세서는 PC가 가리키는 인스트럭션을 반복적으로 실행하고 PC가 다음 인스트럭션을 가리키게 업데이트하기를 반복합니다. 레지스터 파일은 각각의 이름을 갖는 워드 크기의 레지스터 집합으로 구성돼 있습니다.&nbsp; 워드(word)는 고정 크기의 바이트 단위로 시스템마다 한 개의 워드를 구성하는 바이트 수가 다릅니다. 현재 대부분의 컴퓨터는 4바이트(32비트) 또는 8바이트(64비트)입니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 인스트럭션 요청이 오면 CPU는 다음과 같은 작업을 실행합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 적제(Load)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>메인 메모리에서 레지스터로 한 바이트 또는 워드를 이전 값에 덮어쓰는 방식으로 복사합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 저장(Store)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>레지스터에서 메인 메모리로 한 바이트 또는 워드를 이전 값을 덮어쓰는 방식으로 복사합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 작업(Operate)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>두 레지스터의 값을 ALU로 복사하고 두 개의 워드로 수식연산을 수행한 뒤, 결과를 덮어쓰기 방식으로 레지스터에 저장합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 점프(jump)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>인스트럭션 자신으로부터 한 개의 워드를 추출하고, 이것을 PC에 덮어쓰는 방식으로 복사합니다.</span></p>
<h4 style="color: #000000; text-align: start;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>메인 메모리(Main Memory)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>CPU 근처에 위치해 있습니다. 프로세서가 프로그램을 실행하는 동안 데이터와 프로그램을 모두 저장하는 임시 저장장치입니다. 임시이기 때문에 휘발성 메모리입니다. 논리적으로 연속적인 바이트들의 배열로 이루어져 있고 0부터 시작하는 고유의 주소를 가지고 있습니다.</span></p>
<h4 style="color: #000000; text-align: start;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>입출력 장치(I/O device)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>시스템과 외부세계를 연결하는 역할을 합니다. 각 입출력 장치는 입출력 버스와 컨트롤로 또는 어댑터를 통해 연결됩니다. 컨트롤러와 어댑터의 차이는 패키징(packaging)에 있습니다. 컨트롤러 디바이스는 자체가 하나의 칩셋이거나 시스템의 머더보드에 장착되어 있습니다. 반면 어댑터는 머더보드 슬롯에 장착되는 카드입니다.</span></p>
<h4 style="color: #000000; text-align: start;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>버스(bus)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Data control signal을 싣고 다니는, 시스템 내를 관통하는 전기적 배선군입니다.</span></p>
<h2 style="color: #000000; text-align: start;" data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>hello 프로그램 실행</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>이제부터 hello 프로그램이 실행되는 과정을 살펴보겠습니다. 아래의 설명에는 각 인터럽트 과정과 프로세스에 대한 설명은 생략되어 있습니다. 인터럽트에 대한 설명은 글 <a href="https://www.skullkim-dev.com/2023/03/12/interrupt/" target="_blank" rel="noopener">Interrupt</a>를 참고하시면 됩니다. 프로세스에 대한 설명은 <a href="https://www.skullkim-dev.com/2023/02/01/introduction-to-os-chapter-3-1/" target="_blank" rel="noopener">chapter3-1. 프로세스의 개요</a>를 참고하시면 됩니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자가 './hello'라고 터미널에 입력하면 쉘 프로그램은 다음과 같은 과정으로 각 문자를 레지스터에 읽어 들인 뒤 메모리에 저장합니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1440" data-origin-height="1160"><span data-url="https://blog.kakaocdn.net/dn/bcs376/btr4wMJ2xuu/kI4Cw7I1Qmc8Ib99gJcr31/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbcs376%2Fbtr4wMJ2xuu%2FkI4Cw7I1Qmc8Ib99gJcr31%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="635" height="512" data-origin-width="1440" data-origin-height="1160"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; './hello'를 입력한 뒤 엔터를 누르면 쉘은 명령어가 완료된 것을 알 수 있습니다. 이때, 만약 자주 사용하는 명령어라면 해당 명령어는 메인 메모리에 존재하게 됩니다. 'ls'와 같은 명령어가 그 예시입니다. 하지만, './hello'는 자주 사용하는 명령어가 아니므로 쉘은 파일 내의 코드와 데이터를 복사하는 인스트럭션을 실행해 실행 파일 hello를 디스크에서 메인 메모리로 로딩합니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1448" data-origin-height="1170"><span data-url="https://blog.kakaocdn.net/dn/AaXcC/btr4w5JtHpU/jXqHe0MvvXxK0JblBAwcKK/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_6.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAaXcC%2Fbtr4w5JtHpU%2FjXqHe0MvvXxK0JblBAwcKK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="671" height="542" data-origin-width="1448" data-origin-height="1170"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 과정에서 주의할 점은 인터럽트 대신 DMA(Direct Memory Access)를 사용한다는 점입니다. DMA는 디바이스 컨트롤러가 CPU를 통해 메모리로 데이터를 보내지 않고 직접 데이터를 local buffer보다 큰 블록 단위로 메인 메모리로 보내는 방법입니다. 이 방법을 사용하는 이유는 local buffer의 크기가 작아, 디스트에 있는 파일을 일반적인 인터럽트 방식으로 보내면 너무 많은 인터럽트가 발생하기 때문입니다. DMA를 사용하면 오직 블록이 하나가 보내졌을 때, 모든 내용이 메모리에 완벽히 저장된 후에만 인터럽트가 발생합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 hello 목적 파일의 코드와 데이터가 메모리에 모두 적제 되었습니다. 프로세서는 hello 프로그램의 main 루틴 기계어 인스트럭션을 실행합니다. 이 인스트럭션들은 "hello world" 스트링을 메모리에서 레지스터 파일로 복사하고, 디스플레이 장치로 전송합니다. 그러면 "hello world"라는 스트링이 화면에 보이게 됩니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1456" data-origin-height="1156"><span data-url="https://blog.kakaocdn.net/dn/cfTPCW/btr4uQ7xMfw/vJeD8OINzdKv6ffm85Unik/img.png" data-lightbox="lightbox"><img src="/img/2023-03-17-computer-structure-program/img_7.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfTPCW%2Fbtr4uQ7xMfw%2FvJeD8OINzdKv6ffm85Unik%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="718" height="570" data-origin-width="1456" data-origin-height="1156"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp;</p></div>