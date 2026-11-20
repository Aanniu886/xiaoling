# 第三方组件与来源说明

小灵自有应用源码保持闭源。本仓库公开的是产品说明、发行记录与第三方资料，不把所有内嵌组件统一重新许可。第三方权利、许可证、必要源码与允许的修改/替换权利分别保留。

## 本次发行版的资料适用范围

`0.4.0-r18-261120-1044-protected` 继续使用 `xiaoling-1844-third-party-materials.zip` 与 `xiaoling-scan-source-1.1.0.tgz`。已逐字节核对相关内嵌工具、原始模块、来源与许可证条目未变化；历史资料包中的“1844”表示资料首次发布版本，相关 Termux、Frida 更正及库替换说明也适用于本次发行版。

应用的 RT JNI 桥接有更新，不属于第三方资料包原样复用的声明范围。本次比较不等于对全部 DEX 中第三方代码完成逐类审计。下载本次 Release 的 `SHA256SUMS.txt` 校验最新 APK 与资料附件。

## 对 1844 包内旧说明的更正

### Termux 终端库

所使用的 `termux-app v0.118.3` 中，`terminal-view` 与 `terminal-emulator` 属于 **Apache-2.0** 许可的终端库。Termux 官方维护者在 [issue #4257](https://github.com/termux/termux-app/issues/4257#issuecomment-2473058490) 中明确说明了两个目录的许可，另见[后续维护者说明](https://github.com/termux/termux-app/issues/4257#issuecomment-2474327922)。

1844 APK 内较早的 Termux NOTICE 将这两个库推导为要求整个小灵组合应用提供 GPL 源码，表述不准确；本发布说明纠正该结论。Termux 仓库其他部分及其命令行软件包各有自己的许可证，不因此改为 Apache-2.0。

锁定上游 commit：`5b657c6adf4304e5198951ce815fe0205dcac29c`。保留原版权、Apache-2.0 文本、上游许可证和 JNI 修改补丁说明。

### Frida 运行组件

1844 的实际锁定组件为 **17.24.3 第三方构建**，来源为 [zer0def/undetected-frida](https://github.com/zer0def/undetected-frida/releases/tag/17.24.3)。包内旧 NOTICE 中“官方未修改 16.6.1”的版本/来源表述已过时，以本条与发布附件的锁定清单为准。这里说明来源，不对检测规避效果作保证。

### RT 原始版本包

发布者已确认取得在公开 APK 中再分发现有 RT 包的许可。旧构建清单中的 `redistribution_permission_not_supplied` 是生成当时未收到授权确认的记录，不代表本次发布者重新授予用户任意修改或转售权。原提供方的频道验证和使用条件仍保留，RT 源码不由扫描模块源码替代。

## 主要组件

| 组件 | 版本/来源 | 许可与资料 |
| --- | --- | --- |
| Termux 终端库 | v0.118.3，固定上游 commit | Apache-2.0；保留版权、NOTICE 与修改记录 |
| Termux CLI 软件包 | 随发行版清单固定的 127 个包 | 各包分别适用 GPL/LGPL、BSD、MIT、Apache 等；附包版本与构建配方来源 |
| 小灵扫描 KPM | 1.1.0 / ABI 1 | GPL-2.0；提供对应完整构建源码归档 |
| Rizin | 0.9.1 | 保留 COPYING/COPYING.LESSER 与对应源码归档 |
| DexKit | 2.0.6 | LGPL-3.0；保留许可证、对应库源码和替换说明 |
| Rhino | 1.7.15 | MPL-2.0；提供精确上游源码来源，不把 MPL 扩展到无关自有文件 |
| JNA | 5.13.0 | 使用上游提供的 Apache-2.0 许可选项 |
| Ghidra C++ 核心及本地 runner | 随包版本 | Apache-2.0 及随包声明；不是完整 Ghidra 桌面程序 |
| Perfetto / LLDB | 随包锁定版本 | 保留 Apache/LLVM 等相应声明 |
| TShark / Mono / Cpp2IL | 随包精确版本清单 | 各组件与依赖分别保留许可证及来源 |
| UnityPy / LIEF / il2cpp bridge | 随包锁定版本 | 保留各自许可、来源和已有源码材料 |
| 语音与媒体库/模型 | Sherpa、Vosk、Media3 等 | 按随包 LICENSE/NOTICE 和模型声明处理 |
| CyberStrikeAI 移动组件 | 随包固定移动版本 | 保留 Apache-2.0 与依赖声明；用户运行配置不随包发布 |

发行附件的第三方资料包保留现有许可证、来源锁定信息、已随包提供的源码和本次补充的精确上游资料。源码/配方索引中的版本和链接用于定位材料；不将上游首页链接或二进制哈希冒充完整源码。

对于依法适用的第三方许可，不因小灵应用闭源而撤销用户修改相应库、重新组合，以及调试这些修改所必需的权利。请同时阅读每个组件的完整许可。
