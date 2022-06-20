## IoT-data-simulator

## 启动

1. 使用docker-compose启动容器
```shell
docker-compose pull
docker-compose up
```

2. 使用浏览器打开 `http://localhost:8090`，配置数据集，可以参考：[IoT-data-simulator](https://github.com/IBA-Group-IT/IoT-data-simulator)

3. 下载和安装[telegraf](https://portal.influxdata.com/downloads/)

4. 根据data-simulator配置的数据集对telegraf的inputs.mqtt_consumer做配置
    > 主要关注以下配置，用来和data-simulator生成的数据做适配，文件配置在这./conf/telegraf/telegraf.conf
    ```
   [[inputs.mqtt_consumer]]
     topics = [
     "telegraf/host01/cpu",
     "telegraf/+/mem",
     "sensors/#",
     ]
     [[inputs.mqtt_consumer.topic_parsing]]
     [[inputs.mqtt_consumer.topic.types]]
   ```
   
5. 启动telegraf

```shell
telegraf --config ./conf/telegraf/telegraf.conf
```
