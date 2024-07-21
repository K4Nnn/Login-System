## 实现功能
----------
**(1)密钥协商**
 1. Server和Client希望共享一个会话密钥Ks。首先由服务器端生成RSA密钥对，并在连接之初将公钥送给客户端。
 2. 随后客户端使用公钥加密Client生成的会话密钥送给Server，Server使用私钥解密。
 3. 同时，Client、Server应当附上身份验证信息。eg. 随机数验证
    预改进：如何证明身份？发送信息包括RSA加密的AES会话密钥，以及AES会话密钥的Hash值（取SHA-256）。

Tip: 
- 在AES、RSA算法中。各密钥的存储都以Base64编码形式。即：传输，存储的过程中基本都是Base64编码。
- RSA类是类方法，而AES类是对象方法。

**(2)C/S模式**
 - 实现客户端登陆界面、服务器端存储数据于数据库。数据库采用MySQL；在server文件夹下的DatabaseConnector.java下，填写必要的数据库信息。

**(3)程序流程**
Server启动后，接收socket连接（多线程）。Client通过Login界面，输入已有的账号密码，登录至Server，再启动下一步的服务。
    预改进：添加Client端的Register注册系统界面。

**(4)如何编译运行**
 1. 编译命令： 
    `javac -cp "lib/mysql-connector-j-9.0.0.jar;src" -d bin -encoding UTF-8 src/server/*.java src/client/*.java src/cryptoUtils/*.java`
 2. 运行命令：
    启动Server：`java -cp "bin;lib/mysql-connector-j-9.0.0.jar" server.ServerTest 40101`
    启动Client：`java -cp "bin;lib/mysql-connector-j-9.0.0.jar" client.ClientTest localhost 40101`<br>
 3. server接收一个参数，代表待连接端口号`port`。client接收两个参数，第一个为`ipAddress`，第二个为连接端口号`port`。
