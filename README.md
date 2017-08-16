# openstack_ocata_ansible

For install openstack ocata on ubuntu 16.04.2 with ansible2.3.2.0 （neutron use opensvswitch 2.6.2）

使用ansible 2.3.2.0 在ubunut 16.04.2 64位系统上安装 openstack ocata ，其中neutron网络使用openvswitch 2.6.2

注1：此版本为在线安装版本，安装过程中需要下载依赖包及相应的软件包

注2：此版本支持自定义所有主机名、openstack组件密码，自动修改主机hosts


部署拓扑 ：

ansible----------------------switch
                                |
                                |
                                |
                                |
                                |
         ----------------------------------------------------------
         |              |           |           |         |        |
         |              |           |           |         |        |
         |              |           |           |         |        |
         |              |           |           |         |        |
     controller     compute1   compute2     compute3  compute4   compute5
     
controller节点安装组件如下：

   - ntp
   
   - mariadb
   
   - rabbitmq
   
   - memcache
   
   - shade
   
   - keystone
   
   - glance
   
   - nova
   
   - neutron
   
   - dashboard
   
   - swift
   
   - flavor
        
compute计算节点安装组件如下： 

   - ntp-compute
   
   - nova-compute
   
   - neutron-compute
   
swift存储节点安装组件如下：

   - ntp-compute
   
   - swift-storage 
   
    （在此处安装swift存储节点安装在compute4和compute5上的sdc磁盘上，当然也可以独立安装到单纯的swift存储节点上）

部署步骤：

  【ansible安装】---【关联ssh秘钥】---【配置变量】---【开始安装openstack ocata】


1、【ansible安装】

   请参照ansible官方文档
 
2、【关联ssh秘钥】

   ssh-keygen
 
   ssh-copy-id root@controller 
 
   ...
 
3、【配置变量】

   编辑hosts_common：根据部署规划填写主机ip 此处[all:var]请保持不变
 
   编辑hosts_ocata： 根据部署规划填写主机ip
 
   编辑group_vars/all： 根据实际情况填写
 
4、【开始安装openstack ocata】

   执行 bash cmd_deploy
 
 5、【FAQ】
 
 5.1、脚本可以分步安装
 
    依照先安装common 基础组件部分，然后在安装openstac ocata服务组件
    
 5.1.1【安装common 基础组件部分】
 
    ansible-playbook -i hosts_common deploy_common.yml
    
    如果在需要查看安装过程中输出的详细信息可以执行如下命令:
    
    ansible-playbook -i hosts_common deploy_common.yml -vvv
    
 5.1.2【安装openstac ocata服务组件】
 
    ansible-playbook -i hosts_ocata deploy_ocata.yml
    
    如果在需要查看安装过程中输出的详细信息可以执行如下命令:
    
    ansible-playbook -i hosts_ocata deploy_ocata.yml -vvv
   
5.2、其他问题

   如有其他问题请联系:chen1893@163.com 或者chen1893@gmail.com




     
     
     
     
