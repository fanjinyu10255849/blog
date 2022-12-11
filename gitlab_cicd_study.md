#gitlab cicd
## 安装配置gitlab
参考官方教程
https://about.gitlab.com/install/#ubuntu
步骤如下：
1. 安装依赖
```
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
sudo apt-get install -y postfix
```
2. 安装gitlab
```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
sudo EXTERNAL_URL="https://gitlab.example.com" apt-get install gitlab-ee
```
3. 使用设置号的url登陆
浏览器输入url，登陆gitlab
账号为root
密码通过如下方式查看
```
sudo cat /etc/gitlab/initial_root_password
```
4. 修改配置
gitlab.rb官方模板
https://gitlab.com/gitlab-org/omnibus-gitlab/-/blob/master/files/gitlab-config-template/gitlab.rb.template
修改方式如下
```
sudo vim /etc/gitlab/gitlab.rb
sudo gitlab-ctl reconfigure
```
5. 服务控制
```
sudo gitlab-ctl start
sudo gitlab-ctl status
sudo gitlab-ctl stop
```
6. 


## 遇到的问题
##### git clone有问题
```
fanjinyu@ubuntu:~/workspace$ git clone git@gitlab.com:blog_fjy/blog.git
Cloning into 'blog'...
Connection closed by 172.65.251.78 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
解决方法

参考
https://gitlab.com/gitlab-org/gitlab-foss/-/issues/43185

```
ssh-keygen -lf ~/.ssh/id_rsa.pub
```
重试，遇到另一个问题
```
Connection reset by 172.65.251.78 port 22
```
解决方法
```
ssh -T -p 443 gitlab.com
```