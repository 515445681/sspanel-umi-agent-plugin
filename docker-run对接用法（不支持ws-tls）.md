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