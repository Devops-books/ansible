# Command

在远程节点上执行命令。和Shell Module类似，不过不支持$HOME and operations like "<", ">", "|", ";" and "&"。



## 与Shell相同点
* 像Shell一样调用单条命令
  ```yaml
  - command: /sbin/shutdown -t now
  ```

* 和Shell一样，可以在执行命令钱改变目录，并检查文件database不存在时再执行
  ```yaml
  - command: /usr/bin/make_database.sh arg1 arg2
    args:
      chdir: somedir/
      creates: /path/to/database
  ```



## 与Shell不同点

* 与Shell不同，多了一个传参方式：
  ```yaml
  - command: /usr/bin/make_database.sh arg1 arg2 creates=/path/to/database
  ```
* 不支持&&和>>

  下面的写法，没有办法创建~/tmp/test3和~/tmp/test4的
  ```yaml
  - name: test $home
    command: echo "test3" > ~/tmp/test3 && echo "test4" > ~/tmp/test4
  ```
