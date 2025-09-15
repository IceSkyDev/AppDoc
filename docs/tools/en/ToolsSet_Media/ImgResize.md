---
title: Image Resize
class: heading_no_counter
keywords: Format, Resize
desc: Batch adjust and convert image formats and sizes.
---

## Introduce

Images can be batch converted in format and size.

![](../../assets/images/ToolsSet/TSMImageResize.png)

## How to use

* Click the left area to open the image file, and a preview of the image will be displayed after opening. 
* On the right side, you can set the conversion target parameters which include:
  * Type: The dropdown box contains a custom list and various predefined types. Selecting the custom list option allows you to specify the conversion target yourself. Each predefined type includes multiple target formats and sizes. After choosing a predefined type, the content of the list below will automatically update.
  * Default Margin: The default margin used during conversion, which will be applied if no margin is set in the list below. The default margin is a percentage value that will take effect on all items in the list that do not have a margin set, with a default of 10% and a maximum of 30%.
  * Use %: When the switch is turned on, items in the list will be scaled using ratio; otherwise, they will be adjusted using pixel. 
  * Lock Ratio: This is effective when the [Use %] switch is off; when turned on, it will lock the width and height ratio of the image while resizing, otherwise it will stretch the image. 
  * Stretch to Fill: This is effective when the [Use %] switch is off; when turned on, it will stretch the image to cover the target size while resizing.
  * Conversion list: In the list below, you can define multiple target conversion formats and sizes. Sizes can be set using pixel or ratio. The first default option in the target format is [NoChange], which means only the size is modified without changing the image format. You can also customize the file name of the conversion result in the list, this file name does not need a suffix.
    > Items in the list can be added using the add button at the top of the list, but they cannot be deleted. Switching the conversion type can reset the list to its initial state.

    > Both custom lists and predefined lists can added or modified by the user.

    > Only the selected items in the list with a size greater than 0 will be converted during the conversion process, and items with the same filename will be automatically renamed.
  * Background: The switch at the bottom of the list is used to set the background color of the conversion result. When the switch is off, transparent background is used, which is only effective for png format; when the switch is on, you can specify the background color of the image.
* Clicking the save button will open a folder selection window to choose the target path. After confirmation, the results will be saved with the file names in the list.
  