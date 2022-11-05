---
layout:       post
title:        "Process, Thread"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- ComputerScience
- OS
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스는 사전적으로 '무엇인가 진행되고 있는 것'을 의미한다. 컴퓨터에서 프로세스는 실행중인 프로그램이다. 컴퓨터 프로그램은 프로그래밍 언어로 작성되고 컴파일 과정을 통해 object file(또는 실행 파일) 형태로 하드디스크에 저장된다. 즉, 프로그램은 목적코드로 작성된 하나의 파일이다. 이런 프로그램을 실행하기 위해 주기억장치에 적재하고 운영체제하의 관리 개체로 등록된다. 이 상태가 프로세스이다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 범용 컴퓨터에서는 여러개의 프로세스가 동시에 존재한다. 따라서 프로세스를 식별하고 관리하기 위해 다음과 같은 속성들이 필요하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>1. PID(Process Identification Number)</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 새로운 프로세스가 생성될 때마다 운영체제는 고유한 식별 번호를 부여한다. 여기서의 고유함은 현재 실행 중인 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 프로세스들로 제한된다. 따라서 한 프로세스가 끝나면 이 프로세스에게 부여된 PID가 다른 프로세스에게 할당된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>2. 프로세스 메모리 정보</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 하나의 연속된 메모리 공안에 여러 개의 프로세스가 할당된다. 따라서 각각의 프로세스가 메모리의 어느 부분을 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 차지하고 있는지 관리해서 프로세스들이 서로의 메모리 공간을 침범하지 않게 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>3. Process Status</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 운영체제가 CPU를 어느 프로세스에게로 점프(할당)시켜 줄 것인가를 탐색하기 위해서는 프로세스 현재 상태가 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 필요하다.(프로세스가 I/O가 완료되기를 기다리는지, CPU할당을 기다리는 지 등).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;<i><b> 4. Program Counter</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 운영체제가 선택한 프로세스에게 CPU를 점프시켜주기 위해서는 프로세스별로 실행지점이 관리되야 한다. 즉, 선택된 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 프로세스를 처리 중이던 CPU는 운영체제가 설정해 둔 timer interrupt에 의해 언젠가 그 프로세스를 떠나게 된다. 이 때&nbsp; &nbsp; &nbsp; 다음 실행할 기계 명령어에 대한 주소를 기록해 둬야만 다음 기회에 연속된 처리가 가능하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>5. Process Context</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 모든 연산은 CPU 안에서 이뤄진다. 따라서 연산 명령어가 실행되는 과정에서 메모리에 존재하는 피연산자가 CPU로 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 옮겨지고, 연산 결과는 CPU안에 임시 존재하게 된다. 피연산자와 연산 결과는 CPU안에 저장 장소인 레지스터에 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 저장된다. 이렇게 현재 프로세스에 의해 CPU 안에서 생산되 보관 중인 값 들을 process context라 한다. 연산이 끝난 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 시점에서 interrupt에 의해 CPU가 운영체제로 되돌아가면 프로세스에서 생산된 CPU 레지스터 값들이 파괴된다. 이 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 상태에서 해당 프로세스를 나중에 연속해서 실행하게 되면 이전 연산값들이 파괴되 정상적인 진행을 할 수 없다. </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 따라서 CPU가 진행 중이던 프로세스를 떠날 때 process context는 보관되었다가 나중에 처리를 재개하기 직전에 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 복원되야 한다. 이를 context switching이라 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>6. Process Priority</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 운영체제는 CPU를 점프시켜 줄 프로세스를 선택해야 한다. 이 때 우선순위가 필요하다. process priority는 최초에 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 기본으로 설정되었다가 CPU를 기다린 시간, 입출력 여부, 메모리 포화 여부 등 주변 환경에 따라 운영체제에 의해 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 동적으로 조정되거나 관리자에 의해 변경될 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>7. Process Resource</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 프로세스는 진행 중 운영체제에서 다양한 자원을 요청한다. 메모리, 디스크 파일 등 물리적인 자원들과 네트워크 포트 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 등 논리적인 자원들을 사용한다. 프로세스별로 할당 자원들이 관리되야 사후 자원의 회수와 재활용이 가능하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; <i><b>8. Accounting Information</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; &nbsp; 프로세스가 최초로 생성되 지금까지 머무른 시간, 실제로 CPU가 배정되 실행된 시간, 메모리 사용량 등 프로세스의 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 성능이나 비용 산정에 필요한 정보가 관리되야 한다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">PCB(Process Control Block)</span></b></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스가 생성된다는 것은 프로세스가 운영체제에 의해 하나의 관리 개체로 등록됨을 의미한다. 이때 프로세스 관리를 위해 모든 정보를 기록하는 표를 PCB라 한다. PCB의 수는 생성 가능한 최대 프로세스 수를 의미한다. PCB는 위에서 언급된 속성들을 저장한다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/UHJvY2VzcywgVGhyZWFk/img.png">
    </span>
    <figcaption>PCB</figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Process Status</span></b></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;생성된 프로세스는 종료될 때까지 운영체제에 의해 다음과 같은 상태를 오가면서 진행된다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/UHJvY2VzcywgVGhyZWFk/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>준비(Ready)상태</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i></i>&nbsp; &nbsp; 운영체제 외부로부터의 요청에 의해 최초로 프로세스가 생성되었거나, CPU를 배정받아 실행 도중 주어진 시간이 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만료되 다음 CPU </span><span style="font-family: 'Noto Serif KR';">배정 차례를 기다리고 있는 상태이다. 여러 개의 프로세스가 이 상태에 있을 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>실행(Running)상태</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i></i>&nbsp; &nbsp; 운영체제에 의해 준비 상태에 있던 프로세스에게 CPU가 배정되면 그 프로세스는 실행 상태가 된다. CPU 배정은 CPU의&nbsp; &nbsp; 제어 흐름이 해당 프로세스로 점프함을 의미한다. 이 과정을 dispatch라고도 한다. 준비 상태의 프로세스가 여러개면 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 운영체제는 프로세스 우선순위 등 다양한 기준 설정 방법에 의거해 CPU를 배정할 프로세스를 선택한다. 운영체제의 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이런 활동을 CPU 스케줄링이라 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>대기(Blocked) 상태</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp; &nbsp;&nbsp;</b>프로세스가 입출력을 하기 위해서는 시스템 호출을 이용해 운영체제의 도움을 받아야 한다. 이 경우, 해당 프로세스를 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 실행되지 못하고 입출력이 완료될 때까지 기다려야 한다. 즉, 이경우 프로세스는 CPU 배정 대상이 아니기 때문에 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 운영체제는 그 프로세스를 대시 상태로 기록했다가, 입출력 완료 interrupt를 받으면 준비 상태로 전환시켜 CPU 배정 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 대상 프로세스에 추가한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; <i><b>보류(Suspended) 상태</b></i></span></p>
