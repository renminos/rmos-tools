# RMOS Tools

RMOS 用到的第三方工具集中放在这里。这个仓库**极少更新**，所以下游（用户服务器、矿机客户端）可以安全地长期使用
`https://github.com/renminos/rmos-tools/releases/latest/download/<文件名>` 这种稳定地址 —— 正式版的
`rmos-server` 仓库会清理历史 release，把工具放在那里迟早会失效（这就是之前踩过的坑）。

## 当前包含

| 文件 | 版本 | 用途 |
|---|---|---|
| `nvflash-linux-x86_64` | NVIDIA NVFlash **5.867**（2024，x86_64） | 读取/刷写 NVIDIA 显卡 vBIOS；RMOS 控制台「vBIOS」页签读卡用它 |
| `nvflash-5.867-linux.zip` | 同上（官方分发包，含 x64 / aarch64 / ppc64 / x86） | 保留原始分发包，便于校验与取其他架构 |
| `SHA256SUMS.txt` | — | 上面两个文件的 sha256 |

## 分发链（用户服务器与矿机怎么拿到 nvflash）

1. **用户服务器**：有人打开「vBIOS」页签（或收到读卡请求）时，服务器自动从
   `releases/latest/download/nvflash-linux-x86_64` 下载一份到 `data/downloads/nvflash/`，
   并通过 `/dl/nvflash/nvflash-linux-x86_64` 提供给矿机；下载后记录 sha256。
   控制台不再需要「让服务器下载 nvflash」这个按钮。
2. **矿机客户端**：先找本机已有的 nvflash（`/home/rmos/bin`、HiveOS 自带的 `/hive/bin/nvflash_linux` 等）；
   没有、或者本机那份读不到这张卡（HiveOS 自带的是 5.833，读不了 RTX 50 系）时，
   从**自己的用户服务器**下载并校验 sha256，服务器没有镜像时回退到上面的 GitHub 地址。

## 关于 nvflash 的版权

nvflash 是 NVIDIA 的专有免费工具，二进制内自带声明：
`NVIDIA Firmware Update Utility (Version 5.867.0) / Copyright (C) 1993-2024, NVIDIA Corporation. All rights reserved.`

本仓库只是为 RMOS 的内部分发链保存一份**固定版本**：文件未做任何修改、未改名、未去除版权声明，
并保留官方压缩包作为来源凭证。最新版本请到 NVIDIA 官方渠道或
[TechPowerUp](https://www.techpowerup.com/download/nvidia-nvflash/) 获取。
若 NVIDIA 方面要求撤下，请开 issue，我们会立即删除。
