# Lucent Fold — Android

直板 Android 手机上的“虚拟折叠 / 霜玻璃”效果 Demo。应用通过旋转矢量、陀螺仪和重力传感器估算手机姿态，将设备倾角映射到虚拟折叠角；Android 13+ 使用 AGSL RuntimeShader 做透视重投影与霜玻璃效果。

## 已整理内容

- 原生 Android + Jetpack Compose
- `minSdk 26` / `targetSdk 35`
- Android 13+ 使用 AGSL；旧系统使用 `rotateY + RenderEffect` 降级方案
- 旋转矢量优先，陀螺仪预测，重力/加速度计回退
- 手动滑块、体感模式、校准
- 屏幕常亮、竖屏、沉浸式显示
- 已移除 Web/PWA 项目依赖
- 已修复 `PreviewScreen.kt` 中重复 `Modifier` 导致的 Kotlin 编译错误
- 已避免 Activity 与 Compose 同时重复注册传感器监听
- 附带 GitHub Actions，可在云端直接构建 APK

## Android Studio

用 Android Studio 打开本目录：

`android/LucentFold/`

即包含 `settings.gradle.kts` 的目录。

推荐 JDK 17。Android Studio 会自动识别 Gradle 项目；如果本机没有 Gradle Wrapper，使用 Android Studio 的 Gradle 设置生成/同步即可。

构建：

`Build > Make Project`

Debug APK 输出：

`app/build/outputs/apk/debug/app-debug.apk`

## 不使用电脑：GitHub Actions 云端构建

本项目包含：

`.github/workflows/build-apk.yml`

将整个项目上传到 GitHub 仓库后，在仓库的 **Actions** 中运行 **Build Lucent APK**。构建完成后，从该 workflow 的 Artifacts 下载 `LucentFold-debug-apk`，其中的 `app-debug.apk` 可传到 Android 手机安装。

Workflow 使用 JDK 17、Gradle 8.9、Android SDK 35。

## 真机使用

1. 安装 APK。
2. 打开 Lucent。
3. 首次默认是“手动”模式。
4. 点击“体感”。
5. 将手机保持在希望作为零点的姿态，点击“校准”。
6. 左右倾斜/转动手机，观察虚拟折叠。

## 注意

这不是对真实 Android 系统 UI 的替换，也不能让普通直板手机获得真正的物理折叠屏结构；它是在应用自身画布内模拟折叠视觉效果。
