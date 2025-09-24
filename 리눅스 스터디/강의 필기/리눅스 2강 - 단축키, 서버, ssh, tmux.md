### 서버와 리눅스의 연관성   
리눅스는 운영체제. 리눅스의 프로그램 중 하나가 서버. 리눅스 대상의 서버가 훨씬 많고, 그렇게 만들어짐. 또한 프로그램 설계가 용이.   
윈도우는 일반 사용자들을 위한 운영체제임.   
<br>
### 리눅스 서버 설치 및 체험   
리눅스는 접근 방법은 크게 두가지.   
윈도우에서는 GUI만 사용. 리눅스에서는 GUI와 CLI(Command Line Interface) 사용.   
CLI 환경의 자유도 : 리눅스 > 맥 > 윈도우   
<br>   
### 리눅스 단축키    
- mkdir 폴더명 : make directory, 폴더 생성   
- cd 경로 :  change directory, 경로로 이동. 경로에는 상대 경로와 절대 경로가 존재.  
  절대경로 : 파일 시스템이 있는 최상위 디렉토리는 / 인데, 최상위 디렉토리부터 파일명에 이르는 경로   
상대경로 : 현재 자신이 위치한 디렉토리를 기준으로 하는 경로   
- cd .. : 상위 디렉토리로 이동.   
- ls : list, 폴더의 파일 목록을 불러옴.   
- ls -a : 숨김 파일까지 확인 가능   
- ls -al : 폴더의 파일 목록을 리스트 형식으로 볼 수 있음.   
- touch 파일명 : 파일이 만들어짐. ex) touch hi.py   
- sudo apt intall 프로그램명 : 해당 프로그램을 설치. system 전체가 사용할 수 있게 system folder에 설치. 관리자 권한 획득 필요 (super user -> sudo). 파일명 여러 개 쓰면 여러 개 한 번에 설치 가능.
- apt list : 설치할 수 있는 목록을 보여줌.
	apt는 프로그램 설치 툴. 의존성 체크 x.   nix도 프로그램 설치 툴. nix는 추후 공부 필요. 더 많이 씀.   

### [[서버]]   
클라이언트에게 네트워크를 통해 정보나 서비스를 제공하는 컴퓨터 시스템으로 컴퓨터 프로그램 또는 장치를 의미.   
포트(통로)를 점유하고 있는 프로그램.   
	[[인터넷]]에 어떻게 연결할지 : 밖에서 접속 가능한 [[ssh]](secure shell) 설치.   
<br>

### ssh 서버 설치   
설치 : sudo apt install openssh-server   
설치 확인 : netstat -lnap   
	22번 포트를 확인할 수 있음. 외부에서 내 컴퓨터로 접속 가능.   
	IP 확인 : ifconfig
		inet 000.000.0.00   
		공유기에 받은 IP임.   
		외부 IP와는 다름.

<br>
[[IP]]를 할당하는 것은 인터넷 사업자(KT, SKT, LG U+)   

하나의 IP로 여러 기기 사용 불가능하지만, 그걸 여러 기기가 사용하기 위해 우리는 공유기를 통해 공유기 자체에서 IP를 만들어서 여러 기기에서 이용할 수 있게 함.   
외부에서 IP로 우리에게 접근하려면 외부에선 공유기의 IP까지밖에 알지 못 함. 따라서 리눅스(한 기기)에 연결해주기 위해 22번에 온 요청을 22번으로 보내주어야 함   
-> [[포트포워딩]](공유기 자체 기능)   
	

<br>

### 강의 질문   
**Q1. 윈도우 cmd에서 어떻게 ssh가 작동하나요?**   
	 A1. ssh는 서버와 클라이언트로 나눌 수 있음. 윈도우에선 ssh 서버에 접속할 수 있는 ssh 클라이언트가 깔려있음. 리눅스엔 두 개 다 깔려있음.    
	윈도우는 ssh 서버가 없고, 존재한다 해도 cmd 명령어가 매우 약함. 윈도우에서 서버를 쓰기엔 좋지 않음.   
	
