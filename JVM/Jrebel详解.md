## 部署Jrebel代理服务器教程

拉取代理镜像
```bash
docker pull qierkang/golang-reverseproxy
```
运行代理容器
```bash
docker run --restart=always --network=host -dit --name=jrebel-proxy qierkang/golang-reverseproxy
```
查看是否运行
```bash
docker ps
```
运行
```bash
curl http://localhost:8888
```
使用教程：
```bash
# url格式: 服务器公网ip地址:8888/GUID
$ http://127.0.0.1:8888/1782cd13-a1d1-4a14-9a91-085bb84eafd9
# guid生成地址访问下面这个链接：
$ https://www.guidgen.com/
```
