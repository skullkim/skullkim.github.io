---
layout:       post
title:        "Chapter 3-2. 프로세스 제어 블록과 문맥 교환"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>프로세스 제어 블록</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; PCB는 다음과 같은 구조를 가진다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="265" data-origin-height="479"><span data-url="https://blog.kakaocdn.net/dn/uOiMC/btrXQhJJIhI/ZFOjBkcESKYj5I1ON3DcKk/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-2/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuOiMC%2FbtrXQhJJIhI%2FZFOjBkcESKYj5I1ON3DcKk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="265" data-origin-height="479"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>포인터</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; PCB를 연결해 준비 상태나 대기 상태의 큐를 구현할 때 포인터를 사용한다. 대기 상태에서 빠르게 프로세스를 탐색하기 위해 같은 입출력을 요구하는 프로세스들끼리만 하나의 대기 큐에 모아놓는다. 이후에 입출력 매니저로 부터 인터럽트가 도착하면 PCB를 대기 큐에서 찾아 준비 상태로 이동시키면서 큐에서 제거한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="458" data-origin-height="269"><span data-url="https://blog.kakaocdn.net/dn/ev8AwJ/btrXM3zx8AR/rKtTMlLqYdniZe6NqXzCF0/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-2/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fev8AwJ%2FbtrXM3zx8AR%2FrKtTMlLqYdniZe6NqXzCF0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="458" data-origin-height="269"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>프로세스 상태</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스의 현재 상태를 나타낸다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>프로세스 구분자</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여러 프로세스를 구별하기 위한 구분자를 저자앟ㄴ다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>프로그램 카운터</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다음에 실행될 명령어의 위치를 가리키는 프로그램 카운터 값을 저장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>프로세스 우선순위</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 대기 큐에 있는 모든 프로세스는 각자의 우선순위를 가진다. 사용자 프로세스 보다 커널 프로세스의 우선순위가 더 높다. 사용자 프로세스끼리도 우선순위가 갈린다. CPU 스케줄러는 준비 상태에서 실행 상태로 프로세스를 옮길 때 이 우선순위를 기준으로 한다. 높은 우선순위를 가진 프로세스가 더 먼저 더 자주 실행된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>각종 레지스터 정보</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스가 실행 중 사용하면 레지스터의 중간값이 저장된다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>메모리 관리 정보</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스가 위치하는 메모리 주소, 메모리 보호를 위한 경계 레지스터 값과 한계 레지스터 값 등이 저장된다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>할당된 자원 정보</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스를 실행하기 위해 사용하는 입출력 자원이나 오픈 파일 등에 대한 정보다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>계정 정보</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 계정 번호, CPU 할당/사용 시간 등의 정보</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>부모 프로세스 구분자(PPID)와 자식 프로세스 구분자(CPID)</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>부모 프로세스를 가리키는 PPID, 자식 프로세스를 가리키는 CPID가 저장된다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>문맥 교환(Context Switching)</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>Context swithcing은 실행 상태이던 프로세스가 준비 상태가 되고, 다른 프로세스가 실행 상태가 되는 것을 의미한다. Context switching은 다음과 같은 절차로 이루어진다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="474" data-origin-height="452"><span data-url="https://blog.kakaocdn.net/dn/tziDJ/btrXK7ITuMF/eU6U8IQZoUNysXp5k5Iko0/img.png" data-lightbox="lightbox"><img src="/img/2023-02-01-introduction-to-os-3-2/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtziDJ%2FbtrXK7ITuMF%2FeU6U8IQZoUNysXp5k5Iko0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="474" data-origin-height="452"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p></div>