**Q2. 크롬으로 서버에 접속하려고 했는데 안 되는 이유는 무엇인가요?**   
A2. ssh는 ssh server와 ssh client로 나뉨. 22번   
web도 web server와 web client로 나뉨. 80번   
서버마다 클라이언트를 따로 두는 이유는 통신 규격이 다르기 때문. ssh에서 web으로 web에서 ssh로 단순 접속 불가능.    
구글링을 통하면 접속하는 방법을 찾을 수 있음. 



## 실습
### ssh 접속   
**ssh dudgus@192.168.56.1 -p 5272**   
dudgus -> 내 리눅스 계정 이름   
192.168.56.1 -> 연결할 ip   
5272 -> 네트워크 추가 창에서 설정한 포트 번호   
virtual box 환경이기 때문에 cmd창에서의 ip로 접속해야 했음.   

### 우분투 네트워크 설정(virtual box) - 포트포워딩   
네트워크 설정 - 고급 - 포트포워딩    
cmd 창에서 ipconfig 입력 후 IPv4 주소를 호스트IP에   
호스트포트는 사용자가 설정 (이미 사용하고 있는 포트는 안 됨, 구글링)   
터미널창에서 ifconfig 입력 후 inet 주소를 게스트IP에   
게스트포트는 ssh 22번 포트를 열어두었기 때문에 22를 적어주어야 함.

<br>

## Trouble Shooting
#### IP 확인 불가, net-tool 설치 불가 등
**문제상황**
ssh설치를 확인하고 IP를 확인하기 위해
![[Pasted image 20240512203940.png|400]]
해당 명령어들을 입력하였는데 net-tools를 설치하라고 안내가 나와 sudo apt install net-tools 명령어를 입력하였지만,
![[Pasted image 20240512204004.png]]
위와 같은 오류 발생.
**'[kr.archive.ubuntu.com](http://kr.archive.ubuntu.com)'의 주소를 알아낼 수 없습니다.** 로 검색하여 오류 원인을 찾아보는 중인데 찾지 못 함.
['kr.archive.ubuntu.com'의 주소를 알아낼 수 없습니다. 오류 발생 시 해결방법](https://shinit0519.tistory.com/48)
**해결방법**

<br>

#### RSA 공유키 충돌로 인해 접속 불가
**cmd 창에서 접근시 오류 발생.**
```cmd
C:\Users\sy020>ssh [dudgus@192.168.56.1](mailto:dudgus@192.168.56.1) -p 5272 @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ @ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @ @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY! Someone could be eavesdropping on you right now (man-in-the-middle attack)! It is also possible that a host key has just been changed. The fingerprint for the ED25519 key sent by the remote host is SHA256:VruuH5qgg1m0Lf3vrSn/wGfvPC3XuPY6ETL+Zcq2RQE. Please contact your system administrator. Add correct host key in C:\\Users\\sy020/.ssh/known_hosts to get rid of this message. Offending ECDSA key in C:\\Users\\sy020/.ssh/known_hosts:9 Host key for [192.168.56.1]:5272 has changed and you have requested strict checking. Host key verification failed.
```

**원인**
호스트가 서버에 접속할 때 발생했음. 서버의 ssh나 OS를 설치, 재설치 했을 때 생긴 걸로 보임.
호스트에선 서버의 IP와 RSA 키를 가지고 있는데, 서버의 ssh, OS를 재설치 함으로써 RSA키가 바뀌어 위와 같은 현상이 생긴다고 함.

**해결 방법**
known_hosts 파일을 지우기 위해, windows cmd의 경우 C:\Users\계정명\.ssh 안에있는 파일 삭제.

**참고 사이트**
[cmd, ssh 원격접속 오류 WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!](https://pepega.tistory.com/18)

