

### 1.SSH登录

```nginx
// 进入家目录
cd ~
// 删除.ssh 目录
rm -rvf .ssh
// 运行命令生成.ssh 密钥目录
ssh-keygen -t rsa -C atguigu2018ybuq@aliyun.com
//进入.ssh 目录查看文件列表
cd .ssh
cat id_rsa.pub
//复制 id_rsa.pub 文件内容
```

![image-20200913210535545](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200913210535545.png)

![git](https://github.com/pavi-du/note/blob/master/git.png)

### 2.merge后

```
git merge 解决冲突后：git commit -m ""//不用加文件名
```

### 3.基本流程

```nginx
// address 仓库名
git clone address
// 查看别名
git remote -v 
// 创建别名 name：别名
git remote add name address
// 推送
git push name master
git pull name master

```

