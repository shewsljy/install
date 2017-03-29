# 安装 GitLab Community Edition (CE)
使用国内清华大学提供的镜像安装,注意
```
GitLab packages 是专为64位系统编译的
```

## 安装配置依赖项
如想使用Postfix来发送邮件,在安装期间请选择'Internet Site'
```
sudo apt install curl openssh-server ca-certificates postfix
```

## 添加GitLab仓库(国内镜像),并安装到服务器上
1. 信任GitLab的GPG公钥
```
curl https://packages.gitlab.com/gpg.key 2> /dev/null | sudo apt-key add - &>/dev/null
```
2. 添加国内GitLab仓库源,文本框中内容写进 `/etc/apt/sources.list.d/gitlab-ce.list`
```
deb https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu xenial main
```

## 安装gitlab-ce
```
sudo apt update
sudo apt install gitlab-ce
```
## 启动GitLab
```
sudo gitlab-ctl reconfigure
```
## 使用浏览器访问GitLab
配置文件为`/etc/gitlab/gitlab.rb`,初次登录默认root用户,并且要设置密码`she1qaz@WSX`
```
external_url 'http://jiayu'
gitlab_rails['time_zone'] = 'Asia/Shanghai'
```
http://jiayu

## 屏蔽Gravatar头像
将`http://jiayu/admin/application_settings`中的`Account and Limit Settings`下面`Gravatar enabled`的选项钩去掉

# 安装 GitLab Runner
使用国内清华大学提供的镜像安装,注意
```
GitLab packages 是专为64位系统编译的
```

## 添加GitLab仓库(国内镜像),并安装到服务器上
1. 信任GitLab的GPG公钥
```
curl https://packages.gitlab.com/gpg.key 2> /dev/null | sudo apt-key add - &>/dev/null
```
2. 添加国内GitLab仓库源,文本框中内容写进 `/etc/apt/sources.list.d/gitlab-ci-multi-runner.list`
```
deb https://mirrors.tuna.tsinghua.edu.cn/gitlab-ci-multi-runner/ubuntu xenial main
```

## 安装gitlab-runner
```
sudo apt update
sudo apt install gitlab-ci-multi-runner
```
## 注册gitlab-runner
`gitlab-ci token`在`http://jiayu/admin/runners`有
```
sudo gitlab-ci-multi-runner register
Running in system-mode.

Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
http://jiayu
Please enter the gitlab-ci token for this runner:
dL6t9XPyxeaiPgaX_1-h
Please enter the gitlab-ci description for this runner:
[jiayu]: This is a Shared Runner
Please enter the gitlab-ci tags for this runner (comma separated):
test       
Whether to run untagged builds [true/false]:
[false]: false
Whether to lock Runner to current project [true/false]:
[false]: false
Registering runner... succeeded                     runner=dL6t9XPy
Please enter the executor: virtualbox, docker-ssh+machine, shell, ssh, docker+machine, kubernetes, docker, docker-ssh, parallels:
shell
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!
```
