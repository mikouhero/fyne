## 开始

使用 Fyne 工具包构建跨平台应用程序非常简单，但在开始之前需要安装一些工具。如果您的计算机设置为使用 Go
进行开发，则可能不需要执行以下步骤，但我们建议您阅读适用于您的操作系统的提示，以防万一。如果本教程中的后续步骤失败，那么您应该重新访问以下先决条件。

## 先决条件

Fyne 需要 3 个基本元素，即 Go 工具（至少版本 1.12）、C 编译器（用于连接系统图形驱动程序）和系统图形驱动程序。这些说明因您的操作系统而异，不同环境系统安装说明。

`请注意，这些步骤只是开发所必需的 - 您的 Fyne 应用程序不需要最终用户进行任何设置或依赖项安装！`

### Windows
1. 从[官网](https://golang.org/dl) 下载 Go并按照说明进行操作
2. 安装适用于 Windows 的可用 C 编译器之一，以下内容已使用 Go 和 Fyne 进行测试：
   - MSYS2 with MingW-w64 - [msys2.org](https://www.msys2.org/)
   - TDM-GCC - [tdm-gcc.tdragon.net](https://jmeubank.github.io/tdm-gcc/download/)
   - Cygwin - [cygwin.com](https://www.cygwin.com/)
3. 在 Windows 中，您的图形驱动程序已安装，但建议确保它们是最新的。

使用MSYS2安装（推荐）步骤如下：

- 从 [msys2.org](https://www.msys2.org/) 安装 MSYS2 
- 安装后请勿使用打开的 MSYS 终端 
- 从开始菜单打开“MSYS2 MinGW 64-bit” 
- 执行以下命令（如果询问安装选项，请务必选择“全部”）：

```
$ pacman -Syu
$ pacman -S git mingw-w64-x86_64-toolchain    
```

- 您需要将 /c/Program\ Files/Go/bin 和 ~/Go/bin 添加到您的 $PATH，对于 MSYS2，您可以将以下命令粘贴到终端中：

```
 $ echo "export PATH=\$PATH:/c/Program\ Files/Go/bin:~/Go/bin" >> ~/.bashrc
```

- 为了让编译器在其他终端上工作，您需要设置 Windows `%PATH%` 变量来查找这些工具。进入“编辑系统环境变量”控制面板，点击“高级”并将“C:\msys64\mingw64\bin”添加到路径列表中。 


### macOS X
1. 从[官网](https://golang.org/dl) 下载 Go并按照说明进行操作
2. 从[Mac App Store](https://apps.apple.com/us/app/xcode/id497799835?mt=12)安装 Xcode
3. 通过打开终端窗口并键入以下内容来设置 Xcode 命令行工具： `xcode-select --install`
4. 在 macOS 中，图形驱动程序已安装。


### Linux

- 您需要使用包管理器安装 Go、gcc 和图形库头文件，以下命令之一可能会起作用。
-  Debian / Ubuntu: `sudo apt-get install golang gcc libgl1-mesa-dev xorg-dev`
-  Fedora: `sudo dnf install golang gcc libXcursor-devel libXrandr-devel mesa-libGL-devel libXi-devel libXinerama-devel libXxf86vm-devel`
-  Arch Linux: `sudo pacman -S go xorg-server-devel libxcursor libxrandr libxinerama libxi`
-  Solus: `sudo eopkg it -c system.devel golang mesalib-devel libxrandr-devel libxcursor-devel libxi-devel libxinerama-devel`
-  openSUSE: `sudo zypper install go gcc libXcursor-devel libXrandr-devel Mesa-libGL-devel libXi-devel libXinerama-devel libXxf86vm-devel`
-  Void Linux: `sudo xbps-install -S go base-devel xorg-server-devel libXrandr-devel libXcursor-devel libXinerama-devel`
-  Alpine Linux: `sudo apk add go gcc libxcursor-dev libxrandr-dev libxinerama-dev libxi-dev linux-headers mesa-dev`
-  NixOS `nix-shell -p libGL pkg-config xorg.libX11.dev xorg.libXcursor xorg.libXi xorg.libXinerama xorg.libXrandr xorg.libXxf86vm`


## 安装

使用 Go 模块时（Go 1.16 及更高版本需要），您需要先设置模块，然后才能使用包。

Go modules （适用于 Go 1.16 或更高版本）
如果您没有使用模块或者已经初始化了模块，则可以跳到下一步。运行以下命令并替换`MODULE_NAME`为您首选的模块名称（应在特定于您的应用程序的新文件夹中调用该名称）。
```angular2html
$ cd myapp
$ go mod init MODULE_NAME
```

您现在需要下载 Fyne 模块和帮助工具。这将使用以下命令完成：
```angular2html
$ go get fyne.io/fyne/v2@latest
$ go install fyne.io/fyne/v2/cmd/fyne@latest
```

如果您不确定 Go 模块如何工作，请考虑阅读教程：创建 Go 模块。

### 较旧的 Go 安装
要使用较旧的 Go 版本安装 Fyne 工具包和帮助程序，只需执行 go get 命令：
```angular2html
$ go get fyne.io/fyne/v2
$ go get fyne.io/fyne/v2/cmd/fyne
```

### 检查您的安装
在编写应用程序或运行示例之前，您可以使用Fyne [安装工具检查安装](https://docs.fyne.io/faq/troubleshoot) 。只需从链接下载适合您计算机的应用程序并运行它，您应该会看到类似以下屏幕的内容：
![](https://docs.fyne.io/images/started/setup.png)

如果您的安装有任何问题，请参阅故障排除部分以获取提示。

### 运行演示
如果您想在开始编写自己的应用程序之前查看 Fyne 工具包的运行情况，您可以通过执行以下命令来查看我们的演示应用程序在您的计算机上运行：
```
$ go run fyne.io/fyne/v2/cmd/fyne_demo@latest
```
请注意，第一次运行必须编译一些 C 代码，因此可能需要比平时更长的时间。后续构建会重用缓存，速度会快得多。

### 较旧的 Go 版本
要在旧版本的 Go 上运行演示，只需执行以下命令：
```
$ go run fyne.io/fyne/v2/cmd/fyne_demo

```
安装
如果需要，您还可以使用以下命令安装演示（需要 Go 1.16 或更高版本）：
```
$ go install fyne.io/fyne/v2/cmd/fyne_demo@latest

```
对于早期版本的 Go，您需要使用以下命令：
```
$ go get fyne.io/fyne/v2/cmd/fyne_demo
```
如果您的`GOBIN`环境已添加到路径（macOS 和 Windows 上应默认为），则可以运行演示：

```
$ fyne_demo
```


