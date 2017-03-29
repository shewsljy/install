# atom

## atom镜像地址
- 国外[cnpmjs](https://cnpmjs.org/mirrors/atom/)
- 国内[taobao](http://npm.taobao.org/mirrors/atom/)

## atom本地安装插件
1. 在[官网插件库](https://atom.io/packages)里查找需要安装的插件(这里以git-plus为例)，点击"Repo"找到其在GitHub的路径，并拷贝
2. 在本机路径下`mkdir -p /home/jiayu/.atom/src_packages`(如我"/home/jiayu/.atom/src_packages/")，执行命令`git clone https://github.com/akonwi/git-plus.git`
3. 进入插件源码目录(如我"/home/jiayu/.atom/src_packages/git-plus")，执行命令`apm install git-plus`，待输出以下信息`Installing git-plus to /home/jiayu/.atom/packages ✓`则表示插件安装完毕
