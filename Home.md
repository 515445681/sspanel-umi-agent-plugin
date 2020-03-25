使用方法：

```
mkdir v2ray-agent  &&  \
cd v2ray-agent && \
curl https://raw.githubusercontent.com/hulisang/v2ray-sspanel-v3-mod_Uim-plugin/dev/install.sh -o install.sh && \
chmod +x install.sh && \
bash install.sh
```
想使用旧版将网址里的dev改成master

docker run用法

第一个docker（v2ray主程序）
```
docker run -d --name=v2ray \
-e speedtest=6  -e api_port=2333 -e usemysql=1 -e downWithPanel=0 \
-e node_id=1  -e MYSQLHOST=数据库ip地址  \
-e MYSQLDBNAME=demo_dbname -e MYSQLUSR=demo_user -e MYSQLPASSWD=demo_dbpassword -e MYSQLPORT=3306 \
--log-opt max-size=10m --log-opt max-file=5 \
--net=host --restart=always \
hulisang/v2ray_v3:go_pay
```

第二个docker（caddy镜像）
```
docker run -d --name=caddy \
-e CLOUDFLARE_EMAIL=${cloudflare_email} \
-e CLOUDFLARE_API_KEY=${cloudflare_key} \
-e V2RAY_DOMAIN=${v2ray_domain} \
-e V2RAY_PATH=/v2ray \
-e V2RAY_EMAIL=邮箱 \
-e V2RAY_PORT=10550 \
-e V2RAY_OUTSIDE_PORT=443 \
--log-opt max-size=10m --log-opt max-file=5 \
--network=host --restart=always \
hulisang/v2ray_v3:caddy
```

欢迎补充wiki