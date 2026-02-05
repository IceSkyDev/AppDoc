---
title: WpfMonaco
class: heading_no_counter
keywords: Wpf, Monaco, control, editor, Syntax
desc: 微软开源编辑器Monaco editor的WPF封装，支持依赖属性绑定、常用方法和事件
---

## 介绍
这是微软开源编辑器Monaco editor的WPF封装控件，支持依赖属性绑定、常用方法和事件


[GitHub](https://github.com/IceSkyDev/WPFMonaco)

**Monaco Editor 版本** *v0.55.1*

## 依赖属性
* Theme：设置编辑器主题，支持Light、Dark、HCLight、HCDark四种主题风格
* ModelLanguage：设置语法着色时使用的语言
* Text：文本内容
* ReadOnly：是否只读，为true时编辑器为只读模式，默认为false
* Fontfamily：设置编辑器字体
* FontSize：设置编辑器字号，默认为14
* MinimapEnabled：设置右侧Minimap导航是否可用，默认为true
* TabSize：设置Tab宽度，默认为4
* WordWrap：设置是否自动换行，默认为true
* ShowLineNumber：设置是否显示行号，默认为true
* LineNumbersChars：设置行号显示时的宽度，默认为5
* LineHeight：设置编辑器行高，默认为19
* Folding：设置是否显示代码折叠区，默认为true
* ContextMenuEnable：设置右键菜单是否可用，默认为true
* HorizontalScrollBarVisibility：设置水平滚动条显示方式，默认为auto
* VerticalScrollBarVisibility：设置垂直滚动条显示方式，默认为auto
* ShowStickyScroll：设置是否显示StickyScroll区，默认为true
* AutoClosingQuotes：设置是否自动关闭引号
* AutoClosingBrackets：设置是否自动关闭括号

## 方法
* GetLanguages：获取编辑器支持的语言列表
* GetText：获取编辑器中的文本内容
* UpdateOptions：设置编辑器配置参数
* SetText：设置编辑器中的文本内容
* GetPosition：获取当前光标所在位置
* SetPosition：设置光标到指定位置
* GetSelection：获取当前选择的文本内容
* SetSelection：设置选中指定区域的文本
* Focus：编辑器获得焦点
* Format：根据语言类型格式化编辑器的内容
* Clear：清空编辑器的内容
* SelectAll：选中编辑器的所有内容
* GoToLine：滚动到指定行
* GoToPosition：滚动到指定位置
* GoToRange：滚动到指定区域
* InsertText：在指定区域插入指定文本
* ExecuteTrigger：执行指定的触发器

## 事件
* ContentChanged：文本内容改变后执行
* CursorPositionChanged：光标位置改变后执行
* SelectionChanged：选择区域改变后执行
* EditorFocused：获取焦点后执行
* EditorBlurred：失去焦点后执行
* MouseDown：鼠标按键按下执行
* MouseUp：鼠标按键抬起执行
* KeyDown：键盘按键按下执行
* KeyUp：键盘按键抬起执行
* LanguageChanged：语言切换后执行
* ScrollChanged：滚动条位置改变后执行
* EditorPaste：在编辑器粘贴内容后执行


## 基本使用
* 前提条件
  * .NET 6.0 以上
  * Microsoft Edge WebView2 Runtime
  * Visual Studio 2022 以上

* 添加引用

``` shell
dotnet add package WPFMonaco
```

* 使用控件
``` xml
<Window xmlns:editor="clr-namespace:WPFMonaco;assembly=WPFMonaco">
  ...
  <editor:MonacoEditor Text="{Binding Text}"/>
  ...
</Window>
```

### 示例截图：

![WpfMonaco](../assets/images/WpfMonaco.gif)


* [Monaco Editor Documentation](https://microsoft.github.io/monaco-editor/)
* [WebView2 Documentation](https://docs.microsoft.com/en-us/microsoft-edge/webview2/)