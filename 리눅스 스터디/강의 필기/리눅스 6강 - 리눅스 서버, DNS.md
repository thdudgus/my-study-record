서버 종류에는
웹서버, DNS, VPN, WAS, ...

# DNS
Domain Name System

## Bind9 Server
DNS [[서버]]의 표준.
open source로 free sw임.

DNS 서버는 www.naver.com 이라고 했을 때 그 IP 주소가 매핑되어 있음. 
www와 naver와 com을 따로 생각하면 편함.
DNS 서버는 전세계에 분산이 되어 있음. root 서버는 com, kr, net 등의 DNS 서버를 각각 갖고 있음.
com의 주소를 알려달라고 root에게 요청하면 root가 알려줌. 그 위치에 naver를 요청하면 naver의 위치를 알려줌. 그 위치에 www를 요청하면 www의 위치를 알려줌. => 이런 방식으로 주소를 알게 됨.

Root -> first level domain (com) -> second level domain (naver) -> sub domain (www)

DNS서버는 53번 포트를 점유. 이를 확인하기 위해 아래 명령어 입력.

sudo netstat -lnap : 포트를 확인하는 명령어. -lnap는 파라미터로 p는 program. 포트, 소켓을 쓰는 다양한 프로그램을 볼 수 있음. 
	너무 많이 나와서 보기 힘듦. 이때 파이프라이닝 이용. ( | ( \\ + shift)을 파이프라인이라 부름.)
		명령어1 | 명령어2 : 명령어1의 output이 명령어2의 파라미터로 들어감.
		![[Pasted image 20240502120324.png]] 어느 IP에서든 53번이 들을 수 있게 named(bind9의 다른 이름)가 듣고 있음. 
		=> DNS가 정상 동작
		
man netstat : netstat 명령어에 대한 설명을 볼 수 있음.

### DNS 서버 설정
도메인과 IP가 있는데 이를 매핑하는 DB의 이름이 zone. 이 zone은 /etc에 있음. root 디렉토리의 etc. 
![[Pasted image 20240502121700.png]]
conf가 있는 걸 찾으면 됨.

vim named.config.options를 입력하면
![[Pasted image 20240502122204.png]]
위 화면이 나옴. forwarders는 cache 역할을 하는 recursive server

vim named.config.local을 입력하면
도메인과 IP를 매핑하는 zone을 볼 수 있음.
![[Pasted image 20240502122430.png]]
DNS 서버는 계속 꺼지지 않고 동작해야 하는데, 같은 역할을 하는 2개의 서버가 있음. 하나는 진짜, 다른 하나는 계속 업데이트 하면서 진짜가 죽었을 때 대신 한다든가 부하가 걸릴 때 같이 일을 함. 진짜는 master, 보조는 slave라고 함.

전문적으로 할 게 아니라면 master만 있어도 됨.

dns명을 만들고 file의 위치에 만든 도메인의 정보를 넣어두면 됨.
/etc/bind에 zones를 만들고 db.도메인명을 쓰는 게 규칙
vim db.moyak.kr
![[Pasted image 20240502122810.png]]
$TTL : 내 컴퓨터에서 root에서 kr에서 moyak으로 간다고 할 때, moyak의 IP나 위치가 바뀐다고 한다면 이를 DNS 서버에 갱신. 그 갱신의 주기를 적어둠. 86400. (하루에 한 번)
서브 도메인들은 필요에 따라 작성.

![[Pasted image 20240502123258.png]]
커서 잡힌 부분이 한 줄.
@ : moyak.kr을 의미
루트.도메인이름은 메일 도메인.
Serial이 업데이트 되면 slave가 캐치. slave서버가 없으면 신경 쓸 필요 x.

localhost까지는 그대로 쓰면 됨. 

NS : name server
localhost : 나의 컴퓨터

~~ IN A IP : \~~로 들어왔을 때 IP


kr에 moyak을 들어야 가능
등록 대행사가 존재. 가비아나 호스팅 케이알이 있음. 이런 데에서 구매.
설정페이지 -> 네임버서등록 -> 내 IP 작성.

### 요약
1. 우분투에서 bind9 설치 : sudo apt install bind9
2. bind9 설치 확인 : sudo netstat -lnap | grep 53
3. bind9 실행 : /etc/bind/named.conf에서 include한 걸 보면, option(안 건드려도 됨)과 local이 있음. local에서 zone을 생성. 따옴표 안에 들어갈 DNS 주소는 대행사에서 구매한 걸 넣어주면 됨.![[Pasted image 20240502145840.png|500]]
4. zone 설정
5. reload 필요 (컴퓨터 껐다 켜도 됨.) : sudo sevice bind9 reload
	sudo sevice bind9 restart
	sudo rebbot 중 하나 하면 됨.

### 활용
서비스를 구현할 때도 쓰임 (map.naver.com, comic.naver.com)
서버를 운영하고 있다고 한다면, 서버의 IP 주소를 기억하기 힘들 때 DNS로 만들어두면 편리. (서버의 접근성이 높아짐.)
대부분의 리눅스 유저들은 bind9 활용.

### http / https
https는 http에 secure이 추가되어있음.