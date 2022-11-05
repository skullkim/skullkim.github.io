---
layout:       post
title:        "VPC (Virtual Private Cloud)"
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
                            <p data-ke-size="size16">&nbsp; AWS가 VPC를 출시한 이후 고객은 각자의 네트워크를 구상하고 가상의 데이터 센터를 설정할 수 있게 되었다. VPC를 구성하게 되면 내부적인 통신을 위해 사용하는 인스턴스 별로 private IP를 설정하고 VPC 내에서 서브넷이라는 단위로 분리해 사용할 수 있다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" width="742" height="366">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img.png" width="742" height="366">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h3 data-ke-size="size23"><b>VPC 설정하기</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>VPC를 만들기 위해선 크게 4단계를 거친다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. IP 주소 범위 선택</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. 가용 영역(AZ)별 서브넷 설정</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. 인터넷으로 향하는 경로(route) 만들기</p>
<p data-ke-size="size16">&nbsp; &nbsp; 4. VPC로 부터의 트래픽 설정</p>
<h4 data-ke-size="size20"><b>1. IP 주소 범위 선택</b></h4>
<p data-ke-size="size16">&nbsp; AWS는 IP 주소를 표현하기 위해 CIDR(Classless Inter-Domain Router)를 사용하고 있다. IP는 IPv4 기준으로 32비트로 이뤄져 있고 4개의 옥탯으로 나눠져 있다. IPv4의 형식은 a.b.c.d와 같으므로 각 a,b,c,d가 하나의 옥탯이다. CIDR는 사용 가능한 IP의 범위를 나타내는 방식이다. 예컨데 172.31.0.0/16은 앞에서 부터 16비트 이후의 비트를 모두 사용가능(172.31.0.0~172.31.255.255) 하다는 의미다. 16을 마스킹값이라 한다.</p>
<p data-ke-size="size16">&nbsp; AWS의 VPC에서 IP를 설정 할 때는 <a href="https://ko.wikipedia.org/wiki/%EC%82%AC%EC%84%A4%EB%A7%9D" target="_blank" rel="noopener">RFC1918</a>을 따르는 것을 권장한다. RFC1918은 사설망에 주소 할당에 대한 표준이다. 또 한, 가능하면 마스킹 값을 16으로 하는 것을 권장한다. VPC를 설정하면 다른 여러 VPC, 데이터 센터와 통신하게 된다. 이때, 연결할 주소와 주소가 겹치면 통신이 불가능하다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; RFC 1918에서 표준으로 정해진 private IP의 표준은 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; - 10.0.0.0 ~ 10.255.255.255 (10/8 prefix)</p>
<p data-ke-size="size16">&nbsp; &nbsp; - 172.16.0.0 ~ 172.31.255.255 (172.16/12 prefix)</p>
<p data-ke-size="size16">&nbsp; &nbsp; - 192.168.0.0 ~ 192.168.255.255 (192.168/16 prefix)</p>
<h4 data-ke-size="size20"><b>&nbsp;2. 가용 영역(AZ)별 서브넷 설정</b></h4>
<p data-ke-size="size16">&nbsp; AWS는 지역 내에 여러개에 가용영역(avaliablity zone)을 지원해 가용성을 극대화고 있다. 서브넷은 이런 가용영역 내에 만들어진다. 여기서 VPC는 172.31.0.0/16 이라는 네트워크다. 따라서 서브넷을 만든다는 것은 이 네트워크 내에서 서브넷을 나눈다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_1.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; VPC의 CIDR의 값이 16이라면 서브넷의 CIDR는 24로 생성하는 것을 권장한다. VPC 서브넷 권고사항을 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; &nbsp; 1. /16 VPC (64K addresses)</p>
<p data-ke-size="size16">&nbsp; &nbsp; 2. /24 subnets (251 addresses)</p>
<p data-ke-size="size16">&nbsp; &nbsp; 3. One subnet per Availability Zone</p>
<p data-ke-size="size16">&nbsp; 여기서 서브넷의 CIDR가 /24라면 이론적으로 256개의 IP를 사용할 수 있어야 한다. 하지만 실제로는 251개의 IP만 사용할 수 있다. 이는 첫 IP와 마지막 IP를 각각 broadcast IP, network를 나타내는 IP로 사용하며 두번째 부터 네번쨰 IP를 AWS가 관리 목적으로 사용하기 떄문이다.</p>
<p data-ke-size="size16">&nbsp; &nbsp;<i> broadcast IP: 특정 호스트에게 패킷을 전송하는 것이 아닌 특정 네트워크 전체로 패킷을 전송하기 위해 사용되는 IP</i></p>
<h4 data-ke-size="size20"><b><span>3. 인터넷으로 향하는 경로(route) 만들기</span></b></h4>
<p data-ke-size="size16"><b><span>&nbsp;&nbsp;</span></b><span>서브넷을 생성했다면 서브넷이 외부 인터넷과 연결되는 경로를 만들어야 한다. 즉, route 정보를 만들어야 한다. 라우팅은 경로를 찾아가는 과정을 의미하며 라우팀의 결과가 라우트다. VPC는 생성되면 디폴트로 서브넷 내에서 통신할 수 있는 route table을 생성한다. 모든 서브넷이 이 route table을 사용할 필요는 없다. 원하는 route table을 만들고 설정해 사용하면 된다.</span></p>
<p data-ke-size="size16"><span>&nbsp; VPC를 만들었다면 다음과 같은 default route table이 생성된다.</span></p>
<p></p><figure class="imageblock alignCenter" width="671" height="444">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_2.png" width="671" height="444">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h4 data-ke-size="size20"><b>&nbsp;4. VPC로 부터의 트래픽 설정</b></h4>
<p data-ke-size="size16">&nbsp; 특정 서브넷에 있는 인스턴스가 외부와 통신하기 위해선 게이트웨이를 설정해야 한다. 게이트웨이는 한 네트워크에서 다른 네트워크로 이동하기 위해 거치는 지점이다. 게이트웨이를 설정하고 기존 VPC와 매핑을 시켜야 해당 VPC 내부에 존재하는 서브넷에 존재하는 트정 EC2 인스턴스에서 인터넷으로 트래픽을 보낼 수 있다.</p>
<p></p><figure class="imageblock alignCenter" width="820" height="365">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_3.png" width="820" height="365">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h4 data-ke-size="size20"><b>&nbsp;5. VPC의 네트워크 보안</b></h4>
<p data-ke-size="size16">&nbsp; 게이트웨이를 설정해 인터넷과 통신을 할 수 있는 경로를 만들었다면 이제는 접속을 허용한 사용자만 접속할 수 있게 보안 정책을 만들어야 한다. AWS는 기본적으로 모든 접속을 불허하기 때문에 외부의 접속을 허용하기 위해 방화벽 설정을 해야 한다. AWS는 크게 두 개의 방화벽 설정을 제공하며 이들은 다음과 같다.</p>
<p data-ke-size="size16"><b>Network ACLs(Access Control List): Stateless firewalls</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>서브넷 단위로 적용되며 stateless로 동작한다. Network ACL은 디폴트로 모든 접근을 허용한다. 하지만 시큐리티 그룹이 모든 접속을 허용하지 않기 때문에 트래픽을 받거나 전속할 수 없다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_4.png">
    </span>
    <figcaption>모든 접속을 허용하는 network ACL</figcaption>
