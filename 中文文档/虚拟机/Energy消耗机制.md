
## ENERGY 消耗机制


### Energy消耗
顺序如下：

1. 按照合约中设置的比例消耗合约创建者冻结的Energy，若不足优先扣除合约创建者剩余所有Energy,剩余消耗需调用者提供
1. 调用者消耗顺序（优先消耗调用者冻结获取的Energy，为保证合约可正常执行，不足部分通过销毁TRX相抵）
1. 若创建者无冻结Energy资源，则所有消耗需调用者提供


### 相关接口

##### getTransactionInfoById
```
getTransactionInfoById needs 1 parameter, transaction id
```
相关字段

```
energy_usage: //本次合约调用者消耗的Energy数量
0
energy_fee: //本次合约调用者消耗TRX数量（SUN）
120
origin_energy_usage: //本次合约创建者提供的Energy数量
0
energy_usage_total: //本次合约总共消耗的Energy数量（包含energy_usage，origin_energy_usage 和energy_fee对应的Energy数量）
252
net_usage: //本次合约消耗的Bandwidth(不包含NetFee对应的)
0
net_fee: //本次合约因Bandwidth不足消耗的TRX
0
```
##### FreezeBalance
```
freezeBalance frozen_balance frozen_duration [ResourceCode:0 BANDWIDTH,1 ENERGY]
```

### 使用说明

部署合约和调用合约的过程中需传入参数 "fee_limit"

本次执行总共消耗的Energy所对应的TRX数量

对应关系：

```
已冻结Energy部分：(冻结的balance数量/冻结获得总共的Energy)*消耗Energy数量
销毁TRX获得Energy部分：按照比例消耗的TRX数量
```

#### 注意事项：
详见 [a relative link](异常处理.md)


#### 相关名词：

合约创建者：即创建合约的账户

合约调用者：即调用合约的账户

Energy资源：执行合约过程中所消耗的资源类型
