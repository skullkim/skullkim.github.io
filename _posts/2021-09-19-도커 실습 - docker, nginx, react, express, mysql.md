---
layout:       post
title:        "도커 실습 - docker, nginx, react, express, mysql"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- Docker
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
                            <p data-ke-size="size16">실습 전체 파일:<a href="https://github.com/skullkim/docker-practice" target="_blank" rel="noopener">https://github.com/skullkim/docker-practice</a></p>
<figure id="og_1632040530280" contenteditable="false" data-ke-type="opengraph" data-ke-align="alignCenter" data-og-type="object" data-og-title="GitHub - skullkim/docker-practice" data-og-description="Contribute to skullkim/docker-practice development by creating an account on GitHub." data-og-host="github.com" data-og-source-url="https://github.com/skullkim/docker-practice" data-og-url="https://github.com/skullkim/docker-practice" data-og-image="https://scrap.kakaocdn.net/dn/0Gzw2/hyLFtm4qSA/i3BcKBy40kIrzZqCwRBgPK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600"><a href="https://github.com/skullkim/docker-practice" target="_blank" rel="noopener" data-source-url="https://github.com/skullkim/docker-practice">
<div class="og-image" style="background-image: url('https://scrap.kakaocdn.net/dn/0Gzw2/hyLFtm4qSA/i3BcKBy40kIrzZqCwRBgPK/img.png?width=1200&amp;height=600&amp;face=0_0_1200_600');">&nbsp;</div>
<div class="og-text">
<p class="og-title" data-ke-size="size16">GitHub - skullkim/docker-practice</p>
<p class="og-desc" data-ke-size="size16">Contribute to skullkim/docker-practice development by creating an account on GitHub.</p>
<p class="og-host" data-ke-size="size16">github.com</p>
</div>
</a></figure>
<p data-ke-size="size16">&nbsp; 도커 실습위한 것이니 express, react 코드에 대한 설명을 스킵하자.</p>
<p data-ke-size="size16">Dockerfile 설명:</p>
<p data-ke-size="size16">client/Dockerfile</p>
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
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">FROM</span>&nbsp;node:alpine</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;working&nbsp;디렉토리를&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app으로&nbsp;설정</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;이미지가&nbsp;생성되면&nbsp;해당&nbsp;디렉터리&nbsp;역시&nbsp;생성된다.</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;working&nbsp;디렉터리를&nbsp;설정하면&nbsp;명령어가&nbsp;해당&nbsp;디렉터리에서&nbsp;실행된다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">WORKDIR</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;서버&nbsp;자체에&nbsp;존재하는&nbsp;파일을&nbsp;도커이미지의&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app에&nbsp;복사한다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app은&nbsp;WORKDIR로&nbsp;설정했다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">COPY</span>&nbsp;package.json&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">COPY</span>&nbsp;package<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>lock.json&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;클라이언트&nbsp;루트&nbsp;폴더에&nbsp;있는&nbsp;모든&nbsp;것을&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app에&nbsp;복사&nbsp;한다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">COPY</span>&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;모듈&nbsp;다운로드</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">RUN</span>&nbsp;npm&nbsp;i</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;express&nbsp;실행을&nbsp;위한&nbsp;npm&nbsp;<span style="color: #066de2;">run</span>&nbsp;<span style="color: #066de2;">start</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">CMD</span>&nbsp;[<span style="color: #63a35c;">"npm"</span>,&nbsp;<span style="color: #63a35c;">"run"</span>,&nbsp;<span style="color: #63a35c;">"start"</span>]</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;다음&nbsp;명령어로&nbsp;위의&nbsp;Dockefile을&nbsp;이용해&nbsp;client라는&nbsp;이미지를&nbsp;만든다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;docker&nbsp;<span style="color: #066de2;">build</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>f&nbsp;Dockerfile&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>t&nbsp;client&nbsp;.</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;그&nbsp;후&nbsp;다음&nbsp;명령어를&nbsp;이용해&nbsp;client이미지를&nbsp;이용한&nbsp;컨테이너가&nbsp;제대로</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;작동되는지&nbsp;실행해&nbsp;보자</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">#&nbsp;docker&nbsp;<span style="color: #066de2;">run</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>it&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>p&nbsp;<span style="color: #0099cc;">8080</span>:<span style="color: #0099cc;">3000</span>&nbsp;client</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">server/Dockerfile</p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"># 위 클라이언트 Dockerfile 설명 참고</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">FROM</span>&nbsp;node:alpine</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">WORKDIR</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">COPY</span>&nbsp;package.json&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">COPY</span>&nbsp;package<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>lock.json&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">COPY</span>&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">RUN</span>&nbsp;npm&nbsp;i</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #066de2;">CMD</span>&nbsp;[<span style="color: #63a35c;">"npm"</span>,&nbsp;<span style="color: #63a35c;">"run"</span>,&nbsp;<span style="color: #63a35c;">"start"</span>]</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">nginx/default.conf</p>
</div>
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
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
<div style="line-height: 130%;">35</div>
<div style="line-height: 130%;">36</div>
<div style="line-height: 130%;">37</div>
<div style="line-height: 130%;">38</div>
<div style="line-height: 130%;">39</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">#Client&nbsp;upstream</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">upstream&nbsp;client&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">#client&nbsp;port</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;server&nbsp;client:<span style="color: #0099cc;">3000</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">#Api&nbsp;server&nbsp;upstream</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">upstream&nbsp;api&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">#api&nbsp;server&nbsp;port</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;server&nbsp;api:<span style="color: #0099cc;">3001</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">#main&nbsp;cocnfig</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">server&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">#nginx&nbsp;server&nbsp;listening&nbsp;to&nbsp;port&nbsp;80</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;listen&nbsp;<span style="color: #0099cc;">80</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">#경로가&nbsp;/으로&nbsp;시작하면&nbsp;클라이언트&nbsp;서버로&nbsp;&nbsp;&nbsp;&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#client는&nbsp;docker-compose.yml에서&nbsp;구성할</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#react&nbsp;애플리케이션의&nbsp;이름이다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_pass&nbsp;http:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>client;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">#클라이언트가&nbsp;웹소켓&nbsp;연결과&nbsp;서버에&nbsp;연결할&nbsp;수&nbsp;있게&nbsp;한다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>sockjs<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>node&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_pass&nbsp;http:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>client;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_http_version&nbsp;<span style="color: #0099cc;">1.</span><span style="color: #0099cc;">1</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_set_header&nbsp;Upgrade&nbsp;$http_upgrade;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_set_header&nbsp;Connection&nbsp;<span style="color: #63a35c;">"Upgrade"</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;<span style="color: #999999;">#경로가&nbsp;/api로&nbsp;시작하면&nbsp;api&nbsp;서버로</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;location&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>api&nbsp;{</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #999999;">#/api로&nbsp;시작하는&nbsp;모든&nbsp;경로가&nbsp;/로&nbsp;바뀐다</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rewrite&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>api<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>(.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">*</span>)&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>$1&nbsp;<span style="color: #a71d5d;">break</span>;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;proxy_pass&nbsp;http:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span><span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>api;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;}</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">}</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">nginx/Dockerfile</p>
<div class="colorscripter-code" style="color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position: relative !important; overflow: auto;">
<table class="colorscripter-code-table" style="margin: 0; padding: 0; border: none; background-color: #fafafa; border-radius: 4px;" cellspacing="0" cellpadding="0" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="padding: 6px; border-right: 2px solid #e5e5e5;">
<div style="margin: 0; padding: 0; word-break: normal; text-align: right; color: #666; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="line-height: 130%;">1</div>
<div style="line-height: 130%;">2</div>
<div style="line-height: 130%;">3</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999;">#위&nbsp;클라이언트&nbsp;Dockerfile&nbsp;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">FROM&nbsp;nginx</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">COPY&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>default.conf&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>etc<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>nginx<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>conf.d<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>default.conf</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">docker-compose.yml</p>
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
<div style="line-height: 130%;">9</div>
<div style="line-height: 130%;">10</div>
<div style="line-height: 130%;">11</div>
<div style="line-height: 130%;">12</div>
<div style="line-height: 130%;">13</div>
<div style="line-height: 130%;">14</div>
<div style="line-height: 130%;">15</div>
<div style="line-height: 130%;">16</div>
<div style="line-height: 130%;">17</div>
<div style="line-height: 130%;">18</div>
<div style="line-height: 130%;">19</div>
<div style="line-height: 130%;">20</div>
<div style="line-height: 130%;">21</div>
<div style="line-height: 130%;">22</div>
<div style="line-height: 130%;">23</div>
<div style="line-height: 130%;">24</div>
<div style="line-height: 130%;">25</div>
<div style="line-height: 130%;">26</div>
<div style="line-height: 130%;">27</div>
<div style="line-height: 130%;">28</div>
<div style="line-height: 130%;">29</div>
<div style="line-height: 130%;">30</div>
<div style="line-height: 130%;">31</div>
<div style="line-height: 130%;">32</div>
<div style="line-height: 130%;">33</div>
<div style="line-height: 130%;">34</div>
<div style="line-height: 130%;">35</div>
<div style="line-height: 130%;">36</div>
<div style="line-height: 130%;">37</div>
<div style="line-height: 130%;">38</div>
<div style="line-height: 130%;">39</div>
<div style="line-height: 130%;">40</div>
<div style="line-height: 130%;">41</div>
<div style="line-height: 130%;">42</div>
<div style="line-height: 130%;">43</div>
<div style="line-height: 130%;">44</div>
<div style="line-height: 130%;">45</div>
<div style="line-height: 130%;">46</div>
<div style="line-height: 130%;">47</div>
<div style="line-height: 130%;">48</div>
<div style="line-height: 130%;">49</div>
<div style="line-height: 130%;">50</div>
<div style="line-height: 130%;">51</div>
<div style="line-height: 130%;">52</div>
<div style="line-height: 130%;">53</div>
<div style="line-height: 130%;">54</div>
<div style="line-height: 130%;">55</div>
<div style="line-height: 130%;">56</div>
<div style="line-height: 130%;">57</div>
<div style="line-height: 130%;">58</div>
<div style="line-height: 130%;">59</div>
<div style="line-height: 130%;">60</div>
<div style="line-height: 130%;">61</div>
<div style="line-height: 130%;">62</div>
<div style="line-height: 130%;">63</div>
<div style="line-height: 130%;">64</div>
<div style="line-height: 130%;">65</div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">version:&nbsp;<span style="color: #63a35c;">'3'</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">services:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;#mysql&nbsp;server</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;mysql_db:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">image:</span>&nbsp;mysql</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;restart:&nbsp;always</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;cap_add:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;SYS_NICE</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;volumes:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #63a35c;">"./setup.sql:/docker-entrypoint-initdb.d/setup.sql"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">ports:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #63a35c;">"9906:3306"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;environment:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MYSQL_ROOT_PASSWORD:&nbsp;mysql</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MYSQL_HOST:&nbsp;localhost</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;#nginx</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;nginx:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;depends_on:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;api</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;client</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;restart:&nbsp;always</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;build:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dockerfile:&nbsp;Dockerfile</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;context:&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>nginx</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">ports:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #63a35c;">"3050:80"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;#api&nbsp;server</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;api:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;build:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dockerfile:&nbsp;Dockerfile</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;context:&nbsp;<span style="color: #63a35c;">"./server"</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;depends_on:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;mysql_db</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;volumes:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>node_modules</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>server:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;environment:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MYSQL_HOST_IP:&nbsp;mysql_db</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;#client&nbsp;server</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;client:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;stdin_open:&nbsp;<span style="color: #0099cc;">true</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;environment:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;CHOKIDAR_USEPOLLING<span style="color: #0086b3;"></span><span style="color: #a71d5d;">=</span><span style="color: #0099cc;">true</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;build:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dockerfile:&nbsp;Dockerfile</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;context:&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>client</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;volumes:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>node_modules</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;.<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>client:<span style="color: #0086b3;"></span><span style="color: #a71d5d;">/</span>app</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;#Adminer를&nbsp;인터페이스로&nbsp;사용해&nbsp;디비&nbsp;서버에&nbsp;엑세스한다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;#&nbsp;만들어진&nbsp;디비,&nbsp;테이블,&nbsp;CRUD를&nbsp;볼&nbsp;수&nbsp;있다</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;adminer:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">image:</span>&nbsp;adminer:latest</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;restart:&nbsp;unless<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>stopped</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #066de2;">ports:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;<span style="color: #0099cc;">8000</span>:<span style="color: #0099cc;">8080</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;depends_on:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0086b3;"></span><span style="color: #a71d5d;">-</span>&nbsp;mysql_db</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;environment:</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ADMINER_DEFAULT_SERVER:&nbsp;mysql_db</div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></td>
</tr>
</tbody>
</table>
</div>
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