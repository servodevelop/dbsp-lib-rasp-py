# 树莓派与DBSP进行串口通信

## 概要

本文主要侧重讲解树莓派的硬件串口与DBSP进行串口通信的时候, 树莓派串口对象的初始化问题.

在阅读本文之前, 请按照`doc/树莓派硬件串口配置与实验/树莓派硬件串口配置与实验.md`里面的内容， 对树莓派进行串口配置.


## 导入依赖


```python
import time

# PySerial库用于串口通信
# 使用此脚本之前, 请确保已经安装好了PySerial
# PySerial安装过程及使用说明见官方文档
# https://pyserial.readthedocs.io/en/latest/pyserial.html
import serial

# 自定义的PyDBSP库文件, 将dbsp.py放置在测试工程的同极目录
from dbsp import *
```

## 初始化串口

树莓派3上面硬件串口的PORT名称是固定的, 端口号为`/dev/ttyAMA0`

树莓派与DBSP开发板之间的串口通信, 默认波特率是**57600**

> 注: PC/树莓派与DBSP的usb1进行串口通信的默认波特率为**115200**


```python
# 端口号
PORT_NAME = '/dev/ttyAMA0'
    
# 创建串口对象
# PySerial相关的API文档
# https://pyserial.readthedocs.io/en/latest/pyserial_api.html  
# 设置timeout=0 不等待直接返回
uart = serial.Serial(port=PORT_NAME, baudrate=57600,\
                     parity=serial.PARITY_NONE, stopbits=1,\
                     bytesize=8,timeout=0)

# 初始化DBSP
DBSP.init(uart, is_debug=False)
```

## 后续

DBSP的API使用说明请参阅`doc/PyDBSP例程演示/PyDBSP例程演示.md`
