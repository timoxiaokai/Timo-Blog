---
title: HWiNFO：硬件极客的「X 光机」
published: 2025-12-26T19:25:00.000+08:00
cover: https://picsum.photos/seed/HWiNFO-2025/1600/900.jpg
tags:
  - 硬件检测
  - 传感器监控
  - 超频
  - 开源工具
category: 系统
draft: false
---
> 如果你只想用一款软件就把 CPU 体质、内存颗粒、电源功耗、风扇曲线、主板 VRM 温度全部看透——**HWiNFO** 几乎是唯一答案。

---

## 一、HWiNFO 是谁？

- 1999 年发布，**26 年历史**，更新比 Windows 补丁还勤快  
- 原生支持 **Windows XP → Windows 11 24H2**，同时提供 DOS 版救砖  
- 个人免费、商用需授权；无广告、无捆绑、无 telemetry  
- 官方仅 10 MB 单文件，绿色版点开即跑，不写垃圾注册表  

官网（建议收藏）：  
👉 [https://www.hwinfo.com](https://www.hwinfo.com)

---

## 二、一句话看懂特色

| 维度 | HWiNFO 能做到什么 | 同级对手 |
|---|---|---|
| 🔍 检测深度 | 读到 DIMM 颗粒编码、显卡 VBIOS 版本、电源最大瞬时功耗 | AIDA64 部分隐藏 |
| 🌡️ 传感器 | 7000+ 传感器、0.5 s 刷新、自定义公式、RTSS OSD 叠加 | GPU-Z 只能看显卡 |
| 📈 日志 | 每秒 CSV 导出，持续 7×24 小时，文件 1 GB 自动切分 | Open Hardware Monitor 掉数据 |
| 🧪 超频辅助 | 实时显示 FIT/V/F 曲线，帮助找到“电压墙” | BIOS 需要重启 |
| 🚨 告警 | 温度>95 ℃自动弹窗+邮件+Webhook 钉钉 | 其他软件需脚本 |
| 🖥️ 远程 | 通过 HWiNFO Remote Monitor 把数据推到手机、Home Assistant | 付费插件 |

---

## 三、30 秒极速上手

1. 下载 **Portable** 版（zip）→ 解压 → 双击 `HWiNFO64.exe`  
2. 弹出欢迎向导，建议勾选  
   ✅ “仅显示传感器” 可跳过冗长报告  
   ✅ “最小化启动” 常驻托盘  
3. 主窗口 = 树状硬件列表；传感器窗口 = 实时折线  
4. 右键任意条目 → `Add to Tray` → 任务栏即刻显示 CPU 温度数字  
5. 点击 `Run` → `Logging` → 设定 1 s 间隔 → 开始记录，玩完游戏后看 CSV 就知道哪一刻撞温度墙

---

## 四、高阶玩法选读

### 1. 看内存颗粒厂商（不拆机）

展开 **Memory → DIMM SPD** → 右侧找到 **Module Part Number**  
把编码扔到 [https://www.chiphell.com](https://www.chiphell.com) 或 Reddit 搜索，立刻知道是 **三星 B-die** 还是 **海力士 A-die**，对超频玩家价值千金。

### 2. 计算电源真实功耗

传感器里找到 **CPU Package Power** + **GPU Chip Power** + **12 V Rail Power**  
三者和 × 0.92（电源转换效率）≈ 整机瞬时功耗，比插座功率计误差 < 5 W。

### 3. 自定义“风扇墙”

- 进入 `Customize Values` → 新建 `Fan1_Ratio = (Fan1 RPM / max RPM) * 100`  
- 搭配 [FanControl](https://github.com/Rem0o/FanControl) 插件，HWiNFO 把温度数据通过共享内存喂给 FanControl，实现 **“GPU 核心温度 < 55 ℃ 则风扇 0 RPM”** 的高级曲线，比主板 BIOS 更细。

### 4. 手机实时监控

安卓端安装 **HWiNFO Remote Monitor**（开源）  
扫码即可在局域网看 **CPU 温度、帧率、风扇转速**，直播拷机无需双屏。

---

## 五、HWiNFO vs 主流工具

| 场景 | HWiNFO | AIDA64 | CPU-Z | GPU-Z | OCCT |
|---|---|---|---|---|---|
| 检测深度 | ★★★★★ | ★★★★☆ | ★★ | ★★ | ★ |
| 传感器数量 | 7000+ | 3000+ | 几十 | 显卡专用 | 压力测试 |
| CSV 日志 | ✅ 免费 | ✅ 收费 | ❌ | ❌ | ✅ |
| OSD  overlay | ✅ RTSS | ✅ RTSS | ❌ | ✅ | ❌ |
| 远程监控 | ✅ 插件 | ❌ | ❌ | ❌ | ❌ |
| 体积 | 10 MB | 100 MB+ | 2 MB | 5 MB | 50 MB |

一句话总结：**检测最全、日志最稳、免费最良心。**

---

## 六、常见疑问 FAQ

**Q1. 传感器里一堆“Auxiliary”温度是什么？**  
A：主板未使用的空探头，可右键 `Hide` 之，强迫症福音。

**Q2. 为什么 CPU 温度比 BIOS 低 5 ℃？**  
A：BIOS 使用主板探头，HWiNFO 读取 CPU 内部 TjMax；两者基准不同，**以 HWiNFO 为准**。

**Q3. 日志文件太大怎么办？**  
A：设置 `Split File Size = 100 MB`，并勾选 `Compress CSV`（自动 zip），一周拷机数据压完不到 300 MB。

**Q4. 会触发游戏反作弊吗？**  
A：HWiNFO 仅读取 MSR、SMBus，**不注入驱动**，BattlEye / EAC / VAC 均白名单；若担心，可勾选 `Safe Mode` 关闭内核驱动。

---

## 七、2026 路线图（官方透露）

- Linux 全功能 CLI 版（已内测）  
- 支持 **PCIe 6.0 / CXL 3.0** 新传感器  
- 集成 **AI 健康度预测**（基于历史日志，提前 14 天预警风扇/电容故障）  
- 开放 REST API，可直连 Grafana Cloud，无需插件

---

## 八、结语

从 DOS 时代走到 AI 时代，HWiNFO 始终只做一件事：**把硬件的黑盒变成白盒**。  
它或许没有 RGB 灯效那么炫酷，却是超频玩家、维修工程师、二手贩子、数据中心运维共同的“听诊器”。

**下载链接再提醒一次：**  
[https://www.hwinfo.com/download.php](https://www.hwinfo.com/download.php)  
 portable 版点开即用，**用完你会回来点赞**。

---

> 彩蛋：在 HWiNFO 关于界面连续点击版本号 7 次，会解锁 **“经典 DOS 皮肤”** 传感器主题，复古味拉满 🤎
