---
layout:       post
title:        "03. 운영체제의 구조"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
- ComputerScience
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>커널과 인터페이스</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>커널은 프로세스 관리, 메모리 관리, 저장장치 관리와 같은 운영체제의 핵심적인 기능을 모아놓은 것으로 OS의 성능을 좌우한다. OS에는 인터페이스가 존재하는데, 이는 유저의 명령을 전달하고 실행 결과를 알려주는 역할을 한다. 인터페이스의 예로는 유닉스의 셸(shell)이 있다. 따라서 운영체제는 다음과 같이 크게 인터페이스와 커널로 나눠져 있다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="307" data-origin-height="245"><span data-url="https://blog.kakaocdn.net/dn/b5hYYm/btrWdeWS1tN/Sz6y69j9OfoZtsJU2AcbmK/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-introduction-to-operating-system-chapter3/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5hYYm%2FbtrWdeWS1tN%2FSz6y69j9OfoZtsJU2AcbmK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="307" data-origin-height="245"></span></figure>
<p></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>시스템&nbsp; 호출과 디바이스 드라이버</b></span></h2>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>시스템 호출(system call)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 커널은 사용자나 애플리케이션으로부터 컴퓨터 리소스를 보호하기 위해 자원에 직접 접근하는 것을 막는다. 대신 시스템 호출이라는 인터페이스를 이용해 간접적으로 접근할 수 있게 해 준다. 이를 통해 접근하면 안 되는 리소스에 접근하지 못하게 한다. 시스템 호출의 예로는 write(), read(), c언어의 printf() 등이 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 시스템 호출을 기준으로 사용자 모드와 커널 모드가 나뉜다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="396" data-origin-height="249"><span data-url="https://blog.kakaocdn.net/dn/GgInH/btrWll02KWV/uSDRviEDdC076yD1kMDFk1/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-introduction-to-operating-system-chapter3/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGgInH%2FbtrWll02KWV%2FuSDRviEDdC076yD1kMDFk1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="396" data-origin-height="249"></span></figure>
<p></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>유저 모드(user mode)와 커널 모드(kernel mode)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 유저모드는 일반 사용자 애플리케이션이 실행되는 곳이며 제한적인 명령만 수행할 수 있다. 코드를 작성하고 프로세스를 실행시키는 행위는 모두 유저모드에서 일어난다. 반면 커널 모드는 OS가 CPU의 제어권을 가지고 OS 코드를 실행하는 모드라 모든 종류의 명령을 다 실행할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로세스가 실행될 때 유저모드와 커널 모드를 수 없이 왕래한다. 프로세스가 실행되다가 인터럽트가 걸려서 OS가 호출되면 커널 모드가 실행된다. CPU는 유저모드와 커널 모드를 판별하기 위해 mode bit라는 비트를 사용한다. mode bit가 0이면 커널모드, 1이면 유저 모드다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>드라이버(driver)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>커널과 하드웨어의 인터페이스가 드라이버다. 하드웨어 종류는 매우 다양하기에 모든 하드웨어에 맞는 인터페이스를 다 개발하지 못한다. 따라서 커널은 기본적인 I/O 부분만 제작하고, 하드웨어 특성을 반영한 드라이버를 하드웨어 제작자에게 받아 커널이 실행될 때 같이 실행시킨다. 마우스 같이 간단한 디바이스 드라이버는 커널에 포함돼 있지만 그래픽 카드 같은 복잡한 디바이스 드라이버는 사용자가 직접 설치해야 한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>커널의 구성</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 커널이 하는 일은 다음과 같다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">핵심 기능</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">프로세스 관리</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">프로세스에 CPU를 배분하고 작업에 필요한 제반 환경을 제공한다</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">메모리 관리</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">프로세스에 작업 공간을 배치하고 실제 메모리보다 큰 가상공간을 제공한다</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">파일 시스템 관리</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">데이터를 저장하고 접근할 수 있는 인터페이스를 제공한다</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">입출력 관리</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">필요한 입력과 출력 서비스를 제공한다</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">프로세스 간 통신 관리</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">공동 작업을 위한 각 프로세스 간 통신 환경을 지원한다.</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 커널은 위와 같은 기능을 구현하는 방식에 따라 단일형 구조 커널, 계층형 구조 커널, 마이크로 구조 커널로 나뉜다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>단일형 구조 커널(monolithic architecture kernel)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>커널의 핵심 기능을 구현하는 모듈들이 구분 없이 하나로 구성돼 있는 구조다. MS-DOS가 단일형 구조 커널의 예시다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 단일형 구조 커널은 다음과 같은 장단점을 가진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>장점</b><b></b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 모듈이 분리돼 있지 않기 때문에 모듈 간의 통신 비용이 줄어들어 효율적인 운영이 가능하다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>단점</b></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 단일형 구조 때문에 버그나 오류를 처리하기 어렵고, 상호 의존성이 높아 결함이 시스템 전체로 확산될 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 여려 종류의 컴퓨터에 이식하기 위해선 수정이 필요하다. 하지만 단일형 구조는 수정이 어려워 이식이 어렵다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 현대의 OS는 크고 복잡하기 때문에 단일형 OS로 구현하기 어렵다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="391" data-origin-height="260"><span data-url="https://blog.kakaocdn.net/dn/cIkYDA/btrWc1DnlYM/2ZQGPRj84YJzYeKjyK1nvK/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-introduction-to-operating-system-chapter3/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIkYDA%2FbtrWc1DnlYM%2F2ZQGPRj84YJzYeKjyK1nvK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="391" data-origin-height="260"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>계층형 구조 커널(layered architecture kernel)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>비슷한 기능을 가진 모듈을 묶어서 하나의 계층으로 만들고 계층 간 통신을 통해 OS를 구현한 방식이다. 비슷한 기능들이 모듈로 묶어져 있기 때문에 결함을 모듈 내로 가둘 수 있고 해당 계층만 수정하면 되기에 디버깅에 용이하다. 윈도우 같이 현재 사용되는 대부분의 OS가 이 구조로 되어있다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="384" data-origin-height="342"><span data-url="https://blog.kakaocdn.net/dn/cQTPY3/btrWed4eR3q/RYUsiqu6XCvbjJiz4KoaTk/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-introduction-to-operating-system-chapter3/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQTPY3%2FbtrWed4eR3q%2FRYUsiqu6XCvbjJiz4KoaTk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="384" data-origin-height="342"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>마이크로 구조 커널(micro architecture kernel)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>계층형 구조 커널이 다양한 하드웨어와 사용자 요구를 수용하기 위해 계층과 기능을 지속적으로 추가하다 보니, 필요한 하드웨어 용량과 커널 소스가 비약적으로 늘어났다. 그에 따라 오류를 잡기 어려워져서 마이크로 구조 커널이 개발되었다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 마이크로 구조 커널의 OS는 프로세스 관리, 메모리 관리, 프로세스 간 통신 관리 등 기본적인 기능만 제공한다. 대신 사용자 영역에 많은 부분이 구현돼 있다. 각 모듈은 세분화되어 모듈 간 정보 교환은 프로세스 간 통신으로 이뤄진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 각 모듈이 독립적으로 작동하기에 하나의 모듈이 실패해도 전체 OS가 멈추지 않는다. 많은 컴퓨터에 이식이 쉽고 가볍기에 CPU 용량이 적은 시스템에도 적용 가능하다. 마하(Mach)라는 커널이 이 구조를 채택하고 있다. 마하는 OS X와 ios에 사용되었다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="539" data-origin-height="452"><span data-url="https://blog.kakaocdn.net/dn/cIF9d9/btrWefuf8AF/BmoqIr5cT57fbhLsm8ziUk/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-introduction-to-operating-system-chapter3/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcIF9d9%2FbtrWefuf8AF%2FBmoqIr5cT57fbhLsm8ziUk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="539" data-origin-height="452"></span></figure>
<p></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>가상머신</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; C 언어와 같이 플랫폼에 의존적인 언어는 호환성이 떨어져서 한쪽에서 만든 소스코드가 다른 OS에서는 작동하지 않는다. 이런 호환성 문제를 해결한 언어가 자바다. 자바는 OS 위에 가상머신을 띄우고 그 위에서 실행된다. 가상머신은 애플리케이션과 OS 사이에서 작동하는 프로그램으로, 가상머신을 설치하면 애플리케이션이 모두 동일한 환경에서 작동하는 것처럼 모인다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="271" data-origin-height="220"><span data-url="https://blog.kakaocdn.net/dn/UXWBV/btrWedJZd6T/JSv8KDd61pzv5eVSjUWwDK/img.png" data-lightbox="lightbox"><img src="/img/2023-01-15-introduction-to-operating-system-chapter3/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUXWBV%2FbtrWedJZd6T%2FJSv8KDd61pzv5eVSjUWwDK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="271" data-origin-height="220"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - 쉽게 배우는 운영체제</span></p></div>