---
layout:       post
title:        "Chapter3-1. 프로세스의 개요"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16">&nbsp; OS에서 프로세스는 하나의 작업 단위다. 사용자가 프로그램을 실행하면 프로세스가 된다. 폰노이만 구조에서 프로그램을 실행한다는 것은 해당 코드가 메모리에 올라와 작업이 진행된다는 의미다. 프로그램은 저장장치에 저장되어 있는 정적 상태이고, 프로세스는 실행을 위해 메모리에 올라온 동적인 상태다.</p>
<h2 data-ke-size="size26"><b>프로그램에서 프로세스로의 전환</b></h2>
<p data-ke-size="size16">&nbsp; 프로세스는 컴퓨터 시스템의 작업 단위로 테스크(task)를 사용한다.</p>
<p data-ke-size="size16">&nbsp; 프로그램이 프로세스로 전환될 때 운영체제는 프로그램을 메모리에 올린다. 그와 동시에 해당 프로세스 처리에 대한 정보를 지닌 PCB(Process Control Block)를 만든다. PCB에는 여러 가지 정보가 있지만 대표적인 세 가지는 다음과 같다.</p>
<p data-ke-size="size16"><b>프로세스 구분자(PID)</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>메모리에는 다수의 프로세스가 존재하기 때문에 프로세스를 구분하는 고유한 값이 필요하다. 이 값이 PID다.</p>
<p data-ke-size="size16"><b>메모리 관련 정보</b></p>
<p data-ke-size="size16">&nbsp; CPU는 프로세스가 존재하는 메모리 주소를 알아야 실행할 수 있다. 따라서 PCB에는 프로세스의 메모리 위치 정보가 담겨있다. 또한, 메모리 보호를 위해 경계 레지스터와 한계 레지스터도 포함되 있다.</p>
<p data-ke-size="size16"><b>각종 중간값</b></p>
<p data-ke-size="size16">&nbsp; PCB에는 해당 프로세스가 사용했던 중간값이 저장된다. 이는 시분할 시스템에서 여러 프로세스가 번갈아 가며 실행되기 떄문에 다음에 작업해야 할 코드의 위치를 저장하고 있어야 하기 때문이다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp; PCB는 OS가 프로세스를 관리하기 위해 생성되므로 OS 영역에 만들어진다. 프로세스가 종료되면 해당 프로세스가 메모리에서 삭제되고 PCB도 폐기된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="364" data-origin-height="264"><span data-url="https://blog.kakaocdn.net/dn/2DuSn/btrWK2Af4gb/7PfxVfGHZwlb5fD5Euc4EK/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-1/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F2DuSn%2FbtrWK2Af4gb%2F7PfxVfGHZwlb5fD5Euc4EK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="364" data-origin-height="264"></span></figure>
<p></p>
<h2 data-ke-size="size26"><b>프로세스의 상태</b></h2>
<p data-ke-size="size16">&nbsp; OS에서는 여러가지 이유로 프로세스 상태(process status)가 변화된다. 일괄 작업 시스템은 프로세스가 생성된 후 CPU를 얻어 실행되고 작업을 마치면 종료하기 때문에 프로세스 상태는 생성(create), 실행(run), 완료(terminate)이다. 시분할 시스템에서는 CPU가 여러 프로세스를 옮겨 다니며 실행하기에 일괄 작업 시스템보다 복잡하다.</p>
<h3 data-ke-size="size23"><b>프로세스의 네 가지 상태</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>간단한 프로세스 상태는 다음과 같다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="782" data-origin-height="124"><span data-url="https://blog.kakaocdn.net/dn/ccfxoE/btrWI9AELxc/4CTDicOSjCDD1tmVPhtgB0/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-1/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FccfxoE%2FbtrWI9AELxc%2F4CTDicOSjCDD1tmVPhtgB0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="782" data-origin-height="124"></span></figure>
<p></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;">상태</td>
<td style="width: 50%;">설명</td>
</tr>
<tr>
<td style="width: 50%;">생성 상태(create status)</td>
<td style="width: 50%;">프로세스가 메모리에 올라와실행 준비를 완료한 상태다. 프로세스를 관리하는 데 필요한 PCB가 생성된다.</td>
</tr>
<tr>
<td style="width: 50%;">준비 상태(ready status)</td>
<td style="width: 50%;">생성된 프로세스가 CPU를 얻을 때까지 기다리는 상태다. PCB들은 다수의 준비 큐에서 대기한다. CPU 스케줄러가 운영할 준비 큐 갯수와 실행 상태로 보낼 PCB를 결정한다.</td>
</tr>
<tr>
<td style="width: 50%;">실행 상태(running status)</td>
<td style="width: 50%;">프로세스가 CPU를 얻어 실제 작업을 수행하는 상태다. 'execute status'라 표현하기도 한다. 실행 상태의 프로세스는 일정 시간 동안 CPU를 사용한다. 이 시간을 타임 슬라이스 또는 타임 퀀텀이라 한다. 만약 이 시간 동안 작업을 완료하지 못하면 다시 준비 상태로 돌아가 대기한다. 이를 타임아웃이라 한다.<br>CPU 개수 만큼 준비 상태에서 실행 상태로 프로세스가 들어갈 수 있다.</td>
</tr>
<tr>
<td style="width: 50%;">완료 상태(terminate status)</td>
<td style="width: 50%;">실행 상태의 프로세스가 주어진 시간 동안 작업을 마치면 완료 상태로 진입한다. PCB가 사라진 상태를 의미한다. 만약 프로세스가 비정상 종료 됐다면 디버깅을 위해 강제 종료 직전의 메모리 상태를 저장장치로 옮긴다. 이를 코어 덤프(core dump)라 하낟.</td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp; CPU 스케줄러(CPU scheduler)는 준비 상태 맨 앞에 있는 PCB를 CPU에 전달해 작업을 실행한다. 이 같이 준비 상태 프로세스를 골라 실행 상태로 바꾸는 CPU 스케줄러의 작업을 dispatch라 한다.</p>
<p data-ke-size="size16">&nbsp; CPU는 새로운 프로세스가 들어왔을 때 타임 슬라이스가 지나면 알 수 있게 클록을 요청한다. 그러면 일정 시간이 지난 뒤 클록이 인터럽트를 발생시켜서 CPU에게 통지한다.</p>
<h3 data-ke-size="size23"><b>프로세스의 다섯 가지 상태</b></h3>
<p data-ke-size="size16">&nbsp; 위에서 설명한 프로세스 네 가지 상태에서 효율을 높이기 위해 한 가지 상태를 더 추가했다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="733" data-origin-height="278"><span data-url="https://blog.kakaocdn.net/dn/biBAm6/btrXOupw5pC/FVXROSY7llg6HkNYh9KkOk/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-1/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbiBAm6%2FbtrXOupw5pC%2FFVXROSY7llg6HkNYh9KkOk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="733" data-origin-height="278"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 인터럽트 시스템에서 프로세스가 I/O를 요구하면 CPU는 입출력 관리자에게 명령을 내린다. 이 상태에선 느 프로세스가 아무 일도 하지 않기 때문에 CPU 역시 작업을 하지 않는다. 이런 비효율을 막기 위해 입출력이 완료되기까지 기다리는 대기 상태(blocking status)를 만들었다. 프로세스가 입출력을 요청하면 대기상태로 옮겨지고 CPU 스케줄러는 준비 상태에서 새로운 프로세스를 실행시킨다.</p>
<p data-ke-size="size16">&nbsp; 대기 상태의 프로세스는 요청한 입출력이 완료되면 입출력 관리자로부터 인터럽트를 받는다. 그러면 대기 상태에 있던 프로세스는 준비 상태로 돌아간다.</p>
<p data-ke-size="size16">&nbsp; 위 그림의 각 상태 전환 과정을 작업 이름으로 서술하면 다음과 같다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="753" data-origin-height="277"><span data-url="https://blog.kakaocdn.net/dn/DoGGP/btrXLq9BwO9/oUKjohJKIBXQmoWXCzDPd0/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-1/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDoGGP%2FbtrXLq9BwO9%2FoUKjohJKIBXQmoWXCzDPd0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="753" data-origin-height="277"></span></figure>
<p></p>
<h3 data-ke-size="size23"><b>휴식 상태와 보류 상태</b></h3>
<p data-ke-size="size16">&nbsp; 위에서 서술한 다섯 가지 상태를 활성 상태(active status)라 한다. 프로세스는 활성 상태 외에도 다음과 같은 특별한 상태도 갖는다.</p>
<h4 data-ke-size="size20"><b>휴식 상태(pause status)</b></h4>
<p data-ke-size="size16">&nbsp; 프로세스가 램에 존재하지만 작업을 일시 중단한 상태다. 유닉스에서 프로그램 실행 도중 Ctrl+z를 누르면 실행을 멈추는 것이 이 예시다.</p>
<h4 data-ke-size="size20"><b>보류 상태(suspend status)</b></h4>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>프로세스가 메모리에서 스왑 영역(swap area)으로 전환된 상태를 의미한다. 스왑 역역은 메모리에서 쫒겨난 데이터가 임시로 보관되는 장소다. 보류 상태를 '일시 정지 상태'라고도 부른다. 프로세스는 다음과 같은 경우 보류 상태가 된다.</p>
<p data-ke-size="size16">&nbsp; - 메모리가 다 차서 일부 프로세스를 메모리 밖으로 내보낼 때</p>
<p data-ke-size="size16">&nbsp; - 프로그램에 오류가 있어서 실행을 미룰 때</p>
<p data-ke-size="size16">&nbsp; - 악의적인 공격을 하는 프로세스라 판단될 때</p>
<p data-ke-size="size16">&nbsp; - 매우 긴 주기로 반복되는 프로세스라 메모리 밖으로 쫒아내도 큰 문제가 없을 때</p>
<p data-ke-size="size16">&nbsp; - 입출력을 기다리는 프로세스의 입출력이 계속 지연될 때</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp; 보류 상태는 보류 대기 상태(block suspend status)와 보류 준비 상태(ready suspend status)로 구분된다. 각 상태에서 재시작하면 원래의 활성 상태로 돌아간다. 만약 보류 대기 상태에서 입출력이 완료되면 보류 준비 상태로 옮겨간다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="768" data-origin-height="407"><span data-url="https://blog.kakaocdn.net/dn/b9UFX5/btrXOQMF8eR/Fb6k4ESbgiKOQMhX7UnanK/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-1/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9UFX5%2FbtrXOQMF8eR%2FFb6k4ESbgiKOQMhX7UnanK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="768" data-origin-height="407"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">출처 - 쉽게 배우는 운영체제</p></div>