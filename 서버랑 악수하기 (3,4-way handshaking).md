# 서버랑 악수하기 ( 3/4-way HandShaking)

## 3-way Handshaking?

TCP/IP 프로토콜을 이용해 통신하는 응용 프로그램이 데이터를 전송하기 전, 정확한 전송을 위해 
상대방 컴퓨터와 사전에 세션을 수립하는 과정

장치들 사이의 논리적인 접속을 성립 ( Established )하기 위해 사용한다.

## 연결 과정

### 패킷

- **SYN** : synchronize Sequence Numbers의 약자로, 요청이다.
- **ACK** : Acknowledgment의 약자로, 응답이다.

### Port 상태

- **LISTEN** : 포트가 열린 상태로 연결 요청을 대기하는 상태
- **SYN-SENT** : 연결 요청을 하고 Server의 ACK를 기다리는 상태
- **SYN-RECEIVED** : 연결 요청에 응답/연결을 요청하고 Client의 응답을 기다리는 상태
- **ESTABLISHED** : 연결된 상태

Client와 Server가 둘 다 LISTEN 상태일 때부터 시작한다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1.png)

먼저, 클라이언트가 서버에게 접속을 요청하는 SYN 패킷을 보내고 SYN-SENT 상태가 된다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1%201.png)
서버가 SYN 요청을 받으면, 클라이언트에게 요청을 수락한다는 ACK 패킷을 전송한다.
이와 동시에, 클라이언트에게 연결을 요청하는 SYN 패킷도 전송하게 되며, SYN RECEIVED 상태로 클라이언트의 ACK 을 기다린다.

그리고 클라이언트는 ACK 패킷을 받고 연결이 완료된 ESTABLISHED 상태가 된다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1%202.png)

클라이언트의 연결이 완료된 후, 클라이언트는 서버에게 요청을 수락하는 ACK 패킷을 보낸다.

ACK을 받은 서버도 ESTABLISHED 상태가 되며 연결이 완료된다.

## 그럼 4-way Handshaking는?

3-way handshaking과 반대로 연결을 종료하는 과정이다.

여기서는 FIN 패킷을 이용한다.

- **FIN** : Finish의 약자로, 세션을 종료시키는데 사용되며 더 이상 보낼 데이터가 없음을 의미한다.
실질적으로 SYN 패킷도 포함되어있다.

## 종료 과정

### Port 상태

- **FIN-WAIT** : FIN요청에 대한 응답을 기다리는 상태
- **CLOSE-WAIT** : 서버가 FIN에 대한 ACK을 보낸 후, 자신의 통신이 끝날 때 까지 기다리는 상태
- **LAST-ACK** : 서버가 연결을 종료할 준비가 되어, 클라이언트에게 FIN 플래그를 보낸 상태
- **CLOSE** : 연결이 종료된 상태

Client와 Server가 둘 다 ESTABLISHED 상태일 때부터 시작한다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1%203.png)

클라이언트가 접속을 끊으려고, 연결을 종료한다는 FIN 패킷을 보내고 FIN-WAIT-1 상태가 된다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1%204.png)

서버는 FIN을 받고, 일단 확인했다는 ACK 을 클라이언트에게 보낸다. 그 후 서버는, 자신의 통신이 끝날 때 까지 기다리는 CLOSE-WAIT 상태가 된다.

클라이언트는 서버에서 ACK을 받은 후 서버가 남은 데이터 처리를 끝내고 FIN 패킷을 보낼 때까지 기다리는 FIN-WAIT-2 상태가 된다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1%205.png)

서버가 데이터를 모두 보냈다면, 연결 끊을 준비가 되었다는 의미의 FIN 패킷을 클라이언트에게 전송하며, LAST-ACK 상태가 된다.

![Frame 1.png](img/서버랑%20악수하기%20(3,4-way%20handshaking)/Frame_1%206.png)

클라이언트가 FIN을 받으면, 확인했다는 ACK을 서버에게 보내게 되며, ACK을 받은 서버는 CLOSE 상태가 되어 연결을 종료한다.

```
그런데 만약, “서버에서 FIN을 전송하기 전 보낸 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해서 FIN 패킷보다 늦게 도착하는 상황”이 생긴다면 어떻게 될까?

클라이언트에서 세션을 종료한 후 도착한 패킷들은 DROP되고 데이터가 유실될 것이다.

따라서 클라이언트는 서버로부터 FIN을 수신받더라도 일정시간 (Default : 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리게 된다. 이러한 상태를 TIME-WAIT 상태라고 하며, 일정 시간이 지나면 세션을 만료하고 연결을 종료시켜 CLOSE 상태가 된다.
```