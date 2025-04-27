---
layout:       post
title:        "OpenId Provier 구축 공부 - 4편 (SSO -Single Sign On)"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
  - OAuth
  - SSO
---
- [OpenId Provier 구축 공부 - 1편 (OAuth 2.0)](https://www.skullkim-dev.com/2025/02/13/oidc-oauth2/)
- [OpenId Provier 구축 공부 - 2편 (OAuth 토큰 보안 취약점)](https://www.skullkim-dev.com/2025/02/17/oauth2-token-protection/)
- [OpenId Provier 구축 공부 - 3편 (OAuth2.0에서 사용자 인증)](https://www.skullkim-dev.com/2025/02/27/oidc-openid/)

회사에서 자회사와 본사가 각자 제공하는 여러 서비스들의 회원 시스템을 통합한 통합 회원플랫폼을 구축하고 있다. 그 과정에서 본사, 자회사가 제공하는 다양한 앱들 간의 SSO를 구현해야 하는 요구사항이 있어서 공부한 내용을 정리하고자한다.

본 글은 OAuth 2.0과 OIDC를 알고 있다는 전제 하에 OIDC를 활용한 SSO를 설명한다. 만약 OAuth 2.0, OIDC에 대해 알고싶다면 [OpendId Provider 구축 공부 1,2,3](https://www.skullkim-dev.com/2025/02/13/oidc-oauth2/)편을 참고하자.

# 1. Single-Sign On(SSO)란?

SSO 개념은 매우 간단하다. 한번의 로그인으로 여러 서비스에 접근할 수 있게 해주는 인증 방식이다. 구글 로그인 같은 로그인 방식을 생각하면 된다. 구글 홈페이지에서 한번 로그인하면, 구글이 제공하는 다른 서비스(gmail, youtube 등)에 접근 시 별도 로그인 없이 사용할 수 있다.

# 2. OIDC를 이용한 SSO

OIDC를 이용한 SSO의 주요 과정은 Id token이 발급된 이후에 이루어진다. OIDC 플로우를 간단히 보면 다음과 같다.

![OIDC flow](/img/2025-04-27-native-app-sso/img.png)
그럼에도, OIDC를 이용해 id token, access token를 발급 받는 과정에 SSO를 추가할 경우, 다음과 같은 차이가 발생한다.

- OIDC 트랜잭션을 시작하는 요청에 openid scope과 더불어 device_sso라는 scope을 추가해야한다.
- id token이 발급되는 응답에 device_secret이 추가된다.
- id token 내에 다음과 같은 claim이 필수로 포함돼야 한다.
    - ds_hash: device secrete과 id token를 한 세트로 식별할 수 있게 하는 값. 표준 명세에는 ds_hash를 만드는 방법이 명시되어 있지 않다. 하지만, “The ds_hash value provides a binding between the id_token and the issued device_secret.” 이라고 명시되어 있으므로, device secrete을 통해 해당 device secrete과 한 쌍이라는 것을 간단히 식별하기 위해 device secrete을 해싱한 값을 사용하면 될것으로 보인다.
    - sid: 사용자의 인증 세션을 식별하는 고유 문자열. 이 값은 로그아웃 플로우와 SSO 플로우에서 사용된다.

위 차이를 API 관점으로 보면 다음과 같다.

- OIDC 트랜잭션 시작 API:

```kotlin
https://example.com/login?
 response_type=code
 &scope=openid%20device_sso%20email%20profile
 &client_id=123
 &redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb
```

- id token 발행 응답

```kotlin
HTTP/1.1 200 OK

{
  "access_token"  : "aiK9aehiejohNahk8ia7luh.inohshoh6bahGeL5eife7",
  "token_type"    : "Bearer",
  "expires_in"    : 600,
  "scope"         : "openid email profile",
  "refresh_token" : "eyJraWQiOki8jioWihahpquofiePhieg0a...",
  "id_token"      : "eyJraWQiOiIxZTlnZGs3IiwiYWxnIjoiUl...",
  "device_secret" : "WYqFXK7Q4HFnJv0hiT3Fgw.-oVkvSXgalUuMQDfEsh1lw"
}
```

위와 같은 과정으로 id_token과 device_secrete이 발급되었다면, 앱은 이 둘은 SSO 대상이 되는 다른 앱들과 공유하는 디바이스 스토리지에 저장해야한다. SSO를 지원하는 다른 앱들은 해당 스토리지에 접근해 id_token, device_secrete을 가지고 토큰 교환을 시도한다. 토큰 교환이 성공하면 앱은 새로운 토큰을 발급받게 되고, SSO 절차가 마무리된다. 아래 그림에서 “Native App #1”이 처음으로 id token, device_secret을 발급받아 공유 스토리지에 저장한 앱이고, “Native App #2”가 공유 스토리지에 접근해 토큰 교환을 통한 SSO를 시도하는 앱이다.
![OIDC native app SSO flow](/img/2025-04-27-native-app-sso/img1.png)
9번 과정(token exchange)을 풀어서 설명하면 다음과 같다.

- 앱이 공용 스토리지에 있는 id token, device_secrete에 접근한다
- 이 둘은 이용해 다음과 같은 API 요청을 보내서 토큰을 발급받는다. 아래 요청에서 subject_token은 id token, actor_token은 device_secret이다.

```kotlin
POST /token HTTP/1.1
Host: as.example.com

...
client_id=cid_235saw4r4
&grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Atoken-exchange
&audience=https%3A%3F%3Flogin.example.net&subject_token=<id_token>
&subject_token_type=urn%3Aietf%3Aparams%3Aoauth%3Atoken-type%3Aid-token
&actor_token=95twdf3w4y6wvftw35634t
&actor_token_type=urn%3Aopenid%3Aparams%3Atoken-type%3Adevice-secret
```

만약 해당 디바이스 세션이 아직 유효하다면, 다음과 같은 응답을 받게 된다

```kotlin
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store

{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "issued_token_type": "urn:ietf:params:oauth:token-type:access_token",
  "token_type":"Bearer",
  "expires_in":3600,
  "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
  "id_token":"<id_token>",
  "device_secret":"casdfgarfgasdfg"
}
```

## 2.1 토큰 교환 스펙

### 2.1.1 요청 스펙

위 설명에서 토큰 교환 API에 subject token 등 토큰 교환에서만 사용되는 query string들이 사용되었다. 토큰 교환에 사용되는 query string들의 의미를 알아모자.

- client_id (optional): OAuth client 식별자. 만약 클라이언트가 public client(모바일 앱, 브라우저 등) 이라면 반드시 client_id를 명시해야한다.
- grant type(required): urn:ietf:params:oauth:grant-type:token-exchange 를 grant type으로 명시해야한다.
- audience(required): 발급된 토큰이 유효하게 사용될 수 있는 대상을 지정한다. OpenId Provider의 고유 식별자 역할을 하는 URL이다. 이 값은 id token의 aud claim과 같은 값이다. 때문에 이 값이 aud claim과 다르다면, 유효성 검증에서 실패하게 된다.
- subject_token(required): 공용 스토리지에서 가져온 id token.
- subject_token_type(required): urn:ietf:params:oauth:token-type:id_token 으로 지정돼야한다.
- actor_token(required): 요청을 수행하는 주체이다. 여기서는 공용 스토리지에 있는 device_secret이다.
- actor_token_type(required): urn:openid:params:token-type:device-secret 으로 지정돼야한다.
- scope(optional): 토큰 교환을 요청한 앱이 필요한 scope. 이 파라미터를 사용한다면 openid scope이 반드시 포함되어 있어야 한다.
- request_token_type(optional): 어떤 토큰이 발급되길 원하는지를 명세한다. 만약 사용하지 않는다면, OP가 알아서 적절한 토큰을 발급한다. 사용 가능한 타입은 다음과 같다.
    - urn:ietf:params:oauth:token-type:access_token: 액세스 토큰 요청
    - urn:ietf:params:oauth:token-type:refresh_token: 리프레시 토큰 요청
    - urn:ietf:params:oauth:token-type:id_token: id token 요청
    - urn:ietf:params:oauth:token-type:saml1: base64url-encoded SAML1.0 토큰 요청
    - urn:ietf:params:oauth:token-type:saml2: base64url-encoded SAML2.0 토큰 요청

### 2.1.2 응답 성공 스펙

토큰 교환 응답 필드로는 다음과 같은 값들을 가질 수 있다.

- access_token(required): 클라이언트에게 발급한 access token
- issued_token type(required): urn:ietf:params:oauth:token-type:access_token 으로 지정되야 한다.
- token_type(required): bearer 로 지정돼야 한다.
- expires_in(recommended): access_token이 만료되는 시기
- scope(optional): 위 토큰 교환 과정에서 사용된 scope들
- refresh_token(optional): access_token을 재발급 받기 위핸 refresh token
- id_token(optional): 유저 신원 보증을 제공하는 id_token
- device_secrete(optional): 필요할 경우 업데이트된 device_secrete을 반환한다.

### 2.1.3 응답 실패 스펙

만약 토큰 교환 과정 중 에러가 발생한다면, 아레 스펙에 있는 에러를 응답해야 한다. 상태 코드는 일부 경우를 제외하면 400 - Bad Request로 통일한다.

- error (required):
    - 아래 에러 코드 중 하나
        - invalid_request: 요청이 필요한 파라미터를 포함하지 않거나 잘못된 파라미터를 포함하고 있다.
        - invalid_client: 클라이언트 인증 실패. 이 경우 401 Unauthorized를 반환한다. 만약 Autorization 헤더를 사용해 인증을 시도할 경우 401 Unauthorized를 상태코드로 사용하되 WWW-Authenticate 헤더도 같이 사용해야 한다. 이 헤더는 클라이언트가 어떤 인증 방식(스킴)과 추가 정보(파라미터)를 사용해야 하는지 안내한다. 예시는 다음과 같다
            - WWW-Authenticate: Bearer realm="example", error="invalid_token", error_description="The access token expired"
                - 여기서 realm은 서버가 보호하고자 하는 리소스 영역의 이름이다.
        - invalid_grant: 클라이언트가 전달한 authorization gran(code 등) 또는 refresh token이 유효하지 않다(만료, 철회 등). 또는 다른 클라이언트에게 발급한 값을 사용했다.
        - unauthorized_client: 인증된 클라이언트에게 해당 authorization grant type을 사용할 권한이 없다.
        - unsupported_grant_type: 해당 authorization grant type을 인증 서버가 지원하지 않는다.
        - invalid_scope: 요청한 scope이 유효하지 않거나, 권한 범위를 벗어났다.
    - error는 다음과 같은 범위의 문자만 사용할 수 있다.
        - %x20-21: 공백(스페이스)와 !
        - %x23-5B: # $ % & ' ( ) * + , - . / 0-9 : ; < = > ? @ A-Z [
        - %x5D-7E: ] ^ _ \` { | } ~
- error_description(optional): human-readable한 텍스트. 클라이언트 개발자가 에러 원인을 추정할 수 있는 값. 이 값은 아래와 같은 범위의 문자만 사용할 수 있다.
    - %x20-21: 공백(스페이스)와 !
    - %x23-5B: # $ % & ' ( ) * + , - . / 0-9 : ; < = > ? @ A-Z [
    - %x5D-7E: ] ^ _ \` { | } ~
- error_uri(optional): human-readable한 웹페이지의 URI이다. 클라이언트 개발자에게 에러에 대한 추가적인 정보를 제공하는 웹 페이지. 이 값은 아래 범위 문자만 사용할 수 있다.
    - %x21: !
    - %x23-5B: # $ % & ' ( ) * + , - . / 0-9 : ; < = > ? @ A-Z [
    - %x5D-7E: ] ^ _ \` { | } ~
    - error_description과 다른점: 공백, 큰 따옴표(”), 백슬레시(\)를 포함하지 않는다
# 3. 참고 자료
- [OpenID Connect Native SSO fo Mobile Apps 1.0](https://openid.net/specs/openid-connect-native-sso-1_0.html#AuthZReq)
- [OpenId Connect native SSO explained](https://connect2id.com/learn/openid-connect-native-sso#flow-create-device-session)
- [The OAuth2.0 Authorization Framework](https://www.rfc-editor.org/rfc/rfc6749#section-5.2)
- [RFC 8693 - OAuth2.0 Token Exchange](https://datatracker.ietf.org/doc/html/rfc8693#name-error-response)