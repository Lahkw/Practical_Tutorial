创建一个github仓库并上传一个文件：

#### 1、首先安装git[Windows下只需要在官网下载即可

#### 链接

#### [[](https://git-scm.com/download/win)]

sudo apt install git

#### 2、首次需要配置环境

需要的有用户名、邮箱

git config --global user.name   **用户名**

git config --global user.email    **邮箱**

*此处的用户名和邮箱会在.gitconfig出现，亦可按照那个格式直接编写*

#### 3、在目标位置创建文件夹进行初始化

mkdir **test**

git init

4、创建一个文件

touch **test.c**

#### 5、将文件存在缓存区

git add **test.c**

#### 6、对文件进行编写&重写

git commit -m **需要输入的内容**

git commit --amend

#### 7、上传 --创建GitHub仓库并进行远程连接

1.在进行这一步时首先进行一个ssh公钥的设置

ssh-keygen -t rsa -C "_______________________"（下划线中填入自己的邮箱）

会生成一个.ssh文件![image-20230801200255346](C:\Users\ct202\AppData\Roaming\Typora\typora-user-images\image-20230801200255346.png)

此.ssh文件中有id_res和id_rea.pub分别代表着私有密钥、公有密钥，此处需要公有密钥

将其打开并复制下来然后在GitHub的设置中选择 **SSH and GPG keys**

创建新的SSH keys 即绿色的**New SSH key**将公钥复制进去完成即可



2.其次登录自己的GitHub进行创建仓库(*这一步什么时候操作都可，在最后要将文件推送到远程时有即可*)

![image-20230801160602490](C:\Users\ct202\AppData\Roaming\Typora\typora-user-images\image-20230801160602490.png)

3.然后进行远程连接

git remote add origin   **仓库的ssh代码**（非SSH key）

![image-20230801200939423](C:\Users\ct202\AppData\Roaming\Typora\typora-user-images\image-20230801200939423.png)

4.最后推送到远程

git push -u origin master



以上参考csdn两篇文章

[](https://blog.csdn.net/bjbz_cxy/article/details/116703787)

[](https://blog.csdn.net/qq1713802040/article/details/124831253?app_version=6.0.0&code=app_1562916241&csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22124831253%22%2C%22source%22%3A%22ehsheh%22%7D&uLinkId=usr1mkqgl919blen&utm_source=app)