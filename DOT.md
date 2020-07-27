# DOT

## LINK


节点 git ： [https://github.com/paritytech/polkadot](https://github.com/paritytech/polkadot)


测试网浏览器(各个链可切换) ： [https://westend.subscan.io/account/5GP8isa5UZ7HmRMjjdh4wiFSPMbLdM7mhjDz7j4uhUvMHc2G?tab=transfer](https://westend.subscan.io/account/5GP8isa5UZ7HmRMjjdh4wiFSPMbLdM7mhjDz7j4uhUvMHc2G?tab=transfer)

浏览器1 ： [https://polkadot.js.org/apps/#/js](https://polkadot.js.org/apps/#/js)

浏览器2 ：[https://polkascan.io/](https://polkascan.io/)

api js包 ：[https://github.com/polkadot-js/api](https://github.com/polkadot-js/api)

api 服务 ： [https://github.com/SimplyVC/polkadot\_api\_server](https://github.com/SimplyVC/polkadot\_api\_server)

api ： [https://documenter.getpostman.com/view/1618960/T17Gf7to?version=latest#44822cd7-f4e0-4059-b322-8f5cb21c308f](https://documenter.getpostman.com/view/1618960/T17Gf7to?version=latest#44822cd7-f4e0-4059-b322-8f5cb21c308f)

api github : [https://github.com/itering/subscan-essentials](https://github.com/itering/subscan-essentials)

rpc 文档 ： [https://polkadot.js.org/api/substrate/rpc.html](https://polkadot.js.org/api/substrate/rpc.html)

wiki ：[https://wiki.polkadot.network/docs/en/maintain-networks#westend-test-network](https://wiki.polkadot.network/docs/en/maintain-networks#westend-test-network)


## INSTALL


### 二进制安装节点

下载最新二进制包

>链接列表  https://github.com/paritytech/polkadot/releases

```
wget https://github.com/paritytech/polkadot/releases/download/v0.8.14/polkadot
```

赋予可执行权限

```
chomd +x polkadot
```

运行
> 选择网路 --chain=   [polkadot、kusama、westend]

> 如果要使用 rpc author_rotateKeys  需要加参数 --rpc-methods=Unsafe


运行测试节点

```
./polkadot --chain=westend --pruning=archive --ws-port=9955 --unsafe-ws-external --rpc-cors=all --rpc-port=9998 --rpc-external --base-path = /root/blockchain/dot_path
```

默认文件存储路径

/root/.local/share/polkadot/chains


### api 服务

节点运行需加如下参数

```
 --pruning=archive --ws-port=9944 --unsafe-ws-external --rpc-cors=all
```



####安装
> 前提条件安装node npm

```
git clone https://github.com/SimplyVC/polkadot_api_server.git

cd polkadot_api_server

git checkout -b v1.23.1

npm install

cd config

mv example_user_config_main.ini user_config_main.ini

mv example_user_config_nodes.ini user_config_nodes.ini

```

修改 user_config_nodes.ini 中的端点号


### API 接口

查询余额
```
http://192.168.1.205:3000/api/custom/getSlashAmount?account_address=15j4dg5GzsL1bw2U2AWgeyAk6QTxq43V7ZPbXdAmbVLjvDCK&websocket=ws://127.0.0.1:9944
```

指定块的哈希值；如果未指定哈希值，则为最新块

```
http://192.168.1.205:3000/api/rpc/chain/getHeader?websocket=ws://127.0.0.1:9944
```

指定块高度；如果未指定高度，则为最新高度

```
http://192.168.1.205:3000/api/rpc/chain/getBlockHash?websocket=ws://127.0.0.1:9944
```

...