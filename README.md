# Rust编写的stm32 (stm32f103c8t6) & RS485串口通讯测试

通过 RS485/RTU 在 stm32 上实现 串口通讯测试 的简单示例。

## 器材

* stm32f103c8t6

* UART TTL 转 RS485 (MAX485)

* ST-LINK/V2 (用于烧录)

* 任何 USB 转 RS485  (用于从电脑测试)

## 接线图

![Connection scheme](scheme.png?raw=true "Connection scheme")

## 所需软件

* 任何串口调试器 (例如 https://github.com/favalex/modbus-cli for tests)(汉化者注：可以试试https://github.com/FuZoe/stm32f1-modbus-example/tree/master/%E4%B8%B2%E5%8F%A3%E8%B0%83%E8%AF%95%E5%99%A8)

## 库

* https://github.com/stm32-rs/stm32f1xx-hal/ for STM32F1 HAL

* https://github.com/alttch/rmodbus for Modbus

## 烧录

```shell
cargo install cargo-flash # if not installed yed
cargo flash --chip stm32f103C8 --release
```

## 它能做什么

仅演示。您可以使用任何 Modbus/RTU 客户端读取/写入 Modbus 上下文，
获取/设置任何 Modbus 寄存器。

输入寄存器 0 和 1 包含已处理帧计数器（大端 u32）。

Rmodbus 与“smallcontext”功能配合使用，因此只能访问寄存器 0-999（所有类型）。

尽情使用吧！
