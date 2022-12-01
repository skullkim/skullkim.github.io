---
layout:       post
title:        "Auto Scaling Group, Elastic Load Balancer"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- aws
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><b>Auto Scaling Group</b></h2>
<p data-ke-size="size16">&nbsp; 서비스를 운영하면서 트래픽에 대한 장애 대응을 위해 여러 대의 인스턴스를 사용한다. 이때, Auto Scalilng Group을 사용하면 스케일 아웃을 자동으로 진행할 수 있다. Auto Scaling Group은 AMI를 활용해 같은 사양, 환경, 코드를 가진 EC2 인스턴스를 생성해준다. 또 한, Auto Scaling Group으로 인해 인스턴스에 변화가 생겼을 때 이에 대한 사유를 이메일로 받아볼 수도 있다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 로드 밸런서와 Auto Scaling Group을 사용하면 다음과 같은 서버 아키텍처를 가지게 된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1356" data-origin-height="818"><span data-url="https://blog.kakaocdn.net/dn/q4gOo/btrSxk7AQrO/HvSGkiIqsrovO9PQgnWa71/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fq4gOo%2FbtrSxk7AQrO%2FHvSGkiIqsrovO9PQgnWa71%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="592" height="357" data-origin-width="1356" data-origin-height="818"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; Auto Scaling Group에서 Auto Scaling의 규칙은 리소스 사용량 또는 시간을 기준으로 정할 수 있다. 리소스 사용량의 경우 특정 기간 동한 CPU 사용량이 N% 이상으로 유지되면 scale out을 하는 식이다. 시간 기준을 말 그대로 특정 시간대에만 scale out을 진행한다. 시간 기준의 경우 소셜 커머스 같이 서비스 특성상 일부 시간에만 사용자가 몰릴 경우 유용하다.</p>
<h3 data-ke-size="size23"><b>Auto Scaling Group 실습</b></h3>
<p data-ke-size="size16">&nbsp; Auto Scaling Group을 생성해보자. 이 실습은 EC2 인스턴스 한대가 이미 생성되었다는 전제 하에 진행된다.</p>
<p data-ke-size="size16">&nbsp; 위에서 언급했듯 Auto Scaling Group을 생성하기 위해서는 인스턴스에 대한 AMI가 필요하다. 원하는 인스턴스를 우클릭 -&gt; 이미지 및 템플릿 -&gt; 이미지 생성을 클릭해 이미지를 생성하자.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1340" data-origin-height="920"><span data-url="https://blog.kakaocdn.net/dn/bUbQGH/btrSB4hWRiR/Pb40vQuhkIDLE3sdFUZzrK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbUbQGH%2FbtrSB4hWRiR%2FPb40vQuhkIDLE3sdFUZzrK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="727" height="499" data-origin-width="1340" data-origin-height="920"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 이제 아래와 같이 원하는 이미지 이름을 입력해 이미지를 생성하자.<span id="DragSchLayerPos" style="position: absolute; width: 0px; height: 0px; font-size: 0px;"></span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2580" data-origin-height="1860"><span data-url="https://blog.kakaocdn.net/dn/S6JCz/btrSCKcadgD/yc13UMjy9yoVnfcNGKw6yk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FS6JCz%2FbtrSCKcadgD%2Fyc13UMjy9yoVnfcNGKw6yk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2580" data-origin-height="1860"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 그러면 EC2 side bar에서 이미지 - AMI를 클릭해 방금 생성한 이미지를 확인할 수 있다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2302" data-origin-height="316"><span data-url="https://blog.kakaocdn.net/dn/bMGr49/btrSz61E1gx/iUQdd6cIpKsHNkJHUHQBc1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMGr49%2FbtrSz61E1gx%2FiUQdd6cIpKsHNkJHUHQBc1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2302" data-origin-height="316"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 다시 EC2 side bar에서 인스턴스 - 시작 템플릿을 클릭해 템플릿을 만들자. 템플릿을 만들면 서버 사양, 사용할 AMI, Security group 등을 미리 설정할 수 있다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1492" data-origin-height="1882"><span data-url="https://blog.kakaocdn.net/dn/l0uZt/btrSCcAf2ur/7nKbQZw96i3ZnIGFm4igDK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fl0uZt%2FbtrSCcAf2ur%2F7nKbQZw96i3ZnIGFm4igDK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="724" height="913" data-origin-width="1492" data-origin-height="1882"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 위와 같은 생성 페이지에서 템플릿 이름, 템플릿에 사용할 AMI, subnet, SG, 인스턴스 유형 등을 선택한 뒤 아래와 같이 시작 템플릿 생성 버튼을 누르면 템플릿이 제작된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2214" data-origin-height="1132"><span data-url="https://blog.kakaocdn.net/dn/cq2rGs/btrSz8rHKEt/l5fXqXXkKg7FXGzq7Gh7r1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcq2rGs%2FbtrSz8rHKEt%2Fl5fXqXXkKg7FXGzq7Gh7r1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2214" data-origin-height="1132"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 이제 진짜 Auto Scaling Group을 생성하자. EC2 side bar에서 Auto Scaling - Auto Scaling 그룹을 클릭해 Auto Scaling Group 생성 페이지로 이동하자.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2216" data-origin-height="1844"><span data-url="https://blog.kakaocdn.net/dn/bQMuBx/btrSxkT8kT4/BXLPLEhm08iVAqCVfCGlu0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_6.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbQMuBx%2FbtrSxkT8kT4%2FBXLPLEhm08iVAqCVfCGlu0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="805" height="670" data-origin-width="2216" data-origin-height="1844"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 첫 번째 단계에서 Auto Scaling Group 이름을 입력하고 시작 템플릿을 정한다.</p>
<p data-ke-size="size16">&nbsp; 두 번째 단계에서 VPC, subnet을 정한다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1784" data-origin-height="1454"><span data-url="https://blog.kakaocdn.net/dn/wrIFE/btrSCc8klla/XlPooAI7Hm3RULIQroAuT1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_7.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwrIFE%2FbtrSCc8klla%2FXlPooAI7Hm3RULIQroAuT1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1784" data-origin-height="1454"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 만약 위 설정에서 두 개의 AZ를 선택한다면 인스턴스는 절반 씩 서로 다른 AZ에 띄워지게 된다.</p>
<p data-ke-size="size16">&nbsp; 고급 옵션 구성 부분에서는 아직 ELB를 생성하지 않았으므로 다음과 같이 선택하고 넘어간다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2046" data-origin-height="1690"><span data-url="https://blog.kakaocdn.net/dn/cCAbrv/btrSBoHRVV6/IKBw3WNpoRzJYnKeRPCwy0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_8.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCAbrv%2FbtrSBoHRVV6%2FIKBw3WNpoRzJYnKeRPCwy0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2046" data-origin-height="1690"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 그룹 크기 및 크기 조정 정책 구성에서는 Auto Scaling Group에서 자동으로 Scale Out 할 인스턴스 수와 scale out을 할 조건을 선택하면 된다. 현재 내가 Auto Scaling Group을 등록하는 이유는 ELB 사용과 Elastic Beanstalk을 이용한 자동 배포에 있으므로 평균 CPU 사용률의 대상 값을 높게 잡아주었다(그래야 의도치 않는 비용이 청구되는 것을 막을 수 있다).</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1772" data-origin-height="1740"><span data-url="https://blog.kakaocdn.net/dn/bbxHam/btrSxkGFloI/ZbMYLhlkzANjyFJaU0EnLk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_9.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbxHam%2FbtrSxkGFloI%2FZbMYLhlkzANjyFJaU0EnLk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="690" height="678" data-origin-width="1772" data-origin-height="1740"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 알림 추가도 해보자</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1790" data-origin-height="884"><span data-url="https://blog.kakaocdn.net/dn/b6onD7/btrSBDdVwXB/Miv8vTE3wLGqn5UN9Ki1J1/img.png" data-lightbox="lightbox" data-alt=""><img src="/img/2022-12-01-elb-acg/img_10.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb6onD7%2FbtrSBDdVwXB%2FMiv8vTE3wLGqn5UN9Ki1J1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1790" data-origin-height="884"></span><figcaption></figcaption>
</figure>
<p></p>
<p data-ke-size="size16">&nbsp; 이제 검토 단계를 거치고 생성을 하면, 아래와 같이 최초 1대의 인스턴스가 동작고 있는 것을 볼 수 있다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2536" data-origin-height="400"><span data-url="https://blog.kakaocdn.net/dn/R8elS/btrSy7GHYgP/rzhKeD3xEjGiOpBVfSCvT1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_11.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FR8elS%2FbtrSy7GHYgP%2FrzhKeD3xEjGiOpBVfSCvT1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="879" height="139" data-origin-width="2536" data-origin-height="400"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 여기서 Auto Scaling Group에 의해 관리되고 있는 인스턴스는 기존에 띄웠던 인스턴스와는 다른 인스턴스다. 따라서 인스턴스 목록을 확인하면 두 개의 인스턴스가 작동하고 있음을 알 수 있다. 이제 기존 인스턴스를 종료하면 된다.</p>
<h2 data-ke-size="size26"><b>ELB(Elastic Load Balancing)</b></h2>
<p data-ke-size="size16">&nbsp; ELB는 AWS가 제공하는 로드 밸런서다. ELB를 사용하지 않는다면 L4 스위치 같은 장비를 구매해 관리해야 하지만, ELB를 사용한다면 몇 번의 클릭으로 로드 밸런서를 사용할 수 있다. 로드 밸런서가 받은 요청을 특정 인스턴스나 Auto Scaling Group으로 전달하게 할 수 있다. 로드 밸런서는 너무 많은 트래픽을 감당하고 있거나 정상 동작하지 않는 인스턴스에게 요청을 보내지 않는다.</p>
<h3 data-ke-size="size23"><b>대상 그룹(Target Group)</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>대상 그룹은 로드 밸런서가 요청을 전달할 그룹이다. 이 그룹 하나에 인스턴스나 Auto Scaling Group이 포함된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1466" data-origin-height="426"><span data-url="https://blog.kakaocdn.net/dn/b2f4Zk/btrSAxkYYKe/7t8oZ9ddmF0BdqsN6sJjo1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_12.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb2f4Zk%2FbtrSAxkYYKe%2F7t8oZ9ddmF0BdqsN6sJjo1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1466" data-origin-height="426"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 로드 벨런서가 직접 인스턴스나 Auto Scaling Group에게 로드 벨런싱을 하지 않는 이유는 하나의 요청을 처리할 수 있는 여러 Auto Scaling Group과 인스턴스를 묶어서 요청을 전달하기 위함이다. 예컨대, 8080번 포트로 오는 요청을 특정 대상 그룹으로 전달하는 식이다.</p>
<h3 data-ke-size="size23"><b>로드 밸런서의 상태 검사(Health Check)</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>로드 밸런서는 자신이 관리하는 서버가 정상 동작 중인지를 확인하기 위해 주기적으로 상태 검사를 한다. 이를 통해 정상 동작하고 있는 서버에만 요청을 전달한다. 만약 상태 검사에 대한 응답으로 200이 온다면 서버는 정상 동작하고 있는 것으로 간주한다. 상태 검사를 위해 서버에 물어보는 주기와 비정상 코드를 몇 번 응답으로 받아야 비정상 상태로 변경할지도 설정할 수 있다.</p>
<p data-ke-size="size16">&nbsp; 만약 WAS가 아닌 WS만 살아있어도 서버를 정상이라 판단하고 싶다면, 상태 검사 요청을 WS가 처리하게 하면 된다. 만약 WAS까지 살아있어야 한다면, 이에 대한 요청을 WAS에서 처리하면 된다. 상태 검사 요청 디폴트 요청은 GET / HTTP이다. 만약 상태 검사에 대한 항목을 바꾸고 싶다면 <a href="https://docs.aws.amazon.com/ko_kr/elasticloadbalancing/latest/application/target-group-health-checks.html" target="_blank" rel="noopener">링크</a>를 참고하자.</p>
<h3 data-ke-size="size23"><b>ELB 실습</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>위에서 생성한 Auto Scaling Group을 기반으로 대상그룹을 만들고 로드밸런서를 만들어보자. 우선 EC2 사이드바에서 로드밸런싱 - 로드밸런서를 클릭하고 로드 밸런서 생성으로 들어가자. 여기서 Application Load Balancer를 생성하자.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1358" data-origin-height="1208"><span data-url="https://blog.kakaocdn.net/dn/nwgvN/btrSCwr49FP/VFc9LV1YhmIDQhdaduT1Sk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_13.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnwgvN%2FbtrSCwr49FP%2FVFc9LV1YhmIDQhdaduT1Sk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="713" height="634" data-origin-width="1358" data-origin-height="1208"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 그러면 아래와 같은 화면이 나오게 된다. 여기서 ELB의 이름을 지정하고, 알맞은 VPC, AZ, SG를 선택하면 된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1854" data-origin-height="1896"><span data-url="https://blog.kakaocdn.net/dn/bVkfqb/btrSCqZLpy3/h3O9lFzaEbgP4KVQkpDBdK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_14.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbVkfqb%2FbtrSCqZLpy3%2Fh3O9lFzaEbgP4KVQkpDBdK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1854" data-origin-height="1896"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 여기서 설정을 진행하다 보면, 아래와 같이 Listners ans Routing항목이 나온다. 여기서 target group을 생성하기 위해 Create target group을 클릭해 이동하자.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1740" data-origin-height="836"><span data-url="https://blog.kakaocdn.net/dn/cCkLLA/btrSCHNJsJA/khqLQaizRcAbJEduJiM5m0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_15.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCkLLA%2FbtrSCHNJsJA%2FkhqLQaizRcAbJEduJiM5m0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1740" data-origin-height="836"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; Target gorup 생성 화면에서 다음과 같이 적절한 target type과 상태 체크를 위한 url, port를 지정하면 된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1826" data-origin-height="1888"><span data-url="https://blog.kakaocdn.net/dn/bnMhUX/btrSCKjpMEr/oczYc43elGRPnNV1kiXO50/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_16.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbnMhUX%2FbtrSCKjpMEr%2FoczYc43elGRPnNV1kiXO50%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1826" data-origin-height="1888"></span></figure>
<figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1430" data-origin-height="1368"><span data-url="https://blog.kakaocdn.net/dn/dB6Yur/btrSz8llAyH/wota58mULScXkJHKzdZPaK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_17.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdB6Yur%2FbtrSz8llAyH%2Fwota58mULScXkJHKzdZPaK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1430" data-origin-height="1368"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 이제 다음단계로 넘어가 target group에 넣을 인스턴스를 선택하고 Include as pending below를 클릭하면 target group에 대한 인스턴스가 추가되게 된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2200" data-origin-height="1518"><span data-url="https://blog.kakaocdn.net/dn/lVIIL/btrSDGU9JDp/PKY0L9Gd65LKYYujUlKDk1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_18.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlVIIL%2FbtrSDGU9JDp%2FPKY0L9Gd65LKYYujUlKDk1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="796" height="549" data-origin-width="2200" data-origin-height="1518"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 또 한, 애플리케이션 코드에 상태 체크용 컨트롤러도 만들어 주었다.</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
<div style="line-height: 130%;">4</div>
<div style="line-height: 130%;">5</div>
<div style="line-height: 130%;">6</div>
<div style="line-height: 130%;">7</div>
<div style="line-height: 130%;">8</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">@RestController</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #a71d5d;">public</span>&nbsp;<span style="color: #a71d5d;">class</span>&nbsp;HealthCheckController&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;@GetMapping(<span style="color: #63a35c;">"/application-health"</span>)</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">public</span>&nbsp;ResponseEntity<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&lt;</span>Void<span style="color: #0086b3;"></span><span style="color: #a71d5d;">&gt;</span>&nbsp;checkHealth()&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #a71d5d;">return</span>&nbsp;ResponseEntity.ok().build();</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp; 이제 다시 ELB 생성 페이지로 돌아와 Listeners and routing에 방금 생성한 target group을 선택하면 된다. 만약 target group이 보이지 않는다면 Default action 옆에 존재하는 새로고침 버튼을 클릭하자.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1568" data-origin-height="842"><span data-url="https://blog.kakaocdn.net/dn/PI7h2/btrSz8sau0V/dEkDdMcqPdL2jxMMbHT4WK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_19.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPI7h2%2FbtrSz8sau0V%2FdEkDdMcqPdL2jxMMbHT4WK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1568" data-origin-height="842"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 위와 같은 설정을 하고 ELB를 생성하면 된다. 이제 EC2 사이드바 로드 밸런싱 - 로드밸런서 항목에서 방금 생성한 로드밸런서를 확인할 수 있다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2308" data-origin-height="1226"><span data-url="https://blog.kakaocdn.net/dn/cSYr7m/btrSCv1bxaA/xPoHACVrNanfnCP1cjETQK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-01-elb-acg/img_20.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcSYr7m%2FbtrSCv1bxaA%2FxPoHACVrNanfnCP1cjETQK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2308" data-origin-height="1226"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 만약 ELB가 올바르게 동작하고 있다면 위 로드 밸런서 기본 구성 부분에 존재하는 DNS 이름을 통해 target gorup 내에 존재하는 애플리케이션에 접근할 수 있다.</p></div>