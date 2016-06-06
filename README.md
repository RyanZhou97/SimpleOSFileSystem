#简单文件系统的实现

要求
---

- 内存中开辟一块`虚拟磁盘空间`作为文件存储分区，在其上实现一个简单的基于**多级目录**的`单用户单任务系统`中的文件系统。

- 在退出该文件系统的使用时，虚拟文件系统以一个文件的方式保存到磁盘中，以便下次可以把它恢复到内存的虚拟存储空间

实际实现
---

- 以上两点均实现
- 能处理绝对路径和相对路径的**命令**
    - 例如 :
        -  `cd /home/zy/Desktop/` 这样的绝对路径
        -  `cd ../hah/1/2`      这样的相对路径
    - `mkdir`,`rmdir`,`cd`,`creat`,`rm`均支持
    - `open_path` 是`open`的升级版，也是支持上述函数实现的主要函数。
    
- 包装`open`,`read`,`close`实现了一个`cat`直接打印文件内容。
    - 检查文件是否打开，如果打开了直接进行下一步，没有就打开
    - `read`出所有内容
    - 如果之前不是打开的那么就关闭文件。

截图
---

- 建立目录树，`/home`是用户的根目录

    `/home`下有`/zy`

    `/zy`下有 `/Documents`,`/Desktop`,`/Viedeos`,`Music`等

    ![](http://i.imgur.com/b9JOGKn.png)

- 在`/home/zy/Documents`目录下建立一个文件`Hello.txt`
    - 并输入内容`Hello World!Fisrt`,能正确显示长度和文件内容。
    - 测试了`creat`,`open`,`close`，`read`,`write`等基本用法

    ![](http://i.imgur.com/oTGbTkL.png)
   
- 利用`creat /home/zy/hellozy.txt` 在`/home/zy`下建立了一个`hellozy.txt`
    - 测试了`creat`在**路径**下的用法 

    ![](http://i.imgur.com/T1JBufA.png)

- 测试了`mkdir`,`cd`,`rmdir`在路径下也能正常工作。其余几个类似的同理，OVER
    
    ![](http://i.imgur.com/rMrMpyM.png)
