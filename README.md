# OpenWRT-CI（个人定制版）

基于 [VIKINGYFY/OpenWRT-CI](https://github.com/VIKINGYFY/OpenWRT-CI) 定制的 OpenWrt 云编译仓库，使用 GitHub Actions 自动构建 [VIKINGYFY/immortalwrt](https://github.com/VIKINGYFY/immortalwrt) 源码的固件，仅自用。

## 目标设备

**Cmiot AX18**（Qualcomm IPQ6000 / qualcommax ipq60xx 平台）

## 本仓库的定制

- `Config/CMIOT-AX18-WIFI-NO.txt`：AX18 专用配置（配合 VIKINGYFY/immortalwrt 源码，自带 NSS）
- `Config/KMODS-ZRAM.txt`：ZRAM 配置，内核编入 LZ4 / ZSTD 双压缩后端
- 实际使用参数：ZRAM 256MB、zstd 压缩、vm.swappiness=90

## 固件特性

- NSS 硬件加速（nss-firmware + nss-eip-firmware）
- ZRAM 内存压缩（IPQ6000 内存有限，换取更流畅的多任务表现）
- 精简 LuCI 插件：commands / firewall / package-manager / store / ttyd / upnp
- 无 Wi-Fi：WIFI-NO 配置，无线驱动未编入固件（ath11k 仅编译为可选包），以有线 + 4G 使用为主

## 使用

- 登录地址：`10.3.2.1`（默认用户名root，密码password）
- 刷机文件见 [Releases](../../releases)：
  - `*factory*.ubi`：从原厂固件首次刷入
  - `*sysupgrade*.bin`：OpenWrt 系统内升级
  - `*.manifest` / `Config-*.txt`：包清单与完整编译配置，供核对复现

## 致谢

- [VIKINGYFY/OpenWRT-CI](https://github.com/VIKINGYFY/OpenWRT-CI) —— 云编译模板
- [VIKINGYFY/immortalwrt](https://github.com/VIKINGYFY/immortalwrt) —— 带 NSS 支持的源码
- ImmortalWrt / OpenWrt 社区
