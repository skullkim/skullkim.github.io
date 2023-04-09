---
layout:       post
title:        "Chapter3-4. 스레드"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>스레드의 개념</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>스레드의 정의</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스 작업 과정은 다음과 같다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. OS가 코드와 데이터를 메모리에 올린다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. PCB를 생성한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 작업에 필요한 메모리 영역을 확보한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 준비된 프로세스를 준비 큐에 삽입한다.(준비 상태)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. CPU 스케줄러가 프로세스가 해야 할 일을 CPU에 전달하고 실제 작업을 CPU가 수행한다. (실행 상태)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정에서 CPU 스케줄러가 CPU에 전달하는 일 하나가 스레드다. 따라서 CPU가 처리하는 작업의 단위가 스레드이다. OS입장에서 작업 단위는 프로세스이고 CPU입장에서 작업 단위는 스레드이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 작업을 크기 순으로 나열하면 job &gt; task &gt; operation이다. 이를 프로세스와 스레드 관계로 대입하면 처리(job) &gt; 프로세스(task) &gt; 스레드(operation)가 된다. 여러 개의 프로세스를 모아서 한 번에 처리하는 방법을 일괄 작업(batch job)이라 한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>프로세스와 스레드 차이</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스끼리는 약하게 연결돼 있지만 스레드끼리는 강하게 연결돼 있다. 프로세스와 스레드의 차이는 멀티태스크와 멀티스레드에서 더 극명히 드러난다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>멀티태스크 (multi task)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스는 서로 독립적으로 작동하면서 필요할 때 데이터를 주고받는다. 이때의 통신을 프로세스 간 통신(IPC - Inter Porcess Communicatino)이라 한다. 프로세스들은 서로 독립적이기에 한 프로세스의 비정상 종료가 다른 프로세스들에게 영향을 주지 않는다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>멀티스레드 (multi thread)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>스레드끼리는 강하게 연결돼 있기 때문에, 멀티스레드는 변수나 파일 등을 공유하고, 전역 변수나 함수 호출 등의 방법으로 스레드 간 통신을 한다. 따라서 하나의 프로세스가 종료되면 내부의 스레드도 강제로 종료된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>스레드 관련 용어</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>멀티스레드</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>프로세스가 프로세스 내 작업을 여러 스레드로 분할해 작업 부담을 줄이는 방식이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="446" data-origin-height="368"><span data-url="https://blog.kakaocdn.net/dn/bbx7lt/btrZIfxciSr/kSNnYjtHS3OgXRzGmTulhk/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbbx7lt%2FbtrZIfxciSr%2FkSNnYjtHS3OgXRzGmTulhk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="333" height="275" data-origin-width="446" data-origin-height="368"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>멀티태스킹</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 운영체제가 CPU에 작업을 줄 때 시간을 나누어 배분하는 기법이다. 여러 스레드에 시간을 나누어 주는 시스템을 시분할 시스템(time-sharing system)이라 한다. 시분할 시스템에선 OS가 CPU에 전달하는 작업이 스레드이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="468" data-origin-height="416"><span data-url="https://blog.kakaocdn.net/dn/KuoCK/btrZJcmdFG4/rx0dxOPP591ay4YunT3i1k/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKuoCK%2FbtrZJcmdFG4%2Frx0dxOPP591ay4YunT3i1k%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="342" height="304" data-origin-width="468" data-origin-height="416"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>멀티프로세싱</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; CPU를 여러 개 사용해 여러 개의 스레드를 동시에 처리하는 작업 환경을 말한다. 병렬 처리에서 슈퍼스칼라 기법과 같다. 멀티프로세싱은 하나의 컴퓨터에 여러 CPU 또는 하나의 CPU 내에서 여러 개의 코어에 스레드를 배정해 동시에 작동하는 것이다. 네트워크로 연결된 여러 컴퓨터에 스레드를 나누어 협업하는 분산 시스템도 멀티프로세싱이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="468" data-origin-height="388"><span data-url="https://blog.kakaocdn.net/dn/LMxRd/btrZERRKwq7/u46rTqRBok1OqxPaqwq1xK/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLMxRd%2FbtrZERRKwq7%2Fu46rTqRBok1OqxPaqwq1xK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="373" height="309" data-origin-width="468" data-origin-height="388"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>CPU 멀티스레드</b><b></b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 한 번에 하나씩 처리해야 하는 스레드를 파이프라인 기법으로 동시에 여러 스레드를 처리하는 병렬 처리 기법이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 멀티 스레드: OS가 소프트웨어적으로 프로세스를 작인 단위의 스레드로 분할해 운영하는 기법이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - CPU 멀티 스레드: 하드웨어적인 방법으로 하나의 CPU에서 여러 스레드를 동시에 처리하는 병렬 처리 기법이다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="490" data-origin-height="202"><span data-url="https://blog.kakaocdn.net/dn/cP8yNo/btrZJCrIr52/jsn5MghCUJTskPx3o5vdP0/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcP8yNo%2FbtrZJCrIr52%2Fjsn5MghCUJTskPx3o5vdP0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="323" height="133" data-origin-width="490" data-origin-height="202"></span></figure>
<p></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>멀티스레드의 구조</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스 입장에서 스레드의 생성과 구성을 살펴보자. 멀티 태스킹을 위해 fork() 시스템 호출로 프로세스를 복사하면 코드 영역과 데이터 영역 일부가 메모리에 중복돼 존재한다. 하지만, 이들은 독립적인 프로세스이기에 낭비 요소를 제거할 수 없다. 반면, 멀티 태스킹 대신 멀티 스레드를 사용하면, 코드, 데이터 등을 공유해 여러 개의 일을 하나의 프로세스에서 진행한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스는 실행되는 동안 영역이 바뀌는지에 따라 동적인 영역과 정적인 영역으로 나뉜다. 동적인 영역의 예로는 레지스터 값, 스택, 힙 등이 존재한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1930" data-origin-height="686"><span data-url="https://blog.kakaocdn.net/dn/2Cy4v/btr0KGf9v5X/lUjgB7FoBKN4hoggfYQsKk/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F2Cy4v%2Fbtr0KGf9v5X%2FlUjgB7FoBKN4hoggfYQsKk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1930" data-origin-height="686"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 그림에서 볼 수 있듯이 멀티 스레드는 정적 영역을 공유해 효율을 높인다. 따라서 스레드를 가벼운 프로세스(LWP - Light Weight process)라고도 부른다. 반대로 스레드가 1개인 일반 프로세스는 무거운 프로세스(HWP - Heavy Weight Process)라고도 부른다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>멀티스레드의 장단점</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>멀티 스레드의 장점</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 응답성 향상</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>한 스레드가 입출력으로 인해 작업이 진행되지 않더라도 다른 스레드가 작업을 계속해 사용자의 작업 요구에 빨리 응답할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 자원 공유</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 한 프로세스 내에서 독립적인 스레드를 생성하면 프로세스가 가진 자원을 모든 스레드가 공유하게 되어 작업을 원활하게 진행할 수 있다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 효율성 향상</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여러 개의 프로세스를 생성하는 것과 달리 멀티스레드는 불필요한 자원의 중복을 막아 시스템 효율이 향상된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>- 다중 CPU 지원</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>2개 이상의 CPU를 가진 컴퓨터에서 멀티스레드를 사용하면 다중 CPU가 멀티스레드를 동시에 처리해 CPU 사용량이 증가하고 프로세스 처리 시간이 단축된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>멀티 스레드의 단점</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스레드가 자원을 공유하기 때문에 한 스레드에 문제가 생기면 전체 프로세스에 영향을 미친다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>멀티스레드 모델</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스레드도 프로세스와 마찬가지로 커널 스레드(kernel thread)와 사용자 스레드(user thread)로 나뉜다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 커널 스레드: 커널이 직접 생성하고 관리하는 스레드</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 사용자 스레드: 라이브러리에 의해 구현된 일반적인 스레드.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>사용자 스레드</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 운영체제가 멀티스레드를 지원하지 않을 때 사용하는 방법으로 초기 스레드 시스템에서 이용되었다. 사용자 레벨에서 스레드를 구현하기 때문에 커널이 지원하는 스케줄링이나 동기화 같은 기능을 대신 구현한 라이브러리를 사용한다. 따라서 커널 입장에서는 이 스레드는 하나의 스로세스처럼 보인다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자 스레드는 커널 입장에서 일반 프로세스이지만 커널이 하는 일을 라이브러리가 대신 처리해 여러 개의 스레드를 작동한다. 따라서 사용자 프로세스 내에 여러 개의 스레드가 존재하지만 커널의 스레드 하나와 연결돼 있어 1 to N 모델이라 한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="846" data-origin-height="408"><span data-url="https://blog.kakaocdn.net/dn/kDhvB/btr0RRapR0D/6DKlXStdTroKiuj2xWKpzK/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkDhvB%2Fbtr0RRapR0D%2F6DKlXStdTroKiuj2xWKpzK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="728" height="351" data-origin-width="846" data-origin-height="408"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자 스레드는 라이브러리가 직접 스케줄링을 하고 작업에 필요한 정보를 처리하기 때문에 문맥 교환이 필요 없다. 하지만 여러 개의 스레드가 하나의 커널 스레드에 연결돼 있기 때문에 커널 스레드가 입출력 작업을 위해 대기 상태에 들어가면 모든 사용자 스레드가 같이 대기하게 된다. 또 한, 한 프로세스의 타임 슬라이스를 여러 스레드가 공유하므로 어려 개의 CPU를 동시에 사용할 수 없다. CPU를 여러 개 갖추고 멀티스레드를 지원하는 커널의 경우 스레드를 여러 CPU에 나누어 작업시키는 것이 가능하다. 하지만, 커널 입장에서 사용자 스레드는 하나의 프로세스로 인식되므로 작업을 나눌 수 없다. 마지막으로 공유 변수를 보호하는 장치를 라이브러리가 구현해야 하기에 보안에 취약하다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>커널 스레드(kernel-level thread)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 커널이 멀티스레드를 지원하는 방식으로, 사용자 스레드와 커널 스레드가 1 대 1 대응된다.&nbsp;</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="850" data-origin-height="388"><span data-url="https://blog.kakaocdn.net/dn/7vCrn/btr0RPjjMxb/kAZ5xE5mCWa2teacAeNst1/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_6.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F7vCrn%2Fbtr0RPjjMxb%2FkAZ5xE5mCWa2teacAeNst1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="633" height="289" data-origin-width="850" data-origin-height="388"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 커널 스레드는 커널 레벨에서 모든 작업을 지원하기에 멀티 CPU를 사용할 수 있다. 하나의 스레드가 대기 상태에 있어도 다른 스레드는 작업을 계속할 수 있다. 또 한, 커널의 기능을 사용하므로 보안에 강하고 안정적이다. 하지만 문맥 교환을 할 때의 오버헤드로 인해 느리게 작동한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>멀티레벨 스레드(multi-level thread, hybrid thread)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자 스레드와 커널 스레드를 혼합한 방식으로 M to N 모델이라 부른다. 커널 스레드의 개수가 사용자 스레드보다 같거나 적다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="856" data-origin-height="410"><span data-url="https://blog.kakaocdn.net/dn/66Fi3/btr0NNsFmCR/GPdlCGpgvDrgcuINwFwcKK/img.png" data-lightbox="lightbox"><img src="/img/2023-02-26-introduction-to-os-3-4/img_7.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F66Fi3%2Fbtr0NNsFmCR%2FGPdlCGpgvDrgcuINwFwcKK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="724" height="347" data-origin-width="856" data-origin-height="410"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 멀티레벨 스레드는 커널 스레드와 사용자 스레드의 장단점을 모두 가지고 있다. 하나의 커널 스레드가 대기 상태로 진입하면, 다른 스레드가 대신 작업을 해 유연하게 작업을 처리할 수 있다. 하지만, 문맥 교환 시 오버헤드가 존재해 사용자 스레드만큼 빠르지 않다. 따라서 빠르게 움직여야 하는 스레드는 사용자 스레드로, 안정적으로 움직여야 하는 스레드는 커널 스레드로 작동한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p></div>