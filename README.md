# pomelo分布式部署

##环境配置
1. 所有服务器必须是相同类型的操作系统.
2. 必须有相同的用户名.
3. nodejs版本和路径必须是一致的.
4. game-server代码放置的路径也必须是一致的.
   （/opt /nodepro /bridge）
5. 为服务器之间配置公钥保证能SSH相互连接.

## 文件配置

### 说明 
 master-server, gate-server ,connector-server 部署在服务器A，

IP:xx.xx.xx.xx  公网IP:yy.yy.yy.yy

onstage-server, im-server 部署在服务器B IP: zz.zz.zz.zz


### 配置如下
#### master.json
master.json 里面ip和port也相同

{

    "production":{

        "id":"master-server-1",

        "host":"xx.xx.xx.xx",

        "port":3005

    }
    
}

```
#### server.json
{

    "production":{
        "gate":[
            {"id": "gate-server-1", "host": "xx.xx.xx.xx", "clientPort": 3010, "frontend": true}
        ],
        "connector":[
            {"id":"connector-server-1", "host":"xx.xx.xx.xx", "port":4001, "clientPort": 3006, "clientHost":"yy.yy.yy.yy", "frontend": true, "max-connections":1000},
            {"id":"connector-server-2", "host":"xx.xx.xx.xx", "port":4002, "clientPort": 3007, "clientHost":"yy.yy.yy.yy", "frontend": true, "max-connections":1000},
            {"id":"connector-server-3", "host":"xx.xx.xx.xx", "port":4003, "clientPort": 3008, "clientHost":"yy.yy.yy.yy", "frontend": true, "max-connections":1000}
        ],
        "onstage":[
            {"id":"data-server-1", "host":"zz.zz.zz.zz", "port":5001},
            {"id":"data-server-2", "host":"zz.zz.zz.zz", "port":5002},
            {"id":"data-server-6", "host":"zz.zz.zz.zz", "port":5003}
        ],
        "im":[
            {"id":"activity-server-1", "host":"zz.zz.zz.zz", "port":6001},
            {"id":"activity-server-2", "host":"zz.zz.zz.zz", "port":6002},
            {"id":"activity-server-3", "host":"zz.zz.zz.zz", "port":6003}
        ]
    }

}

同理,也可以将connector-server 两台服务器都部署

###启动说明
只在master.json里配置的ip服务器启动(pomelo start)即可.
