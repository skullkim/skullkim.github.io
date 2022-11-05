---
layout:       post
title:        "CORS request header, response header"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- CORS
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
                            <p><b><b>HTTP 응답 헤더</b></b></p>
<p>&nbsp; 아래에 서술된 헤더들은 서버가 접근 제어 요청을 위해 보내는 HTTP응답 헤더이다.</p>
<p><b>Access-Control-Allow-Origin: &lt;origin&gt; | *</b></p>
<p>&nbsp; 단일 출처를 지정해 브라우저가 해당 출처가 리소스에 접근되도록 허용한다. 자격 증명이 없으면 와일드카드('*')를 사용한다.</p>
<p><b>Access-Control-Expose-Headers: &lt;header-name&gt;[, &lt;header-name]*</b></p>
<p>&nbsp; 브라우저가 접근할 수 있는 헤더를 서버의 화이트리스크에 추가한다</p>
<p><b>Access-Control-Max-Age: &lt;delta-seconds&gt;</b></p>
<p>&nbsp; preflight request요청 결과를 캐시할 수 있는 시간을 나타낸다</p>
<p><b>Access-Control-Allow-Credentials: true</b></p>
<p>&nbsp; credentails 플래그가 true일때 요청에 대한 응답을 표시할 수 있는지를 나타낸다. preflight request에 대한 응답의 일부로 사용할 경우 credentials를 사용해 실제 요청을 수행할 수 있는지를 나타낸다. simple GET requests는 preflighted되지 않으므로 credentials가 있는 리소스를 요청하면 이 헤더는 리소스와 함께 반환되지 않는다. 이 헤더가 없으면 브라우저에서 응답을 무시하고 웹 컨텐츠로 반환되지 않는다.</p>
<p><b>Access-Control-Allow-Methods: &lt;method&gt;[, &lt;method&gt;]*</b></p>
<p><b>&nbsp;&nbsp;</b>리소스에 접근할때 허용되는 메서드를 지정한다. 이 헤더는 preflight request에 대한 응답으로 사용된다.</p>
<p><b>Access-Control-Allow-Headers: &lt;header-name&gt;[, &lt;header-name&gt;]*</b><b></b></p>
<p><b>&nbsp;&nbsp;</b>preflight request에 대한 응답으로 Access-Control-Allow-Headers헤더가 사용된다. 실제 요청시 사용할 수 있는 HTTP헤더를 나타낸다.</p>
<p>&nbsp;</p>
<p><b>HTTP 요청 헤더</b></p>
<p><b>Origin: &lt;origin&gt;</b></p>
<p><b>&nbsp;&nbsp;</b>Origin헤더는 cross-site 접근 요청 또는 preflight request의 출처를 나타낸다. origin 값은 null 또는 URI가 올 수 있다.</p>
<p><b>Access-Control-Request-Method: &lt;method&gt;</b></p>
<p>&nbsp;실제 요청에서 어떤 HTTP메서드를 사용할지 서버에게 알려준다</p>
<p><b>Access-Control-Request-Headers: &lt;field-name&gt;[, &lt;field-name&gt;]*</b></p>
<p><b>&nbsp; &nbsp;</b>실제 요청에서 어떤 HTTP 헤더를 사용할지 서버에게 알려준다. preflight request할때 사용된다.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
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