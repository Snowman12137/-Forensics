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

25	勒索者在数据库中修改了多少个用户的手机号？


26	勒索者在数据库中删除的用户数量为
27	还原被破坏的数据库，分析除技术员以外，还有哪个IP地址登录过管理后台网站？用该地址解压
检材4
28	还原全部被删改数据，用户id为500的注册会员的HT币钱包地址为
29	还原全部被删改数据，共有多少名用户的会员等级为'LV3'
30	还原全部被删改数据，哪些用户ID没有充值记录
31	还原全部被删改数据，2022年10月17日总计产生多少笔交易记录？
32	还原全部被删改数据，该网站中充值的USDT总额为
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMzM2MTIyNTIsLTE5Mjg5Njk4NTYsLT
E2MTU4NzEzNjQsLTE0MjM4NTA5NzksNTUwMjU5ODA4LDI4NjA3
NTgzOSwxMTQ0NDE1MjI5LDEyMzQ3NTcwNjUsODA3MzkwMDg0LD
ExMDY3MTg2MzAsMTQzMTkxNjc0OCwtNDU1Mzc3NTk5LC0yMDgw
MjU2OTE1LC03MjgwNTg1MDEsMTUzMjMzMDUyMywxMjc4MDYwOD
QzLDg3MzI3NDE1NiwtMjQxMDQ0MTA4LDE0ODc2MzI2NjksLTk4
NDIyNTc4MV19
-->