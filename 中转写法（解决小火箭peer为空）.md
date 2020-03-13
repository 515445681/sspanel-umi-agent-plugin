中转用法是在前端节点地址后面加上|outside_port=中转端口|relayserver=中转ip
例：
// ws完整写法示例：
```
xxxxx.com;10550;16;ws;;path=/xxxxx|host=oxxxx.com|outside_port=中转端口|relayserver=中转ip
```
其他写法自行添加
前提：已经将中转ip通过iptables、socat、brook等方法完成中转落地