---
layout:       post
title:        "DNS(Domain Name System)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- DNS
- HTTP
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
                            <p>네트워크 호스트: 컴퓨터 네트워크에 연결된 컴퓨터나 기타 장치이다.</p>
<p>IP: 인터넷 상에 있는 컴퓨터의 고유한 주소이다.&nbsp;</p>
<p>&nbsp; 예~~전에는 IP만으로 호스트를 연결했다. 하지만 IP주소는 기억하기 어렵다는 단점이 있어서 Jon Postel과 Paul Mockapetris에 의해 DNS가 만들어졌다.&nbsp;</p>
<p>&nbsp; DNS의 핵심음 DNS Server이고 이 서버에는 수많은 IP와 대응되는 도메임 주소가저장되 있다. 도메인을 통해 특정 호스트에 접근하려 한다면 먼저 DNS 서버와의 통신을 통해 접속하고자 하는 호스트의 IP주소를 얻고 그 IP주소로 해당 호스트와의 요청, 응답을 주고받는다.</p>
<p>&nbsp;<b>host, IP</b></p>
<p>&nbsp; &nbsp;두 대의 컴퓨터가 인터넷을 통해 접속하기 위해서는 반드시 IP 주소가 있어야된다. 클라이언트가 서버에 접속하기 위해서는 서버의 IP를 알아야하고, 서버가 클라이언트에 접속하기 위해서는 클라이언트의 IP주소를 알아야한다. 여기서 인터넷에 연결된 각 컴퓨터를 호스트라 한다. 그런데 IP주소가 참 기억하기 어렵다. 이를 해결하는 방법 중 하나는 hosts라는 파일을 이용하는 거다. 운영체제 마다 위치는 다르지만 모든 운영체제에는 hosts라는 파일이 존재 하는데 여기에 IP에 대응되는 임의의 도메인과 IP주소를 적으면 적은 도메인으로 접속할 때 대응되는 IP로 접속을 하게 된다. 이 방법을 사용하면 DNS를 사용하지 않고도 호스트에 도메인을 부여할 수 있다.&nbsp;</p>
<p><b>도메인과 보안</b></p>
<p>&nbsp; hots파일에 도메인을 설정하면 그 도메인이 우선권을 갖게 된다. 만약 hosts파일이 변질될 경우 전혀 다른 페이지로 넘어갈 수 있다. 예를 들어 hosts가 변질되 google.com가 다른 IP와 매칭이 됬다면 해당 페이지에서 사용되는 이메일,비밀번호 등을 탈취당할 수 있다.&nbsp;</p>
<p><b>DNS의 원리</b></p>
<p><b>&nbsp;&nbsp;</b>특정 IP를 가진 사용자가 다른 사용자가 특정 도메인을 통해 자신에게 접속을 하게 하고 싶다면 Domain Name System Server(이하 DNSS)에게 IP와 그에 대응되는 도메인을 요청하면 된다. 그러게 되면 DNSS는 해당 도메인과 IP를 기억하게 된다. 그 후 외부 사용자가 특정 도메인으로 접속을 시도하게 되면 이 사용자의 컴퓨터에 존재하는 hosts파일에서 이 도메인을 검색하고 없다면 DNSS에 요청을 보내 IP주소를 알아낸다. 그 후 이 사용자는 알아낸 IP를 통해 통신을 하게 된다.&nbsp;</p>
<p><b>Public DNS의 사용</b></p>
<p>&nbsp; &nbsp;위에서 설명한 대로 DNS를 사용하려면 사용자의 컴퓨터는 DNSS의 도메인 또는 IP를 알고 있어야 한다. 이는 사용자 컴퓨터가 인터넷에 접속을 했을때 Internet Service Provider(ISP, 통신사)가 이 매커니즘을 자동으로 세팅한다. 따라서 사용자의 컴퓨터가 인터넷에 접속을 하면 특정 DNSS의 IP를 가지게 된다. 만약 현재 자신의 컴퓨터가 알고있는 DNSS가 아닌 다른 DNSS를 알고싶다면 본인이 DNSS를 골라서 거기에 등록을하면 된다.&nbsp; &nbsp;&nbsp;</p>
<p><b>도메인 이름의 구조</b></p>
<p>&nbsp; DNSS의 기능은 크게 두가지의 기능을 한다. 1. 도메인 등록, 2. 등록된 도메인의 IP를 알려주는 역할. 전 세계에는 수 많은 DNSS가 존재하고 이들이 서로 상호작용을 한다. blog.example.com이라는 도메인이 있다고 가정해 보자. 사실 '.com'뒤에는 '.'이 하나 더 붇지만 통상적으로 이를 생략하고 사용한다. 따라서 원칙적으로는 blog.example.com.이 되야된다. 여기서 각 부분마다 명칭이 있는데 이 도메인의 경우</p>
<p>blog(sub domain).example(second-level domain).com(top-level domain).(root name)가 된다. 그리고 각 부분을 담당하는 DNSS가 존재한다. 그리고 Root name를 담당하는 DNSS는 top-level domain을 담당하는 DNSS를 알고있고 top-level domain을 담당하는 DNSS는 second-level domain을 담당하는 DNSS를 알고있고 second-level domain을 담당하는 DNSS는 sub domain을 담당하는 DNSS를 알고있다. 여기서 sub domain을 담당하는 DNSS서버가 IP를 알고있다.</p>
<p><b>DNS의 원리</b></p>
<p>&nbsp; Root name server는 ICANN이라는 단체가 관리를 하고 Top-level domain은 Registry라는 기관이 관리를 한다. 도메인을 등록하고 싶을 경우 Registar에 수수료를 지불하고 원하는 도메인을 알려주면 registar는 registry에게 해당 도메인을 알려준다. 그 후 registry는 registar를 통해 도메인 등록자에게 해당 도메인이 등록이 되었음을 알린다.</p>
<p>&nbsp; Root name server는 top-level domain을 관리하는 서버를 알고 있다. 이때 Top-level domain server에 등록하고자 하는 도메인의 아이피주소를 설정할 수 없으므로 개인서버에 name server를 설치해야 하고 도메인을 세팅하거나 Registar가 제공하는 또는 무료 네임 서버를 사용해야 한다. 이때 Top-level domain서버가 name server를 알아야 되므로 Resitar에 원하는 도메인과 네임서버의 도메인을 제공하면 Registar는 Registry에게 이를 알리고 Resigtry는 Top-level domain 서버에 이를 등록한다. 그 후 네임서버에 접속해 도메인과 아이피를 등록하면 된다.&nbsp;</p>
<p></p><figure class="imageblock alignCenter" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    <span data-lightbox="lightbox">
        <img src="/img/RE5TKERvbWFpbiBOYW1lIFN5c3RlbSk=/img.png" data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<p>이때 Root name server가 Top-level server를 기록하는 방식이 com NS a.gtld-servers.net이라 되있고 Top-level domain server가 name server를 기록하는 방식이 example NS a.iana-servers.net이라 되있다. 그에 반해 아이피 주소를 기록하는 네임서버는 example.com A 92.184.216.34로 기록하고 있다. 여기서 'A'와 'NS'는 레코드 타입이다. 'A'는 Address recorde, 'NS'는 Name Server를 의미한다. A는 주어진 호스트에 대한 IPv4 주소를 알려주고 도메인 이름을 해당하는 IP주소로 변환할때 사용된다. NS는 주어진 호스트에 대한 공식적인 이름 서버를 알려준다.&nbsp;</p>
<p>&nbsp; 클라이언트가 인터넷에 접속을 하게 되면 ISP가 해당 클라이언트가 사용한 DNSS를 세팅한다. 따라서 이 DNSS를 통해 원하는 도메인의 IP를 알 수 있다. 또 한 전 세계에 존재하는 Root name server의 주소에 대한 정보를 모든 DNSS, Top-level domain server, name server, Root-name server가 알고있다. 클라이언트가 도메인을 입력하면 DNSS에 전송되고 DNSS는 Root name server에게 요청을 하면 Root name server는 Top-level domain server의 주소를 응답한다. 그러면 DNSS는 Top-level domain server에게 요청을 보내고 Top-level domain server는 name server의 주소를 응답하고 DNSS는 name server에 요청을 보낸다. 그러면 name server가 IP를 응답하게 되고 DNSS는 해당 IP를 클라이언트에게 응답을 한다. 그러면 클라이언트는 IP를 통해 원하는 컴퓨터에 접속할 수 있다.</p>
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