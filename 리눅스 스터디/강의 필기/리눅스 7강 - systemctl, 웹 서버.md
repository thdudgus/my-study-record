지금까지 배운 서버 : ssh, bind => 서비스
	systemctl => 명령어

systemctl status bind9.service : bind9의 상태를 알게 해줌. (뒤에 .service는 안 붙여도 됨.)
	active면 실행 중.
sudo systemctl stop bind9 : bind9을 멈춤.
sudo systemctl start bind9 : bind9을 시작.

sudo systemctl enable bind9 : 컴퓨터를 시작할 때마다 bind9을 실행.
sudo systemctl disable bind0 : 컴퓨터를 시작할 때마다 bind9을 실행하지 않음.
	-able로, 컴퓨터를 켤 때의 설정이기 때문에 현재 상태를 바꾸진 않음. 

/lib/systemd/system : 나의 시스템을 확인할 수 있음. 
vim bind9.service : bind9 service의 설정을 확인


## 웹 서버
가장 초창기의 웹서버에 대해 설명
client가 server에 요청을 하면 server는 html을 전달. 
server는 프로토콜을 통해 http나 https를 전달.

정적인 데이터를 전달할 때 퍼포먼스가 좋음. 

