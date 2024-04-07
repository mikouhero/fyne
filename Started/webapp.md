## 在浏览器中运行
Fyne 应用程序还可以使用标准 Web 浏览器在 Web 上运行！由于不同内核的标准和强度多种多样，这有点复杂。

使用 Fyne 创建的 Web 应用程序将提供 WASM 运行时以及 JavaScript 代码包，这允许生成的网页查看当前浏览器并根据其优势选择正确的实现。这会在大多数系统上带来良好的用户体验。

为了准备您的应用程序在网络上使用，我们再次使用“fyne”cli应用程序，它有一个“serve”命令用于快速测试

```bash 
go install fyne.io/fyne/v2/cmd/fyne@latest
fyne serve
```
片刻之后，您将看到 Web 服务器已在端口 :8080 上启动。只需打开网络浏览器访问 https://localhost:8080 即可使用您的应用程序！

此过程中使用的工具对所使用的 Go 版本非常敏感，因此可能会出现与版本不匹配相关的错误。如果您使用的 Go 版本高于 1.18，您应该确保您拥有 1.18 版本的副本并在您的环境中引用它，例如（对于基于[自制程序](https://brew.sh/)的安装）：
```bash 
export GOPHERJS_GOROOT=/opt/homebrew/Cellar/go@1.18/1.18.10/libexec

```
您可以在GopherJS文档中找到更多相关信息。

用于网络分发的包装
该`fyne serve`命令非常适合本地测试，但就像其他平台一样，您也希望能够分发您的应用程序。要准备要上传的文件，只需使用 `fyne package`与常规[Packaging](https://docs.fyne.io/started/packaging)类似的命令。
```bash 

fyne package -os web
```
您还可以选择仅打包 WASM 或 JavaScript，而不是自动检测设置：
```bash 
fyne package -os wasm
fyne package -os js

```
### 演示
您可以通过访问[demo.fyne.io](https://demo.fyne.io/) 查看正在运行的 Fyne 应用程序，以在您的任何设备上进行测试。

### 局限性
从 v2.4.0 版本开始，Web 驱动程序尚未 100% 完整，因此您的应用程序可能无法使用以下功能：

- 多个窗口（但所有对话框都在当前窗口内运行）
- 文件和偏好的存储
这些问题正在处理中，并将在未来的版本中得到解决。