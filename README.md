# CloudflareSpeedTest Termux 部署指南

适配：Android 9 · arm64-v8a · Termux · v2.3.5

## 📱 设备环境

- **系统**：Android 9
- **架构**：`arm64-v8a` (ARM aarch64)
- **终端**：Termux
- **项目**：[CloudflareSpeedTest (XIU2)](https://github.com/XIU2/CloudflareSpeedTest) v2.3.5
- **安装包**：`cfst_linux_arm64.tar.gz`

---

## 🚀 完整部署步骤

### 1. 准备环境
```bash
pkg update && pkg upgrade -y

```

### 2. 下载安装包

**方式 A：镜像下载（推荐）**

```bash
# 清理旧文件
rm -rf cfst* CloudflareST*

# 镜像加速下载
wget -O cfst_linux_arm64.tar.gz [https://gh.llkk.cc/https://github.com/XIU2/CloudflareSpeedTest/releases/download/v2.3.5/cfst_linux_arm64.tar.gz](https://gh.llkk.cc/https://github.com/XIU2/CloudflareSpeedTest/releases/download/v2.3.5/cfst_linux_arm64.tar.gz)

# 校验文件（≈2.8MB，非0字节）
ls -lh cfst_linux_arm64.tar.gz

```

**方式 B：浏览器导入（下载失败时）**

```bash
# 授权读取存储并复制文件到当前目录
termux-setup-storage
cp ~/storage/downloads/cfst_linux_arm64.tar.gz ~/

```

### 3. 解压并进入目录

```bash
# 解压
tar -zxf cfst_linux_arm64.tar.gz

# 进入程序目录（关键！）
cd cfst_linux_arm64

# 确认文件
ls -la

```

### 4. 赋权并运行

```bash
# 验证架构（应输出 arm aarch64）
file cfst

# 赋予执行权限（仅首次需要）
chmod +x cfst

# 运行测速
./cfst

```

---

## 💡 日常使用与进阶技巧

### 常用命令

```bash
# 基础测速
cd ~/cfst_linux_arm64 && ./cfst

# 自定义测速：测 100 个 IP，取前 10 个，延迟≤500ms
./cfst -num 100 -top 10 -tl 500

# 仅延迟测速（不进行下载测速，速度最快）
./cfst -dn 0

```

### 📥 进阶：将测速结果保存为文件

在手机上查看不方便时，可以将优质 IP 导出保存到文本中：

```bash
# 测速并将结果输出到 result.csv
./cfst -o result.csv

```

### 🔄 进阶：后台运行防止断连

Termux 切换到后台后容易被 Android 系统休眠杀死，建议配合 `nohup` 或 `screen` 使用，或者保持 Termux 保持唤醒锁：

```bash
# 后台运行并将日志输出到 log.txt
nohup ./cfst > log.txt 2>&1 &

```

---

## ⚠️ 避坑要点

* ❌ **不能直接执行 `./cfst**`：必须先 `cd cfst_linux_arm64` 进入目录。
* ❌ **架构别选错**：Android 手机必须选 `linux-arm64`，不要选 `amd64`。
* ❌ **版本差异**：v2.3.x 主程序名是 `cfst`，旧版本可能是 `CloudflareST`。
* ✅ **赋予权限**：`chmod +x cfst` 仅首次执行一次即可。
* ✅ **内置 IP 库**：自带 `ip.txt` / `ipv6.txt`，通常无需额外配置。

---

### 📂 目录结构示例

```text
~/
├── cfst_linux_arm64.tar.gz    # 安装包压缩包
└── cfst_linux_arm64/          # 程序目录
    ├── cfst                   # 主程序
    ├── ip.txt                 # IPv4地址库
    ├── ipv6.txt               # IPv6地址库
    └── ...
