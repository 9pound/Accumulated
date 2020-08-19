# TCP的三次握手与四次挥手

标志字段 6 比特的 

ACK 比特用于指示确认字段中的值是有效的，即 该报文段包括一个对已被成功接收报文段的确认。 

RST、SYN 和 FIN 比特用于连接建立和拆除，

PSH 比特被设置的时候，就指 示接收方应立即将数据交给上层。 

URG 比特用来指示报文段里存在着被发 送端的上层实体置为"紧急"的数据。 紧急数据的最后一个字节由 16 比特的紧急 数据指针字段指出 。 当紧急数据存在并给出指向紧急数据尾的指针的时候， TCP 必须通知接收端的上层实体。 (在实践巾， PSH 、 URG 和紧急数据指针并没有使用。 为了完整性起见，我们才提到这些字段。) 

- SYN(synchronous建立联机) 
- ACK(acknowledgement 确认) 
- PSH(push传送) 
- FIN(finish结束) 
- RST(reset重置) 
- URG(urgent紧急)
- Sequence number(顺序号码)
- Acknowledge number(确认号码)



![image-20200820010802077](C:\Users\shazi\AppData\Roaming\Typora\typora-user-images\image-20200820010802077.png)



第一次握手：主机A发送位码为syn＝1，
　　　　　　　　　　随机产生seq number=1234567   的数据包到服务器，
　　　　　　主机B由SYN=1知道，A要求建立联机；


第二次握手：主机B收到请求后要确认联机信息，
　　　　　　向A发送ack number=(主机A的seq+1)，syn=1，ack=1，
　　　　　　随机产生seq=7654321的包；


第三次握手：主机A收到后检查ack number是否正确，即第一次发送的seq number+1，以及位码ack是否为1，若正确，
　　主机A会再发送ack number=(主机B的seq+1)，ack=1，
　　主机B收到后确认seq值与ack=1则连接建立成功。
　　完成三次握手，主机A与主机B开始传送数据。





在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接。
第一次握手：建立连接时，客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认；

第二次握手：服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；

第三次握手：客户端收到服务器的SYN＋ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。完成三次握手，客户端与服务器开始传送数据.
YN_SENT   :表示请求连接,等待服务器确认
SYN_REC   :服务端被动打开后,接收到了客户端的SYN并且发送了ACK时的状态
ESTABLISHED状  :客户端和服务器 已经建立的连接

C :第一次握手：SYN = J :SYN_SEND_
S :SYN=K     ACK J+1 :SYN_RECV
C : ACK = K+1  :ESTABLISHED  



https://www.cnblogs.com/ldms/p/11399992.html