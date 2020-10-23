# 修改了1.1.4版本

## 背景
#### 公司使用canal做数据到rocketmq上，多次发生了故障，排查后发现是数据变更有4M的大字段，rocketmq接收堵塞了，导致全栈数据同步迟缓。 
#### 官方在1.1.4提供了canal.instance.filter.black.field来过滤掉字段，但是我们不知道哪个库哪个表会突然被插入大字段，可能是测试小伙伴的随机测试。。。 
## 变更
#### 添加字段的长度限制，超过截取，增加报警功能，遇到超过阈值的情况发送警告到运维群，及时提醒小伙伴不要顽皮~
## 使用
#### 在canal目录下 mvn clean install
#### 打包后替换官方下载的canal/lib中的canal.deployer-1.1.4.jar和canal.parse-1.1.4.jar
#### canal/conf/canal/properties 中添加
    canal.instance.threshold.value.field=4000000
    canal.instance.threshold.hook.url=你的钉钉机器人url