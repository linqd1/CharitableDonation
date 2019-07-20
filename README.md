# CharitableDonation
利用区块链技术实现智能合约，某慈善机构将原有捐款流程升级改造为透明、易追溯的智能捐款系统，用户可自主完成以下事务

1. 注册、初始捐款
2. 增加捐款额
3. 查询账户信息
4. 捐款（随机／指定捐款）
5. 查询捐款记录  
6. 查询余额信息
![image](https://github.com/linqd1/CharitableDonation/blob/master/image/1.png)
交易流程由应用客户端发送给特定背书节点的transaction proposal组成。背书节点验证客户端签名，并执行chaincode功能来模拟transaction。输出是链码结果，在链码（读集）中读取的一组键/值版本以及以链码（写集）编写的一组键/值。带有背书签名的proposal响应将被发送回客户端。 客户端将签名装配到transaction有效负载中并将其广播到ordering服务。ordering服务将有序交易作为块传送到这个通道上的所有peers。

在交付之前，peers将验证交易。首先，他们将检查背书策略，以确保指定peer已经对结果进行了签名，并且将根据交易有效负载来验证签名。

其次，peers将针对交易读集执行版本检查，以确保数据的完整性，并防止双花等威胁。Hyperledger Fabric具有并发控制，其中transaction并行执行（通过背书节点）以增加吞吐量，并且在提交（由所有peers）每个transaction时，每个transaction都被验证，以确保没有其他transaction已经修改了已读取的数据。换句话说，它确保在chaincode执行（背书）期间需要读取的数据没有改变，因此执行结果有效，并且可以提交到账本状态数据库。如果读取的数据已被其他transaction更改，则块中的transaction被标记为无效，并且不会写入账本状态数据库。客户端应用程序被提醒，然后可以控制错误或重新尝试。
![image](https://github.com/linqd1/CharitableDonation/blob/master/image/2.png)
![image](https://github.com/linqd1/CharitableDonation/blob/master/image/3.png)
