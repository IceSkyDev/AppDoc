---
title: Path Combine
class: heading_no_counter
keywords: Path Combine, geometry, transform 
desc: Combine multiple paths into one, you can transform each path separately, and the result can be saved as an SVG or image
---

## Introduce

Combine multiple geometry into one, support rotation, translation, scale and custom color, copy the result path data and SVG text, and save as SVG and PNG file

![](../../assets/images/ToolsSet/TSOPathGroup.png)

## How to use
* Paths Operation: The toolbar on the upper left side can be used to operate on the paths
  * Add: Click the [+] button on the left side of the toolbar to add a blank path
  * Clear: Click the [x] button to clear all the paths
  * Simplify paths: The slider on the right side of the toolbar can set the coordinate accuracy of all paths, and click the button on the right to apply
  
    > ⚠️ If you applied simplify paths, the text content of all paths will be updated, and all transformations for the modified paths will be cleared

* Path settings: You can edit a single path in the path list
  * Edit Path: Enter geometry code in the text box to edit the path, if the path format is incorrect, an error message will appear below
  
    > ⚠️ Edit path will clear it's transforms
  * Adjust scale: Click the button on the right below the text box to open the scale adjustment menu, which can be used to adjust the scale of some path coordinates that are too large or too small
    > Click the item \>1 to zoom in, and <1 to zoom out
    > 
    > ⚠️ This operation will change the text of the path, and clear the transforms of the path, and maybe needs to redo simplify
    > 
    > The menu can be used to adjust the scale several times to achieve the final suitable size
  * Adjust the order: The order of the paths in the list determines the order of the stacks when combined, and the lower path will appear at the front of the result
    
    A preview of a path is displayed at the top of the middle, and the three buttons under the preview are used to:
    * Move up: After clicking, the path will move up one line, and this path in the result will go down one level, and the click will be invalid when it is the first row
    * Move down: After clicking, the path will move down one line, and this path in the result will go up one level, and the click will be invalid when it is the last row
    * Remove: Click to remove the path from the list
  
  * Set Border and Fill: You can set the border and fill effect of the path at right, including:
    * Border width: Set by slider, no border when set to 0, maximum value is 10
    * Border Color: The color picker on the left used to select the border color
    * Fill: The checkbox used to set whether the path is filled, and you can select the fill color when selected, otherwise it will be transparent
    * Fill Color: The color picker on the right used to select the fill color, which will be displayed only after the Fill is selected
  
  * Path Transform: The lower right side used to transform the path, the operations from left to right are:
    * Rotate: Set the rotation angle of the path through the slider, the range is 0~360
    * Translate: Tap and hold on the move icon to move the path
      > ⚠️ The start position will reset when start translate transform
    * Scale: Tap and hold on the zoom icon to scale the path
      > ⚠️ The start scale will set to 1 when start scale transform
      > 
      > The scale transform will not change the original code of the path, the scale range is 0.1~2 and cannot be carried out continuously, so it is mainly used for size fine-tuning, if the size is too large or too small, please use the previous adjust scale method to adjust
    * Clear Transforms: Click the rightmost button to clear the rotate, translate, and scale transforms
* View result: The right side of the tool can preview the combined path, and the buttons on the upper right side are used to:
  * Copy the geometry code of the result
  * Copy the SVG code of the result
  * Save the result as an SVG file
  * Save the result as an PNG file