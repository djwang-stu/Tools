# SSH

[参考链接](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)



> SSH是一种网络协议，用以计算机之间的加密登录。如果一个用户从本地计算机，使用SSH协议登录另一台远程计算机，我们就可以认为，这种登录是安全的，即使被中途截断，密码也不会泄露。此协议由芬兰学者Tatu Ylonen于1995年设计，将登录信息全部加密，成为互联网安全的一个基本解决方案，迅速在全世界获得推广，目前成为Linux系统的标准配置。SSH只是一种协议，存在多种实现，既有商业实现，也有开源实现。本文针对OpenSSH，它是自由软件，应用非常广泛。如果要在Windows中使用SSH，会用到另一种软件PuTTY.



## 基本用法

1. 远程登录

   ```
   ssh username@host  //以用户名username登录远程主机host
   ssh host           //本地用户名与远程用户名一致，登录时可以省略用户名
   ssh -p 2222 username@host //SSH默认端口是22，使用p参数可以修改这个端口
   ```

2. 中间人攻击

   > 公钥加密步骤
   >
   > 1. 远程主机收到用户的登录请求，把自己的公钥发给用户
   > 2. 用户使用这个公钥，将登录密码加密后，发送回来
   > 3. 远程主机用自己的私钥，解密登录密码，如果密码正确，就同意用户登录

   以上过程本身安全，但实施存在一个风险：如果有人截获了登录请求，然后冒充远程主机，将伪造的公钥发给用户，那么用户很难辨认真伪。这个风险就是著名的**中间人攻击**(Man-in-the-middle attack)。那么SSH协议如何应对呢？

3. 口令登录

   ```
   　　$ ssh user@host
   　　The authenticity of host 'host (12.18.429.21)' can't be established.
   　　RSA key fingerprint is 98:2e:d7:e0:de:9f:ac:67:28:c2:42:2d:37:16:58:4d.
   　　Are you sure you want to continue connecting (yes/no)?
   ```

   当远程主机的公钥被接收以后，他就会被保存在文件HOME/.ssh/known_hosts之中。下次再连接这台主机，系统就会认出它的公钥已经保存在本地了，从而跳过警告部分，直接提示输入密码。每个SSH用户都有自己的known_hosts文件，此外系统也有一个这样的文件，保存一些对所有永辉都可信赖的远程主机的公钥

4. 公钥登录

   > 公钥登录原理：用户将自己的公钥存储到远程主机上。登录的时候，远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后，再发回来。远程主机用事先存储的公钥进行解密，如果成功，就证明用户是可信的，直接允许登录shell，不在要求密码。

   ```
   ssh-keygen   //运行以上命令生成一个公钥
   在HOME/.ssh目录下，会生成两个文件id_rsa.pub(公钥)和id_rsa(私钥)
   ssh-copy-id username@host  //将公钥传送到远程主机host上面
   ```

   > 如果以上步骤不成功，打开远程主机的/etc/ssh/sshd_config这个文件，检查下面几行前面#注释是否去掉。
   >
   > ```
   > 　　RSAAuthentication yes
   > 　　PubkeyAuthentication yes
   > 　　AuthorizedKeysFile .ssh/authorized_keys
   > ```
   >
   > 然后重启远程主机的ssh服务
   >
   > ```
   > service ssh restart   //ubuntu系统
   > /etc/init.d/ssh restart  //debian系统
   > ```

5. Authorized_keys文件

   远程主机将用户的公钥保存在登录后的用户主目录的HOME/.ssh/authorized_keys文件中。公钥就是一段字符串，只要把它追加到authorized_keys文件的末尾就行了

   > 这里不使用上面的ssh-copy-id命令，改用下面的命令，解释公钥的保存过程：
   >
   > > 　　$ ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
   >
   > 这条命令由多个语句组成，依次分解开来看：（1）"$ ssh user@host"，表示登录远程主机；（2）单引号中的mkdir .ssh && cat >> .ssh/authorized_keys，表示登录后在远程shell上执行的命令：（3）"$ mkdir -p .ssh"的作用是，如果用户主目录中的.ssh目录不存在，就创建一个；（4）'cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub的作用是，将本地的公钥文件~/.ssh/id_rsa.pub，重定向追加到远程文件authorized_keys的末尾。
   >
   > 写入authorized_keys文件后，公钥登录的设置就完成了。