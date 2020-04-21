# ESP8266/8285 开发记录


### 启动报错 csum err ets_main.c 解决办法

```shell
ets Jan 8 2013,rst cause:2, boot mode:(3,6)

load 0x40100000, len 25020, room 16
tail 12
chksum 0xef
ho 0 tail 12 room 4
load 0x00000000, len 0, room 12
tail 0
chksum 0xef
load 0x00000000, len 0, room 4
tail 0
chksum 0xef
csum 0xef
csum err
ets_main.c
```

解决办法：

`FLASH` 刷写模式改为 **DOUT**


