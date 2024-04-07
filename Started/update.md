# 更新GUI 中的内容


完成[hello world](first-fyne-app.md)教程或其他示例后，您将创建一个基本的用户界面。在此页面中，我们了解如何通过代码更新 GUI 的内容。

第一步是将要更新的小部件分配给变量。在 hello world 教程中，我们widget.NewLabel 直接传递到SetContent()，为了更新它，我们将其更改为两行不同的行，例如：
```go 
	clock := widget.NewLabel("")
	w.SetContent(clock)
```

一旦内容被分配给一个变量，我们就可以调用类似的函数SetText("new text")。对于我们的示例，我们将在 的帮助下将标签的内容设置为当前时间 Time.Format。
```go
	formatted := time.Now().Format("Time: 03:04:05")
	clock.SetText(formatted)
```

这就是我们更改可见项目的内容所需要做的全部工作（完整代码见下文）。然而，我们可以更进一步，定期更新内容。

## 在后台运行
大多数应用程序需要有在后台运行的进程，例如下载数据或响应事件。为了模拟这一点，我们将扩展上面的代码以每秒运行一次。

与大多数 go 代码一样，我们可以创建一个 goroutine（使用go 关键字）并在那里运行我们的代码。如果我们将文本更新代码移至新函数，则可以在初始显示以及定期更新的计时器上调用它。通过组合 `goroutine` 和 `time.Tick `for 循环内部，我们可以每秒更新标签。
```go
	go func() {
		for range time.Tick(time.Second) {
			updateTime(clock)
		}
	}()

```

`ShowAndRun`将此代码放置在或调用之前非常重要，`Run`因为它们在应用程序关闭之前不会返回。将所有这些结合在一起，代码将每秒运行并更新用户界面，创建一个基本的时钟小部件。完整代码如下：

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func updateTime(clock *widget.Label) {
	formatted := time.Now().Format("Time: 03:04:05")
	clock.SetText(formatted)
}

func main() {
	a := app.New()
	w := a.NewWindow("Clock")

	clock := widget.NewLabel("")
	updateTime(clock)

	w.SetContent(clock)
	go func() {
		for range time.Tick(time.Second) {
			updateTime(clock)
		}
	}()
	w.ShowAndRun()
}


```