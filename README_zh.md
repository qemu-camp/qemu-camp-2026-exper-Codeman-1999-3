<p align="center"><strong>QEMU 训练营 2026 — 实验仓库</strong></p>
<p align="center"><a href="README.md">English</a> | <a href="README_zh.md">中文</a></p>

本仓库是 QEMU 训练营 2026 专业阶段的实验仓库，专注于 GPGPU 实验方向，基于 RISC-V 架构。

## 在线讲义

| 方向 | 实验手册 | 硬件手册 / 编程指南 |
|------|---------|-------------------|
| **GPGPU** | [GPU 实验手册](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-exper-manual/) | [GPU 硬件手册](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-datasheet/) |

完整讲义网站：<https://qemu.gevico.online/>

## 实验方向

| 方向 | 测试框架 | 测试位置 | 评分 |
|------|---------|---------|------|
| **GPGPU** | QTest (QOS) | `tests/qtest/gpgpu-test.c` | 17 题 -> 100 分 |

## 快速开始

### 第一步：安装依赖

```bash
# Ubuntu 24.04
sudo sed -i 's/^Types: deb$/Types: deb deb-src/' /etc/apt/sources.list.d/ubuntu.sources
sudo apt-get update
sudo apt-get build-dep -y qemu
```

### 第二步：配置

```bash
make -f Makefile.camp configure
```

### 第三步：编译

```bash
make -f Makefile.camp build
```

### 第四步：运行测试

```bash
# 运行 GPGPU 实验测试
make -f Makefile.camp test-gpgpu

# 等同于上一条命令
make -f Makefile.camp test
```

### 第五步：提交代码

```bash
git add .
git commit -m "feat: implement ..."
git push origin main
```

推送到 `main` 后，CI 会自动编译、运行测试、计算得分并上传到排行榜平台。得分为 0 时不会上传。

## 实验详情

### GPGPU 实验（QTest 测题）

实现 PCIe GPGPU 设备，包含 SIMT 执行引擎、DMA 和低精度浮点支持。测试验证设备寄存器、显存、内核执行和 FP8/FP4 转换。

- 设备：`hw/gpgpu/`（PCI 设备 `gpgpu`）
- 测试：`tests/qtest/gpgpu-test.c`（17 个子测试）
- 运行：`make -f Makefile.camp test-gpgpu`
- 文档：[实验手册](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-exper-manual/) | [GPU 硬件手册](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-datasheet/)

## Make 命令一览

```
make -f Makefile.camp help       # 查看所有命令
make -f Makefile.camp configure  # 配置 QEMU
make -f Makefile.camp build      # 编译 QEMU
make -f Makefile.camp test-gpgpu # GPGPU 实验测试
make -f Makefile.camp test       # 所有测试
make -f Makefile.camp clean      # 清理构建
make -f Makefile.camp distclean  # 删除构建目录
```

## 评分规则

- 测试**失败不会**导致 CI 报错，只会降低得分。
- 得分为 **0** 时不会上传到排行榜平台。
- 每次推送到 `main` 都会触发完整的 CI 流程。
