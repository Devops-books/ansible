# 安装Ansible

这里以RedHat系Linux为例，其他系统请参考ansible的官网



## 管理员的电脑上：


* 安裝Ansible软件

```shell
# Redhat/CentOS Linux上，Ansible目前放在的epel源中
# Fedora默认源中包含ansible，直接安装包既可
sudo yum install epel-release 
sudo yum install ansible -y 
# 离线下载
yum install --downloadonly --downloaddir=/opt/ansible epel-release
yum install --downloadonly --downloaddir=/opt/ansible  ansible
```



* 配置Ansible管理节点和主机的连接

其实就是配置从**管理节点到远程主机**之间基于key（无密码的方式）的**SSH连接**：

```shell
# 服务端生成ssh key
ssh-keygen # 连续回车或者输入指定密码
```

```shell
# 拷贝ssh key到远程主机（被控主机），ssh的时候就不需要输入密码了 
# ssh-copy-id remoteuser@remoteserver 
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.8.188
```

```shell
# ssh的时候不会提示是否保存key
ssh-keyscan remote_servers >> ~/.ssh/known_hosts
```

验证下有没有装好: 在管理节点执行下面的ssh命令，既**不需要输入密码**，也**不会提醒你存储key**，那就成功啦。

```shell
ssh remoteuser@remoteserver
ssh root@192.168.8.188
```



- 使用密码连接

```shell
# 主机的清单中配置用户名密码
[test-host]
172.16.60.220 ansible_ssh_user=root ansible_ssh_pass=123456 ansible_ssh_port=22
```



## 被管理的远程主机：

不需要安装特殊的包，只需要python>2.4，RedHat Linux一般安装方式都自带。

- 执行解压命令的时候要有界面命令包`nzip`。
- 执行同步命令要有同步命令包`rsync`。

