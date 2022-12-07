---
layout:       post
title:        "땡쿠 이전하기 - production 편"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 우아한테크코스
- aws
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 우테코가 끝나고 우테코 기간 동안 만들었던 서비스가 우형 AWS에서 내려가게 되었다. 공들여 만든 땡쿠 서비스가 내려가는 게 아쉬워서 AWS free tier에서 최대한 비슷한 환경을 만들어 보고자 이전을 하기로 했다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>기존 아키텍처</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 우형 AWS에서는 오직 EC2만 사용할 수 있다는 제약사항이 존재해서 EC2를 십분 활용해 다음과 같은 백엔드 아키텍처를 구성했다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1280" data-origin-height="788"><span data-url="https://blog.kakaocdn.net/dn/GOFxo/btrS3GIXxLI/FwZHGSAJIJ7hK3a22QE2Nk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-thankoo-move/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGOFxo%2FbtrS3GIXxLI%2FFwZHGSAJIJ7hK3a22QE2Nk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1280" data-origin-height="788"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프론트 아키텍처는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1280" data-origin-height="564"><span data-url="https://blog.kakaocdn.net/dn/d5ZdKJ/btrS3pUP4SY/vvpimkmDxM9F3wJljEMFFk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-thankoo-move/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd5ZdKJ%2FbtrS3pUP4SY%2FvvpimkmDxM9F3wJljEMFFk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1280" data-origin-height="564"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 아키텍처에서 각 EC2 인스턴스는 arm 아키텍처 t4.micro이므로 저 아키텍처를 그대로 옮긴다면 인스턴스 한 대당 1만 원이 조금 넘는 비용이 청구된다. 따라서 한 달에 약 10만 원의 유지비가 필요하다. 이 유지비를 줄이면서 기존 구성을 최대한 살리기 위해 다음과 같은 아키텍처를 구성했다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>AWS 이전 이후의 아키텍처</b></span></h2>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1039" data-origin-height="575"><span data-url="https://blog.kakaocdn.net/dn/dz41CU/btrS3GvppP8/6EdoHQM4tY9WURZkbYhEc0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-thankoo-move/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdz41CU%2FbtrS3GvppP8%2F6EdoHQM4tY9WURZkbYhEc0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1039" data-origin-height="575"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프론트와 어드민은 정적 배포가 가능하므로 S3를 사용했다. EC2하나에 Nginx와 WAS를 넣어놓고, 젠킨스를 사용하는 대신 BeanStalk과 github action을 사용해 무중단 배포를 구현하기 위해 ELB를 앞에 두었다. 이렇게 무중단 배포를 하게 되면 잠시 동안은 두 대의 인스턴스가 작동되므로 약간의 과금이 발생한다. 하지만 프리티어로 제공되는 t2.micro는 한 달 내내 유로로 띄워 놓아도 1만 원가량이 소비되는 것을 감안하면, 많아야 몇백 원 정도의 요금이 발생할 것이라 예상된다. CloudFront는 HTTPS와 커스텀 도메인을 적용하기 위해 사용했다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 자세한 사항은 다른 포스팅에서 다루겠다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Production 부분 이전 완료</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>현재까지 Production 부분을 이전 완료했다. 이전 완료한 부분의 아키텍처는 다음과 같다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1017" data-origin-height="475"><span data-url="https://blog.kakaocdn.net/dn/byjJNL/btrS5N1r7D5/nagn5tLKkN3VgEOVBoFU9K/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-thankoo-move/img_3" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbyjJNL%2FbtrS5N1r7D5%2Fnagn5tLKkN3VgEOVBoFU9K%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1017" data-origin-height="475"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 나는 위 아키텍처를 EC2 - RDS - ELB - S3 - Cloud Front 순서로 이전했다. EC2, RDS 세팅 과정은 굳이 다루지 않겠다(세팅 방법을 소개하는 글이 많다).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">ELB, Auto Scaling Group을 세팅하는 포스팅은 이 <a href="https://www.skullkim-dev.com/2022/12/01/aws-elb-acg/" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">S3, Cloud Front를 세팅하는 포스팅은 이 <a href="https://www.skullkim-dev.com/2022/12/08/s3-cloud-front/" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 일단 바쁜게 다 마무리되면 배포와 관련된 부분도 완성해 추가 포스팅하겠다.</span></p></div>