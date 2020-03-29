新建docker-compose.yml文件写入
```
version: '2'
services:
  v2ray:
    image: hulisang/v2ray_v3:go_pay
    restart: always
    network_mode: "host"
    environment:
      sspanel_url: "sspanel_url"
      key: "mukey"
      speedtest: 6
      node_id: node_id
      api_port: 2333
      downWithPanel: 0
      LDNS: localhost
      TZ: "Asia/Shanghai"
      MYSQLHOST: host
      MYSQLDBNAME: mysqldbname
      MYSQLUSR: myqluser
      MYSQLPASSWD: mysqlpassword
      MYSQLPORT: 3306
      PANELTYPE: 0
      usemysql: 0
      CF_Key: cloudflare_key
      CF_Email: cloudflare_email
      MUREGEX: "%5m%id.%suffix"
      MUSUFFIX: "microsoft.com"
      ProxyTCP: 0
    volumes:
      - /etc/localtime:/etc/localtime:ro
    logging:
      options:
        max-size: "10m"
        max-file: "3"
  caddy:
    image: hulisang/v2ray_v3:caddy
    restart: always
    environment:
      - ACME_AGREE=true
      #      if u want to use cloudflare (for DNS challenge authentication)
      #      - CLOUDFLARE_EMAIL=xxxxxx@out.look.com
      #      - CLOUDFLARE_API_KEY=xxxxxxx
      - V2RAY_DOMAIN=v2ray_domain
      - V2RAY_PATH=/v2ray
      - V2RAY_EMAIL=v2ray_email
      - V2RAY_PORT=10550
      - V2RAY_OUTSIDE_PORT=443
    network_mode: "host"
    volumes:
      - ./.caddy:/root/.caddy
      - ./Caddyfile:/etc/Caddyfile
      - /etc/localtime:/etc/localtime:ro
```
参数自行调整
在docker-compose.yml文件目录下执行doccker-compose up -d