<p data-ke-size="size16">&nbsp; &nbsp; <span style="font-family: 'Noto Serif KR';">어느 한 프로세스가 시스템을 통해 운영체제에게 준비 상태에 있는 다른 프로세스에 대해 보류 요청을 하면, 운영체제는 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 즉시 해당 프로세스를 보류 상태로 놓고 재개 요청이 있을 때까지 CPU 배정 대상에서 제외시킨다. 보류 요청은 외부의 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스에 의해서 뿐만 아니라, 메모리 부족 등 심각한 상황이 발생하면 운영체제 자체의 필요성에 의해 자체적으로 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이루어질 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<i><b>대기 보류(Block-suspended) 상태</b></i></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><i><b>&nbsp; &nbsp;&nbsp;</b></i>메모리 등 시스템 자원이 심각하게 부족하거나, 지나치게 오래 대기 상태를 유지하면 대기 상태의 프로세스를 보류 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 상태로 전환해 자원을 회수한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<b>종료(Terminated) 상태</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 프로세스가 모든 처리르 마치고 시스템 호출을 통해 운영체제에게 완료 요청을 하면 운영체제는 해당 프로세스를 종료 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 상태로 전환하고 제거 준비를 한다. 이 상태의 프로세스를 좀비(Zombie)라 한다. 유닉스의 경우 좁비는 그의 부모 </span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스가 운영체제에게 보낸느 제거 요청에 의해 완전히 사라진다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Thread</span></b></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">스레드는 '실행 줄기'이다. 프로세스는 프로그램의 entry point에서 시작되는 명령어 처리의 흐름 줄기 즉, 실행 줄기를 갖게 된다. 이것이 하나의 스레드이고 스레드가 하나이면 단인 스레드 프로세스이다. 스레드는 프로세스의 구성 요소 중의 하나로서, 프로세스의 다른 구성 요소인 메모리(기계 명령어, 데이터)를 따라 흐르는 개념적인 개체이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하지만 관례적으로 프로세스를 스레드의 상대되는 개념을 정의해 스레드가 하나인 경우엔 스레드란 용어를 결부시키지 않고 단순히 프로세스라 한다. 스레드의 진정한 의미를 다중 스레드 프로세스에서 찾을 수 있기 때문이다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">Multi-thread Process</span></b></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">프로세스는 사용자에 의해 작성된 프로그램이 실행되기 위해 메모리에 적재되 있는 상태를 말한다. 이 때 multi-thread(또는 multi-thread process)는 메모리에 적재된 프로그램의 entry point가 여러 곳 이여서, 해당 프로세스를 바탕으로 진행하는 실행 줄기가 여러 개 존재한다는 의미다. 다중 스레드는 2 개 이상의 CPU가 동일 프로세스 메모리 영역에 있는 기계 명령어를 실행하는 것이다.</span></p>
<p></p><figure class="imageblock alignCenter" width="535" height="482">
    <span data-lightbox="lightbox">
        <img src="/img/UHJvY2VzcywgVGhyZWFk/img_2.png" width="535" height="482">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp;&nbsp;<span style="font-family: 'Noto Serif KR';">위 그림의 경우 CPU1은 main1 함수부터 시작하고 CPU2는 main2 함수부터 시작한다. 이들은 각자의 제어 흐름에 따라 독립적으로 진행되고 이들 각각이 스레드이다. 이 두 개의 CPU가 main1, main2를 각자 실행할 때에는 서로 다른 기계어를 실행하지만 add함수 부분을 실행할 때에는 같은 기계어 코드를 실행한다. 그러면 서로 다른 두 개의 스레드가 거의 동시에 add함수를 실행한다면 각자의 결과 값이 유지될까?</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스레드들이 동일한 기계 명령어를 실행해도 연산 과정이 고유하게 유지된다. 이는 기계 명령어는 동일해도 피연산자를 위한 최종 목적 주소가 분리 되는 원리다. add 함수에서 상요되는 모든 변수는 지역 변수들이다. 지역 변수들은 모두 CPU내에 존재하는 SP(Stack Pointer)에 저장된 주소값을 기준으로 한 상대적 거리로 참조된다. 따라서 thread1을 위한 CPU1의 SP 값과 thread2를 위한 CPU2의 SP 값을 다르게 설정하면 add 함수의 기계어 코드는 동일하지만 그 기계어 코드가 참조하는 최종 피연산자 주소는 다르다. 이와 같이 스레드들의 연산 고유성을 유지하기 위한 저장 공간을 stack 영역이라 한다. stack 영역은 스레드가 시작할 때 할당되고 해당 스레드를 실행하는 CPU의 SP 값은 할당된 스택 영역으로 초기화된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다중 스레드는 반드시 CPU가 여러 개 있어야만 의미가 있는 것은 아니다. 운영체제가 CPU를 배정하는 단위를 프로레스가 아닌 스레드로 세분화 시키기 때문에 하나의 프로세스 위를 여러 개의 스레드들이 통과할 수 있고, 이 떄의 프로세스 개념은 스레드들을 위한 Resource Conatiner로 재정의 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다중 스레드 환경에서는 전역 변수를 참조하는 경우를 주의해야 한다. 위 코드의 경우 s를 참조하는 부분을 주의해야 한다.전역변수는 절대 주소로 참조되기 때문에 해당 변수에 대한 스레드들의 참조 주소는 모두 동일한 메모리 주소이다. 따라서 위 예제에서 동시에 s를 참조할 경우 올바른 계산을 위해 동기화 장치가 필요하다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">프로세스 및 스레드를 위한 운영체제 서비스(기능)</span></b></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">프로세스 생성 및 제거</span></b></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자가 원하는 새로운 프로세스를 생성하고 제거하는 것은 운영체제의 가장 기본적인 기능 중 하나다. 아래의 그림은 유닉스 시스템에서 사용자가 실행시키고자 하는 프로그램을 위한 프로세스 생성, 제거 과정이다.</span></p>
