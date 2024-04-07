## 打包移动端App
您的 Fyne 应用程序代码将作为移动应用程序开箱即用，就像桌面应用程序一样。然而，打包代码进行分发要复杂一些。本页将探讨在 iOS 和 Android 上获取应用程序的过程。

首先你需要安装更多的开发工具来完成移动打包。对于 Android 构建，您必须安装 Android SDK 和 NDK，并设置适当的环境，以便adb可以在命令行上找到工具（例如）。要构建 iOS 应用程序，您需要在 macOS 计算机上安装 Xcode 以及命令行工具可选包。

一旦你有了一个有效的开发环境，打包就很简单了。要构建适用于 Android 和 iOS 的应用程序，以下命令将为您完成所有操作。确保有一个唯一的应用程序标识符，因为在首次发布后更改这些标识符是不明智的。
```bash 

fyne package -os android -appID com.example.myapp -icon mobileIcon.png
fyne package -os ios -appID com.example.myapp -icon mobileIcon.png
```
这些命令完成后（第一次编译可能需要一些时间），您将在目录中看到两个新文件，`myapp.apk`以及 `myapp.app`.您将看到后者与 darwin 应用程序包同名 - 不要让它们混淆，因为它们不能在其他平台上工作。

要在您的手机或模拟器上安装 Android 应用程序，只需调用：
```bash 
adb install myapp.apk
```
要在设备上安装 iOS，请打开 Xcode，然后选择“窗口”菜单中的“设备和模拟器”菜单项。然后找到您的手机并将myapp.app图标拖到您的应用程序列表中。

如果您想在模拟器上安装，请确保使用iossimulatorvs打包您的应用程序ios
```bash 
fyne package -os iossimulator -appID com.example.myapp -icon mobileIcon.png
```
之后您可以使用命令行工具，如下所示：
```bash 
xcrun simctl install booted myapp.app
```
