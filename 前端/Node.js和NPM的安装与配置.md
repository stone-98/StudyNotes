## 介绍

node.js是javascript的一种运行环境，是对Google V8引擎进行的封装。是一个服务器端的javascript的解释器。
node.js与npm是包含关系，nodejs中含有npm。npm是node.js的包管理器。

## 背景

之前为了个人网站所以安装了Node.js，由于Node.js默认安装了NPM所以目前电脑上已经成功安装了Node.js和NPM。

![image-20230519163108775](https://gitee.com/stone-98/picture-bed/raw/master/202305191651796.png)

目前已经安装

Node.js-v12.19.0

NPM-6.14.8

查看Node.js的安装路径

![image-20230519163457407](https://gitee.com/stone-98/picture-bed/raw/master/202305191651816.png)

目前已经安装到了C盘，就先不进行调整了~

查看NPM的仓库路径，NPM的默认路径是C盘，以后如果使用npm install xxx -g命令，都会将包存储再下面的目录，所以需要对改位置进行调整。

![image-20230519163524888](https://gitee.com/stone-98/picture-bed/raw/master/202305191651760.png)

## 配置

首先在D盘创建对应的文件

- node_global：npm的全局安装路径，其中包含了所有通过npm全局安装的包。当你在命令行中使用`-g`选项进行全局安装时，npm会将包安装到该目录下。
- node_cache：npm的缓存路径，其中缓存了所有通过npm下载的包。当你第一次使用npm下载一个包时，npm会将该包下载到该路径下。当你第二次下载该包时，npm会从缓存中读取该包，而不是重新下载。

![image-20230519163900986](https://gitee.com/stone-98/picture-bed/raw/master/202305191651879.png)

通过相关命令对两个目录进行设置：

```bash
npm config set prefix "D:\DevSoftware\FrontEnd\node_global"
npm config set cache "D:\DevSoftware\FrontEnd\node_cache"
```

接下来进行用户变量的调整：

![image-20230519164535465](https://gitee.com/stone-98/picture-bed/raw/master/202305191651877.png)

新建系统变量：

![image-20230519164925296](https://gitee.com/stone-98/picture-bed/raw/master/202305191652376.png)