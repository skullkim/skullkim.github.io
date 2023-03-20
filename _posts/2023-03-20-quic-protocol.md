<div class="tt_article_useless_p_margin contents_style"><h2 data-ke-size="size26"><span style="font-family: 'Noto Serif KR';">TCP</span></h2>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; TCP는 패킷 스위칭을 하는 컴퓨터 커뮤니케이션 네트워크 호스트들 간에 고신뢰성 프로토콜로 사용하기 위해 1970년대에 고안되었습니다. TCP는 HTTP와 같은 application layer protocol들의 기반으로 사용되고 있으며, 현재는 암호화된 데이터를 송수신하기 위해 때로는TLS도 같이 사용하고 있습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; TCP는 개발된 직후 부터 현재까지 직간접적으로 많은 사용자 애플리케이션이 사용하고 있는 프로토콜이며 리눅스에 기본으로 내장되어 있습니다. 하지만 TCP가 개발된 후로 현재까지 네트워크 환경에는 많은 변화들이 있었습니다. 완벽한 프로그램이 없는 이유는 기술이 발전하고 환경이 바뀌면서 기존 기술들이 호평받던 이유가 더 이상 통하지 않기 때문입니다. TCP 통신을 위해 사용하는 일부 기술 역시 시간의 흐름에 따라 현대 네트워크 환경에선 최선이라 불릴 수 없게 되었습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 물론, TCP가 시대 흐름을 쫓기지 않으려 한 것은 아닙니다, 구글이 QUIC 프로토콜을 출시하는 대신 TCP 개선을 고려하지 않은 것도 아닙니다. 그러나, 현재 TCP를 사용하고 있는 디바이스들은 전 세계 곳곳에 흩어져 있고 각기 다른 버전을 사용하고 있습니다. 따라서 새로운 기술을 TCP에 적용해 새로운 버전을 만든다면, 해당 버전을 대부분의 디바이스들이 지원하기까지 수년에서 십수 년이 소요됩니다. 그래서 구글은 TCP를 개선하는 대신 현대 네트워크 환경에 맞는 QUIC 프로토콜을 개발했습니다.</span></p>
<h2 style="text-align: left;" data-ke-size="size26"><span style="font-family: 'Noto Serif KR';"><b>QUIC(Quick UDP Internet Connections) Protoocl</b></span></h2>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC의 탄생 배경을 좀 더 이해하기 위해 우선 현대 인터넷 환경을 살펴보겠습니다. 1990년대 인터넷 환경에서 하나의 웹 페이지는 정적이고 용량이 크지 않았습니다. 웹 페이지 하나는 하나의 리소스만 포함하고 있었습니다. 그러나 2010년대 이후 웹이 빠르게 성장하면서 한 페이를 나타내기 위해 필요한 용량과 리소스가 비약적으로 증가했습니다. 또 한, 사람들은 더 이상 한 곳에 앉아 인터넷을 사용하지 않고 모바일 기기들을 이용해 이곳저곳을 돌아다니며 인터넷을 사용하고 있습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC은 이런 인터넷 환경에서 TCP를 대체할 목적으로 구글이 설계한 connection-oriented transport 프로토콜입니다. QUIC은 모던 웹 애플리케이션에서 경험할 수 있는 여러 문제점들을 개선했지만 개발 프로세스 상에서 차이는 거의 없습니다. QUIC은 TCP + TLS + HTTP2의 조합과 비슷하지만 UDP를 기반으로 동작합니다. 따라서 QUIC을 사용하면 엔드포인트끼리는 UDP datagram을 교환합니다. 이 UDP datagram은 QUIC 패킷을 포함합니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; TCP + TLS + HTTP2 조합과 비교했을 때 QUIC의 장점은 다음과 같습니다.</span></p>
<h3 style="text-align: left;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>QUIC vs TCP</b></span></h3>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>커넥션 연결 지연 감소</b><b></b></span></h4>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">QUIC은 핸드셰이크 과정에서 0번의 roundtrip이 필요합니다. 이는 TCP+TLS가 1~3번의 roundtrip이 필요한 것과 대조적입니다. QUIC을 사용하는 클라이언트는 처음 서버에 커넥션을 요청할 때 한 번의 roundtrip handshake를 실행합니다. 이 과정은 다음과 같습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 클라이언트가 비어있는 client hello(CHLO)를 보냅니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 서버는 source address token과 서버의 인증서를 포함한 클라이언트가 다음 과정 진행에 필요한 정보를 rejection(REJ)와 함께 응답합니다. 다음부터는 이전 커넥션에서 얻은 캐싱된 CHLO를 사용하기에 바로 암호화된 요청을 보낼 수 있습니다.</span></p>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>혼잡제어 개선</b><b></b></span></h4>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">QUIC의 혼잡 제어는 TCP의 혼잡제어 보다 더 많은 정보를 혼잡 제어 알고리즘에 제공합니다. 구글은 TCP cubic을 재구현해 적용하고 있습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">TCP cubic은 TCP에서 혼잡 재어를 위해 나온 기법입니다. 전통적인 혼잡제어 방식인 Tahoe&amp;Reno는 혼자 윈도우 사이즈가 선형적으로 증가하기 때문에, 현대의 넓은 밴드폭에서 적절한 밴드폭 사용량을 발견하기까지 오랜 시간을 소모한다는 문제를 가지고 있습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Cubic은 이 문제를 해결하기 위해 3차 함수(f(x)=x^3)를 사용합니다. 아래의 3차 함수 그래프를 보면 x가 낮을수록 함수 기울기는 커지고, 변곡점에 접근할수록 기울기가 완만해집니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="278" data-origin-height="448"><span data-url="https://blog.kakaocdn.net/dn/cXWJp0/btr42Tooirn/o2zy5dcpT7IAHev0eoKix1/img.png" data-lightbox="lightbox"><img src="/img/2023-03-20-quic-protocol/img.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcXWJp0%2Fbtr42Tooirn%2Fo2zy5dcpT7IAHev0eoKix1%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" data-origin-width="278" data-origin-height="448"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">이런 특성을 혼잡제어 알고리즘에 다음과 같이 사용할 수 있습니다. 패킷 drop이 발생했을 때의 혼잡 윈도우 크기를 변곡점으로 잡는다. 패킷 drop이 발생할 때마다 이 변곡점을 마지막에 발생한 패킷 drop에 대응되는 윈도우 크기로 잡는다. 이런 방식을 사용하면 다음과 같이 윈도우를 사용하게 됩니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 시작 시 혼잡 윈도우 크기를 빠르게 키울 수 있습니다.</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 변곡점에 다가갈수록 윈도우 증가 폭이 완만해집니다</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 변곡점에 도달했음에도 packet drop이 발생하지 않았다면, 다시 윈도우 크기가 빠르게 증가합니다.</span></p>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>head-of-line-blocking</b><b>이 없는 멀티플렉싱</b><b></b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp;head-of-line-blocking은 HTTP2가 가지고 있는 문제 중 하나입니다. HTTP2를 사용하는 애플리케이션은 TCP 커넥션을 하나의 바이트 스트림으로 바라봅니다. 이때, 패킷이 유실되면 HTTP2 커넥션을 맺은 스트림들은 해당 패킷이 재전송될 때까지 커넥션을 지속할 수 없습니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 그에 반해 QUIC은 처음부터 멀티플렉싱을 염두에 두고 설계되었기 때문에 패킷 손실이 발생해도 이에 대한 영향이 해당 스트림에만 국한됩니다. 각 스트림에 있는 프레임은 도착 즉시 해당 스트림을 통해 전송되므로 손실 없이 프레임들을 다시 합치고 애플리케이션은 다음 동작을 수행할 수 있습니다. 만약 허용 범위 내에서 그룹의 패킷이 손실되었다면, FEC 패킷 내의 정보로 손실된 패킷을 복구할 수 있습니다.</span></p>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>FEC(Forward Error Correction)</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; 패킷 손실이 발생했을 때 패킷의 재전송 없이 패킷을 복구하기 위해서, QUIC은 FEC 패킷으로 패킷 그룹을 보완할 수 있습니다. FEC 패킷에는 FEC 그룹에 있는 패킷의 parity가 포함됩니다.</span></p>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>connection migration</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC 커넥션은 64-bit 커넥션 id로 식별됩니다. 이 id는 클라이언트에 의해 랜덤 하게 생성됩니다. 그에 반해 TCP 커넥션은 source address, source port, desination address, destination port로 식별됩니다. 따라서 TCP 커넥션을 유지하는 중 클라이언트의 IP나 PORT가 바뀐다면 해당 TCP 커넥션은 더 이상 유효하지 않게 됩니다. 반면 QUIC은 클라이언트의 IP가 바뀌더라도 요청을 멈출 필요 없이 새로운 IP에서 이전에 연결한 커넥션 ID를 사용할 수 있습니다.</span></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>QUIC packet</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC은 packet의 기밀성과 무결성에 대한 책임을 가지고 있습니다. 이를 위해 QUIC은 TLS handshake에서 파생된 키를 사용합니다. TLS handshake와 alter message들은 QUIC transport 위에 존재합니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="968" data-origin-height="438"><span data-url="https://blog.kakaocdn.net/dn/89pye/btr42yxK6ub/kgO0kzNv9KkP5hrscz5YjK/img.png" data-lightbox="lightbox"><img src="/img/2023-03-20-quic-protocol/img_1.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F89pye%2Fbtr42yxK6ub%2FkgO0kzNv9KkP5hrscz5YjK%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="650" height="294" data-origin-width="968" data-origin-height="438"></span></figure>
<p></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC은 버전에 따라 하나의 UDP datagram은 여러 개의 QUIC 패킷을 가질 수 있습니다. 여기선 버전에 상관없이 공통으로 들어가는 datagram 첫 패킷만 소개합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC은 두 종류의 패킷 헤더를 가지고 있습니다. 각각 long header, short header입니다. long header를 가진 패킷이라면 MSB(Most Significant Bit-Long Header Packet의 첫 요소인 Header Form)가 1입니다.</span></p>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Long Header</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Long Header 구조는 다음과 같습니다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Long&nbsp;Header&nbsp;Packet&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Header&nbsp;Form&nbsp;(1bit,&nbsp;값은&nbsp;1로&nbsp;고정),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Version-Specific&nbsp;Bits&nbsp;(7&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Version&nbsp;(32&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Destination&nbsp;Connection&nbsp;ID&nbsp;Length&nbsp;(8&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Destination&nbsp;Connection&nbsp;ID&nbsp;(0&nbsp;~&nbsp;2040&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Source&nbsp;Connection&nbsp;ID&nbsp;Length&nbsp;(8&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Source&nbsp;Connection&nbsp;ID&nbsp;(0&nbsp;~&nbsp;2040&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Version-Specific&nbsp;Data&nbsp;(정해진&nbsp;길이가&nbsp;없습니다),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
<p data-ke-size="size16">&nbsp;</p>
</div>
<h4 data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Short Header</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Short Header 구조는 다음과 같습니다</span></p>
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
</div>
</td>
<td style="padding: 6px 0; text-align: left;">
<div style="margin: 0; padding: 0; color: #010101; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height: 130%;">
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Short&nbsp;Header&nbsp;Packet&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Header&nbsp;Form&nbsp;(1&nbsp;bit,&nbsp;값은&nbsp;0으로&nbsp;고정),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Version-Specific&nbsp;Bits&nbsp;(7&nbsp;bit),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Destination&nbsp;Connection&nbsp;ID&nbsp;(정해진&nbsp;길이가&nbsp;없습니다),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Version-Specific&nbsp;Data&nbsp;(정해진&nbsp;길이가&nbsp;없습니다),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Connection ID</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Connection ID의 기본적인 기능은 IP, UDP 등 하위 프로토콜에서 주소가 바뀌더라도 QUIC conenction이 잘못된 엔드포인트와 연결되는 것을 막기 위함입니다. Connection ID는 엔드포인트와 QUIC packet이 올바른 엔드포인트로 전송되는 것을 도와주는 중간 매개체에 가 사용합니다. 엔드포인트는 connection ID를 패킷이 의도된 QUIC connection을 식별하는 데 사용합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Connection ID는 각 엔드 포인트에서 versino-specific method를 사용해 선택합니다. 같은 QUIC 커넥션을 사용하는 패킷들은 서로 다른 Connection ID 값을 사용해야 합니다.</span></p>
<h4 style="text-align: left;" data-ke-size="size20"><span style="font-family: 'Noto Serif KR';"><b>Version Negotitation</b></span></h4>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">version field는 4-byte 식별자로 이루어져 있습니다. 이 값은 엔드 포인트가 QUIC 버전을 식별하는 데 사용합니다. 만약 버전 필드 값이 0x00000000이라면 다신 버전 협상에 돌입합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">Version Negotiation 패킷은 첫 비트를 high(1)로 둡니다. 따라서 패킷의 형식은 Long header packet과 동일합니다. 패킷이 Version Negotitation packet인지는 Version field로 식별할 수 있습니다. Version Negotiation packet의 version field 값은 0x00000000입니다.</span></p>
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
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">Version&nbsp;Negotiation&nbsp;Packet&nbsp;{</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Header&nbsp;Form&nbsp;(1&nbsp;bits,&nbsp;1로&nbsp;고정),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Unused&nbsp;(7&nbsp;bits),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Version&nbsp;(0으로&nbsp;고정),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Destination&nbsp;Connection&nbsp;ID&nbsp;Length&nbsp;(8bits),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Destination&nbsp;Connection&nbsp;ID&nbsp;(0&nbsp;~&nbsp;2040&nbsp;bits),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Source&nbsp;Connection&nbsp;ID&nbsp;Length&nbsp;(8&nbsp;bits),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Source&nbsp;Connection&nbsp;ID&nbsp;(0&nbsp;~&nbsp;2040&nbsp;bits),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">&nbsp;&nbsp;Supported&nbsp;Version&nbsp;(32&nbsp;bits,&nbsp;지원하는&nbsp;버전&nbsp;리스트),</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;"><span style="font-family: 'Noto Serif KR';">}</span></div>
<div style="padding: 0 6px; white-space: pre; line-height: 130%;">&nbsp;</div>
</div>
<div style="text-align: right; margin-top: -13px; margin-right: 5px; font-size: 9px; font-style: italic;"><span style="font-family: 'Noto Serif KR';"><a style="color: #e5e5e5text-decoration:none;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener">Colored by Color Scripter</a></span></div>
</td>
<td style="vertical-align: bottom; padding: 0 2px 4px 0;"><span style="font-family: 'Noto Serif KR';"><a style="text-decoration: none; color: white;" href="http://colorscripter.com/info#e" target="_blank" rel="noopener"><span style="font-size: 9px; word-break: normal; background-color: #e5e5e5; color: white; border-radius: 10px; padding: 1px;">cs</span></a></span></td>
</tr>
</tbody>
</table>
</div>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; Version Negotiation 패킷을 받은 엔드포인트는 다음 패킷부터 사용할 QUIC 버전을 바꿔야 합니다.</span></p>
<h3 style="text-align: left;" data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>Using TLS to secure QUIC</b></span></h3>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; QUIC은 보안을 위해 TLS1.3을 사용합니다. TLS 1.3은 이전 버전에 비해 레이턴시를 개선했습니다. TLS에서는 단일 round trip으로 커넥션을 생성하고 암호화를 진행할 수 있습니다. 새로운 커넥션이 생성된 후, 다음 커넥션부터는 클라이언트가 곧바로 애플리케이션 데이터를 송신할 수 있습니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">TLS는 QUIC을 위해 두 가지 핸드셰이크 모드를 제공합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - full 1-RTT handshake: 한 번의 roundtrip이후 클라이언트가 애플리케이션 데이터를 보낼 수 있습니다. 그러면 서버는 클라이언트로부터 첫 핸드셰이크 메시지를 받은 후 곧바로 응답을 합니다.</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; - 0-RTT handshake: 이전세션에서 서버에 대해 얻은 정보를 클라이언트가 사용하는 방식입니다. 서버 정보를 알기 때문에 바로 애플리케이션 데이터를 송신할 수 있습니다.</span></p>
<p></p><figure class="imageblock alignCenter" data-ke-mobilestyle="widthOrigin" data-origin-width="742" data-origin-height="642"><span data-url="https://blog.kakaocdn.net/dn/cDadpP/btr4G64iTo1/pKJaEQ5M2ygyQUQYWXXKMk/img.png" data-lightbox="lightbox"><img src="/img/2023-03-20-quic-protocol/img_2.png" srcset="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcDadpP%2Fbtr4G64iTo1%2FpKJaEQ5M2ygyQUQYWXXKMk%2Fimg.png" onerror="this.onerror=null; this.src='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png'; this.srcset='//t1.daumcdn.net/tistory_admin/static/images/no-image-v1.png';" width="543" height="470" data-origin-width="742" data-origin-height="642"></span></figure>
<p></p>
<h3 data-ke-size="size23"><span style="font-family: 'Noto Serif KR';"><b>참고자료</b></span></h3>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';"><a href="https://www.chromium.org/quic/" target="_blank" rel="noopener">- QUIC, a multiplexed transport over UDP</a></span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- <a href="https://docs.google.com/document/d/1gY9-YNDNAB1eip-RTPbqphgySwSNSDHLq9D5Bty4FSU/edit" target="_blank" rel="noopener">What is QUIC</a></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- <a href="https://squidarth.com/rc/programming/networking/2018/08/01/congestion-cubic.html" target="_blank" rel="noopener">Congestion Control II: CUBIC</a></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- <a href="https://www.youtube.com/watch?v=hQZ-0mXFmk8" target="_blank" rel="noopener">QUIC: next generation multiplexed transport over UDP</a></span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- RFC 8999 - Version-Independent Properties of QUIC</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- RFC 9001 - Using TLS to Secure QUIC</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 1. Introduction</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 2.1 TLS Overview</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - 3. Protocol Overview</span></p>
<p data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">- RFC 793 - Transmission Control Protocol</span></p>
<p style="text-align: left;" data-ke-size="size16"><span style="font-family: 'Noto Serif KR';">&nbsp; &nbsp; - introduction</span></p></div>