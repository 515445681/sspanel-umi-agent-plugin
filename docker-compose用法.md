新建docker-compose.yml文件写入
```
version: '2'
services:
  v2ray:
    image: ${docker_addresss}
    restart: always
    network_mode: "host"
    environment:
      sspanel_url: "${sspanel_url}"
      key: "${sspanel_key}"
      speedtest: ${sspanel_speedtest}
      node_id: ${sspanel_node_id}
      api_port: ${v2ray_api_port}
      downWithPanel: ${v2ray_downWithPanel}
      LDNS: "${LDNS}"
      TZ: "Asia/Shanghai"
      MYSQLHOST: ${v2ray_mysqlhost}
      MYSQLDBNAME: ${v2ray_mysqldbname}
      MYSQLUSR: ${v2ray_myqluser}
      MYSQLPASSWD: "${v2ray_mysqlpassword}"
      MYSQLPORT: ${v2ray_mysqlport}
      PANELTYPE: ${v2ray_paneltype}
      usemysql: ${v2ray_usemysql}
      CF_Key: ${cloudflare_key}
      CF_Email: ${cloudflare_email}
      MUREGEX: "${MUREGEX}"
      MUSUFFIX: "${MUSUFFIX}"
      ProxyTCP: ${ProxyTCP}
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
      - V2RAY_DOMAIN=${v2ray_domain}
      - V2RAY_PATH=${v2ray_path}
      - V2RAY_EMAIL=${v2ray_email}
      - V2RAY_PORT=${v2ray_local_port}
      - V2RAY_OUTSIDE_PORT=${caddy_listen_port}
    network_mode: "host"
    volumes:
      - ./.caddy:/root/.caddy
      - ./Caddyfile:/etc/Caddyfile
      - /etc/localtime:/etc/localtime:ro
```
参数自行调整
在docker-compose.yml文件目录下执行doccker-compose up -d