</figure><p></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>여기서의 stateless는 요청을 기억하지 않는다는 의미다. 따라서 인바운드 규칙과 아웃바운드 규칙을 모두 설정해야 한다. 하지만 아웃바운드 규칙은 특정 포트만 열어줄 수 없다. 서버는 사용하는 포트를 특정지을 수 있다. 하지만 클라이언트가 사용하는 포트의 범위는 굉장히 다양하기 때문에 포트를 특정지을 수 없다. 따라서 1204번 이하의 well-known 포트를 제외한 나머지 포트들을 열어준다.</p>
<p data-ke-size="size16">&nbsp; 반대로 statefull은 요청을 기억하고 있기 때문에 인바운드만 설정하면 된다.</p>
<p data-ke-size="size16"><b>Security groups: 애플리케이션 구조</b></p>
<p></p><figure class="imageblock alignCenter" width="717" height="501">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_5.png" width="717" height="501">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; 하나의 VPC 내부에 다음과 같이 네트워크 구조가 생성되 있다고 해보자. 외부에서의 요청은 오직 web server에서만 받고, BackEnd에서는 오직 web server에서 오는 요청만 받아야 한다. backend에는 DB, WAS 등이 존재하기 때문이다. web server는 443 또는 80번 포트에서 오는 모든 요청을 받아야 한다. 이를 설정하기 위해선 다음과 같이 web server의 security group에서 포트를 허용해 주어야 한다.</p>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_6.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; 예를 들어 위와 같이 securigy group의 인바운드 규칙을 설정했다면 8080 포트로 들어오는 모든 요청을 받을 수 있다. (소스는 받을 IP를 의미하며 0.0.0.0/0은 모든 IP를 허용한다는 의미다.)</p>
<p data-ke-size="size16">&nbsp; 또 다른 security group을 보자</p>
<p></p><figure class="imageblock alignCenter" width="753" height="106">
    <span data-lightbox="lightbox">
        <img src="/img/VlBDIChWaXJ0dWFsIFByaXZhdGUgQ2xvdWQp/img_7.png" width="753" height="106">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p data-ke-size="size16">&nbsp; 이 security group의 소스는 IP로 되어있지 않다. 대신 security group으로 명시되 있다. 이렇게 소스를 security group으로 설정한다면 해당 security group을 사용하는 인스턴스들에 한해서 접근을 허용한다. security group을 소스로 하는 이유는 관리의 편의를 위해서다. 위 예시에서 Backend가 오직 Web server의 접근만을 허용하기 위해 web server로 사용되는 모든 인스턴스의 IP를 일일히 허용해야 한다고 가정해 보자. 그러면 web server 인스턴스가 삭제되거나 추가될 때마다 backend sercurity group의 인바운드 규칙을 수정해야 한다.</p>
<p data-ke-size="size16">&nbsp; security group를 사용할 때 보안을 위해 다음과 같은 규칙을 준수해야 한다.</p>
<p data-ke-size="size16"><b>최소 권한 원칙(Principle of Least Privilege)</b></p>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>필요하지 않은 security group을 열어놓지 않는다. 예를 들어 22번 포트를 관리 목적으로 관리해야 한다면, 회사 내의 관리자 IP만 열어 놓아야 한다.&nbsp;</p>
<p data-ke-size="size16"><b>VPC는 engress(outbound)/ingress(inbound)에 대한 security group 생성 가능</b></p>
<p data-ke-size="size16">&nbsp; security group이 있기 때문에 VPC는 outbound와 inbound에 대한 sercurity group을 각각 설정할 수 있게 되었다.&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
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