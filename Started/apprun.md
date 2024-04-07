## Application and RunLoop

为了使 GUI 应用程序正常工作，它需要运行一个事件循环（有时称为 runloop）来处理用户交互和绘图事件。在 Fyne 中，这是使用`App.Run()` 或`Window.ShowAndRun()`函数开始的。其中之一必须从函数中设置代码的末尾调用`main()`。

一个应用程序应该只有一个运行循环，因此您应该`Run()`在代码中只调用一次。第二次调用会出错

```go
package main

import (
	"fmt"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Hello")
	myWindow.SetContent(widget.NewLabel("Hello"))

	myWindow.Show()
	myApp.Run()
	tidyUp()
	//tidyUp函数在main函数的末尾被调用，但在myApp.Run()之后
	//在Fyne应用程序中，Run方法会阻塞，直到应用程序退出。
	//因此，tidyUp函数实际上会在应用程序窗口关闭且事件循环结束后执行。
}

func tidyUp() {
	fmt.Println("Exited")
}

```


对于桌面运行时，应用程序可以通过调用直接退出`App.Quit()` （移动应用程序不支持此功能） - 通常在开发人员代码中不需要。一旦所有窗口都关闭，应用程序也会退出。另请注意Run()，在应用程序退出之前不会调用之后执行的函数。