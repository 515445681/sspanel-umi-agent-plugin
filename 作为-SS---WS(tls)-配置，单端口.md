### 节点配置
添加一个节点

节点类型为 Shadowsocks - V2Ray-Plugin

节点地址写法
以下是节点地址的基本格式：

> 没有CDN的域名或者IP;外部端口;;协议层;附加协议;额外参数

**额外参数：**

额外参数使用 "|" 来分隔。

- **path** 为访问路径
- **server** 为 TLS 域名和用于当节点藏在 CDN 后时覆盖第一个地址
- **host** 用于定义 headers
配置示例：
```
// ws
没有CDN的域名或IP;端口;;ws;;path=/hls/cctv5phd.m3u8

// ws + tls
没有CDN的域名或IP;443;;ws;tls;path=/hls/cctv5phd.m3u8|server=TLS域名

// ws+tls+中转

没有CDN的域名或IP;443;;ws;tls;path=/hls/cctv5phd.m3u8|server=TLS域名|host=TLS域名|relayserver=中转地址|outside_port=中转端口

// ws + tls+CDN
没有CDN的域名或IP;443;;ws;tls;path=/hls/cctv5phd.m3u8|server=这里写CDN的域名

// obfs-http
没有CDN的域名或IP;端口;;obfs;http;
```