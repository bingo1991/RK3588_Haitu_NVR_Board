# Haitu HT-RK3588 Board

[HT-RK3588](http://www.haitutech.com/proinfo/74.html)是常州海图信息科技股份有限公司的一款RK3588定制板。


### 硬件配置信息 
- CPU: Rk3588
- Memery: 2 x 4GB LPDDR4X@2122MHz, K4UBE3D4AA-MGCL(Samsung, BGA200, 4266Mbps)
- Storage: 32GB eMMC 5.1, KLMBG2JETD-B041(Samsung)
- Power In: 12V DC5525
- Network: 2 x 1GbE(RTL8211 PHY)
- Display: 2 x HDMI 2.1 TX
- Video In: 2 x HDMI 2.0 RX, one with LT6911UXC
- Power Out: 1 x 4Pin D4 (for SATA Power) 
- SATA: 2 x SATA 3.0
- USB:
  - 1 x USB 3.0 Type-A
  - 2 x USB 2.0 Type-A
  - 1 x USB Type-C OTG
- Button: MaskRom, Reset, Recovery, Power On/Off
- FAN: 1 x 4Pin PH2.54 PWM Fan Connector
- UART: 1 x Debug, 1 x RS485, 1 x RS232
- JTAG: 1 x ARM JATG, 1 x MCU JTAG

┌────────────────────────────────────────────────────────────┐
│              海图 HT-RK3588 单板硬件拓扑                   │
├────────────────────────────────────────────────────────────┤
│                                                            │
│┌──────────┐                                                │
││12V DC输入│                                                │
│└────┬─────┘                                                │
│     │                                                      │
│     ├───────────────────────────────────────────────┐      │
│     │                                               │      │
│     ▼                                               ▼      │
│┌──────────┐                                  ┌───────────┐ │
││5V系统电源│                                  │ RK806 PMIC│ │
││ (常开)   │                                  │ (电源管理)│ │
│└───┬──────┘                                  └──────┬────┘ │
│    │                                                │      │
│    ├──────┬───────┬─────────┬───────────┐           │      │
│    │      │       │         │           │           │      │
│    ▼      ▼       ▼         ▼           ▼           ▼      │
│┌──────┐┌─────┐┌──────┐┌──────────┐┌──────────┐┌──────────┐ │
││ USB  ││ USB ││ PCIe ││RK8602/0  ││RK8603/1  ││RK8602/NPU│ │
││ Host ││ OTG ││ 3.3V ││CPU大核0  ││CPU大核1  ││NPU 供电  │ │
││ 5V   ││ 5V  ││      ││0.55-1.05V││0.55-1.05V││0.55-0.95V│ │
│└──────┘└─────┘└──────┘└──────────┘└──────────┘└──────────┘ │
│                                                            │
│┌──────────────────────────────────────────────────────────┐│
││                      RK3588 SoC                          ││
││┌───────────┐┌─────────┐┌────────┐┌───────────┐           ││
│││CPU Cluster││   GPU   ││  NPU   ││  DDR Ctrl │           ││
│││(A76+A55)  ││Mali-G610││ 6TOPS  ││ (2112MHz) │           ││
││└───────────┘└─────────┘└────────┘└───────────┘           ││
││                                                          ││
││┌───────────────────────────────────────────────────────┐ ││
│││                       外设接口控制器                  │ ││
│││┌───────┐┌───────┐┌──────┐┌───────┐┌───────┐┌────────┐ │ ││
││││ GMAC0 ││ GMAC1 ││PCIe3 ││SATA0/1││ SDHCI ││  VOP2  │ │ ││
││││ RGMII ││ RGMII ││ x2   ││SATA3  ││ eMMC  ││显示输出│ │ ││
│││└───┬───┘└───┬───┘└──┬───┘└───┬───┘└───┬───┘└───┬────┘ │ ││
│││    │        │       │        │        │        │      │ ││
│││┌───┴───┐┌───┴───┐┌──┴───┐┌───┴───┐┌───┴───┐┌───┴────┐ │ ││
││││HDMI0/1││HDMI RX││LT6911││  USB  ││ 网络  ││ 存储   │ │ ││
││││ 输出  ││ 内置  ││外置  ││  Host ││ PHY   ││ 设备   │ │ ││
│││└───────┘└───────┘└──────┘└───────┘└───────┘└────────┘ │ ││
││└───────────────────────────────────────────────────────┘ ││
│└──────────────────────────────────────────────────────────┘│
│┌──────────────────────────────────────────────────────────┐│
││                          外部物理接口                    ││
││┌────────┐┌────────┐┌─────────┐┌─────────┐┌────────┐      ││
│││RJ45 #0 ││RJ45 #1 ││HDMI0 Out││HDMI1 Out││HDMI In │      ││
│││千兆网口││千兆网口││8K 输出  ││4K 输出  ││双路输入│      ││
││└────────┘└────────┘└─────────┘└─────────┘└────────┘      ││
││┌──────┐┌─────┐┌─────┐┌─────────┐┌─────────┐┌──────┐      ││
│││ USB3 ││USB2 ││USB2 ││M.2 NVMe ││SATA 接口││Type-C│      ││
│││ Host ││Host0││Host1││PCIe 3.0 ││  x2     ││OTG+PD│      ││
││└──────┘└─────┘└─────┘└─────────┘└─────────┘└──────┘      ││
│└──────────────────────────────────────────────────────────┘│
└────────────────────────────────────────────────────────────┘

### 双路HDMI输入方案
┌────────────────────────────────────────────────────────────┐
│                      HDMI 输入双方案对比                   │
├────────────────────────────────────────────────────────────┤
│                                                            │
│方案 A: RK3588 内置 HDMI RX                                 │
│┌────────┐   ┌───────────────────┐   ┌─────────────────────┐│
││HDMI 源 │──→│RK3588 内置 HDMI RX│──→│VOP2 / DRM 显示子系统││
││输入接口│   │(&hdmirx_ctrler)   │   │(直接显示/采集)      ││
│└────────┘   └───────────────────┘   └─────────────────────┘│
│    │                  │                      │             │
│    │                  ├──→ I2S7 (8ch) 音频   │             │
│    │                  ├──→ DDC (0x50) EDID   │             │
│    │                  ├──→ CEC 控制          │             │
│    │                  └──→ GPIO0_PA4 (HPD)   │             │
│                                                            │
├────────────────────────────────────────────────────────────┤
│                                                            │
│方案 B: LT6911UXC 外置桥接方案                              │
│┌────────┐   ┌──────────────────┐   ┌─────────────────┐     │
││HDMI 源 │──→│LT6911UXC 桥接芯片│──→│MIPI CSI2 (4Lane)│     │
││输入接口│   │(&lt6911uxc@2b)   │   │(&csi2_dphy0)    │     │
│└────────┘   └──────────────────┘   └─────────────────┘     │
│    │                 │                      │              │
│    │                 ├──→ I2S2 (2ch) 音频   │──→ CIF/RKISP │
│    │                 ├──→ I2C6 (0x2B) 控制  │       采集   │
│    │                 ├──→ GPIO4_PA2 (复位)  │              │
│    │                 ├──→ GPIO4_PA5 (中断)  │              │
│    │                 └──→ 24MHz 时钟源      │              │
│                                                            │
└────────────────────────────────────────────────────────────┘

### GPIO Pin定义

| 功能模块 | 信号名称 | GPIO 编号 | 引脚位置 | 有效电平 | 用途说明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PCIe 3.0** | `vcc3v3_pcie30_en` | GPIO2 | PB4 | High | M.2 接口 3.3V 电源使能 |
| **PCIe 3.0** | `pcie3x4_reset` | GPIO4 | PB6 | High | M.2 NVMe 设备复位 |
| **USB Host** | `vcc5v0_host_en` | GPIO3 | PC1 | High | USB Host 端口 5V 电源使能 |
| **USB Host2** | `vcc5v0_usb2_en` | GPIO3 | PC0 | High | USB 2.0 Host 端口 5V 电源使能 |
| **USB OTG** | `vcc5v0_otg_en` | GPIO4 | PA7 | High | Type-C 接口 VBUS 电源使能 |
| **以太网 0** | `gmac0_reset` | GPIO4 | PB2 | Low | 主网口 PHY 芯片复位 |
| **以太网 1** | `gmac1_reset` | GPIO4 | PB3 | Low | 备用网口 PHY 芯片复位 |
| **HDMI 输出 0** | `hdmi0_en` | GPIO4 | PB1 | High | HDMI0 接口使能/热插拔检测 |
| **HDMI 输入 (内置)** | `hdmirx_det` | GPIO0 | PA4 | Low | HDMI 输入信号插入检测 |
| **HDMI 输入 (外置)** | `lt6911_reset` | GPIO4 | PA2 | Low | LT6911UXC 桥接芯片复位 |
| **HDMI 输入 (外置)** | `lt6911_int` | GPIO4 | PA5 | Low | LT6911UXC 中断信号 |
| **Type-C** | `fusb302_int` | GPIO1 | PA0 | Low | FUSB302 PD 控制器中断 |
| **RTC 时钟** | `rtc_int` | GPIO2 | PB5 | Low | 实时时钟闹钟/唤醒中断 |
| **SATA 0** | `sata0_reset` | GPIO4 | PA0 | High | SATA 接口 0 复位 |
| **SATA 1** | `sata1_reset` | GPIO4 | PA1 | High | SATA 接口 1 复位 |

### I2C拓扑

| 总线名称 | 设备名称 | I2C 地址 | 设备类型 | 物理接口 | 用途 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **I2C0** | `rk8602@42` | 0x42 | DCDC Regulator | 板载 | CPU 大核 0 供电 (vdd_cpu_big0) |
| **I2C0** | `rk8603@43` | 0x43 | DCDC Regulator | 板载 | CPU 大核 1 供电 (vdd_cpu_big1) |
| **I2C1** | `rk8602@42` | 0x42 | DCDC Regulator | 板载 | NPU 供电 (vdd_npu) |
| **I2C3** | `fusb302@22` | 0x22 | Type-C Controller | Type-C 接口 | PD 协议/角色切换 |
| **I2C6** | `hym8563@51` | 0x51 | RTC | 板载 | 实时时钟 |
| **I2C6** | `lt6911uxc@2b` | 0x2B | HDMI→MIPI 桥 | HDMI 输入接口 B | 视频转换控制 |
| **DDC0** | `EDID` | 0x50 | EEPROM | HDMI0 输出接口 | 读取显示器 EDID |
| **DDC1** | `EDID` | 0x50 | EEPROM | HDMI1 输出接口 | 读取显示器 EDID |
| **DDC_RX** | `EDID` | 0x50 | EEPROM | HDMI RX 输入接口 | 写入板端 EDID |

> ⚠️ **注意**：DDC 通道通过 HDMI 接口专用引脚通信，不占用系统 I2C 控制器编号，EDID 标准地址固定为 0x50。

### 音视频信号
| 接口 | 方向 | 视频 | 音频 | DDC/I2C 引脚 | CEC 引脚 | HPD 检测 | 设备树状态 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **HDMI0** | 输出 | ✅ | ✅ (I2S5) | HDMIM0_TX0_SCL/SDA | HDMIM0_TX0_CEC | GPIO4_PB1 | `okay` |
| **HDMI1** | 输出 | ✅ | ✅ (I2S6) | HDMIM2_TX1_SCL/SDA | HDMIM2_TX1_CEC | HDMIM0_TX1_HPD | `okay` |
| **HDMI RX** | 输入 | ✅ | ✅ (I2S7) | HDMIM2_RX_SCL/SDA | HDMIM2_RX_CEC | GPIO0_PA4 | `okay` |
| **LT6911** | 输入 | ✅ (MIPI) | ✅ (I2S2) | I2C6 (0x2B) | ❌ | GPIO4_PA5 | `okay` |

| 音频节点名称 | CPU 侧 DAI (控制器) | 编解码器侧 (Codec) | 格式 | 用途 | 状态 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `dp0_sound` | `&spdif_tx2` | `&dp0` | SPDIF | Type-C DP 音频输出 | ✅ 开启 |
| `hdmi0_sound` | `&i2s5_8ch` | `&hdmi0` | I2S 8 通道 | HDMI 0 音频输出 | ⚠️ 默认关闭 |
| `hdmi1_sound` | `&i2s6_8ch` | `&hdmi1` | I2S 8 通道 | HDMI 1 音频输出 | ⚠️ 默认关闭 |
| `hdmiin_sound` | `&i2s7_8ch` | `&hdmirx_ctrler` | I2S 8 通道 | HDMI 输入音频采集 (内置) | ✅ 开启 |
| `lt6911_sound` | `&i2s2_2ch` | `&lt6911_dc` | I2S 2 通道 | HDMI 输入音频采集 (外置) | ✅ 开启 |

### 外设接口信息汇总
| 接口类别 | 接口名称 | 控制器节点 | 物理规格 | 工作模式 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **网络** | Ethernet 0 | `&gmac0` | RJ45 | RGMII (10/100/1000M) | 主网口，PHY 地址 0x1 |
| **网络** | Ethernet 1 | `&gmac1` | RJ45 | RGMII (10/100/1000M) | 备用网口，PHY 地址 0x1 |
| **存储** | eMMC | `&sdhci` | BGA 封装 | 8-bit HS400 | 板载存储，不可移除 |
| **存储** | M.2 Slot | `&pcie3x4` | M-Key | PCIe 3.0 x2 | 支持 NVMe SSD |
| **存储** | SATA 0 | `&sata0` | SATA 端口 | SATA 3.0 | 需外接硬盘 |
| **存储** | SATA 1 | `&sata1` | SATA 端口 | SATA 3.0 | 需外接硬盘 |
| **显示** | HDMI 0 | `&hdmi0` | HDMI Type-A | Output (Tx) | 支持音频输出 (I2S5) |
| **显示** | HDMI 1 | `&hdmi1` | HDMI Type-A | Output (Tx) | 支持音频输出 (I2S6) |
| **显示** | HDMI In (内置) | `&hdmirx_ctrler` | HDMI Type-A | Input (Rx) | RK3588 内置 HDMI RX 控制器 |
| **显示** | HDMI In (外置) | `&lt6911uxc` | HDMI Type-A | Input (Rx) | LT6911 转 MIPI CSI2 输入 |
| **USB** | Type-C | `&usbdrd_dwc3_0` | USB Type-C | OTG (Host/Device) | 支持 PD 充电及 DP 输出 |
| **USB** | USB 3.0 | `&usbhost_dwc3_0` | USB Type-A | Host | 高速主机接口 |
| **USB** | USB 2.0 | `&usb_host0` | USB Type-A | Host | 普通主机接口 |
| **USB** | USB 2.0 | `&usb_host1` | USB Type-A | Host | 普通主机接口 |
| **摄像** | MIPI CSI | `&mipi2_csi2` | FPC 连接器 | 4-Lane Input | 用于接收 LT6911 转换信号 |

### 电源域信息
| 电源名称 | 电压值 | 类型 | 输入来源 | 用途 | 控制方式 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `vcc12v_dcin` | 12.0V | 固定输入 | DC 插座 | 系统主输入电源 | 常开 |
| `vcc5v0_sys` | 5.0V | 固定稳压 | 12V 转换 | 系统 5V 总线 | 常开 |
| `vcc3v3_pcie30` | 3.3V | 固定稳压 | 12V 转换 | PCIe M.2 插槽供电 | GPIO2_PB4 控制 |
| `pcie30_avdd1v8` | 1.8V | 固定稳压 | 1.8V 源 | PCIe PHY 模拟电源 | 常开 |
| `pcie30_avdd0v75` | 0.75V | 固定稳压 | 0.75V 源 | PCIe PHY 核心电源 | 常开 |
| `vdd_cpu_big0` | 0.55-1.05V | DCDC (RK8602) | 5V 系统 | CPU 大核 0 供电 | I2C0 动态调压 |
| `vdd_cpu_big1` | 0.55-1.05V | DCDC (RK8603) | 5V 系统 | CPU 大核 1 供电 | I2C0 动态调压 |
| `vdd_npu` | 0.55-0.95V | DCDC (RK8602) | 5V 系统 | NPU 供电 | I2C1 动态调压 |
| `vcc5v0_otg` | 5.0V | 固定稳压 | 5V 系统 | Type-C VBUS 输出 | GPIO4_PA7 控制 |
| `vcc5v0_host` | 5.0V | 固定稳压 | 5V 系统 | USB Host VBUS 输出 | GPIO3_PC1/PC0 控制 |

![HT-RK3588 NVR Board](/HT-RK3588.png)
![HT-RK3588 NVR Interface](/Brief.png)
