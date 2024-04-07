## 桌面包装
打包图形应用程序进行分发可能很复杂。图形应用程序通常具有与其关联的图标和元数据，以及与每个环境集成所需的特定格式。 Windows 可执行文件需要嵌入图标，macOS 应用程序是捆绑包，而 Linux 则需要安装各种元数据文件。真麻烦啊！

值得庆幸的是，“fyne”应用程序有一个“package”命令可以自动处理这个问题。只需指定目标操作系统和任何所需的元数据（例如图标）即可生成适当的包。 .icns 或 .ico 的图标转换将自动完成，因此只需提供 .png 文件:)。您所需要的只是已经为目标平台构建了应用程序......
```bash
go install fyne.io/fyne/v2/cmd/fyne@latest
fyne package -os darwin -icon myapp.png
```

如果您使用旧版本的 Go (<1.16)，您应该使用以下命令安装 fynego get
```bash
go get fyne.io/fyne/v2/cmd/fyne
fyne package -os darwin -icon myapp.png
```
将创建 myapp.app，这是一个用于分发给 macOS 用户的完整捆绑包结构。然后您也可以构建 Linux 和 Windows 版本......
```bash
fyne package -os linux -icon myapp.png
fyne package -os windows -icon myapp.png
```
这些命令将创建：

myapp.tar.gz 包含一个从 usr/local/ 开始的文件夹结构，Linux 用户可以将其扩展到系统的根目录。
myapp.exe（在第二次构建之后，这是 Windows 软件包所需的）将嵌入图标和应用程序元数据。
如果您只想在计算机上安装桌面应用程序，那么您可以使用有用的 install 子命令。例如，要在整个系统范围内安装当前的应用程序，您只需执行以下命令：
```bash
fyne install -icon myapp.png
```
所有这些命令还支持默认图标文件，Icon.png以便您可以避免每次执行时键入参数。从 Fyne 2.1 开始，还有一个 元数据文件，您可以在其中为项目设置默认选项。

当然，如果您愿意，您仍然可以使用标准 Go 工具运行应用程序。