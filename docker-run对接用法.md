docker run用法

```
docker run -d --name=v2ray \
-e speedtest=6  -e api_port=2333 -e usemysql=0 -e downWithPanel=0 \
-e node_id=65 -e sspanel_url=https://xxxx.com -e key=mukey  -e MYSQLHOST=数据库ip地址  \
-e MYSQLDBNAME="demo_dbname" -e MYSQLUSR="demo_user" -e MYSQLPASSWD="demo_dbpassword" -e MYSQLPORT=3306 \
--log-opt max-size=10m --log-opt max-file=5 \
--network=host --restart=always \
hulisang/v2ray_v3:go_pay
```


如果用到tls需要caddy反代的支持

## 第一步安装caddy
```
curl https://getcaddy.com | bash
```
## 第二步新建/www/root/index.html

这一步是是建立伪装站点可自行发挥，v2ray-sspanel-v3-mod_Uim-plugin/Docker/Caddy_V2ray/里有我提供的站点文件

## 第三步创建etc/caddy/Caddyfile
写入
```
域名:443
{
  root /www/root
  index index.html
  log ./caddy.log
  proxy /v2ray 127.0.0.1:10550 {
    websocket
    header_upstream -Origin
  }
  gzip
  tls 邮箱 {
    protocols tls1.2 tls1.3
    # remove comment if u want to use cloudflare (for DNS challenge authentication)
    # dns cloudflare
  }
}
```
自行修改参数后保存

## 最后运行caddy
```
caddy --conf /etc/caddy/Caddyfile
```
后台运行可用screen或nohup
