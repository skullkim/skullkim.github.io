---
layout:       post
title:        "OpenId Provier 구축 공부 - 3편 (OAuth2.0에서 사용자 인증)"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
  - OAuth
---

- [OpenId Provier 구축 공부 - 1편 (OAuth 2.0)](https://www.skullkim-dev.com/2025/02/13/oidc-oauth2/)
- [OpenId Provier 구축 공부 - 2편 (OAuth 토큰 보안 취약점)](https://www.skullkim-dev.com/2025/02/17/oauth2-token-protection/)

OAuth 2.0은 인증된 사용자 동의를 수집하는 데 사용되고, 처리 절차에서 여러 인증 이벤트를 포함한다. 때문에 일부 개발자들은 OAuth 2.0을 인증 프로토콜이라 생각한다. 하지만 OAuth 2.0은 인증 프로토콜이 아니다.

# 1. OAuth 2.0이 인증 프로토콜이 아닌 이유

인증이란 현재 사용자가 누구인지, 현재 사용자가 애플리케이션을 사용하고 있는지를 애플리케이션에게 알려주는 것이다. 하지만 OAuth 2.0은 자체적으로 사용자에 대한 어떤 정보도 알려주지 않는다. OAuth 2.0 클라이언트는 단지 토큰을 요청해 획득하고, 토큰을 이용해 리소스에 접근할 뿐이다. 클라이언트는 누가 자신을 인가했는지, 인가되는 과정에서 실제 사용자가 있었는지를 알지 못한다.

## 1.2 OAuth 2.0으로 인증 프로토콜 구축하기

### 1.2.1 OAuth 2.0 구성 요소 동작

OAuth 2.0을 이용해 인증 프로토콜을 구축하기 위해서, 우선 OAuth 2.0 구성 요소에 대해 생각해보자. 여기서는 리소스 소유자와 클라이언트, 인가 서버와 보호된 리소스를 하나의 쌍으로 생각해보자. 클라이언트가 리소스 소유자 대신 리소스를 가져오는 행위를 하고, 보호된 리소스는 인가 서버가 만든 토큰을 이용하기 때문이다. 이 관점으로 바라보면 사용자-클라이언트, 인가 서버-보호된 리소스 사이에 보안 경계가 생기게 된다. OAuth 2.0은 이 보안 경계를 가로지르기 위해 사용하는 프로토콜이다.
![oauth](/img/2025-02-27-oidc-openid/img.png)
### 1.2.2 인증 트랜잭션

이번엔 인증 트랜잭션과 이에 필요한 구성 요소를 살펴보자. 인증 트랜잭션은 사용자가 IdP(식별 제공자 - Identity Provider)를 이용해 RP(신뢰 당사자 - Relying Party)에 로그인하는 것을 의미한다. 여기서 IdP, PR 정의는 다음과 같다.

- RP: 리소스에 대한 접근을 통제하는 실체. 이를 위해 리소스 접근 시도를 하는 엔티티들를 인증한다. 통상적으로, 웹에서 RP는 유저 로그인을 허용하는 웹사이트이다.
- IdP: 유저에 대한 자격 증명을 관리하고 인증하는 엔티티

### 1.2.3 OAuth 2.0과 인증 트랜잭션 매핑하기

이제, 단순하게 OAuth 2.0과 인증 트랜잭션의 각 구성 요소들을 비슷한 것 끼리 매핑시켜보자. 그러면, 다음과 같이 매핑이 된다.

- 리소스 소유자 - 유저 (이유: 유저가 리소스 소유자 처럼 인증 방식을 결정해 인증을 시도한다. id/pasword 타이핑 및 로그인 시도 등)
- 클라이언트 - RP (이유: 클라이언트는 액세스 토큰을 이용해 보호된 리소스에 접근한다. RP는 유저는 인증하고 리소스 접근을 허가한다)
- 인가 서버 - IdP (이유: 인가 서버는 OAuth2.0 에서 유저를 인가한다. IdP인 인증을 진행한다.)

위 상관관계를 그림으로 표현하면 다음과 같다.

![oauth-authorization-transction-relatioship](/img/2025-02-27-oidc-openid/img1.png)
여기서 보호된 리소스는 어디에 매핑시켜야 할까? 위에서 RP는 리소스에 대한 접근 통제도 한다고 했으니, RP에 매핑하는게 자연스러워 보인다.
![oauth-authorization-transction-relatioship2](/img/2025-02-27-oidc-openid/img2.png)
하지만, 이렇게 되면 보호된 리소스가 사용자와 직접 상호작용하는 부자연스러운 꼴이 된다. OAuth 2.0에서는 사용자(리소스 소유자)가 아닌 클라이언트가 토큰을 이용해 보호된 리소스와 상호작용하기 때문이다. 즉, 리소스 소유자가 보호된 리소스에 직접 접근하지 않는다. 또한, 보안 경계가 교차된다는 문제도 발생한다.

따라서 관점을 조금 바꾸어보자. 보호된 리소스가 제공하고자 하는 정보는 결국 리소스 소유자의 개인 정보이다. 위에서 IdP는 유저에 대한 자격 증명을 관리한다고 했다. 때문에 인가 서버와 보호된 리소스를 IdP에 매핑해도 무방하다. 클라이언트와 RP는 모두 사용자와 상호작용하므로 그대로 매핑시키자.
![oauth-authorization-transction-relatioship3](/img/2025-02-27-oidc-openid/img3.png)
# 2. 인증을 위해 OAuth 2.0을 사용할 때의 주의할 점

## 2.1 인증 증거로서의 액세스 토큰

액세스 토큰을 인증 증거로 사용하는 것은 적절하지 않다. 액세스 토큰은 인증과 관련된 어떤 정보도 전달하지 않고, 실제 인증 수행 여부를 알려주지 않기 때문이다. 클라이언트는 단지 액세스 토큰을 이용해 특정 리소스에 접근할 수만 있다. 즉, OAuth 2.0에서 액세스 토큰은 클라이언트에게 불투명하다. 물론 클라이언트가 해석 가능한 형태로 토큰 포맷을 정의하고 클라이언트가 검증할 수 있는 사용자 정보와 인증 정보를 포함할 수 있다. 하지만 OAuth 2.0 액세스 토큰은 사양은 액세스 토큰을 위한 특정 포맷, 구조를 정의하지 않는다. 때문에 이미 OAuth를 사용하는 시스템들의 액세스 토큰 포맷 역시 다 다르다.

이런 한계 극복을 위해 OpenID connect 같은 프로토콜에서는 클라이언트에게 인증 정보를 전달하기 위해 액세스 토큰과 별개의 토큰을 하나 더 전달한다.

## 2.2 인증 증거로서 보호된 API에 대한 접근

만약 액세스 토큰을 사용자 속성 정보와 교환할 수 있다면, 해당 토큰을 가지고 있는 것 만으로 사용자가 인증 됐음을 충분히 증명할 수 있을까? 아니다. OAuth 에서는 사용자 존재 여부와 관련 없이, refresh token을 이용해 접근 권한을 얻을 수 있기 때문이다. 통상적으로 인증 프로토콜은 사용자가 있는지를 확인한다. 때문에 액세스 토큰을 통해 사용자가 인증 되었음을 충분히 증명하려면, 해당 액세스 토큰은 반드시 인증 프로세스를 거친 사용자에 대해 인가 서버가 새롭게 발급한 액세스 토큰 이어야한다. 때문에 올바른 인증을 위해서는 액세스 토큰이 아닌, 액세스 토큰과 다른 라이프 사이클을 가지면서 클라이언트가 IdP로 부터 직접 전달 받은 무언가가 필요하다. ID 토큰이 이 무언가의 예시이다.

## 2.3 수신자 제한의 결여

대부분의 OAuth 2.0 API는 액세스 토큰을 어떤 클라이언트에게 발급하는지에 대해 표시할 수 있는 방법이 없다. 때문에 토큰을 받은 클라이언트는, 해당 토큰이 자신을 위해 발급된 것인지를 판단하지 못한다. 이 문제를 해결하기 위해 클라이언트가 자체적으로 판단할 수 있는 식별값을 토큰 응답에 같이 내려주는 방식이 있다.

## 2.4 잘못된 사용자 정보 삽입

공격자는 클라이언트의 요청을 가로채서 클라이언트가 모르게 반환되는 사용자 정보를 내용을 바꿀 수 있다. 이를 방지하기 위해서 클라이언트와 인가 서버 사이의 모든 통신을 TLS로 보호해야 한다. 또 한, 토큰에 서명을 해서 탈취가 되도 변조를 막을 수 있다.

## 2.5 식별 제공자마다 다른 프로토콜 사용

OAuth 2.0 기반 식별 API의 문제 중 하나는 식별 제공자가 OAuth 표준 스펙을 이용해도 각자 다르게 구현된다는 점이다. 예컨데, 유저 식별자를 user_id로도 할 수 있고 sub 필드로도 할 수 있다. 이는 OAuth 2.0에서 인증 정보 전달을 위한 매커니즘을 상세히 제공하고 있지 않기 때문이다. 토큰 포맷, 액세스 토큰을 위한 공통적인 권한 범위, 보호된 리소스가 액세스 토큰을 검증하는 방법 등이 기술되어 있지 않다. 따라서, OAuth를 기반으로 하는 표준 인증 프로토콜이 있어야 식별 정보를 동일하게 전송할 수 있다.

# 3. OpenId Connect: OAuth 2.0 기반 인증과 식별 표준

OpenId connect는 OAuth 2.0을 기반으로 사용자 인증 수행을 위한 방식을 정의한 표준이다.

## 3.1 ID token

Id Token은 서명된 JWT 형태를 지니며 액세스 토큰과 함께 클라이언트에게 전달된다. 다만, 액세스 토큰과 달리 ID token은 RP가 내용을 파싱할 수 있다. ID 토큰은 표준적으로 아래과 같은 claim을 가진다.
![id token claim](/img/2025-02-27-oidc-openid/img4.png)
Id token과 access token은 같은 토큰 엔드포인트를 통해 전달된다. 하지만, 두 토큰은 서로 다른 라이프 사이클을 가지고 있다. Id token은 access token 보다 더 빨리 만료되고 다른 외부 서비스로 전달되지 않는다.

클라이언트는 Id token을 다음과 같은 방식으로 검증해서 공격으로부터 자신을 보호할 수 있다.

- ID 토큰을 파싱해서 그것이 유효한 JWT인지 확인한다
    - “.” 문자를 기준으로 문자열 섹션을 나눈다
    - 각 섹션을 Base64URL decoding한다
    - 처음 두 섹션(header, payload)를 JSON 객체로 파싱한다
- 공개된 IdP의 공개키로 토큰의 시그니처를 검증한다
- ID token이 신뢰할 수 있는 IdP가 발급한 것인지 확인한다
- 클라이언트 자신의 식별자가 ID token의 수신자 리스트에 있는지 확인한다.
- 만료 시간과 issued-at, not-before timestamp 값을 현재 시간과 비교했을 때 적절한지 확인한다.
- nonce 값이 있다면, 자신이 전달한 것과 동일한지 확인한다
- 인가 코드나 액세스 토큰에 해시 값이 있다면, 그것을 확인한다.

## 3.2 UserInfo end point

보호된 리소스에 있는 userInfo endpoint는 액세스 토큰을 사용한다. 이 엔드포인트틑 간단한 HTTP GET 또는 POST를 사용하며 같은 path를 사용한다. 응답의 경우 사용자에 대한 claim을 포함하는 JSON 객체로 전달된다.

- 요청 - 응답 예시
```
GET /userinfo
Authorization: Bearer {access_token}
Accept: application/json

response:
HTTP/1.1 200 OK
Content-Type: application/json
{
	"sub": "",
	"preferred_username": "",
	"name": "",
	"email": "",
	"email_veirfeid": ""
}
```
userInfo endpoint의 응답은 요청에 사용되는 토큰의 scope 범위에 따라 달라진다. OpenId connect는 UserInfo endpoint에 대한 접근을 통제하기 위해 openid라는 scope을 사용한다. 따라서 userinfo에 접근하기 위해선 openid라는 scope이 있어야 하며, 추가적으로 다른 scope에 따라 응답 받는 정보가 달라진다. scope에 따라 얻을 수 있는 유저 정보의 관계는 다음과 같다.
![user info scope](/img/2025-02-27-oidc-openid/img5.png)
