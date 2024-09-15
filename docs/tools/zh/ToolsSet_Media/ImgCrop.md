---
title: 图片分割
class: heading_no_counter
keywords: 图片分割
desc: 按指定数量或尺寸将图片分割为块
---

## 介绍

按数量、尺寸等方式将图片分割为图片块

![](../../assets/images/ToolsSet/TSMImgCrop.png)

## 使用方法

* 点击打开图片按钮打开图片文件，文件打开后会在右侧显示预览
* 可以选择图片分割方式，有四种方式可供选择
  1. Uniform Grid：通过指定行列数量分割图片，默认为3行3列，最多为9行9列
  2. Fixed Size：按指定的图片块尺寸分割图片，默认为100x100，最多支持分割为100个块
  3. Count & Size：指定分割行列数量之后，可以通过预览网格行列的实线调整尺寸
  4. Custom：通过文本自定义行列尺寸及数量，使用空格或“,”分割尺寸，可以使用“*”代表比例，比如在行设置框中输入：**100,\*,2\***，表示第一行高度为100像素，第二行和第三行分别占据剩余高度的1/3和2/3
* 最下方为预览网格颜色设置，点击可以切换不同的网格颜色，改变网格尺寸后可以点击最右侧的刷新按钮刷新预览网格
* 设置好之后点击上方保存按钮会打开对话框，输入文件名点击保存，图片序列将会按照 *文件名-序号* 的命名保存