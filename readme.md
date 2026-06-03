# HAL_5_PWM_Servo

## 简介

本项目基于 STM32F103 系列 MCU 和 STM32 HAL 库，演示了 TIM2 PWM 输出与 OLED 实时显示。
主程序使用 `TIM2_CH2` 在 `PA1` 上输出 PWM 波形，并在 OLED 屏幕上动态显示当前 PWM 值。
本工程由 STM32CubeMX 生成 CMake 构建配置，结合自定义 OLED 软件 I2C 驱动。

## 主要功能

- 使用 STM32 HAL 初始化 STM32F103 MCU
- 配置 TIM2 为 PWM 模式，并在 `PA1` 输出 PWM 信号（TIM2_CH2）
- 实时更新 OLED 显示当前 PWM 值
- 演示 PWM 占空比在 2.5%~12.5% 范围内循环变化，适合伺服控制信号
- OLED 采用软件 I2C 驱动，支持清屏、字符和数字显示
- 兼容 STM32CubeMX 生成的 HAL 代码与手写模块结合

## 关键文件

- `CMakeLists.txt`：项目根 CMake 构建脚本
- `CMakePresets.json`：CMake 预设配置
- `config.ioc`：STM32CubeMX 项目配置
- `Core/Src/main.c`：主程序入口，PWM 控制与 OLED 显示逻辑
- `Core/Src/tim.c`：TIM2 PWM 初始化与 TIM2 GPIO 后初始化
- `Core/Src/gpio.c`：GPIO 初始化，包含 OLED 软件 I2C 引脚配置
- `Core/Src/OLED.c`：OLED 控制逻辑与软件 I2C 实现
- `Core/Inc/OLED.h`：OLED 接口声明
- `Core/Inc/OLED_Font.h`：OLED 字库数据
- `Drivers/`：STM32 HAL 库源文件和 CMSIS 头文件

## 构建环境与依赖

- CMake 3.22 及以上
- Ninja 构建器
- ARM GCC 交叉编译器（例如 `arm-none-eabi-gcc`）
- STM32 HAL 库（已包含在 `Drivers/` 目录中）

## 构建步骤

推荐使用 VS Code 的 CMake 工具或命令行：

```bash
cd d:/Electronics/HAL_Projects/HAL_5_PWM_Servo
cmake --preset Debug
cmake --build --preset Debug
```

## 运行与下载

1. 生成固件后，使用 ST-Link 或其他支持的下载工具将 ELF/HEX/BIN 文件烧录到目标板。
2. 重新上电后，OLED 应显示当前 PWM 值，TIM2_CH2 的 `PA1` 引脚会输出对应的 PWM 波形。

## 硬件说明

- 目标 MCU：STM32F103 系列
- OLED 软件 I2C 默认引脚：
  - `PB8`：SCL
  - `PB9`：SDA
- PWM 输出引脚：
  - `PA1`：TIM2_CH2

## 许可

MIT License
