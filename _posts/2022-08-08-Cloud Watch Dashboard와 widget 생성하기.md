---
layout:       post
title:        "Cloud Watch Dashboard와 widget 생성하기"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- aws
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
                            <h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>CouldWatch</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>AWS cloudWatch 는 AWS에서 제공하는 모니터링 서비스다. 이 모니터링 서비스는 서비스와 사용되고 있는 자원들을 유지보수 하기 위해 고안되었다. cloudWatch 는 특정 AWS 서비스와 사용자가 관리해야 하는 애플리케이션에 대한 통계적 데이터, 지표, 인사이트를 수집하고 로그, 지표, 이벤트 형식으로 보여준다 보여준다.&nbsp;<b></b></span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>용어</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; CloudWatch 내에서 사용되는 용어는 다음과 같다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - namespace: EC2, RDS 등 서비스</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - metric: CPU 사용량 등 지표</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - demension: 인스턴스를 그룹화할 수 있는 지표. type(nano, micro, etc), instance id, 등</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - statistics: 특정 기간동안 집계된 Metrics 데이터들의 집합</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>CouldWatch dashboard</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>CloudWawtch dashboard는 cloudWatch console에서 시스템 리소스 사용량을 한눈에 모니터링할 수 있게 해준다. 리소스들이 서로 다른 리전에 존재한다 해도 하나의 대시보드 내에서 모니터링할 수 있다. Dashboard에 나열 가능한 지표는 <a href="https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/viewing_metrics_with_cloudwatch.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 완성된 dashboard는 다음과 같은 모양을 갖는다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;Dashboard 만들기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; EC2를 모니터링 하는 기준으로 설명하겠다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Dashboard를 만들기 위해선 cloudWatch의 지표 &gt; 모든 지표로 들어가면 된다. 여기서 '찾아보기' 탭에 있는 아래와 같은 검색창에서 모니터링 하길 원하는 EC2 instance id를 검색하면 된다. instance id는 EC2 관련 콘솔창에서 인스턴스 카테고리의 인스턴스 항목에서 조회할 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 원하는 instance id를 입력하면 다음과 같은 항목이 검색된다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_2.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 "EC2&gt;인스턴스별 지표"를 클릭하면 해당 인스턴스에서 모니터링할 수 있는 지표를 조회할 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_3.png">
    </span>
    <figcaption>조회된 지표 중 일부</figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 지표 중 원하는 지표를 선택해 다음과 같은 그래프를 만들 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_4.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 생성한 그래프를 대시보드에 추가하기 위해 작업 &gt; 대시보드 추가를 누르면 다음과 같은 모달이 뜬다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_5.png">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_6.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; "대시보드에 추가" 모달 창에서 기존 대시보드에 만든 그래프를 추가하고 싶다면 해당 대시보드 이름을 검색해 선택하면 된다. 대시보드를 새로 생성해야 한다면 "새로 생성"버튼을 클릭해 생성하면 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; cloudWatch는 다양한 그래프 형태를 "위젯 유형"이라는 이름으로 제공하고 있다. 현재 예시에서 볼 수 있는 유형은 "행"이며 모달 창에서 "위젯 유형" 부분에서 원하는 형태를 선택할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 설정을 완료했다면 "대시보드에 추가" 버튼을 클릭해 대시보드에 추가할 수 있다. 이제 "대시보드 저장" 버튼을 누르면 새로 추가된 그래프를 대시보드에 저장할 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_7.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 대시보드에 추가된 그래프들은 위젯 형태이기 때문에 자유롭게 이동하거나 편집할 수 있다. 원하는 위젯을 클릭해 위치를 바꾸거나&nbsp; 위젯의 우측 하단을 클릭하고 드래그해서 크기를 조절할 수도 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;위젯 편집</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>각 위젯 우측 상단에는 '더보기' 버튼이 존재한다. 이 버튼을 클릭하고 편집 항목을 클릭해 위젯을 편집할 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_8.png">
    </span>
    <figcaption></figcaption>
</figure><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/Q2xvdWQgV2F0Y2ggRGFzaGJvYXJk7JmAIHdpZGdldCDsg53shLHtlZjquLA=/img_9.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; "그래프 편집" 모달 창에서 "찾아보기" 항목을 클릭해 해당 위젯에 그래프를 추가하거나 추가된 그래프를 없앨 수 있다. 위에서 설명한 "dashboard 만들기" 과정과 같이 원하는 그래프를 검색하면 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; "그래프로 표시된 지표"에서는 해당 그래프가 보여주고 있는 통계값을 조정할 수 있다. cloudWatch가 제공하고 있는 통계값들은 <a href="https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/monitoring/Statistics-definitions.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
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