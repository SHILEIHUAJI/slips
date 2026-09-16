CloudflareSpeedTest 安卓9 Termux 部署指南
 
适配：Android 9 · arm64-v8a · Termux · v2.3.5
 
 
 
设备环境
 
- 系统: Android 9
- 架构:  arm64-v8a  (ARM aarch64)
- 终端: Termux
- 项目: CloudflareSpeedTest (XIU2) v2.3.5
- 包名:  cfst_linux_arm64.tar.gz 
 
 
 
完整部署步骤
 
1. 准备环境
 
bash
  
pkg update && pkg upgrade -y
 
 
2. 下载安装包
 
方式A：镜像下载（推荐）
 
bash
  
# 清理旧文件
rm -rf cfst* CloudflareST*

# 镜像加速下载
wget -O cfst_linux_arm64.tar.gz https://gh.llkk.cc/https://github.com/XIU2/CloudflareSpeedTest/releases/download/v2.3.5/cfst_linux_arm64.tar.gz

# 校验文件（≈2.8MB，非0字节）
ls -lh cfst_linux_arm64.tar.gz
 
 
方式B：浏览器导入（下载失败时）
 
bash
  
# 浏览器下载后导入
termux-setup-storage
cp ~/storage/downloads/cfst_linux_arm64.tar.gz ~/
 
 
3. 解压并进入目录
 
bash
  
# 解压
tar -zxf cfst_linux_arm64.tar.gz

# 进入程序目录（关键！）
cd cfst_linux_arm64

# 确认文件
ls -la
 
 
4. 赋权并运行
 
bash
  
# 验证架构（输出 ARM aarch64）
file cfst

# 赋予执行权限（仅首次）
chmod +x cfst

# 运行
./cfst
 
 
 
 
日常使用
 
bash
  
# 最简版
cd ~/cfst_linux_arm64
./cfst

# 懒人版（任意目录直接运行）
cd ~/cfst_linux_arm64 && ./cfst
 
 
常用参数
 
bash
  
# 基础测速
./cfst

# 自定义：测100个IP，取前10，延迟≤500ms
./cfst -num 100 -top 10 -tl 500

# 仅延迟测速（不下载）
./cfst -dn 0
 
 
 
 
避坑要点
 
- ❌ 不能直接  ./cfst  → 必须先  cd cfst_linux_arm64 
- ❌ 架构别选错： arm64-v8a  → linux-arm64，不要选 amd64
- ❌ 版本差异：v2.3.x 程序名是  cfst ，不是  CloudflareST 
- ✅  chmod +x  仅首次执行一次
- ✅ 自带  ip.txt  /  ipv6.txt ，无需额外配置
 
 
 
目录结构
 
text
  
~/
├── cfst_linux_arm64.tar.gz   # 安装包
└── cfst_linux_arm64/         # 程序目录
    ├── cfst                   # 主程序
    ├── ip.txt                 # IPv4地址库
    ├── ipv6.txt               # IPv6地址库
    └── ...
 
 
 
 
✅ 以上内容为标准 Markdown (MD) 格式，代码块可直接在 GitHub 点击复制按钮，无需手动全选。备份到仓库可直接新建  .md  文件，全文粘贴即可。
