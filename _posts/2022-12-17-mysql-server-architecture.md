---
layout:       post
title:        "4.1 Mysql 엔진 아키텍처"
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

<div class="tt_article_useless_p_margin contents_style"><p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Mysql 서버는 Mysql 엔진과 스토리지 엔진으로 구분된다. 스토리지 엔진은 핸들러 API를 만족시키면 누구든지 스토리지 엔진을 구현해 MYSQL 서버에서 사용할 수 있다.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>4.1 Mysql 엔진 아키텍처</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">기본적인 Mysql 엔진 구조는 다음과 같다. Mysql 엔진 구조는 다른 DBMS 구조와 다르기 때문에 다른 DBMS에는 없는 이점을 가진다. 반대로 다른 DBMS에 없는 문제가 생기기도 한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="494" data-origin-height="372"><span data-url="https://blog.kakaocdn.net/dn/nyTtG/btrSM4O0lsN/LfAYuBfE92Yk4aI9q7nGs1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnyTtG%2FbtrSM4O0lsN%2FLfAYuBfE92Yk4aI9q7nGs1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="494" data-origin-height="372"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Mysql은 표준 SQL(ANSI SQL) 문법을 지원하기 때문에 표준 문법에 따라 작성된 쿼리가 다른 DBMS와 호환돼 실행될 수 있다. Mysql 엔진은 SQL 문장 분석과 최적화 등 역할을 한다. 실질적으로 데이터를 가져오는 역할은 스토리지 엔진이 전담한다. Mysql에서는 한 번에 여러 종류의 스토리지 엔진을 사용할 수 있다(ex - CREATE TABLE (...) ENGINE=INNODB;).</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>핸들러 API</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b> </b>Mysql 엔진의 쿼리 실행기에서 데이터를 I/O 할 때 이를 스토리지 엔진에 요청한다. 이 요청을 핸들러 요청이라 하고 여기에 사용되는 API가 핸들러 API다. 아래 쿼리문을 통해 지금까지 사용한 핸들러 API를 이용해 작업한 데이터 양을 확인할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SHOW</span>&nbsp;GLOBAL&nbsp;STATUS&nbsp;<span style="color: #ff3399;">LIKE</span>&nbsp;<span style="color: #7da123;">'Handler%'</span>;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="434" data-origin-height="435"><span data-url="https://blog.kakaocdn.net/dn/0Z1JT/btrSJW5e4Qo/ajZ3wFlBqxdYwcC9di5J2K/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0Z1JT%2FbtrSJW5e4Qo%2FajZ3wFlBqxdYwcC9di5J2K%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="434" data-origin-height="435"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Mysql 스레딩 구조</b></span></h3>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="484" data-origin-height="352"><span data-url="https://blog.kakaocdn.net/dn/dnAxDi/btrSKu1On72/1GYsQvEt03wiYK4WRkD0jK/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdnAxDi%2FbtrSKu1On72%2F1GYsQvEt03wiYK4WRkD0jK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="484" data-origin-height="352"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Mysql 서버는 스레드 기반이며 크게 포그라운드 스레드와 백그라운드 스레드로 나뉘어있다. Mysql 서버에서 실행 중인 스레드의 목록은 다음 쿼리를 통해 확인할 수 있다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;thread_id,&nbsp;name,&nbsp;type,&nbsp;processlist_user,&nbsp;processlist_host&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;performance_schema.threads&nbsp;<span style="color: #ff3399;">ORDER</span>&nbsp;<span style="color: #ff3399;">BY</span>&nbsp;type,&nbsp;thread_id;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1169" data-origin-height="904"><span data-url="https://blog.kakaocdn.net/dn/lheHL/btrSIrd489T/Gbjo7s2c2dILBOLITNkqYk/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_3.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlheHL%2FbtrSIrd489T%2FGbjo7s2c2dILBOLITNkqYk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1169" data-origin-height="904"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">위 스레드 중 thread/sql/one_connection 만이 실제 사용자의 요청을 처리하는 스레드다. 백그라운드 스레드 개수는 Mysql 설정에 따라 가변적이다. 동일 이름의 스레드가 여러 개 존재하는 것은 Mysql 서버 설정 내용으로 인해 스레드가 동일 작업을 병렬로 처리하는 경우다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>포그라운드 스레드(클라이언트 스레드, 사용자 스레드)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">포그라운드 스레드는 최소한 Mysql에 접속한 클라이언트 개수만큼 존재한다. 주로 클라이언트가 요청한 쿼리 문장을 처리한다. 커넥션이 종료되면 스레드는 스레드 캐시로 돌아간다. 이때, 스레드 캐시에서 대기 중인 스레드 수가 일정 개수 이상이면 스레드를 종료시킨다. 스레드 캐시에 유지할 수 있는 최대 스레드 개수는 thread_cache_size 시스템 변수로 설정할 수 있다.</span><br><span style="font-family: 'Noto Serif KR';">포그라운드 스레드는 데이터를 Mysql의 데이터 버퍼나 캐시에서 가져온다. 만약 여기에 데이터가 없다면 직접 디스크나 인덱스 파일로부터 데이터를 읽어온다. MyISAM 테이블은 디스크 쓰기도 포그라운드 스레드가 처리하지만 InnoDB 테이블은 이를 백그라운드 스레드가 처리한다. InnoDB 테이블 포그라운드 스레드는 데이터 버퍼, 캐시까지만 담당한다.</span></p>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>백그라운드 스레드</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">InnoDB는 다음과 같은 작업을 백그라운드로 처리한다.</span><br><span style="font-family: 'Noto Serif KR';">- Insert buffer를 병합하는 스레드 (thread/innodb/io_ibuf_thread)</span><br><span style="font-family: 'Noto Serif KR';">- 로그를 디스크로 기록하는 스레드 (thread/innodb/io_log_thread)</span><br><span style="font-family: 'Noto Serif KR';">- InnoDB 버퍼 풀의 데이터를 디스크에 기록하는 스레드 (thread/innodb/page_cleaner_thread)</span><br><span style="font-family: 'Noto Serif KR';">- 데이터를 버퍼로 읽어오는 스레드 (thread/innodb/io_read_thread)</span><br><span style="font-family: 'Noto Serif KR';">- 잠금이나 데드락을 모니터링하는 스레드</span><br><span style="font-family: 'Noto Serif KR';">위 스레드 중 쓰기 스레드(Write thread)가 가장 중요하다. 쓰기 스레드는 로그 스레드와 버퍼의 데이터를 디스크에 쓰는 작업을 한다. MySql 5.5부터 데이터 I/O를 담당하는 스레드 개수를 각각 설정할 수 있다. InnoDB에서 읽기 작업은 클라이언트 스레드에서 처리되기에 많은 읽기 스레스 드를 설정할 필요가 없다. 하지만 쓰기 스레드는 많은 작업을 백그라운드로 처리하기 때문에 내장 디스크를 사용할 때는 2~4 정도, <a href="https://cheershennah.tistory.com/168" target="_blank" rel="noopener">DAS나 SAN 같은</a> 스토리지 사용 시 가능한 충분히 설정하는 것이 좋다. I/O스레드 개수 설정은 각각 innodb_write_io_threads와 innodb_read_io_threads 시스템 변수로 설정할 수 있다.</span><br><span style="font-family: 'Noto Serif KR';">사용자 요청을 처리할 때 데이터의 쓰기 작업은 지연될 수 있지만 읽기는 지연될 수 없다. InnoDB를 포함한 일반적인 상용 DBMS는 쓰기를 버퍼링 해 일괄 처리한다. 반면, MyISAM은 사용자 스레드가 쓰기 작업까지 함께 처리한다. 이 때문에 InnoDB는 INSERT, UPDATE, DELETE로 인해 데이터가 변경되는 경우 데이터가 디스크의 데이터 파일로 저장될 때까지 기다리지 않아도 된다. 하지만 MyISAM에서 일반적인 쿼리는 쓰기 버퍼링 기능을 사용할 수 없다.</span><br><br></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>메모리 할당 및 사용 구조</b></span></h2>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="966" data-origin-height="603"><span data-url="https://blog.kakaocdn.net/dn/drrDLy/btrTCguAmHE/V1tnXltDTEORUWGnDxIB81/img.jpg" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_4.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdrrDLy%2FbtrTCguAmHE%2FV1tnXltDTEORUWGnDxIB81%2Fimg.jpg" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="966" data-origin-height="603"></span></figure>
<p></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">MySQL이 사용하는 메모리 공간은 글로벌 메모리 영역과 로컬 메모리 영역으로 나뉜다. 글로벌 메모리 영역은 MySQL 서버가 시작되면 할당된다. 이때, 요청된 메모리 공간이 한 번에 모두 할당되는지, 필요할 때마다 필요한 만큼을 할당해 주는지는 운영체제마다 다르다. MySQL이 사용하는 메모리 양을 측정하는 것은 쉽지 않으므로, 단순하게 MySQL의 시스템 변수로 설정해 둔 만큼 운영체제로부터 메모리를 할당받는다.</span><br><span style="font-family: 'Noto Serif KR';">글로벌 메모리 영역과 로컬 메모리 영역의 차이는 여러 스레드가 공유해서 사용하는지 여부에 따라 다르다.</span></p>
<h3 style="text-align: left;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>글로벌 메모리 영역</b></span></h3>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">글로벌 메모리 영역은 스레드 개수와 무관하게 하나의 메모리 공간만 할당된다. 두 개 이상의 메모리 공간을 할당받을 수도 있지만 이 역시 스레드 개수와 무관하다. 할당된 모든 공간은 모든 스레드에 의해 공유된다.</span></p>
<h3 style="text-align: left;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>로컬 메모리 영역</b></span></h3>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">MySQL 서버에 존재하는 클라이언트 스레드가 쿼리를 처리하는 데 사용하는 메모리 영역이다. 클라이언트 하나가 MySQL 서버에 접속하면 MySQL 서버는 클라이언트 커넥션으로부터의 요청을 처리하기 위해 스레드를 하나 할당한다. 여기서 클라이언트 스레드가 사용하는 메모리 공간이 로컬 메모리 영역이라 클라이언트 메모리 영역이라고도 한다. 또 한, 클라이언트와 MySQL 서버 간의 커넥션을 세션이라 하므로 세션 메모리 영역이라고도 한다.</span><br><span style="font-family: 'Noto Serif KR';">로컬 메모리 영역은 각 클라이언트 스레드 별로 할당되어 상호 독립적이다. 일반적으로 메모리 설정 시 글로벌 메모리 영역의 크기만 신청 쓰는데 최악의 경우 MySQL 서버가 메모리 부족으로 멈출 수도 있으므로 적절한 메모리 공간을 설정해야 한다. 로컬 메모리 영역은 각 쿼리의 용도별로 필요할 때만 공간이 할당된다. 따라서 로컬 메모리 공간은 커넥션이 열려 있는 동안 계속해서 할당된 상태로 남아있는 공간이 있고(커넥션 버퍼, 결과 버퍼) 쿼리를 실행하는 순간에만 할당했다가 헤제하는 공간(소트 버퍼, 조인 버퍼)이 있다.</span></p>
<h2 style="text-align: left;" data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>플러그인 스토리지 엔진 모델</b></span></h2>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">MySQL은 플러그인 모델이라는 독특한 모델을 사용한다. 그 때문에 스토리지 엔진뿐만 아니라 전문 검색 엔진을 위한 검색어 파서, 사용자 인증을 위한 Native Authentication 등을 모두 플러그인으로 제작할 수 있다. MySQL은 이미 수많은 스토리지 엔진을 가지고 있지만, 사용자 요구사항 만족을 위해 다른 스토리지 엔진을 개발하는 것도 가능하다.</span><br><span style="font-family: 'Noto Serif KR';">MySQL에서 쿼리가 실행되는 개략적인 과정은 다음과 같다.</span><br><br></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1618" data-origin-height="237"><span data-url="https://blog.kakaocdn.net/dn/bEvJLa/btrTDm9HgHC/fmMWiTgphkZZqCGGPbyB7K/img.jpg" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_5.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbEvJLa%2FbtrTDm9HgHC%2FfmMWiTgphkZZqCGGPbyB7K%2Fimg.jpg" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1618" data-origin-height="237"></span></figure>
<p></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이 과정에서 볼 수 있듯 마지막 Data I/O 부분만 스토리지 엔진에 의해 처리된다. 따라서 사용자가 새로운 스토리지 엔진을 만든다 해도 DBMS의 전체 기능이 아닌 일부분의 기능만 수행하는 엔진을 작성하게 된다.</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;위 과정에서 Data I/O과정은 대부분 1건의 레코드 단위로 처리된다.</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;MySQL을 사용하다 보면 핸들러라는 단어가 종종 등장한다. 프로그래밍 언어에서 어떤 기능을 호출하기 위해 그 기능에 매핑을 시켜주는 역할을 하는 객체를 핸들러라 한다. MySQL 서버에서는 MySQL 엔진이 스토리지 엔진을 조정하기 위해 핸들러를 사용한다. 따라서 MySQL 엔진이 각 스토리지 엔진에게 데이터 I/O 명령을 하기 위해선 반드시 핸들러를 통해야 한다. </span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;MySQL에서 다양한 스토리지 엔진을 사용하는 테이블에 대해 쿼리를 실행해도 MySQL의 처리 내용은 대부분 동일하다. 단순히 데이터 I/O 영역에만 차이가 존재한다. 또 한, GROUP BY나 ORDRE BY 등 복잡한 처리는 스토리지 엔진 영역이 아닌 MySQL 엔진의 쿼리 실행기에서 처리된다. Data I/O 방식에 따라서 작업 처리 방식이 얼마나 변하는지는 추후에 차차 설명하자. 여기서는 하나의 쿼리 작업이 여러 하위 작업으로 나뉘고, 각 하위 작업이 어느 영역에서 처리되는지 구분할 줄 하는 게 핵심이다.</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;이제 설치된 MySQL 서버에서 지원하는 스토리지 엔진 종류를 살펴보자.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="2128" data-origin-height="521"><span data-url="https://blog.kakaocdn.net/dn/xugqB/btrTEzgW6Qe/BqZjdhn6VYKqGZVkhQeiAK/img.jpg" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_6.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxugqB%2FbtrTEzgW6Qe%2FBqZjdhn6VYKqGZVkhQeiAK%2Fimg.jpg" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="2128" data-origin-height="521"></span></figure>
<p></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;위 Support Column에 표시될 수 있는 값은 다음과 같다.</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;- YES: MySQL 서버에 해당 스토리지 엔진이 포함돼 있고, 사용 가능으로 활성화된 상태</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;- DEFAULT: ‘YES’와 동일한 상태지만 필수 스토리지 엔진임을 의미한다(즉, 스토리지 엔진이 없으면 MySQL이 시작되지 않을 수도 있다)</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;- NO: 현재 MySQL 서버에 포함되지 않음을 의미한다.</span><br><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;- DISABLED: 현재 MySQL 서버에는 포함됐지만 파라미터에 의해 비활성화된 상태</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 만약 Support 항목에 NO인(MySQL 서버에 포함되지 않은) 스토리지 엔진을 사용하려면 MySQL 서버를 재 빌드해야 한다. 하지만 MySQL 서버가 포함하고 있는 엔진이라면 플러그인 형태로 빌드된 스토리지 엔진 라이브러리를 다운로드해 끼워 넣기만 하면 된다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 모든 플러그인 항목을 확인해보자.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SHOW</span>&nbsp;PLUGINS;</span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1920" data-origin-height="1792"><span data-url="https://blog.kakaocdn.net/dn/b9S621/btrTQQa8F2H/gAQs6dRKO56KgHG1N4zfl1/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_7.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb9S621%2FbtrTQQa8F2H%2FgAQs6dRKO56KgHG1N4zfl1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="1920" data-origin-height="1792"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">MySQL은 MySQL 서버 기능을 확장할 수 있게 플러그인 API가 매뉴얼에 공개돼 있다. 따라서 기존에 재공 하는 기능을 확장하거나 완전히 새로운 기능들을 구현할 수 있다.<a href="https://dev.mysql.com/doc/refman/8.0/en/server-plugins.html" target="_blank" rel="noopener"> MySQL 플러그인 매뉴얼</a></span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>컴포넌트</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MySQL 8.0부터는 플러그인 아키텍처 대신 컴포넌트 아키텍처를 지원한다. MySQL 서버의 플러그인은 다은과 같은 단점들을 가진다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 플러그인은 오직 MySQL 서버와 통신할 수 있고 플러그인끼리는 통신할 수 없다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 플러그인은 MySQL 서버의 변수나 함수를 직접 호출하기 때문에 안전하지 않다(캡슐화 안됨)</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 플러그인은 상호 의존 관계를 설정할 수 없어서 초기화가 어렵다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 컴포넌트를 설치하면 플러그인과 마찬가지로 새로운 시스템 변수를 설정해야 할 수도 있다. MySQL 서버에서 기본으로 제공되는 컴포넌트에 대한 설명은 <a href="https://dev.mysql.com/doc/refman/8.0/en/components.html" target="_blank" rel="noopener">MySQL 컴포넌트 매뉴얼</a>을 참고하자.</span></p>
<h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>쿼리 실행 구조</b></span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 쿼리 실행 과정을 간략화하면 다음과 같다. 아래 과정에서 각 부분은 다음과 같은 역할을 한다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1118" data-origin-height="728"><span data-url="https://blog.kakaocdn.net/dn/eN0Cl5/btrTPhg23WX/tdEJfRMXtrp9EcT90xkX21/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_8.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeN0Cl5%2FbtrTPhg23WX%2FtdEJfRMXtrp9EcT90xkX21%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="677" height="441" data-origin-width="1118" data-origin-height="728"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';">&nbsp;<b>쿼리 파서</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>사용자 요청으로 들어온 쿼리 문장을 토큰(MySQL이 인식할 수 있는 최소 단위의 어휘나 기호)으로 분리해 트리 형태의 구조로 만들어 내는 작업이다. 쿼리 문장의 문법적 오류가 발견되면 사용자에게 오류 메시지를 전달한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 예를 들어 다음과 같은 SQL 문은</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';"><span style="color: #ff3399;">SELECT</span>&nbsp;id,&nbsp;name&nbsp;<span style="color: #ff3399;">FROM</span>&nbsp;t_user&nbsp;<span style="color: #ff3399;">WHERE</span>&nbsp;status&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">=</span>&nbsp;<span style="color: #7da123;">'ACTIVE'</span>&nbsp;AND&nbsp;age&nbsp;<span style="color: #010101;"></span><span style="color: #0099cc;">&gt;</span>&nbsp;<span style="color: #004fc8;">18</span></span></div>
</div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 쿼리 파서에서 파싱을 거치면 다음과 같은 트리 구조가 된다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="1169" data-origin-height="827"><span data-url="https://blog.kakaocdn.net/dn/t0G2U/btrTMZ2fU9y/7KmmV0904l5QkEtRRESuH0/img.png" data-lightbox="lightbox"><img src="/img/2022-12-17-mysql-server-architecture/img_9.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft0G2U%2FbtrTMZ2fU9y%2F7KmmV0904l5QkEtRRESuH0%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="709" height="502" data-origin-width="1169" data-origin-height="827"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>전처리기</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 파서 과정에서 만들어진 파서 트리를 기반으로 쿼리 문장에 구조적인 문제점이 있는지 확인한다. 각 토큰을 테이블 이름, 칼럼 이름, 내장 함수 같은 개체를 매핑해 객체의 존재 여부와 접근 권한 등을 확인한다. 존재하지 않거나 권한상 사용할 수 없는 개체의 토큰을 거른다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>옵티마이저</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 사용자의 요청으로 들어온 쿼리 문장을 저렴한 비용으로 가장 빠르게 처리할지를 결정한다. DBMS의 두뇌에 해당한다.&nbsp;</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>실행 엔진</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 실행 엔진은 만들어진 계획대로 각 핸들러에게 요청해서 받은 결과를 또 다른 핸들러 요청의 입력으로 연결하는 역할을 한다. 예를 들어 옵티마이저가 GROUP BY를 처리하기 위해 임시 테이블을 만드는 과정은 다음과 같다</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 1. 실행 엔진이 핸들러에게 임시 테이블을 만들라고 요청</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 2. 다시 실행 엔진은 WHERE 절에 일치하는 레코드를 읽어오라고 핸들러에게 요청</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 3. 읽어온 레코드들을 1번에서 준비한 임시 테이블로 저장하라고 핸들러에게 요청</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 4. 데이터가 준비된 임시 테이블에서 필요한 방식으로 데이터를 읽어오라고 핸들러에게 다시 요청</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 5. 최종적으로 실행 엔진은 결과를 사용자나 다른 모듈로 넘김</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>핸들러(스토리지 엔진)</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>핸들러는 MySQL 서버의 가장 밑단에서 MySQL 실행 엔진 요청에 따라 데이터를 디스크에 I/O 하는 역할을 한다. 따라서 핸들러는 결국 스토리지 엔진이다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>쿼리 캐시</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 쿼리 캐시는 SQL 실행 결과를 캐싱해 동일 쿼리가 실행되면 테이블을 읽지 않고 즉시 결과를 반환하기 때문에 성능이 좋다. 하지만, 원본이 변경되면 그에 대응하는 캐싱 데이터를 삭제(Invalidate) 하기 때문에 심각한 동시 처리 성능 저하를 유발한다. 또 한, MySQL 서버가 발전하면서 성능이 개선되는 과정에서 쿼리 캐시는 동시 처리 성능 저하, 버그의 원인이 되었다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 같은 이유 때문에 MySQL 8.0부터 쿼리 캐시 기능을 지원하지 않는다.&nbsp;</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>스레드 풀</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MySQL 서버 엔터프라이즈는 스레드 풀을 제공하지만 커뮤니티 에디션은 지원하지 않는다. 따라서 엔터프라이즈 버전의 스레드 풀이 아닌 Percona Server에서 제공하는 스레드 풀을 살펴보자.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Percona Server의 스레드 풀은 플러그인 형태로 작동한다. 따라서 커뮤 니버전에서 동일 버전의 Percona Server에서 스레드 풀 플러그인 라이브러리(thread_pool.so)를 설치해서 스레드 풀을 사용할 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스레드 풀의 목적은 사용자의 요청을 처리하는 스레드 개수를 줄여서 MySQL 서버의 CPU가 제한된 개수의 스레드 처리에만 집중할 수 있게 해서 서버의 자원 소모를 줄이는 대에 있다. 하지만 단순히 스레드 풀을 설치하는 것만으로는 큰 성능 향상을 기대하기 어렵다. 스레드 풀은 앞에서 말했듯 동시에 실행 중인 스레드들을 CPU가 최대한 잘 처리해낼 수 있는 수준으로 줄여서 빨리 처리하게 하는 것이 목표다. 여기서 만약 스케줄링 과정에서 CPU 시간을 올바르게 확보하지 못하면 쿼릴 처리가 더 느려지는 사례가 발생한다. 물론 적절한 수의 스레드로 CPU가 사용자 요청을 처리한다면 프로세서 친화도(Processor affinity)를 놓이고 불필요한 콘텍스트 스위치를 줄일 수 있다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Persona Server의 스레드 풀은 기본적으로 CPU 코어의 개수만큼 스레드 그룹을 생성한다. 스레드 그룹의 개수는 thread_pool_size 시스템 변수를 변경해 조정할 수 있다. 일반적으로 CPU 코어 개수와 맞추는 것이 CPU 프로세스 친화도를 높이는 데 좋다. MySQL 서버가 처리해야 할 요청이 생기면 스레드 풀로 처리를&nbsp;이관한다. 만약 이미 스레드 풀에서 처리 중인 작업이 있다면 thread_pool_oversubscribe 시스템 변수(deafult 3)에 설정된 개수만큼 추가로 더 받아 처리한다. 이 값이 너무 크면 스케줄링해야 할 스레드가 많아져서 스레드 풀이 비효율적으로 동작한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 스레드 그룹의 모든 스레드가 일을 처리하고 있다면 스레드 풀을 해당 스레드 그룹에 새로운 워커 스레드를 추가할지 결정해야 한다. 스레드 풀의 타이머 스레드는 주기적으로 스레드 그룹의 상태를 체크해서 thread_pool_stall_limit 시스템 변수에 정의된 밀리초만큼 작업 스레드가 작업을 끝내지 못하면 새로운 스레드를 생성해 스레드 그룹에 추가한다. 이때, 스레드 풀에 있는 전체 스레드 개수는 thread_pool_max_threads 시스템 변수에 설정된 개수를 넘어설 수 없다.&nbsp;</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Percona Server의 스레드 풀은 선순위 큐와 후순위 큐를 이용해 특정 트랜잭션이나 쿼리를 우선적으로 처리할 수 있는 기능도 제공한다. 이를 통해 시작된 트랜잭션 내에 속한 SQL을 빨리 처리해 해당 트랜잭션이 가지고 있던 락을 빨리 해제해 락 경합을 낮춰서 전체적인 처리 성능을 향상할 수 있다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>트랜잭션 지원 메타데이터</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><b>&nbsp;&nbsp;</b>데이터베이스 서버에서 테이블 구조 정보와 스토어드 프로그맨 등의 정보를 데이터 딕셔너리 또는 메타데이터라 한다. MySQL 서버는 5.7까지 테이블 구조를 FRM 파일에 저장하고 일부 스토어드 프로그램 역시 파일 기반으로 관리한다. 그 때문에 메타데이터 생성, 변경 작업이 트랜잭션을 지원하지 않아 테이블 생성 또는 변경 도중 MySQL 서버가 비정상 종료되면 일관되지 않는 상태로 남는 문제가 있었다. 이를 흔히 '데이터베이스나 테이블이 깨졌다'라고 한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 위 문제를 해결하기 위해 MySQL 8.0부터는 테이블 구조 정보, 스토어드 프로그램의 코드 관련 정보를 모두 InnoDB의 테이블에 저장한다. MySQL 서버가 장동하는 데 필요한 테이블들을 묶어서 시스템 테이블이라 한다. 시스템 테이블과 딕셔너리 정보는 모두 mysql DB에 저장하고 있다. mysql DB는 통쨰로 mysql.ibd라는 이름의 테이블스페이스에 저장된다. 이로 인해 스키마 변경 작업 중에 MySQL 서버가 비정상적으로 종료돼도 원자성을 보장한다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; MySQL 서버에서 InnoDB를 제외한 다른 스토리지 엔진의 메타 정보는 여전히 저장할 공간이 필요하다. 이를 위해 MySQL은 SDI(Serialized Dictionary Information, *. sdi) 파일을 사용한다. 이 파일들은 기존의 *. RFM 파일과 동일한 역할을 한다. SDI는 직렬화를 위한 포맷이므로 InnoDB 테이블 구조도 SDI 파일로 변환할 수 있다. ibd2 sdi 유틸리티를 사용하면 InnoDB 테이블스페이스에서 스키마 정보를 추출할 수 있다.</span></p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">출처 - Real MySQL 1</span></p></div>