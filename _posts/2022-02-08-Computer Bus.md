---
layout:       post
title:        "Computer Bus"
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
                            <p data-ke-size="size16">&nbsp;&nbsp;<span style="font-family: 'Noto Serif KR';">컴퓨터 버스는 컴퓨터 시스템에서 데이터, 주소, 제어 신호, 파워를 컴퓨터 시스템의 여러 구성 요소들에게 전달하는 연결이다. 컴퓨터 버스는 여러 하드웨어 구성 요소을 연결하는 데 사용된다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23"><b><span style="font-family: 'Noto Serif KR';">Computer Bus</span></b></h3>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">컴퓨터 시스템은 수 많은 구성 요소들로 구성되 있다. 이 부품들은 물리적으로 연결되 있고 컴퓨터 시스템을 가로지르는 전선망을 통해 커뮤니케이션한다. 이 전선망들이 컴퓨터 버스이며 컴퓨터 시스템이 작동하는데 반드시 필요하다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 버스는 하나의 컴퓨터 구성 요소에서 다른 구성 요소로 정보가 흐르는 컴퓨터 시스템에서 사용되는 일반적인 커뮤니케이션 경로다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 버스 시스템은 연결될 구성 요소들과 버스가 하는 기능에 따라 여러 타입들로 구성되 있다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 버스는 connection wire 또는 PCB로 묶인 와이어 세트로 구성될 수 있으며 CPU로부터 메모리와 시스템에 연결된 다양한 구성 요소들로 데이터와 명령들을 전달한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 버스 폭과 버스 속도는 시스템 퍼포먼스에 영향을 미친다.</span></p>
<h3 data-ke-size="size23"><b><span style="font-family: 'Noto Serif KR';">System Bus</span></b></h3>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">시스템 버스는 컴퓨터를 구성하는 주요 요소들을 연결해 정보를 주고 받는 통신 선로다. 와이어 하나 당 0 또는 1 두 가지 정보(1비트)를 전달 할 수 있다.&nbsp;</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q29tcHV0ZXIgQnVz/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Address Bus</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; CPU가 메모리의 정보를 읽거나 쓸 때, 메모리 위치(주소)를 전달하기 위한 버스이다. CPU가 지원할 수 있는 메모리 용량에 따라 와이어 개수가 결정된다. 4G Byte 까지의 메모리 용량을 지원하는 CPU면 32개의 와이어가 필요하다(0 ~ (2^32) - 1)</span></p>
<h4 data-ke-size="size20"><b><span style="font-family: 'Noto Serif KR';">Data Bus</span></b></h4>
<p data-ke-size="size16"><b><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;</span></b><span style="font-family: 'Noto Serif KR';">메모리에 기록할 데이터나 메모리에서 읽힌 데이터를 전달하는 용도로 사용된다. 하드웨어 설계 상 address bus와 data bus가 동시에 사용되지 않을 경우 address bus의 일부를 data bus로 활용하는 경우도 있다. 데이터 버스의 크기는 한번에 실어 나를 수 있는 최대 바이트 수에 따라 결정된다. CPU와 메모리 사이에 최대 4 바이트까지 한꺼번에 전달해야 한다면 데이터 버스는 32개의 선(32비트)로 구성되야 한다.</span></p>
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