---
layout:       post
title:        "5.트랜잭션과 잠금"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- DB
- MySQL
- 도서
- Real MySQL
- ComputerScience
---

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션은 원자성을 보장해 준다. 이를 통해 작업의 부분 업데이트(Partial update - 작업의 일부만 적용되는 현상)가 발생하지 않게 한다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션, 락, 격리가 비슷한 개념 같지만 다음과 같은 차이가 존재한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 트랜잭션: 데이터 정합성을 보장하기 위한 기능.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 락: 동시성 제어를 위한 기능. 여러 커넥션이 동시에 동일한 자원을 요청할 경우 순서대로 한 시점에 하나의 커넥션만 변경하게 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 격리: 하나 이상의 트랜잭션 간의 작업 내용을 공유하고 차단하는 방식을 결정하는 레벨.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>트랜잭션</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MySQL 서버에서 MyISAM과 MEMORY 스토리지 엔진은 트랜잭션을 지원하지 않는 반면 InnoDB는 트랜잭션을 지원한다. 이 차이로 인해 MyISAM, MEMORY 스토리지 엔진의 사용은 많은 고민을 야기한다. 다음과 같이 스토리지 엔진이 각각 MyISAM과 InnoDB인 두 개의 테이블을 만들고 데이터를 insert 해보자.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">16</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">17</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">CREATE</span>&nbsp;<span style="color: #ff3399;">TABLE</span>&nbsp;tab_myisam&nbsp;(</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;id&nbsp;<span style="color: #0099cc;">INT</span>&nbsp;<span style="color: #ff3399;">NOT</span>&nbsp;<span style="color: #ff3399;">NULL</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;">PRIMARY</span>&nbsp;<span style="color: #ff3399;">KEY</span>&nbsp;(id)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">)&nbsp;<span style="color: #ff3399;">ENGINE</span><span style="color: #0099cc;">=</span>MyISAM;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;tab_myisam&nbsp;(id)&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #004fc8;">3</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">CREATE</span>&nbsp;<span style="color: #ff3399;">TABLE</span>&nbsp;tab_innodb&nbsp;(</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;id&nbsp;<span style="color: #0099cc;">INT</span>&nbsp;<span style="color: #ff3399;">NOT</span>&nbsp;<span style="color: #ff3399;">NULL</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;">PRIMARY</span>&nbsp;<span style="color: #ff3399;">KEY</span>&nbsp;(id)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">)&nbsp;<span style="color: #ff3399;">ENGINE</span><span style="color: #0099cc;">=</span>InnoDB;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;tab_innodb(id)&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #004fc8;">3</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;AUTO<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>COMMIT&nbsp;활성화</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;autocommit<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #ff3399;">ON</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;tab_myisam(id)&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #004fc8;">1</span>),&nbsp;(<span style="color: #004fc8;">2</span>),&nbsp;(<span style="color: #004fc8;">3</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;tab_innodb(id)&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #004fc8;">1</span>),&nbsp;(<span style="color: #004fc8;">2</span>),&nbsp;(<span style="color: #004fc8;">3</span>)</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; 그러면 다음과 같이 PK 중복으로 인한 에러가 발생한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1400" data-origin-height="48"><span data-url="https://blog.kakaocdn.net/dn/bqLeMa/btrUHNMHPDG/L00wf5XxsCgmaZHdhbHERK/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbqLeMa%2FbtrUHNMHPDG%2FL00wf5XxsCgmaZHdhbHERK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1400" data-origin-height="48"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 그럼에도 MyISAM을 사용하는 테이블은 트랜잭션을 지원하지 않기에 insert가 된 것을 볼 수 있다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="628" data-origin-height="512"><span data-url="https://blog.kakaocdn.net/dn/JWHet/btrUGH67jgc/DaZDBaK2kizXBKYwi2Lnfk/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJWHet%2FbtrUGH67jgc%2FDaZDBaK2kizXBKYwi2Lnfk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="493" height="402" data-origin-width="628" data-origin-height="512"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 그에 반해 InnoDB를 사용한 테이블은 쿼리 실행 도중 에러 발생을 인해 롤백이 됐다. 이를 통해 정합성이 맞추어진다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="556" data-origin-height="424"><span data-url="https://blog.kakaocdn.net/dn/bd3rTl/btrULOKGlHB/Qy6AoRknS4Z1FBgX5aTvf1/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbd3rTl%2FbtrULOKGlHB%2FQy6AoRknS4Z1FBgX5aTvf1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="469" height="358" data-origin-width="556" data-origin-height="424"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>주의사항</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 프로그램의 코드가 DB 커넥션을 가지고 있는 범위와 트랜잭션이 활성화돼 있는 프로그램의 범위를 최소화해야 한다. 일반적으로 DB 커넥션 개수는 제한적이어서 각 단위 프로그램이 커넥션을 소유하는 시간이 길어질수록 사용 가능한 여유 커넥션 개수가 줄어든다. 이로 인해 각 단위 프로그램에서 커넥션을 가져가기 위해 기다리는 상황이 발생할 수 있다. 추가로 네트워크 작업이 있는 경우에도 트랜잭션에서 배제해야 한다. 이런 주의점을 지키지 않으면 DBMS 서버가 높은 부하 상태로 빠지거나 위험한 상태에 빠지는 경우가 빈번히 발생한다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>MySQL 엔진의 잠금</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MySQL에서 사용되는 잠금은 스토리지 레벨과 MySQL 엔진 레벨로 나뉜다. MySQL 엔진 레벨의 잠금은 모든 스토리지에 영향을 미친다. 그에 반해 스토리지 레벨의 락은 엔진 간 상호 영향을 미치지 않는다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>글로벌 락(Global Lock)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 글로벌 락은 FLUSH TABLES WITH READ LOCK 명령으로 획득할 수 있으며 범위가 MySQL 서버 전체로 MySQL에서 제공하는 락 중에 범위가 가장 크다. 따라서 한 세션에서 글로벌 락을 획득하면 다른 세선에서는 SELECT를 제외한 나머지 문장은 글로벌 락 해제 전까지 대기상태로 남는다. 여러 DB에 존재하는 MyISAM이나 MEMORY 테이블에 대해 mysqldump로 일관된 백업을 받아야 할 때 글로벌 락을 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; InnoDB는 트랜잭션을 지원하기에 글로벌 락처럼 일관된 데이터 상태를 위해 모든 작업을 멈출 필요가 없다. 따라서 좀 더 가벼운 락의 필요성이 생겼다. 그래서 MySQL 8.0부터 백업 툴들의 안정적인 실행을 위해 백업 락이 도입됐다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">LOCK&nbsp;INSTANCE&nbsp;FOR&nbsp;BACKUP;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;백얼&nbsp;실행</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">UNLOCK&nbsp;INSTANCE;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 특정 세션이 백업 락을 획득했다면 모든 세션은 테이블 스키마나 사용자 인증 관련 정보를 변경할 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - DB, table 등 모든 객체 생성 및 변경, 삭제</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - REPAIR TABLE과 OPTIMIZE TABLE 명령</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 사용자 관리 및 비밀번호 변경</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 일반적인 MySQL 서버는 소스 서버와 레플리카 서버로 구성된다. 주로 백업이 진행되는 레플리카 서버에서 글로벌 락을 획득하면 복제가 백업 시간만큼 지연된다. XtraBackup이나 Enterprise Backup 툴이 실행되는 도중 스키마 변경이 실행되면 백업은 실패한다. 백업 락은 이런 목적으로 도입됐으며, 정상적으로 복제는 실행되지만 백업의 실패를 막기 위해 DDL 명령이 실행되면 복제를 일시 중지하는 역할을 한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>테이블 락(Table Lock)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>개별 테이블 단위로 설정되는 잠금이다. 명시적으로는 "LOCK TABLES table_name [ READ | WRITE]" 명령으로 특정테이블의 락을 획득할 수 있다. UNLOCK TABLES 명령으로 잠금을 해제할 수 있다. 테이블 락은 글로벌 락과 동일하게 온라인 작업에 상당한 영향을 미치므로 명시적으로 사용할 필요는 거의 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 묵시적 테이블 락은 MyISAM, MEMORY 테이블에 데이터를 변경하는 쿼리를 실행하면 발생한다. MySQL 서버가 데이터가 변경되는 테이블에 잠금을 설정하고 데이터를 변경한 후, 즉시 잠금을 해제하는 형태다. InnoDB의 경우 레코드 기반 잠금을 제공한다. 따라서 대부분의 데이터 변경(DML) 쿼리에서는 테이블락이 설정되지 않고 스키마를 변경하는 쿼리(DDL)의 경우에만 설정된다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>네임드 락(Named Lock)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>GET_LOCK() 함수를 이용해 설정할 수 있다. 네임드 락은 DB 객체가 아닌 사용자가 지정한 문자열에 대해 락을 획득하고 반납한다. 네임드 락은 자주 사용되지 않지만 여러 클라이언트가 상호 동기화를 처리해야 하는 경우 네임드 락을 사용하면 편리하다. 예를 들어 DB 서버 1대에 5대의 웹 서버가 접속해 서비스할 때 웹 서버들이 어떤 정보를 동기화해야 하는 경우가 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 많은 레코드에 대해 복잡한 요건으로 레코드를 변경하는 트랜잭션에서도 유용하다. 배치 프로그램처럼 한꺼번에 많은 레코드를 변경하는 쿼리는 종종 데드락의 원인이 된다. 이 경우 동일 데이터를 변경하거나 참조하는 프로그램끼리 분류해 네임드 락을 걸로 쿼리를 실행하면 해결할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MySQL 8.0부터 네임드 락을 중첩해 상용하고 현제 세션에서 획득한 네임드 락을 한 번에 모두 해제하는 기능도 추가됐다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #7da123;">"mylock"</span>이라는&nbsp;문자열에&nbsp;대해&nbsp;네임드&nbsp;락&nbsp;설정</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;락을&nbsp;사용중이면&nbsp;2초간&nbsp;대기,&nbsp;대기&nbsp;후&nbsp;자동&nbsp;잠금&nbsp;해제</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;GET_LOCK(<span style="color: #7da123;">'mylock'</span>,&nbsp;<span style="color: #004fc8;">2</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;GET_LOCK(<span style="color: #7da123;">'mylock1'</span>,&nbsp;<span style="color: #004fc8;">2</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #7da123;">"mylock"</span>이라는&nbsp;문자열에&nbsp;대해&nbsp;잠금이&nbsp;설정돼&nbsp;있는지&nbsp;확인</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;IS_FREE_LOCK(<span style="color: #7da123;">'mylock'</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;<span style="color: #7da123;">"mylock"</span>이라는&nbsp;문자열에&nbsp;대해&nbsp;획득했던&nbsp;잠금을&nbsp;해제</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;RELEASE_LOCK(<span style="color: #7da123;">'mylock'</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;해당&nbsp;세션의&nbsp;모든&nbsp;네임드&nbsp;락을&nbsp;해제</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;RELEASE_ALL_LOCKS();</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>메타데이터 락(Metadata Lock)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 메타데이터 락은 DB 객체의 이름이나 구조를 변경하는 경우 획득하는 락이다. 묵시적으로만 획득할 수 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>InnoDB 스토리지 엔진 잠금</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; InnoDB는 MySQL에서 제공하는 락과는 별개로 자체적으로 레코드 기반 락을 제공한다. 이 때문에 MyISAM 보다 훨씬 뛰어난 동시성 처리를 제공한다. 하지만 이원화된 잠금 탓에 InnoDB 스토리지 엔진에서 사용되는 락에 대한 정보를 MySQL 명령을 통해 접근하기 어려웠다. lock_monitor(innodb_lock_monitor라는 이름의 InnoDB 테이블을 생성해 InnoDB의 잠금 정보를 덤프 하는 방법)와 SHOW ENGINE INNODB STATUS 명령이 존재하긴 했지만 거의 어셈블리 코드를 모는 것 같아서 이해하기 어려웠다.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">16</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">17</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">18</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">19</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">20</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">21</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">22</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">23</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">24</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">25</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">26</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">27</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">28</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">29</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">30</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">31</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">32</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">33</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">34</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">35</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">36</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">37</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">38</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">39</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">40</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">41</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">42</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">43</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">44</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">45</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">46</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">47</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">48</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">mysql<span style="color: #010101;"></span><span style="color: #0099cc;">&gt;</span>&nbsp;<span style="color: #ff3399;">SHOW</span>&nbsp;<span style="color: #ff3399;">ENGINE</span>&nbsp;INNODB&nbsp;STATUS\G</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span>&nbsp;<span style="color: #004fc8;">1.</span>&nbsp;row&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span><span style="color: #010101;"></span><span style="color: #0099cc;">*</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Type:&nbsp;InnoDB</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Name:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Status:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #004fc8;">2018</span><span style="color: #0099cc;">-</span><span style="color: #004fc8;">04</span><span style="color: #0099cc;">-</span><span style="color: #004fc8;">12</span>&nbsp;<span style="color: #004fc8;">15</span>:<span style="color: #004fc8;">14</span>:<span style="color: #004fc8;">08</span>&nbsp;<span style="color: #004fc8;">0x7f971c063700</span>&nbsp;INNODB&nbsp;MONITOR&nbsp;OUTPUT</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #010101;"></span><span style="color: #0099cc;">=</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Per&nbsp;second&nbsp;averages&nbsp;calculated&nbsp;<span style="color: #ff3399;">from</span>&nbsp;the&nbsp;last&nbsp;<span style="color: #004fc8;">4</span>&nbsp;seconds</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">-----------------</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BACKGROUND&nbsp;THREAD</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">-----------------</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">srv_master_thread&nbsp;loops:&nbsp;<span style="color: #004fc8;">15</span>&nbsp;srv_active,&nbsp;<span style="color: #004fc8;">0</span>&nbsp;srv_shutdown,&nbsp;<span style="color: #004fc8;">1122</span>&nbsp;srv_idle</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">srv_master_thread&nbsp;log&nbsp;flush&nbsp;and&nbsp;writes:&nbsp;<span style="color: #004fc8;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">----------</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">SEMAPHORES</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">----------</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">OS&nbsp;WAIT&nbsp;ARRAY&nbsp;INFO:&nbsp;reservation&nbsp;count&nbsp;<span style="color: #004fc8;">24</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">OS&nbsp;WAIT&nbsp;ARRAY&nbsp;INFO:&nbsp;signal&nbsp;count&nbsp;<span style="color: #004fc8;">24</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">RW<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>shared&nbsp;spins&nbsp;<span style="color: #004fc8;">4</span>,&nbsp;rounds&nbsp;<span style="color: #004fc8;">8</span>,&nbsp;OS&nbsp;waits&nbsp;<span style="color: #004fc8;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">RW<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>excl&nbsp;spins&nbsp;<span style="color: #004fc8;">2</span>,&nbsp;rounds&nbsp;<span style="color: #004fc8;">60</span>,&nbsp;OS&nbsp;waits&nbsp;<span style="color: #004fc8;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">RW<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>sx&nbsp;spins&nbsp;<span style="color: #004fc8;">0</span>,&nbsp;rounds&nbsp;<span style="color: #004fc8;">0</span>,&nbsp;OS&nbsp;waits&nbsp;<span style="color: #004fc8;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Spin&nbsp;rounds&nbsp;per&nbsp;wait:&nbsp;<span style="color: #004fc8;">2.</span><span style="color: #004fc8;">00</span>&nbsp;RW<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>shared,&nbsp;<span style="color: #004fc8;">30.</span><span style="color: #004fc8;">00</span>&nbsp;RW<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>excl,&nbsp;<span style="color: #004fc8;">0.</span><span style="color: #004fc8;">00</span>&nbsp;RW<span style="color: #010101;"></span><span style="color: #0099cc;">-</span>sx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">------------------------</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">LATEST&nbsp;<span style="color: #ff3399;">FOREIGN</span>&nbsp;<span style="color: #ff3399;">KEY</span>&nbsp;ERROR</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="color: #999999; font-family: 'Noto Serif KR';">------------------------</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #004fc8;">2018</span><span style="color: #0099cc;">-</span><span style="color: #004fc8;">04</span><span style="color: #0099cc;">-</span><span style="color: #004fc8;">12</span>&nbsp;<span style="color: #004fc8;">14</span>:<span style="color: #004fc8;">57</span>:<span style="color: #004fc8;">24</span>&nbsp;<span style="color: #004fc8;">0x7f97a9c91700</span>&nbsp;Transaction:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">TRANSACTION&nbsp;<span style="color: #004fc8;">7717</span>,&nbsp;ACTIVE&nbsp;<span style="color: #004fc8;">0</span>&nbsp;sec&nbsp;inserting</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">mysql&nbsp;<span style="color: #ff3399;">tables</span>&nbsp;in&nbsp;<span style="color: #ff3399;">use</span>&nbsp;<span style="color: #004fc8;">1</span>,&nbsp;locked&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #004fc8;">4</span>&nbsp;lock&nbsp;struct(s),&nbsp;heap&nbsp;size&nbsp;<span style="color: #004fc8;">1136</span>,&nbsp;<span style="color: #004fc8;">3</span>&nbsp;row&nbsp;lock(s),&nbsp;undo&nbsp;log&nbsp;entries&nbsp;<span style="color: #004fc8;">3</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">MySQL&nbsp;thread&nbsp;id&nbsp;<span style="color: #004fc8;">8</span>,&nbsp;OS&nbsp;thread&nbsp;handle&nbsp;<span style="color: #004fc8;">140289365317376</span>,&nbsp;query&nbsp;id&nbsp;<span style="color: #004fc8;">14</span>&nbsp;localhost&nbsp;root&nbsp;<span style="color: #ff3399;">update</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;child&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #ff3399;">NULL</span>,&nbsp;<span style="color: #004fc8;">1</span>),&nbsp;(<span style="color: #ff3399;">NULL</span>,&nbsp;<span style="color: #004fc8;">2</span>),&nbsp;(<span style="color: #ff3399;">NULL</span>,&nbsp;<span style="color: #004fc8;">3</span>),&nbsp;(<span style="color: #ff3399;">NULL</span>,&nbsp;<span style="color: #004fc8;">4</span>),&nbsp;(<span style="color: #ff3399;">NULL</span>,&nbsp;<span style="color: #004fc8;">5</span>),&nbsp;(<span style="color: #ff3399;">NULL</span>,&nbsp;<span style="color: #004fc8;">6</span>)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">Foreign</span>&nbsp;<span style="color: #ff3399;">key</span>&nbsp;<span style="color: #ff3399;">constraint</span>&nbsp;fails&nbsp;for&nbsp;<span style="color: #ff3399;">table</span>&nbsp;<span style="color: #7da123;">`test`</span>.<span style="color: #7da123;">`child`</span>:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #ff3399;">CONSTRAINT</span>&nbsp;<span style="color: #7da123;">`child_ibfk_1`</span>&nbsp;<span style="color: #ff3399;">FOREIGN</span>&nbsp;<span style="color: #ff3399;">KEY</span>&nbsp;(<span style="color: #7da123;">`parent_id`</span>)&nbsp;<span style="color: #ff3399;">REFERENCES</span>&nbsp;<span style="color: #7da123;">`parent`</span>&nbsp;(<span style="color: #7da123;">`id`</span>)&nbsp;<span style="color: #ff3399;">ON</span>&nbsp;<span style="color: #ff3399;">DELETE</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;<span style="color: #ff3399;">CASCADE</span>&nbsp;<span style="color: #ff3399;">ON</span>&nbsp;<span style="color: #ff3399;">UPDATE</span>&nbsp;<span style="color: #ff3399;">CASCADE</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Trying&nbsp;to&nbsp;<span style="color: #ff3399;">add</span>&nbsp;in&nbsp;child&nbsp;<span style="color: #ff3399;">table</span>,&nbsp;in&nbsp;index&nbsp;par_ind&nbsp;tuple:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">DATA&nbsp;TUPLE:&nbsp;<span style="color: #004fc8;">2</span>&nbsp;fields;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #004fc8;">0</span>:&nbsp;len&nbsp;<span style="color: #004fc8;">4</span>;&nbsp;hex&nbsp;<span style="color: #004fc8;">80000003</span>;&nbsp;asc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #004fc8;">1</span>:&nbsp;len&nbsp;<span style="color: #004fc8;">4</span>;&nbsp;hex&nbsp;<span style="color: #004fc8;">80000003</span>;&nbsp;asc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">But&nbsp;in&nbsp;parent&nbsp;<span style="color: #ff3399;">table</span>&nbsp;<span style="color: #7da123;">`test`</span>.<span style="color: #7da123;">`parent`</span>,&nbsp;in&nbsp;index&nbsp;<span style="color: #ff3399;">PRIMARY</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">the&nbsp;closest&nbsp;match&nbsp;we&nbsp;can&nbsp;find&nbsp;is&nbsp;record:</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">PHYSICAL&nbsp;RECORD:&nbsp;n_fields&nbsp;<span style="color: #004fc8;">3</span>;&nbsp;compact&nbsp;format;&nbsp;info&nbsp;bits&nbsp;<span style="color: #004fc8;">0</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #004fc8;">0</span>:&nbsp;len&nbsp;<span style="color: #004fc8;">4</span>;&nbsp;hex&nbsp;<span style="color: #004fc8;">80000004</span>;&nbsp;asc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #004fc8;">1</span>:&nbsp;len&nbsp;<span style="color: #004fc8;">6</span>;&nbsp;hex&nbsp;<span style="color: #004fc8;">000000001e19</span>;&nbsp;asc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;<span style="color: #004fc8;">2</span>:&nbsp;len&nbsp;<span style="color: #004fc8;">7</span>;&nbsp;hex&nbsp;<span style="color: #004fc8;">81000001110137</span>;&nbsp;asc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #004fc8;">7</span>;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">...</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하지만 최근 버전에서 InnoDB의 트랜잭션과 잠금, 잠금 대기 중인 트랜잭션의 목록을 조회할 수 있는 방법이 도입되었다. information_schema DB에 존재하는 INNODB_TRX, INNODB_LOKCS, INNODB_LOCK_WAITS라는 테이블을 조인해 조회하면 현재 잠금을 대기하고 있는 트랜잭션, 잠금을 가지고 있는 트랜잭션 조회와 장시간 잠금을 가지는 트랜잭션 종료를 할 수 있다. Performance Schema를 이용하면 InnoDB 스토리지 엔진 내부 잠금에 대한 모니터링을 할 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>InnoDB 스토리지 엔진의 잠금</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; InnoDB는 레코드 기반 락을 제고하고 락 정보가 상당히 작은 공간으로 관리된다. 일반 상용 DBMS와 다르게 InnoDB에는 레코드 사이를 잠그는 갭 락이 존재한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="564" data-origin-height="808"><span data-url="https://blog.kakaocdn.net/dn/JVr7B/btrVxNqPh7o/v5EwMI0Tl0qsephk0ARK01/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJVr7B%2FbtrVxNqPh7o%2Fv5EwMI0Tl0qsephk0ARK01%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="381" height="546" data-origin-width="564" data-origin-height="808"></span></figure>
<p></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>레코드 락(Record lock, Record only lock)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 레코드 자체만 잠그는 것을 의미한다. InnoDB의 경우 다른 DBMS와 다르게 인덱스의 레코드를 잠근다. 인덱스가 없더라도 클러스터 인덱스를 이용해 락을 설정한다. InnoDB는 보조 인덱스를 이용한 변경 작업은 넥스트 키 락 또는 갭 락을 사용하고 PK 또는 유니크 인덱스에 의한 변경 작업은 레코드 락을 사용한다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>갭 락(Gap lock)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>레코드와 바로 인접한 레코드 사이를 잠근다. 갭 락은 레코드와 레코드 사이의 간격에 레코드가 INSERT 되는 것을 제어한다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>넥스트 키 락(Next Key lock)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 레코드 락과 갭 락을 합친 것을 의미한다.&nbsp; innodb_locks_unsage_for_binlog 시스템 변수를 비활성화하면 변경을 위해 검색하는 레코드에 넥스트 키 락을 건다. InnoDB의 갭 락이나 넥스트 키 락은 바이너리 로그에 기록되는 쿼리가 레플리카 서버에서 실행될 때 소스 서버에서 만들어 낸 결과와 같은 결과를 만드는 것을 보장하는 게 주목적이다. 넥스트 키 락과 갭 락으로 인한 데드락이나 다른 트랜잭션을 기다리게 하는 일이 생각보다 자주 발생한다. 따라서 바이너리 로그 포맷을 ROW 형태로 바꿔서 넥스트 키 락이나 갭 락을 줄여야 한다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>자동 증가 락(Auto increment lock)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>MySQL은 자동 증가하는 숫자 값을 추출하기 위해 AUTO_INCREMENT라는 칼럼 속성을 제공한다. AUTO_INCREMENT를 사용하는 테이블에 여러 레코드가 동시에 INSERT 될 경, 저장되는 각 레코드는 순서대로 중복되지 않는 증가하는 번호를 가져야 한다. InnoDB는 이를 위해 내부적으로 AUTO_INCREMENT 락이라는 테이블 수준의 잠금을 사용한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; AUTO_INCREMENT 락은 INSERT, REPLACE 같은 레코드를 저장하는 쿼리에서만 필요하다. 또 한 트랜잭션과 관련 없이 AUTO_INCREMENT 값을 가져오는 순간만 락이 걸렸다 해제된다. AUTO_INCREMENT 락은 테이블에 하나만 존재하기 때문에 두 개의 INSERT 쿼리가 동시에 실행될 경우 하나의 쿼리가 AUTO_INCREMENT 락을 걸면 나머지 쿼리는 AUTO_INCREMENT 락을 기다려야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 자동 증가 락은 5.1부터 시스템 변수(innodb_autoinc_lock_mode)를 이용해 적용 방식을 선택할 수 있다. 위에서 설명한 적용 방식은 MySQL 5.0까지 적용된 방식이다. 자세한 설명은 <a href="https://dev.mysql.com/doc/refman/5.7/en/innodb-auto-increment-handling.html" target="_blank" rel="noopener">링크</a>를 보자.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>인덱스와 잠금</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 아래와 같은 쿼리가 있고 first_name 칼럼을 인덱싱 했다 하자.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">UPDATE</span>&nbsp;employees&nbsp;<span style="color: #ff3399;">SET</span>&nbsp;hire_date<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>NOW()&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;first_name<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #7da123;">'Georgi'</span>&nbsp;AND&nbsp;last_name<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #7da123;">'klassen'</span>;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp; &nbsp;&nbsp;</b>위 쿼리는 1 건의 업데이트를 하지만 first_name이 인덱스이기 때문에 그와 관련된 모든 레코드를 잠근다. 따라서 UPDATE 문장을 위한 적절한 인덱스가 준비돼 있지 않다면 각 클라이언트 간의 동시성이 떨어져서 산 세션에서 UPDATE 작업을 하는 중에는 다른 클라이언트는 그 테이블을 업데이트하지 못하고 기다리는 상황이 발생한다. 만약 인덱스가 안 걸려 있다면 풀테이블 스캔을 사용해 더 많은 레코드를 잠그게 된다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>레코드 수준의 잠금 확인 및 해제</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>MySQL 5.1부터 레코드 잠금과 잠금 대기에 대한 조회가 가능하다. 레코드 수준의 잠금을 확인하기 위해 다음과 같은 시나리오를 생각해 보자.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">16</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">17</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;connection&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;autocommit&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;<span style="color: #004fc8;">false</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">UPDATE</span>&nbsp;employee&nbsp;<span style="color: #ff3399;">SET</span>&nbsp;birth_date<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>NOW()&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;id<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #004fc8;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;connection&nbsp;<span style="color: #004fc8;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;autocommit&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;<span style="color: #004fc8;">false</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">UPDATE</span>&nbsp;employee&nbsp;<span style="color: #ff3399;">SET</span>&nbsp;hire_date<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>NOW()&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;id<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #004fc8;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;connection&nbsp;<span style="color: #004fc8;">3</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;autocommit<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #004fc8;">false</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">UPDATE</span>&nbsp;employee&nbsp;<span style="color: #ff3399;">SET</span>&nbsp;birth_date<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>NOW(),&nbsp;hire_date<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>NOW()&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;id<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #004fc8;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;connection&nbsp;<span style="color: #004fc8;">4</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SHOW</span>&nbsp;PROCESSLIST;</span></div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 시나리오에서 PROCESSLIST를 조회하면 UPDATE 명령이 실행된 프로세스들을 조회한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2614" data-origin-height="328"><span data-url="https://blog.kakaocdn.net/dn/ZEXXK/btrVzFsSdjy/L4zokgYEOyk9shKeu211kK/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZEXXK%2FbtrVzFsSdjy%2FL4zokgYEOyk9shKeu211kK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="948" height="119" data-origin-width="2614" data-origin-height="328"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 여기서 맨 처음 UPDATE 쿼리가 실행되고 COMMIT을 하지 않았으므로 이후에 실행된 UPDATE가 존재하는 6278, 6289번 스레드는 잠금 대기로 인해 UPDATE 명령을 실행 중이다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 performance_schema의 data_locks 테이블과 data_lock_waits 테이블을 조인해 잠금 대기 순서를 살펴보자.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;r.trx_id&nbsp;waiting_trx_id,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;r.trx_mysql_thread_id&nbsp;waiting_thread,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;r.trx_query&nbsp;waiting_queyr,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;innodb_trx.trx_id&nbsp;blocking_trx_id,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;innodb_trx.trx_mysql_thread_id&nbsp;blocking_thread,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;innodb_trx.trx_query&nbsp;blocking_query</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;performance_schema.data_lock_waits&nbsp;data_lock_waits</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">INNER&nbsp;JOIN&nbsp;information_schema.INNODB_TRX&nbsp;innodb_trx</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;">ON</span>&nbsp;innodb_trx.trx_id&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;data_lock_waits.blocking_engine_transaction_id</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">INNER&nbsp;JOIN&nbsp;information_schema.INNODB_TRX&nbsp;r</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;">ON</span>&nbsp;r.trx_id&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;data_lock_waits.requesting_engine_transaction_id;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="3128" data-origin-height="198"><span data-url="https://blog.kakaocdn.net/dn/Dx1V8/btrVxORx92I/98B32HmD45scIgPjIacgqk/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDx1V8%2FbtrVxORx92I%2F98B32HmD45scIgPjIacgqk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="3128" data-origin-height="198"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위에서 언급한 6278, 6279번 스레드가 대기 중 인 것을 알 수 있다. 또 한 blocking_thread column과 waiting_thread column을 통해 6278번 스레드는 6272번 스레드를 기다리고, 6279번 스레드는 6278번, 6272번 스레드를 기다리는 것을 볼 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이제 performance_shcema의 data_locks 테이블을 조회해 6272번 스레드가 어떤 락을 가지는지 확인해 보자.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;OBJECT_NAME,&nbsp;LOCK_TYPE,&nbsp;LOCK_MODE,&nbsp;LOCK_STATUS,&nbsp;<span style="color: #ff3399;">ENGINE</span>&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;performance_schema.data_locks;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1594" data-origin-height="248"><span data-url="https://blog.kakaocdn.net/dn/rVQmi/btrVv3hgDoa/USkL0ODC1xU0MAzSMr4Nok/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_6.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrVQmi%2FbtrVv3hgDoa%2FUSkL0ODC1xU0MAzSMr4Nok%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1594" data-origin-height="248"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 결과를 통해 employee 테이블이 IX 잠금(Interntional Exclusive)을 가지고 있고, employee 테이블의 특정 레코드에 대해 쓰기 잠금을 가지는 것을 알 수 있다. REC_NOT_GAP 표시가 있으므로 레코드 잠금은 갭 락이 포함되지 않은 것을 알 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 오랜 시간 잠금을 가지는 스레드가 있다면 다음과 같이 강제종료할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">kill&nbsp;<span style="color: #004fc8;">6272</span>;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>MySQL의 격리 수준(Isolation Level)</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션 격리 수준은 여러 트랜잭션이 동시에 처리될 때 특정 트랜잭션이 다른 트랜잭션에 변경하거나 조회하는 데이터를 볼 수 있게 허용할지를 결정한다. 격리 수준은 다음과 같이 총 4개가 존재한다.</span></p>
<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft">
<tbody>
<tr>
<td style="width: 25%; text-align: center;">&nbsp;</td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">DIRTY READ</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">NON-REPEATABLE READ</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">PHANTOM READ</span></td>
</tr>
<tr>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">READ UNCOMMITED</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">O</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">O</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">O</span></td>
</tr>
<tr>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">READ COMMITED</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">X</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">O</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">O</span></td>
</tr>
<tr>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">REPEATABLE READ</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">X</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">X</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">O(InnoDB는 발생하지 않음)</span></td>
</tr>
<tr>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">SERIALIZABLE</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">X</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">X</span></td>
<td style="width: 25%; text-align: center;"><span style="font-family: 'Noto Serif KR';">X</span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 이 4개의 격리 수준은 순서대로 뒤로 갈수록 각 트랜잭션 간의 데이터 격리 정도가 높아지지만 동시에 동시 처리 성능도 떨어진다. READ UNCOMMITTED는 일반적인 DB에서 거의 사용하지 않고, SERIALIZABLE 역시 동시성이 중요한 경우 거의 사용하지 않는다. MySQL은 REPEATABLE READ를 주로 사용한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>READ UNCOMMITED</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>각 트랜잭션의 변경 내용이 COMMIT이나 ROLLBACK 여부와 관련 없이 다른 트랜잭션에서 보인다.</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">14</span></div>
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">15</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;TRANSACTION&nbsp;ISOLATION&nbsp;LEVEL&nbsp;READ&nbsp;UNCOMMITTED&nbsp;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">CREATE</span>&nbsp;<span style="color: #ff3399;">TABLE</span>&nbsp;member&nbsp;(</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;id&nbsp;BIGINT&nbsp;<span style="color: #ff3399;">AUTO_INCREMENT</span>,</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;name&nbsp;<span style="color: #0099cc;">VARCHAR</span>(<span style="color: #004fc8;">255</span>),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #ff3399;">PRIMARY</span>&nbsp;<span style="color: #ff3399;">KEY</span>&nbsp;(id)</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;autocommit<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #004fc8;">false</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;member&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #004fc8;">1</span>,&nbsp;<span style="color: #7da123;">'name'</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;TRANSACTION&nbsp;ISOLATION&nbsp;LEVEL&nbsp;READ&nbsp;UNCOMMITTED&nbsp;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">*</span>&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;member</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="482" data-origin-height="120"><span data-url="https://blog.kakaocdn.net/dn/uB80h/btrVz9N3cKM/m1DPKkXKmUpaxlmKBtaCNk/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_7.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuB80h%2FbtrVz9N3cKM%2Fm1DPKkXKmUpaxlmKBtaCNk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="482" data-origin-height="120"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위와 같이 임의의 트랜잭션에서 처리한 작업이 commit 되지 않았음에도 다른 트랜잭션에서 볼 수 있는 현상을 DIRTY READ라 한다. 더티 리드는 데이터가 나타났다 사라지는 현상을 초래하기에 개발자와 사용자 모두를 혼란스럽게 만든다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>READ COMMITED</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;</b>오라클 DBMS에서 기본으로 사용되는 격리 수준이다. 온라인 서비스에서 가장 많이 선택되는 격리 수준이다. 이미의 트랜잭션에서 데이터를 변경했을 때 COMMIT 된 데이터만 다른 트랜잭션에서 조회할 수 있다.&nbsp; 이는 하나의 트랜잭션이 레코드 업데이트 쿼리를 날리고 커밋을 하지 않으면 다른 트랜잭션은 언두 영역에서 값을 조회하기 때문이다. 트랜잭션에서 업데이트 쿼리를 날리면 새로운 값은 테이블에 기록되고 이전 값은 언두 영역으로 백업된다.&nbsp;</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="703" data-origin-height="484"><span data-url="https://blog.kakaocdn.net/dn/pVrqK/btrVALmcYBC/6KN0jCftS8wcPPZvG05LVK/img.png" data-lightbox="lightbox"><img src="/img/2023-01-06-transaction-lock/img_8.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpVrqK%2FbtrVALmcYBC%2F6KN0jCftS8wcPPZvG05LVK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="703" data-origin-height="484"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 하지만 READ COMMITED에서도 NON_REPEATABLE READ라는 부정합 문제가 발생한다.&nbsp;</span></p>
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
<div style="line-height: 130%;"><span style="font-family: 'Noto Serif KR';">13</span></div>
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;TRANSACTION&nbsp;ISOLATION&nbsp;LEVEL&nbsp;READ&nbsp;COMMITTED&nbsp;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">*</span>&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;member&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;name<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #7da123;">'updatedName'</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SET</span>&nbsp;TRANSACTION&nbsp;ISOLATION&nbsp;LEVEL&nbsp;READ&nbsp;COMMITTED&nbsp;;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">UPDATE</span>&nbsp;member&nbsp;<span style="color: #ff3399;">SET</span>&nbsp;name<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #7da123;">'updatedName'</span>&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;id<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #004fc8;">1</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">COMMIT;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">*</span>&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;member&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;name<span style="color: #010101;"></span><span style="color: #0099cc;">=</span><span style="color: #7da123;">'updatedName'</span>;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 케이스에선 transaction1에서 한 번의 조회가 발생한 뒤 해당 트랜잭션이 끝나지 않은 상태에서 trasaction2에서 레코드를 업데이트하고 커밋을 했다. 이 때문에 transaction1에서 또 한 번의 조회가 발생하면 이전엔 없던 레코드를 조회하게 된다. 이는 하나의 트랜잭션에서 여러 번의 조회가 발생할 때 항상 같은 결과를 지녀야 한다는 REPEATABLE READ 정합성에 어긋난다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 트랜잭션 내에서 실행되는 SELECT 문과 트랜잭션 없이 실행되는 SELECT 문은 READ COMMITTED 격리 수준에선 별 차이가 없다. 하지만 REPEATABLE READ 격리 수준에선 기본적으로 SELECT 쿼리도 트랜잭션 범위 내에서만 작동한다. 따라서 트랜잭션을 시작하면 끝날 때까지 하나의 쿼리는 항상 같은 결과만 반환한다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>REPEATABLE READ</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; InnoDB가 디폴트로 사용하는 격리 수준이다. 바이너리 로그를 가진 MySQL 서버에서는 최도 REPEATABLE READ를 사용해야 한다. InnoDB 스토리지 엔진은 트랜잭션 롤백에 대비해 변경 전 레코드를 언두(undo) 공간에 백업하고 실제 레코드를 변경한다. 이 방식이 MVCC다. READ COMMITTED, REPEATABLE READ 모두 언두 영역에 백업된 데이터를 이용해 COMMIT 되기 이전 데이터를 보여준다. 하지만 언두 영역에 백업된 레코드 버전 중 어느 버전까지 사용하느냐의 차이가 존재한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 모든 InnoDB 트랜잭션은 고유한 트랜잭션 번호(순차적으로 증가)를 가진다. 언두 영역에 백업된 모든 레코드에는 이 트랜잭션 번호가 포함돼 있다. InnoDB는 이 데이터가 불필요하다고 판단될 때 주기적으로 삭제한다. REPEATABLE READ에선 MVCC 보장을 위해 가장 오래된 트랜잭션 번호보다 앞선 언두 영역 데이터를 삭제하지 않는다. 하지만 이를 가장 오래된 트랜잭션에 이전에 변경된 모든 언두 데이터가 필요하다는 의미로 받아들여선 안된다. 정확히는 특정 트랜잭션 번호의 구간 내에서 백업된 언두 데이터가 보존돼야 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 언두 영역엔 하나의 레코드에 대해 백업된 데이터가 얼마든지 한 개 이상 존재할 수 있다. 또 한 트랜잭션이 장시간 유지되면 언두 영역에 백업된 데이터가 커진다. 따라서 MySQL 서버 처리 성능 저하가 발생할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; REPEATABLE READ는 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다 안 보였다 하는 PHANTOM READ라는 문제가 발행한다.</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">*</span>&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;member&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;id&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;<span style="color: #004fc8;">1</span>&nbsp;FOR&nbsp;<span style="color: #ff3399;">UPDATE</span>;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">2</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">BEGIN;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">INSERT</span>&nbsp;<span style="color: #ff3399;">INTO</span>&nbsp;member&nbsp;<span style="color: #ff3399;">VALUES</span>&nbsp;(<span style="color: #004fc8;">2</span>,&nbsp;<span style="color: #7da123;">'name2'</span>);</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">COMMIT;</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">#&nbsp;transaction&nbsp;<span style="color: #004fc8;">1</span></span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">*</span>&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;member&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;id&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;<span style="color: #004fc8;">2</span>&nbsp;FOR&nbsp;<span style="color: #ff3399;">UPDATE</span>;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; SELECT... FOR UPDATE 쿼리는 SELECT 하는 레코드에 쓰기 잠금을 걸어야 하지만 언두 레코드는 락을 걸 수 없다. 이 때문에 언두 영역에서 데이터를 가져오는 대신 실제 레코드에서 값을 가져온다. SELECT ... LOCK IN SHARE MODE도 마찬가지다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>SERIALIZABLE</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>가장 단순하면서 동시에 가장 엄격한 격리 수준이다. 그만큼 동시 처리 성능이 떨어진다. SERIALIZABLE은 다른 격리 수준과 달리 읽기에서 조차 락을 건다. 그 때문에 PHANTOM READ가 발생하지 않는다. InnoDB의 경우 넥스트 키 락과 갭 락 덕분에 REPEATABLE READ에서도 PHANTOM READ가 발생하지 않는다(위 REPEATABLE READ에서 서술한 특수 경우 제외). 따라서 굳이 SERIALIZABLE을 사용할 필요 없다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - Real MySQL</span></p></div>