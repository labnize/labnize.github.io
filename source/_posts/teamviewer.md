title: 内网配置Teamviewer实现mac局域网远程PC桌面
date: 2017-06-06 10:52:19
tags:
---

用到TeamViewer，源于最近刚入职一家整天强调信息安全的某国企，然后内部使用的基础类工具（自研），都不支持mac系统，还不允许装双系统。所以配备的台式机仅用于基础类工具，开发仍使用mac笔记本。

当然，不要在意那么多细节，下面进入正题。。

---

### 首先，因局域网是内网，需要配置代理才能使用TeamViewer，下面讲一下如何给mac配置网络代理。

#### 1. 打开“网络偏好设置”，选中已连接的网络。

![proxy1](/img/proxy1.png)

​    



#### 2. 点击“高级”，选中“代理”，去掉默认的“自动代理配置”，勾选“网页代理(HTTP)”和“安全网页代理(HTTPS)”，配置代理服务器。点击“好”。

![proxy2](/img/proxy2.png)

​         



#### 3. 选择“DNS”，删除所有DNS，点击“好”。

##### ![proxy3](/img/proxy3.png)

​         



#### 4. 最后点击“应用”。







---

### 下面是如何配置TeamViewer实现远程控制



#### 1. 为了防止PC会自动获取IP，所以需要给远程共享的PC配置固定IP，共享的PC和本地笔记本必须在同一网段上。

![teamviewer1](/img/teamviewer1.jpg)

   



#### 2. PC上服务站配置，点击“设置无人值守访问…”

![teamviewer2](/img/teamviewer2.jpg)

​       



#### 3. 点击下一步

![teamviewer3](/img/teamviewer3.jpg)

​       



#### 4. 定义个人密码

![teamviewer4](/img/teamviewer4.jpg)

​       



#### 5. 点击“应用”

![teamviewer5](/img/teamviewer5.jpg)

​       



#### 6. 选择“我不想创建TeamViewer帐户”

![teamviewer6](/img/teamviewer6.jpg)

​       



#### 7. 选择“其他”->"选项"

![teamviewer7](/img/teamviewer7.jpg)

​       



#### 8. 在“常规”里，选择“随Windows一同启动TeamViewer”；“呼入的lan连接”选择“接受”

![teamviewer8](/img/teamviewer8.jpg)

​      



#### 9. 在“安全性”里，“Windows登录”选择“允许所有用户”，然后点击“确定”

![teamviewer9](/img/teamviewer9.jpg)

​      



#### 10. 本地mac配置

![teamviewer10](/img/teamviewer10.jpg)

