environment
1.网络平面：management（管理网络）→软件安装，组件通信

　　　　　　provider（提供实例网络）→：提供者网络：直接获取ip地址，实例之间直接互通

　　　　　　　　　　　　　　　　　　　  自服务网络（私有网络）：创建虚拟网络→创建路由器←设置公有网络网关

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　  ————————————————————→内网到外网转发

2.NTP时间服务（集群必备）

3.SQL数据库

4.Memcached：存放token

5.消息队列：协调组件之间操作和状态信息

6.openstack安装包，启用openstack库

　　yum install centos-release-openstack-ocata

　　yum install python-openstackclient

回到顶部
keystone
1.创库授权

2.安装软件包 yum install openstack-keystone httpd(基于http对外提供服务) mod_wsgi(python应用和web服务中间件，支持python应用部署到web服务上)

3.配置数据库访问

4.初始化数据库

5.创建域 openstack domain create

   创建项目 openstack project create

   创建用户 openstack user create

   赋予用户权限 openstack role add --project demo --user demo user

6.请求认证令牌或创建认证脚本

验证：请求认证令牌

回到顶部
glance
1.创库授权

2.创建用户→创建glance用户

   赋权→赋予admin权限

   创建服务实体→创建glance service

3.创建服务端点API：public

　　　　　　　　　  internal

　　　　　　　　　  admin

4.安装软件包 yum install openstack-glance

5.配置数据库访问

   配置keystone访问

6.初始化数据库

验证：openstack image create　　##上传镜像

　　　openstack image list　　##查看镜像信息

回到顶部
nova
controller node
1.创库授权

2.创建用户→创建nova用户

   赋权→赋予admin权限

   创建服务实体→创建nova service

3.创建服务端点API：public

　　　　　　　　　  internal

　　　　　　　　　  admin

4.安装软件包 yum install openstack-nova-api openstack-nova-conductor(连接数据库) openstack-nova-console(访问控制台) openstack-nova-novncproxy(提供控制台服务) openstack-nova-scheduler(computer调度) openstack-nova-placement-api

5.配置数据库访问（database，api_database）

   配置keystone访问

   配置rabbitmq

6.初始化数据库

验证：openstack computer service list　　##查看服务组件

computer node
1.安装软件包 yum install openstack-nova-computer

2.配置keystone访问

   配置rabbitmq

回到顶部
neutron
controller node
1.创库授权

2.创建用户→创建neutron用户

   赋权→赋予admin权限

   创建服务实体→创建neutron service

3.创建服务端点API：public

　　　　　　　　　  internal

　　　　　　　　　  admin

4.安装软件包 yum install openstack-neutron openstack-neutron-ml2 openstack-neutron-linuxbridge ebtables

5.配置数据库访问

   配置keystone访问

   配置rabbitmq

6.配置ml2插件

   配置linuxbridge代理

   配置l3代理

   配置dhcp代理

7.在nova中配置neutron keystone访问（计算使用网络服务）

8.初始化数据库

验证：openstack network agent list　　##查看代理状态

computer node
1.安装软件包 yum install openstack-neutron-linuxbridge ebtables ipset

2.配置keystone访问

   配置rabbitmq

3.配置linuxbridge代理（启用vxlan）

4.在nova中配置neutron keystone访问

回到顶部
lauch instance
1.创建虚拟网络：创建网络

　　　　　　　   创建子网

　　　　　　　   创建路由器：←添加私网子网接口

　　　　　　　　　　　　　   ←添加公有网络网关

2.创建计算方案

3.创建键值对

4.添加安全规则

5.启动实例←计算方案，镜像，网络，安全组，密钥对
