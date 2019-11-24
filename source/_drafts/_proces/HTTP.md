

-[HTTP 思维导图](https://juejin.im/entry/58ca14c261ff4b006016b0f7 "")
-[HTTP 图解](https://juejin.im/entry/5865c3af1b69e60063cee08b "")
-[图解http（02）-http基础](https://juejin.im/entry/59c3165951882531b21ef63d "")
-[图解http（03）-http首部](https://juejin.im/entry/59c316686fb9a00a5f46f21f "")
-[HTTP 缓存](https://juejin.im/entry/57fb373ad203090068c67883 "")
-[简述HTTP](https://juejin.im/post/5a584c146fb9a01cb508c14f "")
-[从HTTP到HTTPS再到HSTS](http://support.upyun.com/hc/kb/article/1079017/?comefrom=http://blogread.cn/news/ "")
-[《图解HTTP》— HTTP报文信息](https://juejin.im/post/59face7ef265da43215361d3 "")
-[HTTP 协议详解](https://juejin.im/entry/587222418d6d810058929f55 "")
-[面试 -- 网络 HTTP](https://juejin.im/post/5872309261ff4b005c4580d4 "")
-[HTTP----HTTP2.0新特性](https://juejin.im/post/5a4dfb2ef265da43305ee2d0 "")
-[]( "")






















# WEB攻击
## 其他安全漏洞
### 密码破解
密码破解攻击（Password Cracking）即算出密码，突破认证。
攻击不仅限于 Web 应用，还包括其他的系统（如 FTP 或 SSH 等），本节将会讲解对具备认证功能的 Web 应用进行的密码破解。

#### 通过网络的密码试错
对 Web 应用提供的认证功能，通过网络尝试候选密码进行的一种攻击。

##### 穷举法
穷举法（Brute-force Attack，又称暴力破解法）是指对所有密钥集合构成的密钥空间（Keyspace）进行穷举。即，用所有可行的候选密码对目标的密码系统试错，用以突破验证的一种攻击。

比如银行采用的个人识别码是由“4 位数字”组成的密码，那么就要从 0000~9999 中的全部数字逐个进行尝试。这样一来，必定在候选的密码集合中存在一个正确的密码，可通过认证。因为穷举法会尝试所有的候选密码，所以是一种必然能够破解密码的攻击。但是，当密钥空间很庞大时，解密可能需要花费数年，甚至千年的时间，因此从现实角度考量，攻击是失败的。

##### 字典攻击
字典攻击是指利用事先收集好的候选密码（经过各种组合方式后存入字典），枚举字典中的密码，尝试通过认证的一种攻击手法。

还是举银行采用个人识别码是“4 位数字”的密码的例子，考虑到用户使用自己的生日做密码的可能性较高，于是就可以把生日日期数值化，如将 0101~1231 保存成字典，进行尝试。

与穷举法相比，由于需要尝试的候选密码较少，意味着攻击耗费的时间比较短。但是，如果字典中没有正确的密码，那就无法破解成功。因此攻击的成败取决于字典的内容。

利用别处泄露的 ID·密码进行攻击（泄露的密码库，处理信息）

##### 对已加密密码的破解

### 点击劫持
点击劫持（Clickjacking）是指利用透明的按钮或链接做成陷阱，覆盖在 Web 页面之上。然后诱使用户在不知情的情况下，点击那个链接访问内容的一种攻击手段。这种行为又称为界面伪装（UI Redressing）。
已设置陷阱的 Web 页面，表面上内容并无不妥，但早已埋入想让用
户点击的链接。当用户点击到透明的按钮时，实际上是点击了已指定
透明属性元素的 iframe 页面。
点击劫持的攻击案例
下面以 SNS 网站的注销功能为例，讲解点击劫持攻击。利用该
注销功能，注册登录的 SNS 用户只需点击注销按钮，就可以从
SNS 网站上注销自己的会员身份。

### DOS攻击
DOS攻击（Denial of Service attack）是一种让运行中的服务呈停止状态的攻击。有时也叫做服务停止攻击或拒绝服务攻击。DoS 攻击的对象不仅限于 Web 网站，还包括网络设备及服务器等。

#### 攻击方式
1. 集中利用访问请求造成资源过载，资源用尽的同时，实际上服务也就呈停止状态。（大量网络请求，无法分辨真实性）
1. 通过攻击安全漏洞使服务停止。

#### DDoS攻击
DDoS攻击（Distributed Denial ofService attack）是多台计算机发起的 DoS 攻击称。DDoS攻击通常利用那些感染病毒的计算机作为攻击者的攻击跳板。

### 后门程序
后门程序（Backdoor）是指开发设置的隐藏入口，可不按正常步骤使用受限功能。利用后门程序就能够使用原本受限制的功能。

#### 类型
可通过监视进程和通信的状态发现被植入的后门程序。但设定在Web应用中的后门程序，由于和正常使用时区别不大，通常很难发现。
1. 开发阶段作为 Debug 调用的后门程序
1. 开发者为了自身利益植入的后门程序
1. 攻击者通过某种方法设置的后门程序



