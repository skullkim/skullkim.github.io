---
layout:       post
title:        "트랜잭션(Transaction)"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- DB
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
                            <p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션은 작업의 완전성을 보장해준다. 논리적인 작업 셋을 모두 완벽하게 처리하지 못했을 경우 원 상태로 복구해서 작업의 일부만 적용되는 현상이 발생하지 않게 만들어준다. MySql에서는 InnoDB 스토리지 엔진이 트랜잭션을 지원하며 MyISAM, MEMORY 스토리지 엔진은 트랜잭션을 지원하지 않는다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션은 반드시 여러 개의 변경 작업을 수행하는 쿼리가 조합돼야 하는 것은 아니다. 하나의 논리 적인 작업 셋에 하나 이상의 쿼리가 적용될 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>트랜잭션의 특징</b></span></h3>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>원자성(Atomicity)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;트랜잭션이 DB에 모두 반영이 되던가, 모두 되지 않아야 한다. 부분적으로 반영된다면 값을 예측할 수 없게 된다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>일관성(Consistency)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 작업 처리 결과는 항상 일정해야 한다. 트랜잭션이 진행되는 동안 DB가 변경되어도 업데이트 이전의 DB로 진행된다. 이를 통해 일관성 있는 데이터를 볼 수 있다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>독립성(Isolation)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 둘 이상의 트랜잭션이 동시에 진행될 떄, 특정 트랜잭션이 완료될떄까지, 다른 트랜잭션이 특정 트랜잭션의 결과를 참조할 수 없다. 동시에 여러 트랜잭션이 실행되고 있을 경우, 하나의 트랜잭션이 다른 트랜잭션 연산에 끼어들 수 없다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>지속성(Durability)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션이 성공적으로 완료 되면, 결과는 영구적으로 반영되야 한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Commit, Rollback 연산</b></span></h3>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Commit</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>한 개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝났고 DB가 다시 일관된 상태에 있을 때, 이 트랜잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려준다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Rollback</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>하나의 트랜잭션 처리가 비정상적으로 종료되어 DB의 일관성을 깨뜨렸을 때, 트랜잭션이 완벽히 수행되지 않았다면, 트랜잭션의 원자성을 구현하기 위해 트랜잭션이 행한 모든 연산을 취소하기 위한 연산이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>트랜잭션 연산 과정</b></span></h3>
<p></p><figure class="imageblock alignCenter">
    <span data-lightbox="lightbox">
        <img src="/img/7Yq4656c7J6t7IWYKFRyYW5zYWN0aW9uKQ==/img.png">
    </span>
    <figcaption></figcaption>
</figure><p></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>활성(Active)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션이 정상적으로 실행중인 상태</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>실패(Failed)<br></b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>트랜잭션 실행에 오류가 발생해 중단된 상태</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>철회(Aborted)</b><b></b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션이 비정상적으로 종료되 Rollback 연산을 수행한 상태</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>부분 완료(Partially Committed)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션의 마지막 연산까지 실행했고 Commit 연산이 실행되기 직전 상태</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>완료(Committed)</b><b></b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션이 성공적으로 종료되 Commit 연산을 실행한 후의 상태</span></p>
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