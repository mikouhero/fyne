## Canvas 和CanvasObject

在 Fyne 中， `Canvas`是绘制应用程序的区域。每个窗口都有一个可以访问的画布，`Window.Canvas()` 但通常您会在上面找到`Window`避免访问画布的函数。

Fyne 中可以绘制的所有内容都是 的类型`CanvasObject`。这里的示例打开一个新窗口，然后通过设置窗口画布的内容来显示不同类型的原始图形元素。可以通过多种方式自定义每种类型的对象，如文本和圆形示例所示。

除了更改显示的内容之外，还`Canvas.SetContent()`可以更改当前可见的内容。例如，如果您更改`FillColour`矩形的 ，您可以使用 请求刷新此现有组件`rect.Refresh()`。

```go 

package main

import (
	"image/color"
	"time"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Canvas")
	myCanvas := myWindow.Canvas()

	blue := color.NRGBA{R: 0, G: 0, B: 180, A: 255}
	rect := canvas.NewRectangle(blue)
	myCanvas.SetContent(rect)

	go func() {
		time.Sleep(time.Second)
		green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}
		rect.FillColor = green
		rect.Refresh()
	}()
	go func() {
		time.Sleep(time.Second * 2)

		setContentToText(myCanvas)
	}()
	go func() {
		time.Sleep(time.Second * 3)

		setContentToCircle(myCanvas)
	}()
	myWindow.Resize(fyne.NewSize(100, 100))
	myWindow.ShowAndRun()
}

// 绘制很多不同的绘图元素 文字
func setContentToText(c fyne.Canvas) {

	green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}
	text := canvas.NewText("Text", green)
	text.TextStyle.Bold = true
	c.SetContent(text)
}

//绘制很多不同的绘图元素，比如圆形
func setContentToCircle(c fyne.Canvas) {

	red := color.NRGBA{R: 0xff, G: 0x33, B: 0x33, A: 0xff}
	circle := canvas.NewCircle(color.White)
	circle.StrokeWidth = 4
	circle.StrokeColor = red
	c.SetContent(circle)
}


```