<p></p><figure class="imageblock alignCenter" width="603" height="439">
    <span data-lightbox="lightbox">
        <img src="/img/UHJvY2VzcywgVGhyZWFk/img_3.png" width="603" height="439">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정을 설명하면 다음과 같다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 사용자가 키보드에서 하드디스크에 저장된 프로그램(실행 파일)의 이름 'sample'을 입력한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 사용자로부터 문자열 'sample'을 입력 받은 쉘 프로세스가 유닉스 운영체제의 fork() 시스템 콜을 호출하면, 운영체제는 fork()를 요청한 프로세스 즉, 쉘프로세스와 동일한 프로세스를 복사, 생성해 새로운 프로세스 자리를 확보한다. 이 때 부모 프로세스는 물론, 자식 프로세스도 fork()에서 복귀하는 과정부터 실행이 이어진다. 다만, 부모 프로세스에서의 fork()의 복귀 값은 자식 프로세스의 id(&gt; 0)이고, 자식 프로세스에서의 복귀 값은 0이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 새로 확보된 자리를 차지한 자식 프로세스는, 유닉스 운영체제의 exec() 시스템 콜을 호출해 운영체재로 하여금 현재 확보된 프로세스 자리에 새로운 프로그램인 'sample' 프로그램을 적재하도록 요청한다. exec() 시스템 호출이 성고하면 새로운 프로그램 'sample'이 처음부터 실행을 시작한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 'sample' 프로세스가 실행을 종료하기 위해 유닉스 운영체제의 exit() 시스템 콜을 호출하면, 운영체제는 해당 프로세스를 제거하고 그 결과를 wait()에서 대기 중인 부모 프로세스에게 알린다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">프로세스간 통신(Inter-Process Communication: IPC)</span></b></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">처리할 일의 규모가 크거나 복잡해지면 하나의 프로그램을 개발 효율성과 처리 성능 향상을 위해 여러 개의 작은 프로그램으로 분리해야 한다. 여러 개의 작은 프로그램으로 큰 일을 처리하기 위해서는 관련된 프로세스들이 데이터를 주고 받을 수 있는 통신 수단이 필요하다. 가장 일반적인 통신 수단은 TCP/IP(socket)와 pipe이다. 이런 통신 수단 외에도 메시지 큐, 공유 메모리 등이 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">프로세스 통제(Process Control)</span></b></p>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">사용자들은 프로그램을 작성한 후 프로세스에 대해 어떤 조치를 취해야 할 수 있다. 이때, 사용자느 운영체제가 제공하는 프로세스 통제 수단을 통해 원하는 조치를 취할 수 있다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft" data-ke-style="style1">
