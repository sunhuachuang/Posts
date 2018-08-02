#### 前向安全性 Forward Secrecy（FS）
是密码学中通讯协议的安全属性，指的是长期使用的主密钥泄漏不会导致过去的会话密钥泄漏。前向安全能够保护过去进行的通讯不受密码或密钥在未来暴露的威胁。如果系统具有前向安全性，就可以保证在主密钥泄露时历史通讯的安全，即使系统遭到主动攻击也是如此。

主要运用在传输层安全协议（TLS）。

如果采用Perfect Forward Secrecy， 针对每个session客户端和服务器都分别生成临时的(Ephemeral)随机DH/ECDH私钥EPk (DH/ECDH也是一种非对称算法),  根据此随机的私钥EPk和对方传过来的DH/ECDH公钥计算出共享的preMaster key, 再用哈系函数处理preMaster key计算出AES的加密/解密密钥。 由于DH/ECDH私钥不经过网络传输，每次会话结束就被删除，和RAS 私钥Apriv无关，因此即使长期使用的Apriv被非法获取，以往监听到的加密数据也无法被解密(除非有能力拿到每个session的DH私钥，这是不可能的)。  可见密码学安全的随机数生成算法有多重要。

当然除了长期使用的用于身份认证的公钥私钥对Apub/Apriv, 服务器也可以为每次(多次)会话都生成一对新的RSA 公钥/私钥 Tpub/Tpriv用于AES密钥交换。 服务器用证书私钥Apriv签名Tpub的hash值，并传输Tpub和Tpub的hash签名给客户端。 客户端用收到的Tpub加密随机生成的AES密钥K并传给服务器，服务器用Tpriv解密K，双方就可以用K加密解密实际的消息了。 双RSA虽然也能实现PFS，但是效率太差，没有公司会采用， 基本都是RSA+ECDHE。

完美前向安全 Perfect Forward Secrecy（PFS）

#### 前向安全性 Forward Secrecy（FS）
前向安全保证了新加入群组的人无法解密之前的信息。

- 强前向安全(Strong Backward Secrecy): 后面进来的人即时知道之前的信息，但是无法解密。
- 弱前向安全(Weak Backward Secrecy): 后面进来的人完全不知道之前有过什么信息。

#### 后向安全性 Backward Secrecy（BS）
后向安全保证了新加入群组的人无法解密之后的信息。

- 强后向安全(Strong Forward Secrecy): 前面进来的人，虽然能获取信息，但是无法解密。
- 弱后向安全(Weak Forward Secrecy): 前面进来的人，无法获知后面发出的信息。
