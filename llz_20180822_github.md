1.github无法访问的问题

解决这个问题的方法是 更改hosts文件，地址：C:\Windows\System32\Drivers\etc
通过下面这个网站来查找域名的ip
http://ipaddress.com/ip_lookup/

hosts文件最后添加：
192.30.253.113 github.com
151.101.185.194 github.global.ssl.fastly.net
74.125.205.91 dl-ssl.google.com
108.177.112.138 groups.google.com
172.217.4.106 ajax.googleapis.com


2.查看用户名和邮箱地址：
git config user.name
git config user.email
修改用户名和邮箱地址：
git config --global user.name "username"
git config --global user.email "email"

3.ssh key生成步骤：
1）创建SSH Key。在windows下查看/C/User/UserName/.ssh下是否有id_rsa、id_rsa.pub文件，如果没有需要手动生成。
打开git bash，在控制台中输入以下命令。
ssh-keygen -t rsa -C "github注册邮箱" //  C:\Users\tssh\.ssh 下生成 id_rsa id_rsa.pub
2）登录github。打开setting->SSH and GPG keys -->SSH Keys，点击右上角 New SSH key，把生成好的公钥id_rsa.pub中的内容
全部复制到key输入框中，再为当前的key起一个title来区分每个key。

4.将本地仓库上传到github上
git remote add origin git@github.com:lilz0711/git_note.git //关联本地仓库
git push -u origin master   //把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
git push origin master     //此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

5.修改远程仓库地址
git remote set-url origin https://github.com/youname/warehousename.git
git push -u origin master
或者
git remote set-url origin git@github.com:youname/warehousename.git
git push -u origin master

6.查看当前远程仓库使用的那种协议连接：git remote -v

7.移除掉远程仓库的配置：git remote rm origin


8.第一步： 安装Git
第二步： 创建GitHub帐号
第三步： 生成ssh key，使用命令 “ssh-keygen -t rsa -C "your_email@youremail.com"”，your_email是你的email
第四步： 回到github，进入Account Settings，左边选择SSH Keys，Add SSH Key,title随便填，粘贴key
第五步： 测试ssh key是否成功，使用命令“ssh -T git@github.com”，如果出现You’ve successfully authenticated, but GitHub does not provide shell access ，这就表示已成功连上github
第六步： 配置Git的配置文件，username和email
git config --global user.name "your name" //配置用户名
git config --global user.email "your email" //配置email


9.问题
ssh -T git@github.com
ssh: connect to host github.com port 22: Connection timed out
解决方法：
在/C/User/UserName/.ssh目录下创建个文件名为config的文件
用文本编辑器打开，写入以下配置，保存关闭：
Host github.com
User lilz0711   //github账号名
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443

回到命令行窗口再运行ssh -T git@github.com命令，会询问你是否要继续连接，输入yes回车，
如果看到“Hi 你的GitHub名! You've successfully authenticated, but GitHub does not provide shell access.”就表示成功，