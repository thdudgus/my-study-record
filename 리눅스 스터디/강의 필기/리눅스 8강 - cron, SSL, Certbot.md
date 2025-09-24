### 유용한 tool
cron : 일정 시간마다 프로그램을 실행시켜줌.
	어떤 프로그램을 시작할지 정해줄 수 있음  : cron table
	crontab -e : cron table editor를 엶.
		주석들 아래에 어떤 명령어를 실행시킬지 넣으면 됨.
		주기와 program의 이름을 삽입
		![[Pasted image 20240512190906.png]]
		0 5 * * 1이 주기
		=> 분 시간 일 월 요일(0이나 7이면 일요일, 1부터 월요일), \*의 의미는 '모든'
		매주 5a.m에 이 프로그램을 실행 시켜라
	
```bash
* * * * * command  // 이 command가 매 1분마다 동작
10, 30 * * * * command // 매 10분과 30분 마다 command 동작
30 2 * * * command // 매일 2시 30분에 command 동작
10 */2 * * * command // 00시 10분, 02시 10분, 04시 10분,... 에 command 동작
```
crontabl -l : cron table의 list를 확인할 수 있음.
crontab -r : cron table의 list를 삭제함.


## 웹서버
ID와 pw 등 정보를 보낼 때 암호화를 안 하면 그냥 정보를 볼 수 있어 보안이 취약함. 
따라서 SSL을 추가해줘야 함.
SSL : Secure Socket Layer
	SSL 3.0부터는 TLS라고 부름 : Transport Layer Security

암호화는 공개키 암호화를 사용.
공개키(public key)와 개인키(private key, 서버가 가짐)로 나뉨.
공개키는 개인키와 1대1 매칭이 되어있음.
공개키가 f(x)라면 개인키는 f(x)의 역함수.
a라는 데이터를 f함수로 통과 시키면 f(a)가 나오고, 이를 서버로 전송한다. 이를 개인키로 디코드를 a를 알 수 있음.
![[Pasted image 20240512200922.png|200]]

방법
1. SSL 인증서를 발급 받아야 함. (from 공인 인증기관, Let's encrypt: 공식 documentation이 있음.)
	certbot에 접속하면, https://certbot.eff.org/	![[Pasted image 20240512201743.png]]
	우리가 사용하는 software가 무엇인지 cerbot에게 알려줘야 함. 어느 system상에서 동작을 시킬 건지도 알려줘야 함. 
	입력하면 필요한 요구 사항을 알려줌. (command를 쓸 줄 알아야 하고, DNS가 있어야 하고, 웹서버가 있어야 하고, sudo를 쓸 수 있어야 하고 등등등...)
	snapd는 apt와 같은 패키지 manage 툴인데, ubuntu에서 사용할 수 있으며, 의존성 문제를 해결한 툴.
