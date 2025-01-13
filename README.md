### 1、安装docker
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
```
```bash
sudo sh get-docker.sh
```
### 2、安装xdd
Debian：
```bash
apt-get install xxd
```
### 3、拉取镜像
```bash
docker pull ellermister/nginx-mtproxy:latest
```

### 4、自定义安装
获取secret
```bash
secret=$(head -c 16 /dev/urandom | xxd -ps)
```
查看secret
```bash
echo $secret
```
从 https://t.me/MTProxybot 获取tag
```bash
tag="123450c81a27491a867fad333a4e7dbd"
```
添加伪装
```bash
domain="cloudflare.com"
```
部署nginx-mtproxy 添加TAG
```bash
docker run --name nginx-mtproxy -d -e tag="$tag" -e secret="$secret" -e domain="$domain" -e ip_white_list="OFF" -p 8080:80 -p 8443:443 ellermister/nginx-mtproxy:latest
```
部署nginx-mtproxy不添加TAG
```bash
docker run --name nginx-mtproxy -d -e secret="$secret" -e domain="$domain" -e ip_white_list="OFF" -p 8081:80 -p 8443:443 ellermister/nginx-mtproxy:latest
```
部署nginx-mtproxy添加白名单不添加TAG
```bash
docker run --name nginx-mtproxy -d -e secret="$secret" -e domain="$domain" -e ip_white_list="OFF" -p 8081:80 -p 8443:443 ellermister/nginx-mtproxy:latest
```
ip_white_list 可选参数为:

IP 允许单个 IP 访问

IPSEG 允许 IP 段访问

OFF 允许所有 IP 访问

-p端口可自定义

如：-p 8443:443改为-p 1234:443

如果无需tg推广可去掉-e tag="$tag" 

创建完毕后，查看访问链接：

```bash
docker logs nginx-mtproxy
```
### 如果开启白名单，需要浏览器打开一下链接

```bash
http://ip/add.php
```
### service
Stop service / 停止服务
```bash
docker stop nginx-mtproxy
```
Start service / 启动服务
```bash
docker start nginx-mtproxy
```
Restart service / 重启服务
```bash
docker restart nginx-mtproxy
```
Delete service / 删除服务
```bash
docker rm nginx-mtproxy
```
Auto Run / 开机自启
```bash
docker update --restart=always nginx-mtproxy
```
更多使用请参考：https://hub.docker.com/r/ellermister/nginx-mtproxy
