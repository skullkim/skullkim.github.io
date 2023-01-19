---
layout:       post
title:        "JVM 겉핥기"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- java
- ComputerScience
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; JVM의 기술 스택의 구조를 이해해 보자. JVM의 전반적인 구조는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1166" data-origin-height="972"><span data-url="https://blog.kakaocdn.net/dn/b5zcAM/btrWDdg4frm/jAvhe4gyzKfd3QC47goT8K/img.png" data-lightbox="lightbox"><img src="/img/2023-01-18-jvm-quick-start/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5zcAM%2FbtrWDdg4frm%2FjAvhe4gyzKfd3QC47goT8K%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1166" data-origin-height="972"></span></figure>
<p></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>인터프리팅과 클래스로딩</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; JVM은 스택 기반 해석 머신이다. 물리적인 레지스터는 없지만, 일부 결과를 실행 스택에 보관하고 맨 위의 값을 가져와 계산한다. JVM 인터프리터의 기본 로직은, 평가 스택을 이용해 중간값들을 담아두고, 가장 마지막에 실행된 명령어와 독립적으로 프로그램을 구성하는 opcode(operation code)를 순차적으로 처리하는 'while 루프 안의 switch문'이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 자바 애플리케이션을 실행하면 클래스 로딩까지 다음과 같은 일이 발생한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1.&nbsp;OS가 가상 머신 프로세스(자바 바이너리)를 구동한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 자바 가상 환경이 구성되고 스택 머신이 초기화된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 유저가 작성한 클래스 파일이 실행된다. 여기서 엔트리 포인트는 main 메서드이며 제어권을 엔트리 포인트가 존재하는 클래스로 넘기기 위해선 가상 머신의 실행이 시작되기 전에 해당 클래스를 로드해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 클래스를 로드하기 위해 자바 클래스 로딩(classloading) 메커니즘이 관여한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. 클래스 로더에서 부트스트랩 클래스가 자바 런타임 코어 클래스를 로드한다. 다른 클래스로더가 나머지 시스템에 필요한 클래스를 로드할 수 있게 최소한의 필수 클래스(java.lang.Object 등)만 로드한다. 런타임 코어 클래스는 java8 까지는 jre/lib/rt.jar에서 가져왔지만 java 9 이후 /lib 내에서 모듈화 되었다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 6. 부트스트랩 클래스로더를 자기 부모로 설정하고, 필요할 때 클래스로딩 작업을 부모에게 넘긴다. 확장 자바 클래스들을 로드해 플랫폼에서 실행되는 모든 애플리케이션에서 표준 코어 자바 클래스를 사용할 수 있게 한다. 모든 확장 클래스로더는 JDK 확장 디렉터리에서 로드된다. 이 디렉터리 경로는 $JAVA_HOME/lib/ext 또는 java.ext.dirs 시스템 속성에 명시된 경로다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 7. 애플리케이션 클래스 로더가 생성되고 지정된 클래스 패스에 있는 유저 클래스를 로드한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 8. 자바는 프로그램 실행 중 처음 보는 클래스를 의존체(dependency)에 로드한다. 찾지 못한 클래스는 부모 클래스 로더에게 의뢰한다. 그럼에도 찾지 못한다면 ClassNotFoundException을 발생시킨다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 9. 보통 환경에서 자바 클래스를 로드할 때 런타임 환경에서 해당 클래스를 나타내는 Class 객체(. class의 인스턴스)를 만든다. 한 시스템에서 클래스를 패키지명을 포함한 풀 클래스명과 자신을 로드한 클래스로더로 식별하므로&nbsp; 똑같은 클래스를 서로 다른 클래스 로더가 두 번 로드할 가능성도 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>바이트 코드 실행</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>자바 코드가 컴파일되면 바이트 코드를 가진. class 파일로 바뀐다. 자바 컴파일러는 컴파일 과정에서 최적화를 거의 하지 않으므로 생성된 바이트 코드를 쉽게 알아볼 수 있다. 바이트 코드는 특정 컴퓨터 아키텍처에 종속되지 않는 중간 표현형(Intermediate Reprsentaion: 소스코드를 표현하기 위해 컴파일러 또는 가상 시스템에서 내부적으로 사용하는 데이터 구조나 코드)이다.&nbsp; 이 점 때문에 JVM을 지원하는 모든 플랫폼에서 실행할 수 있다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; JVM 플랫폼은 자바 언어에 대해 추상화되어 있다. 따라서 JVM 규격에 맞는 클래스 파일로 컴파일된 JVM 언어는 모두 다 실행할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 컴파일러가 생성한 클래스 파일은 VM 명세에 따라 다음과 같은 구조를 가진다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">컴포넌트</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">설명</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">매직 넘버(magic number)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">0xCAFEBABE(클래스 파일임을 나타내는 4byte 넘버)</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스 파일 포맷 버전</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스 파일의 메이저/마이너 버전(클래스를 실행하는 대상 JVM과 컴파일한 JVM의 버전을 확인하기 위해 사용. 대상 JVM 버전이 더 낮다면 UnsupportedClassVersionError 발생).</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">상수 풀(constant pool)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스 상수(클래스명, 필드명 등)들이 모여 있는 위치. 코드 실행 시 런타임에 배치된 메모리 대신, 상수 풀 테이블을 찾아보고 필요한 값을 참조한다.</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">액세스 플래그(access flag)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">추상 클래스, 정적 클래스 등 클래스 종류를 표시</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">this 클래스</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">현재 클래스명</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">슈퍼클래스(super class)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">슈퍼클래스명</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">인터페이스(interface)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스가 구현한 모든 인터페이스</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">필드(field)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스에 들어 있는 모든 필드</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">메서드(method)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스에 들어 있는 모든 메서드</span></td>
</tr>
<tr>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">속성(attribute)</span></td>
<td style="width: 50%;"><span style="font-family: 'Noto Serif KR';">클래스가 지닌 모든 속성(예: 소스 파일명 등)</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; this class, super class, interface는 클래스에 포함된 타입 계층을 나타내며, 각각 상수 풀을 가리키는 인덱스로 표시된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 필드, 메서드는 시그니처와 비슷한 구조를 정의하고 수정자가 포함돼 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 속성은<span id="DragSchLayerPos" style="position: absolute; width: 0px; height: 0px; font-size: 0px;"></span> 더 복잡하고 크기가 고정되지 않은 구조를 나타낸다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 더 자세한 클래스 파일 설명은 <a href="https://blog.lse.epita.fr//2014/04/28/0xcafebabe-java-class-file-format-an-overview.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>핫스팟 입문</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 핫스팟 JVM 구조는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="674" data-origin-height="335"><span data-url="https://blog.kakaocdn.net/dn/I6TYP/btrWDEsOJML/u65R5rGQz1aD69RgYqiBs0/img.png" data-lightbox="lightbox"><img src="/img/2023-01-18-jvm-quick-start/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FI6TYP%2FbtrWDEsOJML%2Fu65R5rGQz1aD69RgYqiBs0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="674" data-origin-height="335"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>JIT 컴파일</b><b></b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 자바 프로그램은 바이트코드 인터프리터가 가상화한 스택 머신에서 명령어를 실행하며 시작된다. 여기서 프로그램 성능 향상을 위해 네이티브 기능을 활용해 CPU에서 직접 프로그램을 실행시키기 위해 JIT 컴파일이라는 기술을 사용한다. JIT 컴파일은 프로그램 단위(메서드와 루프)를 인터프리트 한 바이트코드에서 네이티브 코드로 컴파일한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 핫스팟은 인터프리티드 모드로 실행되는 동안 애플리케이션을 모니터링하면서 가장 자주 실행되는 코드로 JIT 컴파일을 수행한다. 이를 통해 더 정교하게 최적화를 할 수 있다. 특정 메서드가 임계점(threshold)을 넘어가면 프로파일러가 늑정 코드 섹션을 컴파일/최적화한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; JIT 컴파일러는 해석 단계에서 수집한 추적 정보를 통해 최적화를 진행하기 때문에 다양한 정보로 더 좋은 방향으로 최적화할 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>JVM 메모리 관리</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>자바는 GC(Garbage Collection)라는 프로세스를 이용해 힙 메모리를 자동 관리한다. GC는 JVM이 더 많은 메모리를 할당해야 할 때 불필요한 메모리를 회수하거나 재사용하는 불확정적(non-deterministic: 결과가 정해지지 않은) 프로세스이다. GC가 실행되면 다름 애플리케이션은 중단된다. 중단되는 시간은 짧지만 애플리케이션 부하가 는다면 이 점을 고려해봐야 한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>스레딩과 JMM(Java Memory Model)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>주류 JVM 구현체에서 자바 애플리케이션 스레드는 각각 하나의 전용 OS 스레드에 대응된다. 공유 스레드 풀을 이용해 전체 자바 애플리케이션 스레드를 실행하는 방법(green threads)이 있지만, 복잡도는 증가하고 원하는 수준이 나오지 않는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1990년대 후반부터 자바의 멀티스레드는 다음과 같은 기본 설계 원칙을 기반으로 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 자바 프로세스의 모든 스레드는 가비지가 수집되는 하나의 공용 힙을 가진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 한 스레드가 생성한 객체를 참조하는 다른 스레드가 액세스 할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 객체 필드에 final을 붙여 불변으로 바꾸지 않는 한 기본적으로 객체는 가변이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; JMM은 서로 다른 실행 스레드가 객체 안에 변경되는 값을 어떻게 바라볼지를 기술한 메모리 모델이다. 두 개의 스레드가 같은 객체를 참조할 때 하나의 스레드가 내부 상태를 바꾸었다고 하자. 이때, OS 스케줄러는 CPU 코어에서 강제로 스레드를 방출할 수 있다. 때문에 하나의 스레드가 처리 중인 객체를 다른 스레드가 시작되면서 참조할 때, 잘못된 상태의 객체를 바라볼 수 있다. 이를 방지하기 위해 상호 배타적 락(mutual exclusion lock)을 사용한다.</span></p></div>