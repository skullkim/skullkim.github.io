---
layout:       post
title:        "Chapter3-3. 프로세스의 연산"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스의 생성과 복사를 이해하기 위해선 우선 시스템 프로그래밍을 이해해야 한다. 프로세스의 생성과 복사를 설명하기 전에 우선 프로세스의 구조를 파악하자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스의 구조</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스는 코드 영역, 데이터 영역, 스택 영역으로 구성된다. 데이터 영역은 다신 일반 데이터 영역과 힙 영역으로 구분된다.&nbsp;</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 13.2558%;"><span style="font-family: 'Noto Serif KR';">영역 종류</span></td>
<td style="width: 86.7441%;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr>
<td style="width: 13.2558%;"><span style="font-family: 'Noto Serif KR';">코드 영역</span></td>
<td style="width: 86.7441%;"><span style="font-family: 'Noto Serif KR';">프로그램의 본문이 기술된 역역으로 텍스트 영역(text area)이라고도 한다. 프로그램이 해당 영역에 탑재되고 읽기 전용으로 처리된다. 프로그램이 자기 자신을 수정할 수 없기 때문이다.</span></td>
</tr>
<tr>
<td style="width: 13.2558%;"><span style="font-family: 'Noto Serif KR';">데이터 영역</span></td>
<td style="width: 86.7441%;"><span style="font-family: 'Noto Serif KR';">코드가 실행되면서 사용하는 변수나 파일 등의 각종 데이터를 모아놓은 곳이다. 이 영역의 데이터는 읽기/쓰기가 모두 가능하다. 다만, 상수로 선언된 변수는 읽기 전용이다.</span></td>
</tr>
<tr>
<td style="width: 13.2558%;"><span style="font-family: 'Noto Serif KR';">스택 영역</span></td>
<td style="width: 86.7441%;"><span style="font-family: 'Noto Serif KR';">OS가 프로세스를 실행하기 위해 필요한 기타 데이터를 모아놓은 곳이다. 운영체제가 사용자의 프로세스를 작동하기 위해 유지하는 영역이기 떄문에 사용자에게 보이지 않는다.</span></td>
</tr>
</tbody>
</table>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스의 생성과 복사</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자가 프로그램을 실행하면 OS는 프로그램을 메모리로 가져와 코드 영역에 넣고 PCB를 생성한다. 그 후, 데이터 영역과 스택 영역을 확보하고 프로세스를 실행한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스를 새로 실행하는 것뿐만 아니라 복사하는 방법도 존재한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>fork() 시스템 호출의 개념</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; fork() 시스템 호출은 실행 중인 프로세스로부터 새로운 프로세스를 복사하는 함수다. 크롬에서 command + n을 누르면 크롬이 하나 더 생기는 것이 fork()를 사용한 예시다. 이렇게 생성한 프로세스는 부모-자식 관계를 가진다. 기존 프로세스가 부모, 새로 복사된 프로세스가 자식이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>fork() 시스템 호출의 동작 과정</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>fork()를 호출하면 부모 프로세스 영역의 대부분이 자식 프로세스에게 복사된다. 이때, PCB 중 다음과 같은 일부 데이터는 변경이 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - PID가 바뀐다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 메모리 관련 위치가 바뀐다. 부모 프로세스와 자식 프로세스가 차지하는 메모리 위치는 다르다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 부모 프로세스 구분자(PPID)와 자식 프로세스 구분자(CPID)가 바뀐다. 부모 프로세스의 CPID는 fork()를 통해 생성한 자식 프로세스의 PID이다. 자식 프로세스의 PPID는 자신을 생성한 부모 프로세스의 PID이다. 자식 프로세스가 또 다른 자식 프로세스를 가지지 않는다면 자식 프로세스의 CPID는 -1이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1132" data-origin-height="562"><span data-url="https://blog.kakaocdn.net/dn/rxrBe/btrZH1ZTX72/lp5jIqxxMwD3QUqpG1G0lk/img.png" data-lightbox="lightbox"><img src="/img/2023-02-17-introduction-to-operating-system-process-operation/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrxrBe%2FbtrZH1ZTX72%2Flp5jIqxxMwD3QUqpG1G0lk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="749" height="372" data-origin-width="1132" data-origin-height="562"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>fork() 시스템 호출의 장점</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 새로운 프로세스를 만드는 대신 fork()를 이용해 복사한다면 다음과 같은 이점을 가진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 프로세스 생성 속도가 빠르다</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하드디스크로 부터 가져오는 대신 메모리를 복사했기 때문에 자식 프로세스 생성 속도가 빠르다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 추가 작업 없지 자원을 상속할 수 있다.</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp; </b>부모 프로세서가 사용하던 모든 자원을 추가 작업 없이 자식 프로세스에 상속할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 시스템 관리를 효율적으로 할 수 있다.</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 부모 프로세스와 자식 프로세스가 CPID와 PPID로 연결되 있기 때문에&nbsp; 자식 프로세스를 종료하면 사용하던 자원을 부모 프로세스가 정리할 수 있다. 정리를 부모 프로세스에 맡기기 때문에 시스템이 효율적으로 관리된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>fork() 시스템 호출의 예</b></span></h3>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdio.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>unistd.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdlib.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;pid;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;부모&nbsp;프로세스에게&nbsp;0보다&nbsp;큰&nbsp;값을&nbsp;반환한다</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">//&nbsp;자식&nbsp;프로세스에&nbsp;0을&nbsp;반환한다.&nbsp;반환값이&nbsp;0보다&nbsp;작으면&nbsp;생성되지&nbsp;않았음을&nbsp;의미한다.</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;pid&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;fork();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(pid&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;<span style="color: #0099cc;">0</span>&nbsp;)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"%d&nbsp;Error\n"</span>,&nbsp;pid);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">1</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">else</span>&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(pid&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"%d&nbsp;Child\n"</span>,&nbsp;pid);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #0099cc;">0</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">else</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"%d&nbsp;Parent\n"</span>,&nbsp;pid);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #0099cc;">0</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;Output:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;&nbsp;&nbsp;&nbsp;345295&nbsp;Parent</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;Child</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; fork() 사용 시 다음과 같은 점들을 주의해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; fork() 문 이전에 파일을 열거나 변수를 선언하면, 이들은 자식 프로세스에게 상속된다. 부모 프로세스와 자식 프로세스는 서로 독립적이기에 "Parent", "Child" 중 어느 것이 먼저 실행되는지 알 수 없다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스의 전환</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; exec()를 사용하면 현재 프로세스가 완전히 다른 프로세스로 전환된다. exec()를 사용하면 새로 프로세스를 생성하는 것에 비해 PCB, 메모리 영역, 부모-자식 관계를 그래도 사용하고, 새로운 코드 영역만 가져올 수 있어서 프로세스의 구조체를 재활용할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; exec()를 호출하면 코드영역은 새로운 코드로 채워지고, 데이터 영역은 새로운 변수로 채워지고, 스택 영역은 리셋된다. 또 한, 프로그램 카운터 레지스터 값을 비롯해 레지스터와 사용한 파일 정보는 모두 리셋된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>exec() 시스템 호출의 예</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; exec() 시스템 호출 예시를 위해 execlp()를 사용해 보자. execlp()는 path에 등록된 디렉터리를 참고해 다른 프로그램을 실행시킨다. exec()의 원형은 다음과 같다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;첫&nbsp;번째&nbsp;인자&nbsp;path에&nbsp;등록&nbsp;된&nbsp;모든&nbsp;프로그램을&nbsp;실행시킨다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;arg는&nbsp;실행될&nbsp;프로그램에&nbsp;넣을&nbsp;argument&nbsp;이다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;실패하면&nbsp;-1&nbsp;반환.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;execl(&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;<span style="color: #066de2;">char</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>path,&nbsp;<span style="color: #a71d5d;">const</span>&nbsp;<span style="color: #066de2;">char</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">*</span>arg,&nbsp;...)</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 이 예시를 실행하기 위해 exec() 시스템 콜로 자식 프로세스가 실행할 프로그램을 지정하자. 다음과 같은 간단한 코드를 작성 후 이를 "helloWorld"라는 이름의 오브젝트 파일로 만들자.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdio.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main(<span style="color: #066de2;">int</span>&nbsp;argc,&nbsp;<span style="color: #066de2;">char</span><span style="color: #a71d5d;">*</span>&nbsp;argv[])&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"hello&nbsp;%s\n"</span>,&nbsp;argv[<span style="color: #0099cc;">0</span>]);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;<span style="color: #0099cc;">0</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 예시 다음과 같이 예시를 작성하고 실행해보자.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdio.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>unistd.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #0086b3;">#include</span>&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>stdlib.h<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&gt;</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #066de2;">int</span>&nbsp;main()&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">int</span>&nbsp;pid;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;pid&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;fork();</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(pid&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">&lt;</span>&nbsp;<span style="color: #0099cc;">0</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"%d&nbsp;Error\n"</span>,&nbsp;pid);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #ff3399;"></span><span style="color: #a71d5d;">-</span><span style="color: #0099cc;">1</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">else</span>&nbsp;<span style="color: #a71d5d;">if</span>&nbsp;(pid&nbsp;<span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span><span style="color: #ff3399;"></span><span style="color: #a71d5d;">=</span>&nbsp;<span style="color: #0099cc;">0</span>)&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;execlp(<span style="color: #63a35c;">"./helloWorld"</span>,&nbsp;<span style="color: #63a35c;">"world"</span>,&nbsp;<span style="color: #0086b3;">NULL</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #0099cc;">0</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color: #a71d5d;">else</span>&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;wait(<span style="color: #0086b3;">NULL</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">printf</span>(<span style="color: #63a35c;">"mplayer&nbsp;Terminated\n"</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit(<span style="color: #0099cc;">0</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;output:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;&nbsp;&nbsp;&nbsp;hello&nbsp;world</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">//&nbsp;&nbsp;&nbsp;&nbsp;mplayer&nbsp;Terminated</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;위 예시 동작 과정은 다음과 같다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 부모 프로세스에서 fork() 문을 실행해 자식 프로세스를 생성한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. wait() 문을 실행해 지식 프로세스가 끝날 때까지 기다린다. wait()는 자식 프로세스와 동기화를 위한 코드로, 자식 프로세스가 끝날 때까지 부모 프로세스가 기다린다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 새로 생성된 자식 프로세스는 부모 프로세스와 같지만 execlp()가 실행되는 순간, 자식 프로세스의 코드 영역은 helloWorld의 코드로 바뀌고 처음부터 다시 실행된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. helloWorld의 실행이 끝나면 부모 프로세스의 wait()가 있는 곳으로 돌아오고 부모 프로세스는 "mplayer Terminated"를 출력한다. 다시 부모 프로세스로 돌아올 수 있는 이유는 PCB의 프로세스 구분자(PID, PPID, CPID)가 변경되지 않기 때문이다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스의 계층 구조</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 살펴본 프로세스 복사와 전환은 프로세스 생성과 계층 구조를 이해하는 데 중요한 열쇠가 된다. 이제 유닉스를 통해 프로세스의 계층 구조를 알아보자.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>유닉스의 프로세스 계층 구조</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>유닉스에서 커널이 처음 메모리에 올라와 부팅되면 커널 관련 프로그램을 여러 개 만단다. 그중 init 프로세스가 전체 프로세스의 출발점이 된다. init 프로세스가 생성되면 init이 나머지 프로세스를 자식 프로세스로 생성한다. 따라서 OS의 모든 프로세스는 init의 자식 프로세스다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="822" data-origin-height="894"><span data-url="https://blog.kakaocdn.net/dn/PQ8I5/btrZIs3sB1r/RYHHoddA9IeoFQKYxn2PEk/img.png" data-lightbox="lightbox"><img src="/img/2023-02-17-introduction-to-operating-system-process-operation/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPQ8I5%2FbtrZIs3sB1r%2FRYHHoddA9IeoFQKYxn2PEk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="629" height="684" data-origin-width="822" data-origin-height="894"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>프로세스 계층 구조의 장점</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스의 계층 구조는 동시에 여러 작업을 처리하고 종료된 프로세스의 자원을 회수하는 데 유용하다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>여러 작업의 동시 처리</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 계층구조에서 login 프로세스는 동시에 한 명만 처리할 수 있다. 그래서 동시에 여러 사용자가 접근한다면, OS는 fork() 시스템 호출을 이용해 login 프로세스를 여러 개 만들어 대응한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; login 프로세스를 사용한 뒤에는 shell 프로세스가 필요하다. shell이 존재해야 사용자가 OS에 명령을 내리고 결과를 받을 수 있다. 따라서 login 프로세스를 종료하고 shell 프로세스를 생성해야 하는데, 이때 효율적으로 login 프로세스에 할당한 메모리를 재활용하기 위해 exec() 시스템 호출을 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이후 shell 프로세스에서 명령어로 애플리케이션을 실행할 때도 fork()와 exec()를 사용한다.&nbsp;</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>용이한 자원 회수</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스를 계층 구조로 만들면 프로세스 간의 책임 관계가 명확해져 시스템을 수월하게 관리할 수 있다. 프로세스가 부모-자식 관계를 가지면 부모 프로세스가 자식 프로세스를 회수하면 되지만, 이런 관계가 없다면 OS가 매번 직업 자원을 회수해야 한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>고아 프로세스</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 부모 프로세스가 먼저 동료 되거나, 자식 프로세스가 비정상 종료되면 자식 프로세스가 사용하던 자원이 그대로 남아있게 된다. 이렇게 프로세스가 종료 후에도 남아있는 프로세스는 두 종류로 나뉜다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 고아 프로세스(orphan process): 부모 프로세스가 자식보다 먼저 죽는 경우</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 좀비 프로세스(zombie process): 자식 프로세스가 종료했음에도 부모가 자원을 수거하지 않는 경우</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; C언어에서 main 함수 끝에 작성하는 return 또는 exit는 자식 프로세스가 끝났음을 알려서 부모 프로세스가 자원 정리나 자식 프로세스와의 동기화를 할 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p></div>