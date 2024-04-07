## 处理窗口事件

窗口是使用该函数创建的`App.NewWindow()`，并且需要使用该函数显示`Show()`。`ShowAndRun()` 的帮助器方法`fyne.Window` 允许您显示窗口并同时运行应用程序。

默认情况下，通过检查函数，窗口的大小将适合显示其内容`MinSize()`（在后面的示例中将详细介绍）。您可以通过调用该方法来设置更大的尺寸`Window.Resize()`。向其中传递一个`fyne.Size`包含使用设备独立像素的宽度和高度的值（这意味着它在不同设备上是相同的），例如，默认情况下要制作一个正方形窗口，我们可以：
```go

	w.Resize(fyne.NewSize(100, 100))
```
请注意，桌面环境可能存在限制，导致窗口小于要求的大小。移动设备通常会忽略这一点，因为它们仅以全屏显示。

如果您希望显示第二个窗口，则只需调用该Show() 函数即可。 如果您想在应用程序启动时打开多个窗口，那么`Window.Show()`拆分也很有帮助。App.Run()下面的示例显示了如何在启动时加载两个窗口。
```go
package main

import (
"fyne.io/fyne/v2"
"fyne.io/fyne/v2/app"
"fyne.io/fyne/v2/widget"
)

func main() {
a := app.New()
w := a.NewWindow("Hello World")

	w.SetContent(widget.NewLabel("Hello World!"))
	w.Show()

	w2 := a.NewWindow("Larger")
	w2.SetContent(widget.NewLabel("More content"))
	w2.Resize(fyne.NewSize(100, 100))
	w2.Show()

	a.Run()
}

```

当两个窗口都关闭时，上述应用程序将退出。如果您的应用程序被安排为一个窗口是主窗口，其他窗口是辅助视图，您可以将一个窗口设置为“主”窗口，以便在该窗口关闭时应用程序退出。为此，请使用SetMaster()上的函数Window。

窗口可以随时创建，我们可以更改上面的代码，使第二个窗口（w2）的内容是一个打开新窗口的按钮。您还可以从更复杂的工作流程加载窗口，但要小心，因为新窗口通常会出现在当前活动内容上方。
```go
w2.SetContent(widget.NewButton("Open new", func() {
		w3 := a.NewWindow("Third")
		w3.SetContent(widget.NewLabel("Third"))
		w3.Show()
	}))

```