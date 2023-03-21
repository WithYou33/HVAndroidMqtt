# HVandroidMQTT
高版本android无法使用mqtt问题解决
# 1.添加jar包
# 2.  build.gradle：app下导入依赖
        implementation 'com.blankj:utilcodex:1.31.0'
        api 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.1.0'
# 3.AndroidManifest.xml 的 application 标签下加入
        <service android:name="com.itfitness.mqttlibrary.MqttService"/>

## 使用事例
        val server = "tcp://ip:port" //服务端地址
        val mqttHelper = MQTTHelper(context, server, "你的id", "你的name", "鉴权或密码")
        mqttHelper.connect("主题", 消息质量（int）, false, object : MqttCallback {
            override fun connectionLost(cause: Throwable?) {
            }

            override fun messageArrived(topic: String?, message: MqttMessage?) {
                //收到消息
                message?.payload?.let { ToastUtils.showShort(String(it)) }
                LogUtils.eTag("消息", message?.payload?.let { String(it) })
            }

            override fun deliveryComplete(token: IMqttDeliveryToken?) {
            }
        })
