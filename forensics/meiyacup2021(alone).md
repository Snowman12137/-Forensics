


# 2021美亚杯wp-（个人赛）
>#### 美亚杯第七届电子取证大赛-个人赛
>本次比赛共1 个段落, 62 个小题, 总共114分检材方面，个人赛由一个加密容器和一个update更新的压缩包组成，检材量和题量非常大，很多检材的报告文件都加了压缩包，需要挨个解压，比武时间相对紧凑，想获得好成绩，需要前期认真分析官方给的案情信息，准备多台高性能计算机便于取证分析。
>#### 案情资料揭晓
>资格赛2021年10月某日早上，本市一个名为"大路建设"的高速公路工地主管发现办公室的计算机被加密并无法开启，其后收到了勒索通知。考虑到高速公路的基建安全，主管决定报警。警方调查人员到达现场取证，发现办公室内有三部个人计算机，通过一个老款路由器接入互联网。
经调查相关电子证据后，警方怀疑一位本地男子–阿力士与本案有关，并将他拘捕。现在你被委派处理这起案件,请由以下资料分析阿力士在本案中的违法犯罪行为, 并还原事件经过。

>镜像下载链接：链接：https://pan.baidu.com/s/1EBGxpAyjXGyogyMw7o_Qsg?pwd=ngzs
>提取码：ngzs
>个人赛压缩包
>+2FL?89MajaHRE5Q9pp%@V2rwnwK-M=KD4Y55#vyBq99JhT22$%Z2ebkaTNn^s-n
>加密容器
>HfsCk]<eUqc5Q{(DG$ugiGlt8ezGdaZ>!pQC-H\5BAc^gBo/^qq)/i21ufiN@H"Y


##一、赛前准备
下好个人镜像
![输入图片说明](/imgs/2022-11-02/pRFC72ZuqrE6YXSV.png)
image_updated在后面会用到


阅读文档得到关系图，镜像文件关系如下图所示（不得不说美亚杯的材料真实性实在是太棒了）
![输入图片说明](/imgs/2022-11-03/Qu9yP4xGBMMeip9g.jpeg)

看了下调差报告（PDF）只是一些基本信息，并且还是全英的，而且还有繁体字，推断这是一件香港的案子。

开始做题

## 1-9题
1-9题关键字，工地主管，电话，手机等关键字可以分析出我们要用的是image-VTM-VTM_iphone6
>1. [单选题] 工地主管电话的微信账号是什么? (1分)
A. Kasier751111
B. Kasierlee751111
C. Kasierlee
D. 以上皆非
>2. [填空题] 工地主管的隔空投送装置编号是什么? (请以英文全大写及阿拉伯数字回答) (1分)
> 3. [单选题] 工地主管电话的哪一个应用程序有关于于经纬度24.490474, 118.110220的纪录? (2分)
A. 照片
B. WhatsApp
C. Apple Maps
D. 以上皆非
>4. [多选题] 工地主管的手提电话中下列哪些数据正确? (1分)
A. iOS 版本为 12.5.4
B. IMEI 为 454120637213361
C. Apple ID 为 kaiserlee3660@gmail.com
D. 手机曾经安装dropbox 应用程序
>5. [填空题] 工地主管的电话最常使用的浏览器是什么? (请以英文全大写回答) (1分)
>6. [单选题] 工地主管的电话连接过哪一个WiFi? (1分)
A. Kaiser Lee
B. Kaiser
C. Free Wifi
D. Kaiser Home
>7. [多选题] 工地主管与Alex Chan的Whatsapp 对话中，曾提及以下哪个TeamViewer的用户号码? (3分)
A. 435334881
B. 453851521
C. 435475200
D. 456874155
E. 435270306
>8. [填空题] 工地主管的WhatsApp中有多少个黑名单的记录? (请以阿拉伯数字回答) (2分)
>9. [多选题] 以下哪个蓝牙装置的Uuid 曾连接过工地主管的手机? (2分)
A. 7F1FE70D-2B15-C245-853D-4196F13CC446
B. 1B057C1D-83D3-99A6-D2B1-EC54846C7CEE
C. 134ACD1-83D3-99A6-D2B1-EC54846C7CEE
D. 7D1BE70D-2C16-D246-851D-491613DD776

解压以后得到三个文件
![输入图片说明](/imgs/2022-11-03/p0RlE1hya2BwADgc.png)
这个.exe文件貌似是一个阅读器，并且.ufdr后缀的文件就是这个阅读器打开文件的格式，打开，在tool-setting里面可以设置语言
![输入图片说明](/imgs/2022-11-03/qJRFYVPaJJnOT4VZ.png)
打开以后发发现这个页面
>1. [单选题] 工地主管电话的微信账号是什么? (1分)**C**
A. Kasier751111
B. Kasierlee751111
C. Kasierlee
D. 以上皆非
我们在这里面找到了一个较为WhatsApp的用户，在网上搜索以后发现是香港用的微信，所以选**C**
![输入图片说明](/imgs/2022-11-03/U9E7DnXnCLICcklq.png)

>2. [填空题] 工地主管的隔空投送装置编号是什么? (请以英文全大写及阿拉伯数字回答) (1分)
>**780F624DF099**
>最后在这里找到了一个叫AirDrop ID 的设备![输入图片说明](/imgs/2022-11-03/2rKck55V2XmD2Qaj.png)
>PS(这叫隔空投送装置？？？emmmm也合理)![输入图片说明](/imgs/2022-11-03/0ja2XfEhIzEMCqpS.png)

>3. [单选题] 工地主管电话的哪一个应用程序有关于于经纬度24.490474, 118.110220的纪录? (2分)**C**
A. 照片
B. WhatsApp
C. Apple Maps
D. 以上皆非
找了下WhatsApp没有位置记录，直接搜索了下map找到了记录
![输入图片说明](/imgs/2022-11-03/HxMeSoVNWnG1GWNs.png)
>4. [多选题] 工地主管的手提电话中下列哪些数据正确? (1分)**AC**
A. iOS 版本为 12.5.4
B. IMEI 为 454120637213361
C. Apple ID 为 kaiserlee3660@gmail.com
D. 手机曾经安装dropbox 应用程序
![输入图片说明](/imgs/2022-11-03/Q7kDAXbZ41nePPke.png)
D搜了一下没有

>5. [填空题] 工地主管的电话最常使用的浏览器是什么? (请以英文全大写回答) (1分)
>**SAFARI**
>发现记录全是这个软件![输入图片说明](/imgs/2022-11-03/pL0f2GEGPZEYaahl.png)

>6. [单选题] 工地主管的电话连接过哪一个WiFi? (1分)**A**
A. Kaiser Lee
B. Kaiser
C. Free Wifi
D. Kaiser Home
>![输入图片说明](/imgs/2022-11-03/yhsJPEvL6nm1bLiY.png)

>7. [多选题] 工地主管与Alex Chan的Whatsapp 对话中，曾提及以下哪个TeamViewer的用户号码? (3分)**ACE**
A. 435334881
B. 453851521
C. 435475200
D. 456874155
E. 435270306
>对话里面搜索teamviewer然后细细找一下
![输入图片说明](/imgs/2022-11-03/NLnKhBiX3gLy0ruG.png)

>8. [填空题] 工地主管的WhatsApp中有多少个黑名单的记录? (请以阿拉伯数字回答) (2分)
>![输入图片说明](/imgs/2022-11-03/9X15iLdLI2HZW5xy.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTUyNDQzMzEsMTI0OTE2NDA1NSw0Mz
UxMzM0NjcsLTE2MTI4MjM1MzMsMTg2NzIyMTc4NywtMTQ4NDg4
NzI1MSwxODk1MDUyMTk5LDEwMjAxNDQwMTgsNzYxNjE0NTgzXX
0=
-->