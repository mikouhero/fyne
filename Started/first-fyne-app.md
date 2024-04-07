
## 第一个Fyne 应用程序
[完成入门](readme.md)文档中的步骤后，您就可以构建您的第一个应用程序了。为了说明该过程，我们将构建一个简单的 hello world 应用程序。

一个简单的应用程序首先使用 app.New() 创建一个应用程序实例，然后使用 app.NewWindow() 打开一个窗口。然后定义一个小部件树，在窗口上使用 SetContent() 将其设置为主要内容。然后通过在窗口上调用 ShowAndRun() 显示应用程序 UI。
    

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello World")

	w.SetContent(widget.NewLabel("Hello World!"))
	w.ShowAndRun()
}

```
可以使用该命令构建上面的代码`go build .`，然后通过运行该hello命令或双击图标来执行。您还可以绕过编译步骤，直接使用`go run .`

如果您喜欢浅色主题，那么只需设置环境变量`FYNE_THEME=light`

## 运行 Fyne 演示
如果您想在开始编写自己的应用程序之前查看 Fyne 工具包的运行情况，可以查看我们的演示应用程序。

### 运行
如果需要，您可以使用以下命令直接运行演示（需要 Go 1.16 或更高版本）：
```
go run fyne.io/fyne/v2/cmd/fyne_demo@latest
```
对于早期版本的 Go，您需要使用以下命令：
```
go run fyne.io/fyne/v2/cmd/fyne_demo
```
通过浏览应用程序的不同选项卡，您可以看到 Fyne 工具包的所有功能。

### 安装
可以像计算机上的所有其他应用程序一样将该应用程序安装为图形应用程序。我们有有用的fyne工具可以为您做到这一点。首先您需要安装该工具：
```
go install fyne.io/fyne/v2/cmd/fyne@latest
```
之后，您可以简单地打包并安装演示应用程序：

```
fyne get fyne.io/fyne/v2/cmd/fyne_demo
```
完成此步骤后，您可以在应用程序启动器中找到“Fyne Demo”。



