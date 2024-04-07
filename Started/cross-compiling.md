## 针对不同平台进行编译

使用 Go 进行交叉编译的设计很简单 - 我们只需GOOS为目标操作系统设置环境变量（GOARCH如果针对不同的体系结构）。不幸的是，当使用本机图形调用时，在 Fyne 中使用 CGo 会使这变得有点困难。

### 从开发计算机编译

要交叉编译 Fyne 应用程序，您还必须设置CGO_ENABLED=1告诉 go 启用 C 编译器（当目标平台与当前系统不同时，通常会关闭该编译器）。不幸的是，这样做意味着您必须有一个适合您要编译的目标平台的 C
编译器。安装适当的编译器后，您还需要设置CC环境变量来告诉 Go 使用哪个编译器。

有多种方法可以安装所需的工具 - 以及可以使用的不同工具。 Fyne 开发人员推荐的配置是：

| GOOS (target) | CC | provider | download | notes |
|-------|-------|-------|-------|-------|
| darwin | o32-clang | osxcross |from github.com |您还需要安装 macOS SDK（下载链接中的说明） |
| windows |x86_64-w64-mingw64-gcc    | mingw64 |package manager |对于 macOS，请使用自制程序 |
| linux |gcc or x86_64-linux-musl-gcc | gcc or musl-cross |cygwin or package manager |musl-cross 可从homebrew获得，以提供 Linux gcc。您还需要安装 X11 和 mesa 头文件以进行编译。 |

设置上面的环境变量后，您应该能够以通常的方式进行编译。如果出现更多错误，则可能是由于缺少软件包造成的。某些目标平台需要安装额外的库或标头才能成功编译。

### 使用虚拟环境

由于 Linux 系统能够轻松地交叉编译到 macOS 和 Windows，因此当您不使用 Linux 进行开发时，使用虚拟化环境会更简单。 Docker 镜像是用于复杂构建配置的有用工具，这也适用于 Fyne。可以使用不同的工具。
Fyne 开发人员推荐的工具是fyne-cross。它受到xgo的启发，并使用构建在golang-cross映像之上的docker 映像，其中包括适用于 Windows 的 MinGW 编译器、macOS SDK 以及 Fyne 要求。

fyne-cross 允许为以下目标构建二进制文件并创建分发包：

| GOOS         | GOARCH | 
|--------------|--------|
| darwin    | amd64  |
| darwin    | 386    |
| linux    | amd64  |
| linux    | 386    |
| linux|    arm64  |
| linux    | arm    |
| windows    | amd64 |
| windows|    386  |
| android    | amd64 |
| android    | 386  |
| android|    arm64 |
| android    | arm  |
| ios       |       |
| freebsd    | amd64 |
| freebsd    | arm64 |
|
> 注意：仅 darwin 主机支持 iOS 编译。

要求
- go >= 1.13
- docker

##### 安装
您可以fyne-cross使用以下命令进行安装（需要 Go 1.16 或更高版本）：
```bash

go install github.com/fyne-io/fyne-cross@latest
```
对于早期版本的 Go，您需要使用以下命令：
```bash
go get github.com/fyne-io/fyne-cross
```
#####  用法

```bash 
fyne-cross <command> [options]

The commands are:

	darwin        Build and package a fyne application for the darwin OS
	linux         Build and package a fyne application for the linux OS
	windows       Build and package a fyne application for the windows OS
	android       Build and package a fyne application for the android OS
	ios           Build and package a fyne application for the iOS OS
	freebsd       Build and package a fyne application for the freebsd OS
	version       Print the fyne-cross version information

Use "fyne-cross <command> -help" for more information about a command.

```

#####  通配符
该arch标志支持通配符，以防想要针对指定 GOOS 的所有受支持的 GOARCH 进行编译

##### 例子：
```bash 
fyne-cross windows -arch=*
```
相当于
```bash 
fyne-cross windows -arch=amd64,386
```
#####  例子
下面的示例交叉编译并打包fyne 示例应用程序
```bash 
git clone https://github.com/fyne-io/examples.git
cd examples
```

编译并打包主要示例应用程序
```bash 
fyne-cross linux
```
注意：默认情况下 fyne-cross 会将包编译到当前目录中。

上面的命令相当于：`fyne-cross linux .`

编译并打包特定的示例应用程序
```bash 
fyne-cross linux -output bugs ./cmd/bugs
```
