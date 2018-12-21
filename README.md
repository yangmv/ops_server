## 运维自动化平台2.0

[运维自动化平台2.0](https://github.com/yangmv/ops_server2.git)


### 1.运维自动化平台概述
#### 1.1 什么是运维自动化？
    操作WEB化，部署自动化，监控自动化
 	操作WEB化：
        以WEB的形式批量下发任务，部署服务。批量执行，集中展示；
        无需SSH到服务器，减少人为操作故障；
        权限控制，如普通用户只可以操作某些模块功能；
        操作可以追溯，某人什么时候执行了什么操作，记录一目了然；

    部署自动化：
     	最早是ssh到目标机器上=>下载部署包=>拷贝到指定位置=>重启服务
    	shell/python脚本自动部署，效率低不易维护
    	使用自动化工具saltstack/ansible/Puppe来部署，效率高易维护
    	私有云Cloud,Container部署image
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/001.png)

	监控自动化：
		集中监控报警/展示，故障恢复自动化，即故障自愈
        如监控可疑IP登录主机报警，可自动踢出用户登录来恢复

#### 1.2 自动化运维发展历程
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/002.png)

#### 1.3 运维自动化与标准规范化的关系
	任何一个企业运行都有很多配套的公司流程标准，否则很多事情将一团乱麻，根本无法推行；
	运维自动化也不例外，实施自动化的前提需要标准规范与流程规范化。
	比如如果系统版本，主机名，IP不统一规范，则可能导致satlstack部署执行，zabbix自动化发现，日志监控部署，应用部署等一些列问题。


### 2. 运维管理自动化系统设计
#### 2.1  运维管理自动化需求
	随着业务规模逐渐增大，运维环境会越来越庞大复杂，这些将驱动使运维工作需要科学规范化的管理。这要求我们用较少的人力、物力资源做更多的工作，必须高效、准确执行任务。
	从运维大环境来开，运维IT综合管理已成为主流运维管理发展方向，运维+开发成为运维发展的大趋势。我们不再局限地依靠某个监控产品或部署工具，而是需要运维自动化，提供体系化运维解决方案，包括监控管理、日志管理、备份管理、CMDB资产信息管理、知识库管理、乃至ITSM信息服务流程管理等。

#### 2.2 运维管理自动化系统架构设计
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/003.png)

#### 2.3 运维管理自动化逻辑架构设计
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/004.png)
开发语言及工具：
- 开发语言: Python
- 后端框架: Django
- 前端框架: Bootstrap  JQuery
- 消息队列：RabbitMQ
- 数据库：MySQL
- 配置工具：Saltstck
- 登录验证：Google Auth


### 3. 登录系统
这里用Django admin管理用户用户组及权限，并且用Google Auth进行二次登录验证，保证登录操作的安全性

![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/005.png)

### 4. 欢迎页

云主机概况：这里调用CMDB API简要显示各云平台主机数量
监控报警概况： 调用Zabbix API显示各区域机房报警状况，有报警相应地区会闪烁

![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/006.png)

### 5. 信息管理

![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/009.png)

### 6. 备份管理
#### 6.1 自动备份管理
    区域：全球区，中国区
    类型：Mysql，Redis ，Mongodb
    游戏：所有业务，指定业务
    状态：开启，关闭
    功能：修改配置，立即备份，失败重试，近期备份耗时统计，历史备份详情
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/013.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/014.png)

#### 6.2 git/svn备份管理
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/015.png)


### 7.自动化部署
#### 7.1 批量任务分发
    这里按业务分类显示出所有主机，选中主机即可批量下发命令
    后端是通过salt-api把任务通过异步的方式下发到所有minon，然后返回结果入库
    所有主机结果一目了然，无需单台主机登录执行，也无需登录salt-server手动执行
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/021.png)

#### 7.2 批量服务器初始化
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/022.png)

#### 7.3 批量服务器部署
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/023.png)

### 8. 公共工具
#### 8.1 付费信息管理
    付费信息到期提醒,域名到期提醒,SSL证书到期提醒
    可自定义到期前多少天报警提醒
    域名到底时间调用第三方API获取
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/007.png)

#### 8.2 IT资源借用系统
IT资源借用记录，做到资源借用可追溯
IT资源借用为归还到期邮件提醒报警，提醒借用人归还物品,减轻IT人员重复性工作
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/008.png)

### 9.openvpn管理
    openvpn管理后台,给公司员工开通vpn账号及重置密码
    openvpn自助管理,用户可以在这里自己修改自己vpn的密码
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/010.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/011.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/012.png)

### 8.Blog文章管理系统
#### 8.1后台管理
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/024.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/025.png)

#### 8.2前台展示
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/026.png)


### 8.SQL审核系统
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/030.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/016.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/018.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/019.png)
![image](https://raw.githubusercontent.com/yangmv/ops_server/master/images/020.png)

## License

Everything is [GPL v3.0](https://www.gnu.org/licenses/gpl-3.0.html).