---
layout:       post
title:        "dotenv, morgan, express-session, cookie-parser"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- nodejs
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
                            <p>1. dotenv</p>
<p>&nbsp; 환경 변수를 .env파일에서 불러오는 모듈이다. 세션, 쿠키의 경우 키가 필요한데 이를 코드에 직접 넣을 경우 코드가 유출되면 키도 같이 유출되는 문제가 있다. 이를 방지하기 위해 .env파일에 이를 저장하고 process.env.VALUE_NAME을 통해 불러온다.</p>
<p>&nbsp; .env에는 VALUE_NAME=value_name이런식으로 쌍을 이루게 해서 저장하면 된다.</p>
<p>2. morgan</p>
<p>&nbsp; morgan은 서버 실행 시 request/response 로그를 서버 터미널에서 보여준다. app.use(morgan(option))을 통해 사용 가능하며 option에는 dev, tiny, short, common, combined가 들어갈 수 있다. 각 option별로 터미널에서 보여주는 로그의 정보 양이 다르다.&nbsp;</p>
<p>3. express-session</p>
<p>&nbsp; 세션 미들웨어다. session({option})을 통해 만들 수 있고 option을 통해 세션의 세부적인 내용을 설정할 수 있다.</p>
<p>4. cookie-parser</p>
<p>request cookie를 파싱한다.</p>
<pre id="code_1606382046475" class="javascript" data-ke-language="javascript" data-ke-type="codeblock"><code>const express = require('express');
const morgan = require('morgan');
const cookie_parser = require('cookie-parser');
const session = require('express-session');
const dotenv = require('dotenv');
const path = require('path');

dotenv.config();
const index_router = require('./routes');
const user_router = require('./routes/user');

const app = express();
app.set('port', process.env.PORT || 3000);

app.use(morgan('dev'));

app.use('/', express.static(path.join(__dirname, 'public')));
//미들웨어이다. json request를 파싱한다
app.use(express.json());
//form을 보냈을떄 req.body로 파싱한다. extended가 false면 querystring, true면 qs를 사용한다
app.use(express.urlencoded({extended: false}));
//주어진 secret으로 쿠키를 서명한다. 
app.use(cookie_parser(process.env.COOKIE_SECRET));
//주어진 옵션에 따라 세션을 만드는 미들웨어
app.use(session({
    resave: false,//session store에 session 저장
    //session은 새로 선언됬지만 수정되지 않았을때 unintialized하다
    saveUninitialized: false,
    //session ID cookie에 서명을 할떄 사용된다. 
    secret: process.env.COOKIE_SECRET,
    //session ID cookie의 객체 세팅. 
    cookie: {
        httpOnly: true,
        secure: false,
    },
    //응답에 설정할 세션 쿠키
    name: 'session-cookie',
}));

app.use('/', index_router);
app.use('/user', user_router);

app.use((req, res, next) =&gt; {
    res.status(404).send('Not Found');
});

app.use((err, req, res, next) =&gt; {
    console.error(err);
    res.status(500).send(err.message);
})

app.listen(app.get('port'), () =&gt; {
    console.log(`${app.get('port')} start server`);
});</code></pre>
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