---
title: Directory Viewer
class: heading_no_counter
keywords: Directory Viewer, path
desc: Directory Viewer, you can copy the path and file name, and you can choose whether to include subdirectories
---

## Introduce

View the subdirectories and files of a specified directory, copy the directory and file paths and names, and select whether to include subdirectories

![](../../assets/images/ToolsSet/TSODirectory.png)

## How to use

* Select path: You can enter the path in the text box at the top of the left side and click the arrow button to jump to the specified path, or select the path through the tree below
  > Click the button on the right side of the jump path to go to the root directory

* View content: Double-click the directory node of the tree on the left to toggle the expansion and collapse state, and click the arrow icon of the tree to toggle the catalog expansion and collapse state without selecting the directory. After the path is selected, the subdirectories and file information contained in the selected path are displayed on the right, including the name, file size, creation time, modification time, and file type. You can double-click a folder to view its contents.
  > Inaccessible system directories display empty files

* Copy Path or Name: There are two ways to copy a path or name

  1. Click the right mouse button on the directory or file selected in the right list, and a menu will pop up, select the copy path or name, and you can copy the path or name of the selected directory and file
     > The folder option and include subdirectory option in the top toolbar are invalid, and the operation will only be performed on the currently selected directory and files

  2. When you use the buttons in the top toolbar, the folder options and Include subdirectories options can take effect. By default, only the paths or names of files are copied
     * When the folder option is turned off, only the file path or name will be copied, and when it is opened, the file and directory will be copied
     * When the subdirectory option is turned off, only the path or file name of the current directory will be copied, and when it is turned on, the path and file name under all subdirectories will be copied
     
     > When no directories and files are selected, current path will be the path selected of the tree directory on the left

     >! When the Include subdirectories option is turned on, an error is prompted if there are too many directories
  