<tbody>
<tr>
<td style="width: 8.91465%;">통제 유형</td>
<td style="width: 45.5426%;">통제 내용</td>
<td style="width: 45.5426%;">사용 시점</td>
</tr>
<tr>
<td style="width: 8.91465%;">강제 종료</td>
<td style="width: 45.5426%;">1. 실행중인 프로그램이 스스로 종료하기 전에 무조건 강제 종료하게 한다</td>
<td style="width: 45.5426%;">1. 오류로 인해 프로그램이 무한 루프로 실행되고 있을 때<br>2. 프로그램이 아무런 반응 없이 정지(hold) 상태일 때</td>
</tr>
<tr>
<td style="width: 8.91465%;">일지 중지</td>
<td style="width: 45.5426%;">1. 완전히 종료하도록 하는 것은 아니고, 임시로 CPU의 할당을 받지 못하여 더 이상의 실행이 이뤄지지 않게 한다.</td>
<td style="width: 45.5426%;">1. 프로그램의 출력 결과를 감시하고 있는 도중 잠시 자리를 비울 때<br>2. 프로그램을 단계적으로 실행하면서 진행 과정을 분석할 때<br>3. 운영체제의 부하가 심해서 일지적으로 수행을 보류시킬 때</td>
</tr>
<tr>
<td style="width: 8.91465%;">실행 재개</td>
<td style="width: 45.5426%;">1. 일시 중시 상태에 있는 프로세스가 CPU를 할당 받아서 계속 수행될 수 있도록 한다.<br>2. 우선 순위에 따라 다른 프로세스와 공평하게 CPU를 할당받는다.</td>
<td style="width: 45.5426%;">1. 일시 중지된 프로그램을 재개할 때</td>
</tr>
<tr>
<td style="width: 8.91465%;">약속 처리</td>
<td style="width: 45.5426%;">1. 프로그램을 작성할 때 약속했던 처리 부분들을 실시간으로 지시한다.</td>
<td style="width: 45.5426%;">1. 프로그램 안에 저장된 특정 변수의 값을 임의의 시점에 덤프하고 싶을 때&nbsp;<br>2. 특정 상태를 초기화시켜 처음부터 새로 시작하도록 할 때<br>3. 자식 프로세스의 종료 등 특정 이벤트에 대한 처리를 지시하고자 할 때</td>
</tr>
<tr>
<td style="width: 8.91465%;">우선순위 변경</td>
<td style="width: 45.5426%;">1. 실행 중인 프로그램의 우선순위를 올리거나 내린다.<br>2. 일반 사용자는 내리기만 가능하고, 관리자는 양쪽 모두 가능하다.</td>
<td style="width: 45.5426%;">1. 프로세스 우선순위를 올리거나 내려서 처리 완료 시간을 조정하고자 할 때</td>
</tr>
</tbody>
</table>
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