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
