
### public key cryptography
有一对key，用`KeyA`加密，只能用`KeyB`解密。且`KeyA`和`KeyB`不相同

所以要**接受信息**的人，可以生产一对Key，将其中一个公钥`KeyA`交给发送者A。注意，这里`KeyA`可以被公众知道，因为即使知道`KeyA`也不能解密`KeyA`加密的文件，`KeyA`加密的文件只有`KeyB`能解密。

对应在Github的SSH上，本地生成一对SSH Key，将`KeyA`交给Github，当我需要向Github请求获取信息的时候，例如`clone`时，Github将信息用`KeyA`加密，在过程的中即使加密的信息和`KeyA`被截获，对方仍然不能解密。而正在解密信息的`KeyB`始终在本地，不会传输，这样也保证了安全性。

可以推测，处理手动在Github上添加SSH的Key以外，在交互的过程中，Github也会将他生成的公钥`KeyB'`发送给本地。这样本地也可以通过`KeyB'`加密信息，传给Github。

1. 问题是什么
	- 如果加密和解密共用一个Key，在交换Key等时候有丢失Key的风险，如果丢失Key，加密系统就失效了
2. 如何解决的
	- 加密和解密的密钥分开，这样自己保留解密的KeyB，将加密的KeyA告诉传输加密传输方。由于即使KeyA被公众知道，公众也无法解密信息，所以称KeyA为公钥
	- KeyA加密的信息只有本地保留的KeyB可以解密   （**公钥加密信息：保证信息不被第三方解密**）
	- 通过KeyB加密的信息传递给加密方，有公钥的对象可以知道获得的指令没有被更改   （**私钥数字签名：保证请求未被修改，即使被解密**）
3. 如何操作
	- （以和Github建立SSH为例）
	- 在本地生成SSH key
	- 将公钥添加到Github账户中保存
	- 通过SSH通道，客户端和服务器交互访问

### 认证证书
1. 存在问题是什么
	- 可能有攻击者用自己的公钥替换掉原先的公钥，如果用攻击者公钥加密传输，攻击者就可以用自己的私钥解密获得信息
2. 如何解决
	- 需要确认先有公钥的可靠性
3. 如何操作
	- https就是加密传输，客户端获得服务器的公钥，将信息（如密码）加密传输给服务器
	- 客户端可以查看收到的公钥是否可靠，可靠公钥需要在信任机构颁布的证书中注册
	- 如果公钥所对应的网站和正在浏览的网站不一致，公钥可以就被伪造
	- 「受信任的根证书颁发机构」存放在浏览器中 （所以如果修改浏览器...）

## SSH

1. 问题是什么
	- 传统的网络服务如rsh、FTP。POP和Telnet都不安全，因为他们在网络上用明文传输数据、用户账号和用户口令，很容易受到中间人方式的攻击
2. 如何解决
	- 可以接收服务器的公钥，将用户信息等加密传输
3. 问题
	- SSH不像https有证书认证，所以可能会被攻击者伪造公钥，进行中间人攻击
4. 如何解决
	- 用户只有手动将本地公钥和远程服务器公开的公钥对比，手动确认
	- 这样用户就可以确认登陆信息不被截获
5. 问题
	- 用户如何省去重复登陆的麻烦
6. 如何解决
	- 客户端本地生产公钥，服务器通过公钥加密传输，只有生成公钥的客户端可以解密
7. 问题
	- 如何确保服务器的公钥是来自客户端，而不是攻击者利用公钥仿造
8. 解决
	- 客户端将用户信息和公钥一并传给服务器
(之前使用的同一WiFi内的攻击应该就属于中间人攻击，像baidu，taobao这些https加密的网站就不能简单截取，发送的账户信息都是加密的，而163，zhihu这些就很容易破解。)

传输过程中，最需要保护的是用户的身份信息。不管是登陆时公钥加密的用户账号信息，或者是SSH时服务器保有用户的公钥。


参考：
[对公钥讲解的很清楚](https://www.youtube.com/watch?v=GSIDS_lvRv4)

[数字签名是什么？](http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html)

[SSH原理与运用（一）：远程登录](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)
[]()
[]()
