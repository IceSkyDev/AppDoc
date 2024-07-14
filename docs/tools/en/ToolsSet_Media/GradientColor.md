---
title: Gradient Color
class: heading_no_counter
keywords: Gradient Color, Linear gradient, Radial Gradient
desc: The gradient tool can generate 30 linear or radial gradients consisting of a specified number of random colors, or you can specify a color or position to generate
---

## Introduce

You can generate 30 random gradients according to specified parameters, or one gradient color with a specified color or position, and support linear and radial gradients, linear gradients can specify angles, radial gradients can specify center points, and CSS and XAML code can be generated

Linear Gradient:
![](../../assets/images/ToolsSet/TSMGradient.png)

Radial Gradient:
![](../../assets/images/ToolsSet/TSMGradient1.png)

## How to use

* Configure parameters
  * Stop Count: Used to set the count of color stops, and the value range is 2~5
    > When you turn on the Offset or Color switch below, this setting will be invalidated, and the count is determined by the Offset and Color count
  * Color Type: Specify the type of color included when generat, the types are light, medium, and dark, you can select multiple type, and all of them will be included if you don't have a selection
  * Gradient Type: You can choose either linear gradient or radial gradient
  * Angle or center point: The angle can be set for the linear gradient, the range is 0~360, the center point can be set for the radial gradient, the center point can be set according to the ratio of horizontal and vertical directions, you can click the button on the right side to reset to the center
  * Offset Setting: After turning on the [Offset] switch, you can set the color stop offsets in the text box below
    > Input one offset per line, the range is 0~100, must be an integer
    >
    > If the Color switch is off, clicking the [Generate] button will generate a random gradient at each offset

  * Color Setting: After turning on the [Color] switch, you can set the stop color in the text box below
    > Input one color per line, which must be a hexadecimal color value starting with #
    >
    > If the Offset switch is off, clicking the [Generate] button will generate a gradient that is evenly distributed according to this color and offset
  
  * If the Offset and Color switch are turned on, there are three types of cases depending on the count of inputs
    * The count of offsets and colors are equal: Clicking the [Generate] button will generate a gradient that corresponds to the color and offset
    * Count of offsets less than count of colors: When generating a gradient, colors that do not correspond to a offset will be distributed evenly from the last offset
    * Count of offsets more than count of colors: Offset that do not have a color corresponding to the gradient will use a random color, the type specified by the color type above

  * Below the generate button on the left are the CSS and XAML code areas, when only one color is displayed, the content is the code of that color, otherwise that is the code of the clicked color in the list, you can copy the code by click the copy button on the right