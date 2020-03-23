使用方法：

```
mkdir v2ray-agent  &&  \
cd v2ray-agent && \
curl https://raw.githubusercontent.com/hulisang/v2ray-sspanel-v3-mod_Uim-plugin/dev/install.sh -o install.sh && \
chmod +x install.sh && \
bash install.sh
```
想使用旧版将网址里的dev改成master

docker run -d --name=v2ray \
-e speedtest=0  -e api_port=2333 -e usemysql=0 -e downWithPanel=0 \
-e node_id=73 -e sspanel_url=网站WebAPI地址 -e key=Sspanel_Mu_Key  -e MYSQLHOST=数据库ip地址  \
-e MYSQLDBNAME="demo_dbname" -e MYSQLUSR="demo_user" -e MYSQLPASSWD="demo_dbpassword" -e MYSQLPORT=3306 \
--log-opt max-size=10m --log-opt max-file=5 \
--net=host --restart=always \
hulisang/v2ray_v3:go_pay


欢迎补充wiki