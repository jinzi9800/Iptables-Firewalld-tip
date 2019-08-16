# IPtables的bash命令  
---  
## iptables的规则  
通和堵（包含转发）

## iptables的规则链的大分类  
1. PREROUTING   //路由前处理数据包  
2. INPUT    //流入数据包  
3. OUTPUT   //流出数据包  
4. FORWARD  //处理转发数据包  
5. POSTROUTING  //路由后处理数据包  
## iptables的规则执行顺序  
从上到下  
## iptables一般会把来的流量的处理动作分成4类：  
1. ACCEPT //允许流量  
2. REJECT //拒绝流量  
3. LOG  //记录日志  
4. DROP //拒绝流量  
## REJECT和DROP动作的区别  
REJECT 有返回  
DROP 没有搭理  
## 常用命令  
`iptables -L`   //列出所有防火墙规则  
`iptables -F`   //清空已有防火墙规则  
`iptables -P [chain name] [动作]`   //设置默认规则  
`iptables -A`   //在规则链的末尾加入新规则  
`iptables -I [chain name] [num]`   //在某个规则链中头部的第某项加入一条规则  
`iptables -D [chain name] [num]`   //在某个规则链中头部的第某项删除一条规则  
`-s [ip/MASK]`  //匹配来源ip  
`-s ![ip/MASK]`  //匹配来源ip以外的其他ip  
`-d [ip/MASK]`  //匹配目标地址  
`-i [网卡名称]` //匹配流入网卡名称   
`-o [网卡名称]` //匹配流出网卡名称  
`-p [TCP UDP ICMP等协议]`   //通信协议规则  
`--dport [端口号]`  //匹配目标端口号  
`--sport [段口号]`  //匹配来源段口号  
`-j [动作]` //处理方式为【动作】  

## 应用举例  
`iptables -P INPUT DROP`    //把INPUT这个chain的默认规则改为DROP  

`iptables -I INPUT 2 -p icmp -j ACCEPT` //增加INPUT这个chain的第二条防火墙规则设置为所有icmp流量设置为允许流量  

`iptables -D INPUT 1`   //删除INPUT这个chain的第一条规则  

`iptables -I INPUT -s 192.168.111.0/22 -p tcp --dport 22 -j ACCEPT`   //在INPUT这个chain的第一条规则增加一条：允许来自192.168.111.0/22网段的tcp流量匹配到22端口  

`iptables -A INPUT -p tcp --dport 22 -j REJECT`   //在INPUT这个chain后面增加规则：拒绝22端口来的所有流量  


