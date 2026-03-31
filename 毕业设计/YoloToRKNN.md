# Yolo2ONXX
## 1. 使用conda配置环境
1. 安装yolo11环境：

## 2.Rknn-Toolkit

### 概述

1. https://docs.radxa.com/rock5/rock5b/app-development/ai/rknn-install
2. https://doc.embedfire.com/linux/rk356x/Ai/zh/latest/lubancat_ai/env/toolkit2.html
- RK3588搭载神经网络处理器 NPU，利用 RKNN 可以帮助用户快速部署 AI 模型到 Rockchip 芯片上使用 NPU 硬件加速模型推理。为了使用 RKNPU，用户首先需要在 x86 计算机上使用 RKNN-Toolkit2 工具，将训练好的模型转换为 RKNN 格式的模型，然后在开发板上使用 RKNN C API 或 Python API 进行推断。RKNN软件栈可以帮助用户快速将AI模型部署到Rockchip芯片上。整体框架如下：

[![](https://github.com/airockchip/rknn-toolkit2/raw/master/res/framework.png "RKNN")](https://github.com/airockchip/rknn-toolkit2/blob/master/res/framework.png)

包含工具：

- RKNN-Toolkit2 是一个软件开发工具包，供用户在 PC 和 Rockchip NPU 平台上执行模型转换、推断和性能评估。
- RKNN-Toolkit-Lite2 为 Rockchip NPU 平台提供了 Python 编程接口，帮助用户部署 RKNN 模型并加速实施 AI 应用。
- RKNN Runtime 为 Rockchip NPU 平台提供了 C/C++ 编程接口，帮助用户部署 RKNN 模型并加速实施 AI 应用。
- RKNPU 内核驱动负责与 NPU 硬件交互。
### 步骤
1. 根据版本使用conda配置python环境
- 版本对应关系如下：

- 使用RKNN-Toolkit2时需要满足以下运行环境要求：

|操作系统版本|Ubuntu18.04 (x64)|Ubuntu20.04 (x64)|Ubuntu22.04 (x64)|Ubuntu24.04 (x64)|
|---|---|---|---|---|
|Python版本|3.6 / 3.7|3.8 / 3.9|3.10 / 3.11|3.12|

- ARM64版本运行环境要求：

|操作系统版本|Debian10 (arm64)|Debian11 (arm64)|Debian12 (arm64)|
|---|---|---|---|
|Python版本|3.6 / 3.7|3.8 / 3.9|3.10 / 3.11 / 3.12|

2. 下载需要SDK
	~~~ bash
	git clone -b v2.3.2 https://github.com/airockchip/rknn-toolkit2.git
	~~~
3. 如有需要可以配置pip源解决下载缓慢的问题
~~~bash
pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/
~~~
4. 安装依赖库
	(该文件位置在rknn-toolkit2/packages/x86_64下,根据python版本选择)
~~~bash
pip install numpy
pip install -r ./requirements_cp310-2.3.2.txt
~~~
4. 根据python环境选择合适版本安装
	(该文件位置在rknn-toolkit2/packages/x86_64下,根据python版本选择)
~~~bash
pip install rknn_toolkit2-2.3.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
~~~
5.  验证安装
	没有报错则安装成功
~~~bash
$ python3
>>> from rknn.api import RKNN
~~~


## 3. Rknn-Toolkit-lite2
1. 