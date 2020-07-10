## link

节点地址 ：[https://github.com/cosmos/gaia](https://github.com/cosmos/gaia)

restfulApi文档 : [https://cosmos.network/rpc/v0.37.9](https://cosmos.network/rpc/v0.37.9)

主网浏览器 : [https://www.mintscan.io/](https://www.mintscan.io/)

测试网浏览器 : [https://cosmos.bigdipper.live/](https://cosmos.bigdipper.live/)

## 节点搭建
```
git clone -b v2.0.11 https://github.com/cosmos/gaia.git

cd gaia

make install
```

## 启动节点

### 重置数据
```
rm $HOME/.gaiad/config/addrbook.json $HOME/.gaiad/config/genesis.json 
gaiad init David --chain-id=gaia-13007
```

主网 genesis

```
curl https://raw.githubusercontent.com/cosmos/launch/master/genesis.json > /root/.gaiad/config/genesis.json
```

测试网 genesis

```
curl https://raw.githubusercontent.com/cosmos/testnets/master/latest/genesis.json > genesis.json
```
或

```
curl https://raw.githubusercontent.com/cosmos/testnets/master/gaia-13k/13007/genesis.json > genesis.json
```

运行
```
gaiad start
```

>如果出现错误 ：ERROR: error during handshake: error on replay: validator set is nil in genesis and still empty after InitChain

```
gaiad unsafe-reset-all
```

更改程序目录
```
vim conf.toml
更改 db_dir
```


## rpc
查询链信息
```
curl -X GET "127.0.0.1:1317/node_info" -H "accept: application/json"
```

## restfulApi

启动:

`gaiacli rest-server --chain-id gaia-13007 --trust-node  --laddr tcp://0.0.0.0:1317`


## cli操作

### 创建账户
>password must be at least 8 characters

```
gaiacli keys add <yourKeyName>
```

```

- name: DavidKey
  type: local
  address: cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44
  pubkey: cosmospub1addwnpepqvwd3xcac84dgd9d9x94krcjjtxvf7a6awdj8kzjay2n8lpeerwnsvywh09
  mnemonic: ""
  threshold: 0
  pubkeys: []


**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

shadow learn print program hobby vehicle park identify kid slice oxygen cigar cliff screen device leg rabbit echo will initial glory smoke modify model
```

### 获取测试币
[faucet](https://riot.im/app/#/room/#cosmos-faucet:matrix.org)

> YOURADDRESS 你的钱包地址

发送 "show me the money! YOURADDRESS" 获取测试币


### 质押
>节点需同步完成

#### cli操作 

委托
```
gaiacli tx staking delegate cosmosvaloper1ck3kl0xe48zynr0nuf4tvvx8s7nhkehzpmyg8h 10umuon --from cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44 --gas auto --gas-
adjustment 1.5 --gas-prices 0.025umuon --chain-id gaia-13007
```

response :

```
height: 0
txhash: C20789F6950A1791429C4E84DEA3AAAC49106717E2AF5CFF05A389A0DEC792F8
code: 0
data: ""
rawlog: '[{"msg_index":0,"success":true,"log":"","events":[{"type":"message","attributes":[{"key":"action","value":"delegate"}]}]}]'
logs:
- msgindex: 0
  success: true
  log: ""
  events:
  - type: message
    attributes:
    - key: action
      value: delegate
info: ""
gaswanted: 0
gasused: 0
codespace: ""
tx: null
timestamp: ""
events: []
```

提取奖励

```
gaiacli tx distribution withdraw-all-rewards --from <delegatorKeyName> --gas auto --gas-adjustment 1.5 --gas-prices <gasPrice>
```

解除委托
>Unbond a certain amount of Atoms from a given validator , You will have to wait 3 weeks before your Atoms are fully unbonded and transferrable 

```
gaiacli tx staking unbond <validatorAddress> <amountToUnbond> --from <delegatorKeyName> --gas auto --gas-adjustment 1.5 --gas-prices <gasPrice>
```

#### api查询

查询该用户所有委托

```
curl -X GET "127.0.0.1:1317/staking/delegators/cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44/delegations" -H "accept: application/json"
```

response :

```
{"height":"3063260","result":[
  {
    "delegator_address": "cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44",
    "validator_address": "cosmosvaloper1ck3kl0xe48zynr0nuf4tvvx8s7nhkehzpmyg8h",
    "shares": "10000010.000000000000000000",
    "balance": "10000010"
  }
]}
```

查询该用户绑定的所有验证器

```
curl -X GET "127.0.0.1:1317/staking/delegators/cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44/validators" -H "accept: application/json"
```

获取所有验证器

```
curl -X GET "127.0.0.1:1317/staking/validators?status=bonded&page=1&limit=10" -H "accept: application/json"
```

查询验证人和委托人之间的当前委托

```
curl -X GET "127.0.0.1:1317/staking/delegators/cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44/delegations/cosmosvaloper1ck3kl0xe48zynr0nuf4tvvx8s7nhkehzpmyg8h" -H "accept: application/json"
```


获取所有奖励总额

```
curl -X GET "127.0.0.1:1317/distribution/delegators/cosmos1ey2musq8uh64h2t9x0xpaqpjarsd5698x9dm44/rewards" -H "accept: application/json"
```

response :

```
{"height":"3063624","result":{"rewards":[{"validator_address":"cosmosvaloper1ck3kl0xe48zynr0nuf4tvvx8s7nhkehzpmyg8h","reward":null}],"total":null}}
```

#### 实现

前端 ：

- 委托 离线签名

- 提取奖励 离线签名

- 解绑 离线签名

后端：

- 所有验证者列表接口

- 用户委托列表接口

- 用户收益接口

- 广播



## 参考

[https://github.com/cosmos/gaia/tree/main/docs](https://github.com/cosmos/gaia/tree/main/docs)

[https://blog.csdn.net/kk3909/article/details/106355041/](https://blog.csdn.net/kk3909/article/details/106355041/)


