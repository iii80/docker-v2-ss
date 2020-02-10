# 使用 Docker 快速部署 Shadowsocks-libev + v2ray-plugin

# 条件准备

* 一台墙外VPS；
* 一台安装好 SSH 客户端的本地电脑；
* 如果需要 tls 功能则需要准备一个域名以及一个 Cloudflare 账号。

一、安装 Docker

1.1 以 root 用户登录，执行一键脚本安装 Docker

* 以Debian系为例，升级源并安装软件

```bash
apt-get update && apt-get install -y wget vim
```
* 执行此命令等候自动安装 Docker

```bash
wget -qO- get.docker.com | bash
```
说明：推荐使用 KVM 架构的 VPS，OpenVZ 架构的 VPS 不支持安装 Docker，另外 CentOS 8 不支持用此脚本来安装 Docker。

1.2 对 Docker 的一些命令操作

查看 Docker 安装版本等信息

```bash
docker version
```
启动 Docker 服务
```bash
systemctl start docker
```
查看 Docker 运行状态
```bash
systemctl status docker
```
将 Docker 服务加入开机自启动
```bash
systemctl enable docker
```

二、用 Docker 部署 Shadowsocks-libev + v2ray-plugin over websocket (HTTP)

2.1 创建配置文件

在 /etc 目录下创建 shadowsocks-libev 目录
```bash
mkdir /etc/shadowsocks-libev
```
