# 本机domain的简单规划
1. gitlab   lijiayu.me/gitlab

## 本机hosts配置
```
sudo vi /etc/hosts
127.0.0.1   lijiayu.me
```

## 本机gitlab配置
```
sudo vi /etc/gitlab/gitlab.rb
external_url 'http://lijiayu.me/gitlab'
```
