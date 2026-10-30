<p align="center"><img src="icon.png" width="120" alt="K2 Studio 图标"></p>

# 维简 K2 Studio

**WITRN K2 USB 功率表的原生 macOS 上位机**

在 Mac 上查看电压、电流与功率曲线，记录充电过程、分析 CSV，并捕获和解码 USB PD 报文。

作者：[Andyshenjx](https://github.com/Andyshenjx) · **LGPL-3.0-or-later** · **macOS 14+**

> 本项目是独立开发的第三方工具，与 WITRN / 维简官方无关联，未获官方授权或背书。相关名称、商标与图标归各自权利人所有。

## 下载与开始使用

前往 [Releases](https://github.com/Andyshenjx/K2-Studio/releases) 下载现有的 **K2-Studio-2.0.0-macOS-arm64.zip**，解压后将「维简 K2 Studio.app」放入「应用程序」文件夹。

- 当前下载包面向 **Apple Silicon（M 系列）Mac**；Intel Mac 需自行从源码构建。
- 下载包直接来自作者提供的现有 App。本次发布没有重新编译、启动应用或连接硬件验证，未确认与当前源码逐项一致。
- 当前未提供 Developer ID 公证发行保证。若 macOS 阻止打开，请先核对下载来源，再按系统提示在「系统设置 → 隐私与安全性」中处理。
- 用数据线连接 K2 的独立 HID 接口，在「设备」页选择并连接设备。
- PD 抓包需要设备端启用「PD 联机开关」，具体要求请参阅[官方 K2 说明书](https://www.witrn.com/?p=2105)。

## 2.0.0 更新

- 新增「个性化」：表盘、开机图与全部资源。
- 支持 BMP / PNG / JPEG 图片导入、裁剪、缩放与适配，表盘布局编辑、拖动定位、撤销与重做。
- 支持资源保存、搜索、预览、重新编辑，外观工程保存与 `.pic` / BMP 导出，以及通过 DFU 写入设备。
- 增加固件升级入口。

> **固件升级功能未经测试。** 尚未进行实际设备升级、恢复或读回验证，请勿将其视为已验证可用的功能。固件或外观资源写入涉及设备擦写，失败可能导致设备无法正常启动或资源丢失；使用前请了解风险并准备可靠的恢复方式。本次发布未编译或运行验证，个性化资源写入也未做实机验证。

## 功能

| 模块 | 能力 |
| --- | --- |
| 实时测量 | 电压、电流、功率、D+/D−、CC1/CC2、温度原值；本次测量与设备累计容量 |
| 曲线浏览 | 多指标叠加、独立刻度、冻结、光标读数、全程导航、缩放和平移 |
| 文件记录 | CSV 持续保存、暂停与继续、记录间隔和自动停止条件 |
| 历史分析 | 导入 WITRN 官方四列 CSV / 本软件 CSV，全程与区间统计、容量和能量积分 |
| PD 抓包 | 连接后自动保存、筛选、搜索、报文详情、原始十六进制、K2PD 保存与重放 |
| PD 解码 | 常见控制消息、PDO/RDO、PPS、基础 Structured VDM、扩展消息重组与 EPR Capabilities |
| 个性化（2.0.0 新增） | 表盘与开机图编辑、图片适配、布局预览、资源库、工程保存及资源导出与写入 |
| 固件升级（未测试） | 本地固件检查、DFU 检测、备份与恢复、擦写及读回校验；未经实机测试 |
| Mac 体验 | SwiftUI 原生界面、深浅外观、主题色、快捷键、拖放导入与自选保存目录 |

完整操作说明、数据计算规则和快捷键见 [使用指南](USER_GUIDE.md)。

## 兼容设备

| 设备 | 支持情况 |
| --- | --- |
| **WITRN / 维简 K2** | 当前适配目标，USB HID 实时测量与 PD 抓包 |
| 其他型号 | 尚未验证，不承诺兼容 |

应用按 K2 的 USB 标识（VID `0x0716` / PID `0x5060`）识别设备。请使用支持数据传输的 USB 线连接 K2 的独立 HID 接口；PD 抓包需在设备端启用「PD 联机开关」。当前发布包适用于 **Apple Silicon Mac、macOS 14 或更新版本**。以上为代码适配范围，本次发布未进行硬件验证。

## 功能边界
- 正常测量与抓包只接收 HID 输入；固件与个性化维护使用独立 DFU 模式写入，与测量和抓包互斥。不发送诱骗命令或 Feature Report。
- 固件升级功能未经测试；个性化写入也未做实机验证。设备维护仅面向 K2，不提供设备内部设置或设备内部历史记录读取。
- 新功能的格式与操作细节见 Release 源码附件中的 `Documentation/K2PICTURE.md` 和 `Documentation/FIRMWARE.md`。
- PD 解码保留原始报文；CRC 未校验，缺少上下文时不猜测 RDO 物理量。
- 图表预览有抽稀和缓存上限，精确区间统计读取完整记录文件。

## 发布文件与源码

本仓库用于发布应用和使用说明。开发工程以单独的压缩包随 Release 提供，不展开在仓库文件列表中。

[Releases 下载页](https://github.com/Andyshenjx/K2-Studio/releases) 中：

- `K2-Studio-2.0.0-macOS-arm64.zip`：现有 macOS 应用。
- `K2-Studio-source-2.0.0.zip`：本次发布时整理的源码快照、构建工程与许可证；没有重新构建确认与现有 App 完全对应。

## 致谢与开源协议

协议实现参考 JohnScotttt / JohnScott 的 [WITRN_HID_API](https://github.com/JohnScotttt/WITRN_HID_API) 与 [USB_PD_Parser_API_Py](https://github.com/JohnScotttt/USB_PD_Parser_API_Py)；固件协议与容器参考 lliooly 的 [witrn-k2-mac](https://github.com/lliooly/witrn-k2-mac)。具体来源、改编范围和品牌资源说明见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

代码采用 **LGPL-3.0-or-later**，许可证见 [LICENSE](LICENSE) 与 [COPYING](COPYING)。品牌资源不属于本项目 LGPL 授权范围。

## 赞赏

如果这个工具对你有帮助，可以自愿赞赏支持维护。赞赏不影响任何功能。

<img src="andy-support.jpg" width="360" alt="Andy 的赞赏码">

## 反馈与免责声明

欢迎通过 [Issues](https://github.com/Andyshenjx/K2-Studio/issues) 提交问题，注明 macOS 版本、Mac 芯片、K2 固件版本及复现步骤。分享记录前请自行检查设备序列号等信息。

本软件按许可证约定以「原样」提供，不附带担保。当前发布未做编译、运行或硬件验证；测量与协议解码结果需结合实际设备核对。

**商标声明：**「WEIJIAN / 维简」是其各自权利人的注册商标；WITRN 名称、标识及相关图标亦归各自权利人所有。本项目仅为说明适配设备而使用相关名称，不拥有这些商标，也不代表商标权利人。K2 Studio 为独立第三方项目，与上述品牌的商标权利人及官方团队无关联，未获其授权、认可或背书。
