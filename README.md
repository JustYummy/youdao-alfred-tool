# 利用Alfred调用有道翻译程序

![gif1](https://github.com/JustYummy/AlfredToolForYoudaoApp/blob/master/GIF/gif1.gif)
调用关键词是`yd`

## 实现方法
1、通过Swift调用系统接口(NSPerformService),调用有道词典服务接口
```swift
let pb = NSPasteboard.general   //获取系统剪切板

let arguments = CommandLine.arguments //获取要翻译的数据
var text = ""
for n in arguments[1...] {
    text += n + " "
}

pb.clearContents()
pb.writeObjects([text as NSString]) //将数据赋值到剪切板

NSPerformService("有道词典 • 查询选中内容", pb)   //调用有道

```
2、利用Alfred调用脚本
```applescript
on run argv
  set theQuery to item 1 of argv
	set beforecmdtext to "swift main.swift "
	set b2 to "swift sec.swift "
	set cmdtext to beforecmdtext & theQuery
	set cmd2 to b2 & theQuery
	do shell script cmdtext
	do shell script cmd2
  return theQuery
end run
```

### 注：如果不能用则需要打开对应的权限

![sug](https://github.com/JustYummy/youdao-alfred-tool/blob/master/GIF/sugestion.png)

## 可配合 [有道翻译](https://github.com/wensonsmith/YoudaoTranslate)使用
![gif2](https://github.com/JustYummy/AlfredToolForYoudaoApp/blob/master/GIF/gif2.gif)
下载Youdao Translate.alfredworkflow
调用关键词是`f`，调用应用是`option + enter`
可根据使用习惯更改

下载地址：[releases](https://github.com/JustYummy/AlfredToolForYoudaoApp/releases/tag/1.0)
