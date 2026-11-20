# 第三方库修改与替换

此说明保留 LGPL/MPL 等适用许可证下的权利，不把第三方库的许可扩展为要求公开小灵所有自有源码，也不限制许可证允许的修改及调试这些修改所需的逆向。

## DexKit 2.0.6

本版直接使用 `org.luckypray:dexkit:2.0.6`。对应源码和原始 AAR 的来源在第三方资料包中；源代码适用 LGPL-3.0。小灵没有修改 DexKit 上游源码。

1844 与本次 `0.4.0-r18-261120-1044-protected` 的 R8 配置均包含：

```proguard
-keep class org.luckypray.dexkit.** { *; }
```

该边界保留原类名和成员，不允许对这些库类作混淆、裁剪或优化。APK 本身提供已编译的应用对象代码与资源，可使用 Android DEX/APK 工具将兼容的修改版库与之重新组合。

可复现的替换流程：

1. 按提供的精确 DexKit 源码版本构建修改后的 AAR，保持应用调用的 Java/JNI 接口兼容。保留必要的原生依赖。
2. 使用 Apktool 将发行 APK 解码到新目录。保留其资源和所有非 DexKit 的 smali；在各 `smali*` 目录删除原 `org/luckypray/dexkit/` 库类。
3. 从修改后的 AAR 提取 `classes.jar`，用 Android Build Tools 的 D8（`--min-api 26`）转换成 DEX，再用相同版本的 baksmali 转换为 smali。将生成的 `org/luckypray/dexkit/` 加回解码项目，避免重复类。
4. 用 AAR 的对应 ABI JNI 库替换项目 `lib/<abi>/` 中相同名称的库；不要混用不同版本的 JNI 与 Java 接口。
5. 用 Apktool 重建，再用 `zipalign` 和 `apksigner` 按你自己的密钥对齐、签名。修改版不可使用发布者的私钥；Android 会拒绝与原签名不同的直接覆盖更新。请先备份，再在可恢复的测试设备安装。
6. 检查新的 APK 是否仍有原库类、缺失依赖或 JNI 符号错误，并验证实际 DexKit 查询及应用相关功能。

上述步骤说明重新组合所需材料与方法，不代表任意修改的库都与小灵兼容。修改后产生的 APK 不属于发布者签名的原发行物，原 SHA256 不再适用。本次没有进行修改版库的完整手机运行验收。

## Rhino 1.7.15

使用上游 MPL-2.0 库，未修改上游源文件。精确版本的源代码 JAR 与上游链接随第三方资料提供。若分发修改后的受 MPL 覆盖文件，应按 MPL 提供对应文件源码；这不等于所有无关自有文件都必须公开。

## 单独运行的 CLI 与扫描模块

Termux CLI、Rizin、TShark、扫描 KPM 等是各自运行的组件，各自版权和源码义务独立处理。资料包包含固定的 Termux 构建配方与补丁、包版本索引，以及已提供的组件源码。扫描 KPM 的源码包含编译脚本、协议与兼容性说明，可以单独构建。

保留每个组件的原始许可证。Termux 两个 Android 终端库按 Apache-2.0 处理，不要把它们与 CLI 软件包中各自适用 GPL 的程序混为一谈。
