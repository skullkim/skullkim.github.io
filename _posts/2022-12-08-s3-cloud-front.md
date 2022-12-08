---
layout:       post
title:        "S3, Cloud Front"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- aws
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>S3 (Simple Storage Service)</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>S3는 여러 곳에서 파일에 접근할 수 있게 만들어진 서비스다. 웹 서비스에서 많이 사용하며 다양한 목적을 가진 파일들을 보관하는 데 사용된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; S3는 내구성, 가용성, 확장성에 대해 강점을 가진다. 내구성은 99.999999999%이며 파일 수와 용량에&nbsp; 제한이 없다(단, 하나의 파일(객체) 용량은 5TB로 제한돼 있다.). 또 한, 액세스 패턴과 사용 사례에 따라 다양한 스토리지 클래스를 이용해 데이터를 저장할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 파일 보안에 대해서도 IAM, ACL 등의 방식을 혼용해 다양한 유저가 다양한 파일에 접근하는 권한을 유연하게 제어할 수 있다. 또 한, 누나 어떤 데이터에 액세스 했는지를 알 수 있게 S3 리소스에 대한 요청 목록을 표시하는 감사 로그를 지원한다. S3&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; S3는 웹 콘솔을 지원하기 때문에 반드시 EC2를 통해서 접속하지 않아도 된다. 따라서 큰 데이터를 S3에 업로드하면서 동시에 AWS의 다른 서비스를 이용해 해당 파일들을 쿼리하고 분석할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; S3에는 버킷과 객체라는 개념이 존재한다. 버킷은 리소스다. S3는 데이터를 버킷이라는 리소스에 객체로 저장한다. S3는 디렉터리라는 개념이 존재하지 않기 때문에 필요하다면 객체 이름에 "/" 문자를 포함해 디렉터리를 조회하는 것처럼 이용할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; S3는 위와 같이 파일 스토리지의 역할뿐만 아니라 파일 제공 역할도 수행할 수 있다. 클라이언트에게 제공해야 하는&nbsp; 파일 중 코드와 같이 서버에 배포되지 않은 파일들은 모두 S3에 업로드하는 것이 좋다. 그러면 DB에 S3에 업로드된 객체 URL을 보관하는 것으로 클라이언트가 파일을 요청해 내려받을 수 있다. 이 방식을 채택한다면, 용량 확장, 파일 유식, 트래픽 등 운영에 필요한 내용을 걱정할 필요가 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; S3는 정적 호스팅도 지원한다. S3 정적 호스팅을 사용하면 서버의 트래픽에 대해 걱정할 필요가 없다. 또 한, AWS 웹 콘솔 클릭 몇 번으로 새로운 버전의 파일을 올릴 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; S3에 대한 더 자세한 설명은 <a href="https://aws.amazon.com/ko/s3/features/" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>S3로 리액트 앱 배포하기</b><b></b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 터미널을 통해 S3에 리액트 앱을 배포하기 위해 IAM 권한 설정을 먼저&nbsp;하자. IAM 사용자에서 사용자 추가를 클릭해 사용자 생성 화면으로 이동하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1836" data-origin-height="538"><span data-url="https://blog.kakaocdn.net/dn/bWkZ3U/btrSE8rxq24/sq7PE232ok5T22zKqtahr1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWkZ3U%2FbtrSE8rxq24%2Fsq7PE232ok5T22zKqtahr1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1836" data-origin-height="538"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여기서 원하는 사용자 이름을 입력하고, 액세스 유형은 프로그래밍 방식 액세스를 선택하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1968" data-origin-height="976"><span data-url="https://blog.kakaocdn.net/dn/mJ6ch/btrSCHBHO8P/4uzzbnjpata8iYKkCLCpfK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmJ6ch%2FbtrSCHBHO8P%2F4uzzbnjpata8iYKkCLCpfK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1968" data-origin-height="976"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">다음 페이지에서는 기존 정책 직접 연걸을 선택하고 AmazoneS3FullAccess를 선택하자. AmazoneS3FullAccess는 S3의 모든 사용 권한을 부여해준다. S3 정책과 권한에 대한 기본 요소 내역은 <a href="https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/access-policy-language-overview.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2032" data-origin-height="1380"><span data-url="https://blog.kakaocdn.net/dn/ehWOTc/btrSDGoOydV/7HcU4G2Hgnl7xbsOJfg8Sk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FehWOTc%2FbtrSDGoOydV%2F7HcU4G2Hgnl7xbsOJfg8Sk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2032" data-origin-height="1380"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 태그 선택과 확인 절차를 거치면 아래와 같이 액세스 키가 생성된다. 여기서. csv 다운로드를 클릭해 파일을 다운로드하고 안전하게 저장하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2038" data-origin-height="822"><span data-url="https://blog.kakaocdn.net/dn/bz1T3k/btrSHkZeFyB/qs9cqYeNkcCWzrOAkhvay1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbz1T3k%2FbtrSHkZeFyB%2Fqs9cqYeNkcCWzrOAkhvay1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2038" data-origin-height="822"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 AWS CLI를 설치하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; AWS CLI를 맥에서 터미널로 설치하기 위해서는 다음과 같은 명령어를 입력하면 된다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">5</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">6</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">7</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">8</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;curl&nbsp;명령어를&nbsp;이용해&nbsp;파일&nbsp;다운로드.&nbsp;-o는&nbsp;다운로드할&nbsp;패키지가&nbsp;기록되는&nbsp;파일&nbsp;이름을&nbsp;지정한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">curl&nbsp;<span style="color: #63a35c;">"https://awscli.amazonaws.com/AWSCLIV2.pkg"</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>o&nbsp;<span style="color: #63a35c;">"AWSCLIV2.pkg"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;다운로드한&nbsp;파일을&nbsp;소스로&nbsp;지겅해&nbsp;표준&nbsp;macos&nbsp;installer&nbsp;프로그램을&nbsp;실행한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;-pkg는&nbsp;설치할&nbsp;패키지&nbsp;이름을&nbsp;지정한다&nbsp;.&nbsp;-target은&nbsp;패키지를&nbsp;설치할&nbsp;드라이브를&nbsp;지정한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;파일은&nbsp;/usr/local/aws-cli에&nbsp;설치되고,&nbsp;/usr/local/bin에&nbsp;symlink가&nbsp;자동으로&nbsp;만들어진다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;해당&nbsp;폴더에&nbsp;쓰기&nbsp;원한&nbsp;부여를&nbsp;위해선&nbsp;sudo를&nbsp;포함해야&nbsp;한다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;디버그&nbsp;로그는&nbsp;/var/log/install.log에&nbsp;기록된다.</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">sudo&nbsp;installer&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>pkg&nbsp;AWSCLIV2.pkg&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>target&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; AWS CLI를 설치하는 다양한 방법은 <a href="https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/getting-started-install.html" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 설치 완료 후 다음 명령어를 입력해 설치가 올바르게 되었는지를 확인해보자.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">which&nbsp;aws</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;/usr/local/bin/aws</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">aws&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>version</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">#&nbsp;aws-cli/2.9.3&nbsp;Python/3.9.11&nbsp;Darwin/20.3.0&nbsp;exe/x86_64&nbsp;prompt/off</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp;만약 위와 같은 결과가 나오지 않았다면 <a href="https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-chap-troubleshooting.html" target="_blank" rel="noopener">링크</a>를 참고해 문제를 해결하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 아래 명령어를 입력해 CLI 유저를 생성하자. 아래 커맨드에서 요구하는 Access Key ID와&nbsp; Secret Access Key는 위에서 다운로드한. csv 파일에 존재한다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">aws&nbsp;configure&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>profile&nbsp;{user_name}</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1140" data-origin-height="184"><span data-url="https://blog.kakaocdn.net/dn/bFEt6h/btrSGR4eJdz/fuvquoCesagLm5NRa5KEv0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbFEt6h%2FbtrSGR4eJdz%2FfuvquoCesagLm5NRa5KEv0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1140" data-origin-height="184"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 S3 버킷을 생성하자. 다음과 같이 버킷 이름을 입력하고, 퍼블릭 액세스 차단을 해제하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1578" data-origin-height="976"><span data-url="https://blog.kakaocdn.net/dn/drk6Lw/btrSEfx5c24/pKzuWTKliJJiYrKV27kKLK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_5" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdrk6Lw%2FbtrSEfx5c24%2FpKzuWTKliJJiYrKV27kKLK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1578" data-origin-height="976"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">버킷을 생성한 후 해당 버킷의 정책으로 가자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1398" data-origin-height="1670"><span data-url="https://blog.kakaocdn.net/dn/XavKG/btrSHywwrj8/AflK8Yk0zMXuxBO6suk7Kk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_6" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXavKG%2FbtrSHywwrj8%2FAflK8Yk0zMXuxBO6suk7Kk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="745" height="890" data-origin-width="1398" data-origin-height="1670"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">여기서 버킷 정책에 다음과 같이 입력하자. 여기서 bucket-name에는 자신의 버킷 이름을 입력하면 된다.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">4</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">5</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">6</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">7</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">8</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">9</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">10</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">11</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">12</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #63a35c;">"Version"</span>:<span style="color: #63a35c;">"2012-10-17"</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #63a35c;">"Statement"</span>:[</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"Sid"</span>:<span style="color: #63a35c;">"AddPerm"</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"Effect"</span>:<span style="color: #63a35c;">"Allow"</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"Principal"</span>:&nbsp;<span style="color: #63a35c;">"*"</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"Action"</span>:[<span style="color: #63a35c;">"s3:GetObject"</span>],</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"Resource"</span>:[<span style="color: #63a35c;">"arn:aws:s3:::bucket-name/*"</span>]</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;]</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 정책을 변경한 뒤 해당 버킷 속성에 있는 "정적 웹 사이트 호스팅"에서 웹 사이트를 호스팅 하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1262" data-origin-height="830"><span data-url="https://blog.kakaocdn.net/dn/YeScC/btrSGVsdEqs/FPFU1S3TULmAKNYXYTLmYK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_7" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYeScC%2FbtrSGVsdEqs%2FFPFU1S3TULmAKNYXYTLmYK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1262" data-origin-height="830"></span></figure>
<figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1228" data-origin-height="1594"><span data-url="https://blog.kakaocdn.net/dn/cgCAlh/btrSDJl3JBp/uIWDyaoO81WakYXrUcu2u0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_8" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgCAlh%2FbtrSDJl3JBp%2FuIWDyaoO81WakYXrUcu2u0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="761" height="988" data-origin-width="1228" data-origin-height="1594"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이제 배포를 시작해보자. 패키지 매니저는 yarn을 기준으로 한다. 우선 package.json의 scripts 부분에 "deploy"항목을 추가하자.</span></p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">1</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">2</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">3</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #63a35c;">"scripts"</span>:&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #63a35c;">"deploy"</span>:&nbsp;<span style="color: #63a35c;">"aws s3 sync ./dist s3://{bucket_name} --profile={user_name}"</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; bucket_name과 user_name은 자신에게 맞는 세팅으로 변경해주자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 그 후 yarn bulild를 통해 빌드 파일을 생성하자. 만약 빌드 파일 이름이 dist가 아닌 build라면, 위 "deploy"의 "./dist"를 "./build"로 바꾸고 다시 빌드하자. 그 후, yarn deploy를 입력하면 파일이 업로드된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 Clould Front를 이용해 HTTPS와 커스텀 도메인을 연동해보자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>Cloud Front</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>Cloud Front는 AWS에서 제공하는 CDN이다. CDN은 클라이언트가 데이터를 요청했을 때 오리진 서버까지 요청을 보내지 않고, 물리적으로 가까운 위치에서 대신 응답을 해주는 역할을 한다. 이를 통해 응답 시간을 단축할 수 있다. 이 덕분에 오리진 서버가 모든 요청을 처리하지 않아 오리진 서버의 부하를 분산시키는 효과도 누릴 수 있다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Cloud Front는 S3를 오리진 서버로 두고 이미지, JS와 같은 정적 파일, 스트리밍 같은 콘텐츠도 전달할 수 있다. 이 경우 Cloud Front는 요청을 가장 가까이 있는 엣지 로케이션에 전달한다. 만약 응답할 데이터가 엣지 로케이션에 없다면 오리진 서버에서 데이터를 가져와 임시 보관하고 응답한다. 이후의 요청부터는&nbsp;임시 저장한 데이터를 이용해 응답한다. S3의 원본 데이터가 변경된 경우 역시 모든 CDN 서버의 데이터를 업데이트하거나 삭제할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Cloud Frontsms API 가속화 역할도 한다. 클라이언트가 물리적으로 멀리 있는 오리진 서버와 TLS 연결을 하지 않고, 엣지 로케이션과 연결을 하고, 그 뒷단은 AWS 백본 네트워크를 통해 API 서버에 빠르게 도달할 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Cloud Front에 S3 연결 및 프론트 커스텀 도메인, HTTPS 적용하기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>cloud front에서 배포 생성을 클릭하고 위에서 생성한 S3의 버킷 웹 사이트 엔드포인트를 선택하자. 버킷 웹 사이트 엔드포인트는 해당 S3 버킷 속성 맨 아래에서 확인할 수 있다. 그 후 원하는 이름을 입력하고 뷰어 프로토콜 정책은 Redirect HTTP to HTTPS를 선택하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1700" data-origin-height="1672"><span data-url="https://blog.kakaocdn.net/dn/bkRJ1k/btrSHMuKeHw/qCMmsjtPcV6m2m9M4awUOk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_9.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkRJ1k%2FbtrSHMuKeHw%2FqCMmsjtPcV6m2m9M4awUOk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1700" data-origin-height="1672"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">그 후 배포 생성을 클릭해 Cloud Front를 생성하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이제 커스텀 도메인을 사용하기 전에, ACM(Amazon Certificate Manager)에서 SSL 인증서를 발급해야 한다. ACM을 방문해 퍼블릭 인증서를 요청하자. 여기서 주의할 점은 Clouf Front에 ACM을 통해 발급한 SSL 인증서를 연동하기 위해선 반드시 버지니아 북부 리전에 존재하는 ACM에서 SSL 인증서를 발급받아야 한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="582" data-origin-height="462"><span data-url="https://blog.kakaocdn.net/dn/dsin0p/btrSZyqCtjl/TRukLq9DTYVzux3edKH2P1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_10.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdsin0p%2FbtrSZyqCtjl%2FTRukLq9DTYVzux3edKH2P1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="582" data-origin-height="462"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같이 원하는 도메인 이름을 입력하고 요청을 클릭하면 된다. 그리고 검증 방법은 "이메일 검증"을 선택하자. DNS 검증을 하는 것이 권장되나, 이를 이용하려면 가비아에서 구매한 도메인을 Route53에서 호스팅 역역을 만들고 관리해 주어야 한다. 비용이 청구되므로 여기선 이 방식을 사용하지 않겠다. 이제 다음과 같이 생성된 인증서 상태가 "검증 대기 중" 인것을 볼 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="779" data-origin-height="258"><span data-url="https://blog.kakaocdn.net/dn/l9EDK/btrS1P5rwLi/2sALN0v2VApg9j2zkjDpy0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_11.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fl9EDK%2FbtrS1P5rwLi%2F2sALN0v2VApg9j2zkjDpy0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="779" data-origin-height="258"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 생성됨과 동시에 해당 도메인 구입 시 사용한 이메일로 다음과 같은 검증 메일이 올 거다. 이 메일을 클릭해 검증을 완료하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="632" data-origin-height="731"><span data-url="https://blog.kakaocdn.net/dn/oFSP4/btrSYnCO27m/oKbwPF0KLFk6lI0FaIqJD0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_12.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoFSP4%2FbtrSYnCO27m%2FoKbwPF0KLFk6lI0FaIqJD0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="632" data-origin-height="731"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이메일 검증을 완료하면 다음과 같이 인증서 발금이 완료된 것을 알 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="899" data-origin-height="279"><span data-url="https://blog.kakaocdn.net/dn/sPSDc/btrSYnbRsZb/M58MkHnJ2wKpWGXENTrMmk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_13.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsPSDc%2FbtrSYnbRsZb%2FM58MkHnJ2wKpWGXENTrMmk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="899" data-origin-height="279"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 다시 CloudFront로 돌아가서 커스텀 도메인을 연결하길 원하는 cloudFront를 선택하자. 그리고 일반 - 설정 부분에서 설정을 편집하자. 다음과 같이 AWS Certificate Manager로 인증서를 발급한 도메인을 "대체 도메인 이름(CNAME) - 선택 사항"에 입력해주고 위에서 발급한 인증서를 "사용자 정의 SSL 인증서 - 선택사항"에서 선택한 뒤 설정을 저장하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="852" data-origin-height="894"><span data-url="https://blog.kakaocdn.net/dn/nVDpQ/btrS4ZOe3qg/MikatR2X3ffJnPWWxMCa10/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_14.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnVDpQ%2FbtrS4ZOe3qg%2FMikatR2X3ffJnPWWxMCa10%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="852" data-origin-height="894"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 백엔드도 원하는 도메인으로 접근할 수 있게 Cloud Front를 설정하면 된다. 설정 방법은 Cloud Front 설정 시 위 방식에서 원본 도메인을 S3 대신 ELB를 선택하면 된다(ELB를 이용했다면).</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 과정을 모두 마치면 다음과 같은 아키텍처를 가지게 된다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="488" data-origin-height="300"><span data-url="https://blog.kakaocdn.net/dn/1BlD8/btrS6S81JRj/JC6C9NHGuyumDl9tDXUKS1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_15.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1BlD8%2FbtrS6S81JRj%2FJC6C9NHGuyumDl9tDXUKS1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="488" data-origin-height="300"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여기서 클라이언트는 무조건 Cloud Front와 커뮤니케이션을 한다는 것에 주목해야 한다. 즉, 클라이언트는 최초 접속 때 S3에서 페이지를 응답으로 받고, 페이지에서 요청을 보내면 Cloud Front가 받아서 Backend로 전달한다. 따라서 Cloud Front에서 설정한 Backend 배포에 CORS 정책을 추가해야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Cloud Front는 간단한 설정이 된 정책을 제공하고 있다. 미리 설정된 응답 정책을 보고 싶다면 <a href="https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/using-managed-response-headers-policies.html" target="_blank" rel="noopener">링크</a>를 참고하자. 관리형 오리진 요청 정책을 보고 싶다면 <a href="https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-managed-origin-request-policies.html?icmpid=docs_cf_help_panel" target="_blank" rel="noopener">링크</a>를 참고하자.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여기서는 직접 요청과 응답 정책을 커스텀해서 사용할 것이다. CloudFront에서 정책 - 원본 요청 부분에서 "사용자 정의 정책" 부분의 "원본 요청 정책 생성"을 클릭해 요청 정책을 생성하자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="815" data-origin-height="765"><span data-url="https://blog.kakaocdn.net/dn/9HeEx/btrS5Nf67u1/duXtjLN4GrzfGwyCQEkqBk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_16.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F9HeEx%2FbtrS5Nf67u1%2FduXtjLN4GrzfGwyCQEkqBk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="815" data-origin-height="765"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여기서 각자 상황에 맞게 헤더, 쿼리 문자열, 쿠키를 선택하면 된다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 응답 헤더 정책을 만들어보자. CloudFront-정책-응답 헤더에서 "사용자 정의 정책"의 "응답 헤더 정책 생성"을 클릭해 응답 헤더 정책을 생성하자. 여기서 "CORS 구성"을 선택하고 각자 상황에 맞게 세팅한 뒤 생성하면 된다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="687" data-origin-height="818"><span data-url="https://blog.kakaocdn.net/dn/MjojC/btrS5zvvul7/7nWHGxmm9xQXpeXP7KUwKk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_17.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMjojC%2FbtrS5zvvul7%2F7nWHGxmm9xQXpeXP7KUwKk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="687" data-origin-height="818"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 CloudFront에 매핑한 커스텀 도메인을 통해 외부에서 CloudFront에 접근할 수 있도록 DNS 설정을 해주자. 설정한 CloudFront는 아래와 같이 "배포 도메인 이름"을 가지게 된다.&nbsp;</span></p>
<p></p>
<figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2570" data-origin-height="500"><span data-url="https://blog.kakaocdn.net/dn/REwGO/btrS7Jxuxj6/twdz25F8YFKorrJ4IwbtIK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_18.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FREwGO%2FbtrS7Jxuxj6%2Ftwdz25F8YFKorrJ4IwbtIK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2570" data-origin-height="500"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 "배포 도메인 이름"을 통해 클라이언트는 CloudFront에 접근할 수 있다. 커스텀 도메인을 활용해 CloudFront로 접근하게 하려면 커스텀 도메인을 CloudFront "배포 도메인 이름"의 별칭(CNAME)으로 사용하는 레코드가 존재해야 한다. 나는 가비아에서 도메인을 구매했으므로 다음과 같이 가비아에서 DNS 설정을 바꾸어주자.</span></p>
<p></p>
<figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1702" data-origin-height="198"><span data-url="https://blog.kakaocdn.net/dn/c8Ars4/btrS6XiuYzn/cc7WhKU3dAikFLnRXka8v0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-08-s3-cloud-front/img_19.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc8Ars4%2FbtrS6XiuYzn%2Fcc7WhKU3dAikFLnRXka8v0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1702" data-origin-height="198"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 다음과 같이 타입을 CNAME, 값/위치에 CloudFront의 "배포 도메인 이름"을 넣어주면 된다.</span></p>
</div>