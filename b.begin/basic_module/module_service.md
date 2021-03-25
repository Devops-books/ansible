# Service

管理远程节点上的服务，什么是服务呢，比如httpd、sshd、nfs、crond等。



## 启动、停止、重启和重新加载服务

* 启动httpd服务

  ```yaml
  - service:
      name: httpd
      state: started
  ```

* 停止服务

  ```yaml
  - service:
      name: httpd
      state: stopped
  ```

* 重起服务

  ```yaml
  - service:
      name: httpd
      state: restarted
  ```

* 重载服务

  ```yaml
  - service:
      name: httpd
      state: reloaded
  ```



## 设置开机启动



```yaml
- service:
    name: httpd
    enabled: yes
```



## 启动网络服务下的接口

```yaml
- service:
    name: network
    state: restarted
    args: eth0
```
