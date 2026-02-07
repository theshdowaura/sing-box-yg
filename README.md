# sing-box-yg（精简版）

本仓库当前仅保留核心脚本：`sb.sh`。

该脚本用于在 VPS 上进行 sing-box 相关的安装、配置、升级与运维，包含：
- Vless-reality-vision
- Vmess-ws（可结合 TLS/Argo）
- Hysteria2
- Tuic-v5
- 域名分流、WARP 相关能力、证书管理、订阅输出等

## 目录结构

- `sb.sh`：主脚本（唯一业务文件）

## 使用前提

- 必须使用 `root` 运行
- 支持系统：Ubuntu / Debian / CentOS / Alpine（脚本会自动识别）
- 不支持 `arch` 系统
- 支持架构：`amd64` / `arm64` / `armv7`
- 需要能访问 GitHub（用于下载内核与组件）

## 快速开始

建议先下载到本地审计后再执行，不建议直接管道执行远程脚本。

### 方式 1：Git 克隆

```bash
git clone https://github.com/theshdowaura/sing-box-yg.git
cd sing-box-yg
chmod +x sb.sh
bash sb.sh
```

### 方式 2：仅下载脚本

```bash
curl -fL -o sb.sh https://raw.githubusercontent.com/theshdowaura/sing-box-yg/main/sb.sh
chmod +x sb.sh
bash sb.sh
```

## 主菜单（运行 `sb.sh` 后）

- `1` 一键安装 Sing-box
- `2` 删除卸载 Sing-box
- `3` 变更配置（TLS/UUID 路径/Argo/IP 优先/TG 通知/Warp/订阅/CDN 优选）
- `4` 更改主端口/添加多端口跳跃复用
- `5` 三通道域名分流
- `6` 关闭/重启 Sing-box
- `7` 更新脚本（本地安全更新流程）
- `8` 更新/切换/指定 Sing-box 内核版本
- `9` 刷新并查看节点（Clash-Meta / Sing-box 配置 / 订阅链接）
- `10` 查看 Sing-box 运行日志
- `11` 一键 BBR 加速
- `12` 管理 Acme 域名证书
- `13` 管理 Warp（含解锁检测）
- `14` 管理 WARP-plus-Socks5 代理模式
- `15` 刷新本地 IP、切换 IPv4/IPv6 配置输出
- `16` 使用说明与项目信息
- `0` 退出

## 安全说明（当前版本）

本仓库当前脚本已进行基础安全加固，重点包括：
- 下载统一走 HTTPS 且启用 TLS 约束
- 关键二进制/发布资产按摘要校验（可用时）
- 外部辅助脚本改为固定 commit + SHA256 校验后执行
- 移除 `--insecure` 下载路径
- GitLab 推送不再持久化 token 到磁盘
- GitLab 订阅链接不再包含 `private_token` 查询参数

## 常用运维建议

- 初次安装后先执行菜单 `9`，确认节点与订阅输出正常
- 若服务异常，先看菜单 `10` 日志，再考虑菜单 `8` 切换稳定内核
- 若修改了端口或协议参数，建议重启服务并重新导出订阅
- 使用 GitLab 订阅时，请确保目标仓库文件具备可读取策略（否则 raw 链接无法拉取）

## 故障排查

### 1) 下载失败 / 版本获取失败

- 检查 VPS 到 GitHub 网络连通性
- 检查系统时间是否正确（TLS 校验依赖时间）

### 2) 服务未启动

- 使用菜单 `10` 查看日志
- 使用菜单 `8` 切换到稳定正式版内核重试

### 3) WARP / Argo 异常

- 先停止对应功能，再重新按菜单配置
- 检查端口占用和 DNS 解析情况

## 免责声明

本项目仅供学习与运维研究使用。请在遵守当地法律法规和服务商条款的前提下使用。
