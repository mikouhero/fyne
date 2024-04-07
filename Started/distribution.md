## 上架到应用商店
如打包页面中所述打包图形应用程序 提供了可以直接共享或分发的文件或捆绑包。然而，签名并上传到应用程序商店和市场是一个额外的步骤，需要特定于平台的配置，我们将在本页中介绍这一点。

在每个步骤中，我们将使用一个新工具，它是 fyne 命令行实用程序的一部分。该fyne release步骤处理每个商店的签名和准备，但参数因平台而异，如下所示。

### macOS 应用商店（自 fyne 1.4.2 起）
先决条件：

- 运行 macOS 和 Xcode 的 Apple Mac
- 苹果开发者帐户
- Mac App Store应用程序证书
- Mac App Store 安装程序证书
- App Store 中的 Apple Transporter 应用
- 设置您的应用程序/版本，准备好在AppStore Connect上上传构建版本 。
2. 打包完成的应用程序进行发布：
```bash
$ fyne release -appID com.example.myapp -appVersion 1.0 -appBuild 1 -category games
```
3. 将 拖至`.pkg`Transporter 上，然后点击“提交”。

4. 返回 AppStore Connect 网站，选择要发布的版本并提交以供审核。

### Google Play 商店（安卓）
先决条件：

- Google Play 管理中心帐户
- 分发密钥库（ android 文档中的创建说明）

1. 设置您的应用程序/版本，准备好在Google Play Console上上传 。关闭“Play 应用程序签名”选项，因为我们自己管理它。
2. 打包完成的应用程序进行发布

```bash 
$ fyne release -os android -appID com.example.myapp -appVersion 1.0 -appBuild 1
```

3. 将.apk文件拖到 Play 管理中心应用版本页面的构建拖放区域中
4.开始推出新版本。

### iOS 应用商店（自 fyne 1.4.1 起）
先决条件：

- 运行 macOS 和 Xcode 的 Apple Mac
- 苹果开发者帐户
- iOS App Store分发证书
- App Store 中的 Apple Transporter 应用
1. 设置您的应用程序/版本，准备在AppStore Connect上上传构建版本 。

2. 打包完成的应用程序进行发布：
```bash 
$ fyne release -os ios -appID com.example.myapp -appVersion 1.0 -appBuild 1
 ```
3. 将 拖至.ipaTransporter 上，然后点击“交付”。
4. 返回 AppStore Connect 网站，选择要发布的版本并提交以供审核。