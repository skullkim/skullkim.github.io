---
layout:       post
title:        "3-5 동적 할당 영역과 시스템 호출"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스의 동적 할당 영역</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>프로세스는 다음과 같은 구조를 가진다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="488" data-origin-height="494"><span data-url="https://blog.kakaocdn.net/dn/bbBCtI/btr0RKpeJ1K/kYtKKzcbL7KLM4a5ORI231/img.png" data-lightbox="lightbox"><img src="/img/2023-02-27-introduction-to-os-3-5/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbBCtI%2Fbtr0RKpeJ1K%2FkYtKKzcbL7KLM4a5ORI231%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="372" height="377" data-origin-width="488" data-origin-height="494"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 코드 영역에는 프로그램 본체가 위치한다. 데이터 영역은 프로그램이 사용하려고 정의한 변수와 데이터가 존재한다. 포인터를 제외하면 일반적인 변수는 크기가 결정된다. 따라서 프로세스 실행 직전에 위치와 크기가 결정되기 때문에 정적 할당 영역이라 부른다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 힙 영역과 스택 영역은 프로세스 실행 중에 크기가 변하므로 동적 할당 영역이라 한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>스택 영역</b><b></b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스택 영역은 함수 호출 시 두 가지 작업을 구현하기 위해 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 호출한 함수가 종료되면 함수를 호출하기 전 코드로 되돌아오기 위해 되돌아올 메모리 주소를 스택에 저장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 변수 사용 범위에 영향을 미치는 영역(scope) 구현에 사용된다. 지역 변수는 함수가 호출될 때만 사용되다가 종료하면 사용한 공간을 반환해야 한다. 따라서 지역 변수를 스택에 저장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스택은 프로세스를 작동하기 위해 커널이 유지하는 자료구조다. 스택은 스레드가 작동하는 동안 추가되거나 삭제되는 동적할당 영역이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>힙 영역</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>동적으로 할당되는 변수 영역이다. 프로그램 실행 중 할당되는 데이터가 위치하게 된다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdio.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdlib.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main(<span style="color: #a71d5d;">void</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;sarr[<span style="color: #0099cc;">50</span>];</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>darr;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;darr&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;(<span style="color: #066de2;">int</span><span style="color: #a71d5d;">*</span>)<span style="color: #066de2;">malloc</span>(<span style="color: #a71d5d;">sizeof</span>(<span style="color: #066de2;">int</span>)&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>&nbsp;<span style="color: #0099cc;">50</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">free</span>(darr);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 코드에서 sarr과 darr은 크기가 같으므로 겉 보기에는 별 차이가 없어 보인다. 하지만 sarr은 프로세스 종료 전까지 메모리를 차지한다. 반면, darr은 필요할 때 메모리를 할당받고, 필요 없을 때 메모리를 반환한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>exit()와 wait() 시스템 호출</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>exit() 시스템 호출</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>exit() 함수는 작업의 종료를 알려주는 시스템 호출이다. 모든 프로세스는 부모-자식 관계를 가진다. 유닉스 프로세스가 init 프로세스로 부터 부모-자식 관계를 만드는 이유는 사용하던 자원을 회수하기 위함이다. exit()을 사용하면 부모 프로세스는 자식 프로세스가 사용하던 자원을 빨리 수거할 수 있다. exit() 인자로 0을 넘기면 정상 종료, -1이면 비정상 종료다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>wait() 시스템 호출</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>자식 프로세스가 종료되길 기다리지 않고 부모 프로세스가 먼저 종료되었다면 자식 프로세스는 고아 프로세스가 된다. 고아 프로세스는 추후 os가 회수하긴 하지만, 시스템 자원을 낭비한다. wait() 시스템 호출은 고아 프로세스 생성을 막기 위해 사용된다. wait() 시스템 호출은 자식 프로세스가 끝나기를 기다렸다가 자식 프로세스가 종료되면 다음 문장을 실행한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p></div>