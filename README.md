# OPPO Find X8 Ultra AGC 9.6 V5 滤镜 SO 研究

这是一个面向 OPPO Find X8 Ultra 的 AGC 9.6 V5 滤镜原生库研究项目。

## 基础环境

- 手机：OPPO Find X8 Ultra
- 相机：BigKaka AGC 9.6.19 V5.0
- APK 构建版本：9.6.080.695519101.19
- ABI：ARM64 / arm64-v8a
- 配置底座：`Legendary_9.6_X8Ultra_v4_capture_fix_builtin_filters.agc`
- 当前底座状态：四颗镜头可以正常启用，照片可以正常拍摄和保存

## 项目目标

制作一个真正由 ARM64 `.so` 执行滤镜处理的原生库，并通过 AGC 配置中的库名、profile 和滤镜参数调用它。

目标风格包括：

- 哈苏 Hasselblad
- 徕卡 Leica
- 蔡司 Zeiss
- 胶片和黑白风格
- 人像、电影、复古等色彩风格

## 重要说明

`.agc` 只是配置和调用钥匙，不是滤镜算法本体。真正的滤镜处理逻辑和色彩数据必须位于 `.so` 内部。

当前已确认 AGC V5 中存在以下滤镜相关调用：

- `initCustomLib`
- `initCustomLut`
- `CubeUtil`
- `ImageProcessing.setLutParamters`
- `lib_custom_lib_open_key`
- `lib_lut_key`
- `lib_lut_id_key`
- `lib_lut_intensity_key`

目前仍需要确认第三方滤镜 SO 的原生 ABI、图像输入输出格式和调用生命周期。

## 当前进展

已经完成：

- 四颗镜头配置适配；
- 拍照保存问题修复；
- AGC V5 APK 和 DEX 静态分析；
- 自定义库和 LUT 相关字段整理；
- 当前 SO 的 ARM64 架构与导出符号分析。

尚未完成：

- 真正兼容 AGC 9.6 V5 的滤镜 `.so`；
- 将 70 组滤镜算法烧录进原生库；
- 在手机上验证滤镜实际改变成片。

欢迎提供已经实际生效的 AGC 9.6 V5 `.so + .agc` 配套样本。
