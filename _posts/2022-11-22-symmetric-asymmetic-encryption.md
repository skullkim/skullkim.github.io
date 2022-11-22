---
layout:       post
title:        "대칭키 암호화와 비대칭키 암호화"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- ComputerScience
- 암호화
---

<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><b>암호화</b></h2>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>암호화는 평문을 암호문으로 바꾸는 것을 의미한다. 암호화의 세 가지 보안 기능성은 다음과 같다.</p>
<p data-ke-size="size16">&nbsp; - 기밀성(Confidentiality): 인가된 당사자에 의해서만 데이터 접근이 가능해야 한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; - 무결성(Integrity): 데이터가 인가된 당사자에 의해서만 인가된 방식으로 변경돼야 한다.</p>
<p data-ke-size="size16">&nbsp; - 인증(Authentication): 접근한 당사자가 권한이 있는지를 체크한다.</p>
<p data-ke-size="size16">&nbsp; 보통 암호화라 하면 encryption과 cryptographic processing이라는 단어를 떠올린다. 때로는 이 들을 혼용한다. 이 둘은 다음과 같은 차이가 존재한다.</p>
<p data-ke-size="size16">&nbsp; - Cryptographic Processing은 기밀성, 무결성, 인증에 사용하는 넓은 개념이다.</p>
<p data-ke-size="size16">&nbsp; - Encryption은 좁은 의미에서는 기밀성을 유지하는 도구이며 넓은 의미에서는 cryptographic processing과 같은 의미를 가진다.</p>
<p data-ke-size="size16">&nbsp; 암호화는 암호 알고리즘, 암호키 두 가지를 기반으로 작동한다.</p>
<h2 data-ke-size="size26"><b>대칭키 암호화</b></h2>
<p data-ke-size="size16">&nbsp; 대칭 알고리즘은 대칭키 암호화 알고리즘의 핵심이며 이를 통해 암/복호화를 할 수 있다. 대칭키 암호화는 암/복호화에 같은 암호키를 사용한다. 대칭키 암복호화 알고리즘은 데이터 기밀성을 보장한다.</p>
<p data-ke-size="size16">&nbsp; 대칭키 알고리즘은 대칭 암호화 알고리즘, 대칭 사이퍼, 비밀키 알고리즘, 벌크 사이퍼로도 불린다.</p>
<p data-ke-size="size16">&nbsp; AES 128 기준, 대칭키 알고리즘은 다음과 같이 동작한다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1044" data-origin-height="124"><span data-url="https://blog.kakaocdn.net/dn/Zo83u/btrRMcgPgfl/IS2YEuGySVJk6HZl5wqxr0/img.png" data-lightbox="lightbox"><img src="https://blog.kakaocdn.net/dn/Zo83u/btrRMcgPgfl/IS2YEuGySVJk6HZl5wqxr0/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZo83u%2FbtrRMcgPgfl%2FIS2YEuGySVJk6HZl5wqxr0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1044" data-origin-height="124"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 대칭키 알고리즘이기 때문에 위 과정에서 암호화 키와 복호화 키는 동일하다.</p>
<p data-ke-size="size16">&nbsp; 대칭키 알고리즘은 대용량 데이터 처리를 위해 고안된 암호화 방식이다. 따라서 비대칭키 알고리즘에 비해 가볍다. 반면, 비대칭키는 CPU 리소스를 많이 차지한다. 하지만, 적은 양의 데이터를 안전하지 않은 공개된 채널에서 키를 배포하기에 적절하다.</p>
<p data-ke-size="size16">&nbsp; 대칭키 알고리즘은 취약점으로 인해 공개된 채널에서 단독으로 사용하는 것을 권장하지 않는다. 이 취약점은 키 배포와 키 관리에서 발생한다.</p>
<p data-ke-size="size16">&nbsp; - 키 배포를 위해선 안전한 커넥션이 필요하다</p>
<p data-ke-size="size16">&nbsp; - 많은 사람들이 대칭키를 가지고 있다면, 추후 추적에 어려움이 있다.</p>
<p data-ke-size="size16">&nbsp; 대칭키 암호화를 사용하는 가장 이상적인 방식은, 커뮤니케이션에 참여하는 참여자들이 사전에 키를 공유하는 것이다. 이때, 물리적 만남으로 키를 교환하면 좋겠지만, 많은 경우 물리적인 만남을 할 수 없다. 따라서 비대칭 알고리즘을 사용해 키를 교환한다. 비대칭키를 이용하면 안전하지 않은 공개 채널에서 대칭키를 교환할 수 있게 해 준다. 이에 대한 대표적인 예시가 TLS handshake다. TLS handshake는 다음과 같은 목적으로 비대칭키 암호화를 이용한다.</p>
<p data-ke-size="size16">&nbsp; - 디지털 서명을 인증한다</p>
<p data-ke-size="size16">&nbsp; - 클라이언트와 서버가 대칭 세션 키를 만드는대 사용하는 재료를 암호화한다.</p>
<h3 data-ke-size="size23"><b>대칭키 알고리즘 분류</b></h3>
<p data-ke-size="size16">&nbsp; 대칭키 알고리즘은 크게 Block cipher와 Stream cipher로 나뉜다.</p>
<h4 data-ke-size="size20"><b>Block cipher</b></h4>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>block cipher는 평문을 고정길이 비트로 쪼갠다. 이 고정길이 비트 하나를 블록이라 한다. 그리고 각 블록을 암호화한다. 만약 암호화해야 하는 데이터 길이가 블록의 길이보다 작다면, 뒤에 padding을 추가한다. 현재 사용되는 대부분의 대칭키 암호화 알고리즘이 block cipher에 속한다.</p>
<h4 data-ke-size="size20"><b>Stream cipher</b></h4>
<p data-ke-size="size16">&nbsp; Stream cipher는 한 번에 하나의 비트만 암호화한다. 따라서 리소스를 덜 소모하고, 접근이 용이하다. Block cipher와 Stream cipher의 세부적인 차이는 <a href="https://www.thesslstore.com/blog/block-cipher-vs-stream-cipher/" target="_blank" rel="noopener">링크</a>를 참고하자.</p>
<h2 data-ke-size="size26"><b>비대칭키 암호화</b></h2>
<p data-ke-size="size16">&nbsp; 비대칭키 암호화는 두 개의 수학적으로 연관돼 있으며 고유한 한 쌍의 키를 사용한다. 이 두 개의 키 이름은 각각 공개키(public key)와 비밀키(private key)이다. 공개키는 암호화에, 비밀키는 복호화에 사용된다.</p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="964" data-origin-height="108"><span data-url="https://blog.kakaocdn.net/dn/dRTOuG/btrRMKEynIa/ZmCMcFHm1OjSTAKDWSm411/img.png" data-lightbox="lightbox"><img src="https://blog.kakaocdn.net/dn/dRTOuG/btrRMKEynIa/ZmCMcFHm1OjSTAKDWSm411/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdRTOuG%2FbtrRMKEynIa%2FZmCMcFHm1OjSTAKDWSm411%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="964" data-origin-height="108"></span></figure>
<p></p>
<p data-ke-size="size16">&nbsp; 비대칭키 암호화는 다음과 같은 장점을 가진다.</p>
<p data-ke-size="size16">&nbsp; - 인증(Authenticatino): 위조할 수 없는 방식(non-repudiation)으로 암호화를 진행하기 때문에 신원을 알 수 없는 서드파티와 통신 과정에서 암호화하기 적절한 방식이다.</p>
<p data-ke-size="size16">&nbsp; - 안전한 키 교환: 비대칭 키 교환 프로토콜은 대칭키 교환을 안전하게 이행해준다.</p>
<p data-ke-size="size16">&nbsp; - 데이터 무결성(Data Integrity): 디지털 서명을 통해 데이터가 변경되지 않음을 보장한다.</p>
<h2 data-ke-size="size26"><b>대칭키 암호화와 비대칭키 암호화의 차이</b></h2>
<p data-ke-size="size16">&nbsp; 대칭키 암호화와 비대칭키 암호화의 차이는 키와 암호화 알고리즘에 기인한다. 그에 따라 다음과 같은 세부적 차이들이 존재한다.</p>
<h3 data-ke-size="size23"><b>암호화 키의 개수, 특징, 크기</b></h3>
<p data-ke-size="size16">&nbsp; 대칭키는 암/복호화에 모두 사용되기 때문에 대칭적이다. 그에 반해 비대칭키는 공개키, 비밀키가 서로 수학적으로 연관돼 있으며 하나의 고유한 쌍이다. 대칭키는 통상적으로 비대칭키보다 짧다. 대칭키는 통상적으로 128bit, 192bit, 256bit 길이를 가지는 반면, 비대칭키 길이는 2048bit 이상일 것을 권장한다.</p>
<h3 data-ke-size="size23"><b>키 배포 방식</b></h3>
<p data-ke-size="size16"><b>&nbsp;&nbsp;</b>비대칭키 암호화 방식은 공개 채널에서 키 교환해도 문제가 되지 않는다. 애초에 비대칭 키 교환 프로토콜이 이 목적으로 설계되었기 때문이다. 그에 반해 대칭키는 공격받기 쉽기 때문에 공개 채널에서 그냥 교환하면 안 된다. 대신 비대칭 키 교환 프로세스를 사용해야 한다.</p>
<h3 data-ke-size="size23"><b>암호화 알고리즘의 타입과 복잡도</b></h3>
<p data-ke-size="size16">&nbsp; 대칭키 알고리즘과 비대칭키 알고리즘이은 서로 다른 암호화 알고리즘을 사용한다. 대칭키 알고리즘은 block cipher나 stream cipher 두 분류의 알고리즘을 사용하며 DES, TDEA/3 DES, AES 등이 두 분류 내에 속한다. 비대칭키 암호화 알고리즘으로는 RSA, DSA, ECC 등이 존재한다.</p>
<h3 data-ke-size="size23"><b>시간과 리소스 소모량에 따른 차이</b></h3>
<p data-ke-size="size16">&nbsp; 대칭키 암호화는 하나의 키만 사용하기 때문에 속도가 빠르다. 따라서 대량의 데이터를 암호화해야 할 때 적합하다. 비대칭 암호화는 두 개의 서로 다른 키를 사용하기 때문에 더 복잡한 알고리즘이 필요하다. 그 때문에 암/복호화하는 데이터가 클수록 속도가 느리다.</p>
<p data-ke-size="size16">&nbsp; 대칭키 암호화와 비대칭키 암호화 중 어떤 것을 사용해야 할지 결정해야 한다면, 채널의 공개 여부를 고민하라. 대칭키 암호화 사용은 비공개 채널에서 사용하기 적절하고 비대칭키 암호화는 공개 채널에서 사용하기 적절하다.</p>
<p data-ke-size="size16">&nbsp;</p></div>