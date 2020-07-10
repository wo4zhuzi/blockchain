## Link
浏览器 [https://filscan.io/#/](https://filscan.io/#/)

rpc [https://docs.lotu.sh/en+api](https://docs.lotu.sh/en+api)

文档  [https://docs.lotu.sh/](https://docs.lotu.sh/)

## cli 操作
运行守护进程 `lotus daemon`

指定目录运行 `lotus --repo="/root/blockchain/lotus_path"  daemon`

查看运行状态 `lotus --repo="/root/blockchain/lotus_path" sync status`

查看当前同步情况 `lotus --repo="/root/blockchain/lotus_path" sync wait`

创建新钱包 `lotus --repo="/root/blockchain/lotus_path" wallet new`  

response : `t1kp2kflqrkp27w3x2ijvxxddxombuddlfgbo2mli`

Do it again

response : `t1swsxo2sqfsdbshhevar3icl65ljkrxncwd4dyai`

[水龙头](https://faucet.testnet.filecoin.io/)

查询钱包地址余额
`lotus --repo="/root/blockchain/lotus_path" wallet balance t1kp2kflqrkp27w3x2ijvxxddxombuddlfgbo2mli`

response : 100

要将FIL从您的默认帐户发送到另一个钱包 :

`lotus send <target> <amount>`

example:
`lotus --repo="/root/blockchain/lotus_path" send t1swsxo2sqfsdbshhevar3icl65ljkrxncwd4dyai 10`

response : `bafy2bzacecickwwe4kzmv36scszc2gaqqzqjjc5wnrtiwk52bwqsesehb7hy6`

view in explorer : [https://filscan.io/#/message/detail?cid=bafy2bzacecickwwe4kzmv36scszc2gaqqzqjjc5wnrtiwk52bwqsesehb7hy6](https://filscan.io/#/message/detail?cid=bafy2bzacecickwwe4kzmv36scszc2gaqqzqjjc5wnrtiwk52bwqsesehb7hy6)

## rpc 操作

查看头信息 ：

```
curl -X POST \
     -H "Content-Type: application/json" \
     --data '{ "jsonrpc": "2.0", "method": "Filecoin.ChainHead", "params": [], "id": 3 }' \
     'http://127.0.0.1:1234/rpc/v0'
```

广播 :

```
curl -X POST \
     -H "Content-Type: application/json" \
     --data '{ "jsonrpc": "2.0", "method": "Filecoin.MpoolPush", "params": ["***"], "id": 3 }' \
     'http://127.0.0.1:1234/rpc/v0'
```
     
 >rpc接口广播需要 write 的权限
 
 
设置 jwt 权限
`lotus auth api-info --perm write`
     
加上授权标头进行广播

```
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $(cat ~/.lotusstorage/token)" \
     --data '{ "jsonrpc": "2.0", "method": "Filecoin.ChainHead", "params": [], "id": 3 }' \
     'http://127.0.0.1:1234/rpc/v0'
```

>注意 ：如果想设置rpc可以外网访问修改 config.toml
`[API]
  ListenAddress = "/ip4/0.0.0.0/tcp/1234/http"`
  

## 扫链程序

安装 ： 
`git clone https://github.com/ipfs-force-community/filscan-backend.git`

`cd filscan-backend`

`make`

`cd conf && vim app.conf`

修改如下

```
mongoHost = "127.0.0.1:27017"
mongoUser = ""
mongoPass = ""
mongoDB   = "filscan"
lotusGetWay="127.0.0.1:1234"
```

执行

`./filscan-backend`
  
