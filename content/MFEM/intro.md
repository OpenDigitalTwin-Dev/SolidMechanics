# MFEM

[MFEM](https://mfem.org/)（Modular Finite Element Methods）是一个开源的 C++ 库，专注于有限元方法的高性能实现。它提供了灵活、模块化的框架，支持多种有限元空间和自适应网格剖分，广泛应用于科学计算、工程仿真和多物理场问题

## 安装MFEM

从[MFEM官网](https://mfem.org/)下载库文件
```
tar -zxvf mfem-4.8.tgz && cd mfem-4.8
mkdir install build && cd build
```

默认编译 Release 版本
```
cmake -DCMAKE_INSTALL_PREFIX=../install ..
```
编译所有应用并测试
```
make exec -j8 && make test
```
或仅编译库文件和简单测试
```
make -j8 && make check
```
安装
```
make install
```

## 调试 MFEM
如果想要在 VSCode 中调试 MFEM 的算例，则需要编译 Debug 版本
```
cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=../install ..
make -j8
```
以调试 `ex1` 为例
```
make ex1
```
并创建 `launch.json` 文件，内容如下
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "调试 ex",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build/examples/ex1",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}/build/examples",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb"
        }
    ]
}
```

## GLVis 安装

[GLVis](https://glvis.org/) 是转为 MFEM 设计的轻量化有限元计算可视化软件，在安装之前需要先安装一下依赖库
```
sudo apt-get install libfontconfig1-dev libfreetype-dev libsdl2-dev libglew-dev libglm-dev libpng-dev
```
解压并进入目录
```
tar -zxvf glvis-4.4.tgz && cd glvis-4.4
mkdir install build && cd build
```
编译
```
cmake -DCMAKE_INSTALL_PREFIX=../install -DMFEM_DIR=../../mfem-4.8/install ..
make -j8 && make install
```
设置软链
```
sudo ln -s ~/software/glvis-4.4/install/bin/glvis /usr/local/bin/glvis
```
