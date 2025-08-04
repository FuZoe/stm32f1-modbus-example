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

* 任何Modbus客户端软件 (例如 https://github.com/favalex/modbus-cli for tests）

## 库

* https://github.com/stm32-rs/stm32f1xx-hal/ for STM32F1 HAL

* https://github.com/alttch/rmodbus for Modbus

* https://github.com/probe-rs/probe-rs

## 环境配置

```shell
#如果您的电脑上还没有安装cargo-flash （汉化者注：cargo-flash现被整合到probe-rs库中 --2025/08/04）
# 先下载脚本
Invoke-RestMethod https://github.com/probe-rs/probe-rs/releases/latest/download/probe-rs-tools-installer.ps1 -OutFile probe-rs-installer.ps1
# 以管理员身份运行 PowerShell，然后执行：
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
# 然后执行脚本
.\probe-rs-installer.ps1
```

```shell
#安装 Rust 目标平台
rustup target add thumbv7m-none-eabi
```

## 烧录

```shell
#检查编译
cargo check --target thumbv7m-none-eabi
#编译
cargo build --target thumbv7m-none-eabi --release
#烧录
cargo flash --chip stm32f103C8 --release
```


## 它能做什么

仅演示。您可以使用任何 Modbus/RTU 客户端读取/写入 Modbus 上下文，
获取/设置任何 Modbus 寄存器。

输入寄存器 0 和 1 包含已处理帧计数器（大端 u32）。

Rmodbus 与“smallcontext”功能配合使用，因此只能访问寄存器 0-999（所有类型）。

尽情使用吧！
