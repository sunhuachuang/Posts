### NAT - Network Address Translators (网络地址转换)

原因：局域网的设备要想访问国际互联网，必须有国际IP（全球固定IP），所以设备需要先链接到有国际IP的设备，才能通过国际IP访问全球资源。

##### 命名
- 本地设备 A(IPa, PORTa), 例如 192.168.0.2:5000
- NAT服务（路由器/ISP设备） R(IPr, PORTr)，例如 33.23.12.32:60000
- 远程单一公共服务器 S(IPs, PORTs)，例如 8.8.8.8:80
- 远程STUN辅助探测服务器 T1(IPt1, PORTt1),T2（IPt2, PORTt2） 例如 123.123.123.1:8080, 123.123.123.2:8080

##### NAT 种类
- Cone 同一个设备的相同端口发送的被分配到同一个国际IP和端口
  - Full cone -> 来者不拒
  - Restricted cone -> 必须先向对方发送，对方才能发送
  - Port restricted cone -> 端口也必须一致
- Symmertric 同一个设备每次发送都重新分配另一个国际IP和端口

#### 第一种方式 直连式 - 单IP服务器
1. 中央服务器记录下设备A访问的时候的 国际IP和端口，记录下设备B的 国际IP和端口
2. S 命令 B 向 A 的国际IP打洞, 这样负责B的NAT上就有了洞口，A再通过B的NAT洞口访问B，成功后，A与B就可以相互发送

#### 第二种方式 STUN - 2个IP服务器
1. 需要有一个公开的STUM服务器（两个IP，T1, T2）
2. 设备A -> NAT -> T1
3. T1(将收到的NAT信息包装起来) -> NAT -> A 保证NAT设备正常和鉴定自己是不是有公网的IP地址
3. T1 收到 T1的信息后，从T2发送一个包给设备A，如果能收到 说明 NAT 是一个Full cone.
4. 如果收不到，B 再次发送 -> NAT -> T2, T2(将收到的NAT信息包装起来) -> NAT -> A
5. 比较T2传输过来的NAT信息和T1传输过来的NAT信息对比
6. 如果一致，NAT则是Cone类型，否则无法使用P2P通信了已经
7. 判断是 Restricted 还是 Port Cone。设备A -> NAT -> T1, T1改变端口，返回数据包, 如果成功，则是Restricted, 否则是Port Cone
