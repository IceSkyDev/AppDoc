---
title: Big Number
class: heading_no_counter
keywords: Big number calculation, high precision, random, pi
desc: The bi number calculation tool can perform arithmetic operations with high precision and big numbers, as well as generate random numbers and obtain the specified number of decimal places of pi
---

## Introduce

This tool supports arithmetic operations with high precision and big numbers, and can also generate numbers with a specified number of integer and decimal places, as well as a specified range of digits after obtaining the decimal point of pi

![](../../assets/images/ToolsSet/TSNBigNumber.png)

## How to use

* Arithmetic operations
  Enter the value in the upper two text boxes, then select the operation type in the middle, and then click the [=] button to get the result below, the maximum value of the result is 1E1073741790, the maximum number of digits of the calculation result is about 3000. Types of operations include:
  1. Four arithmetic
     * Operands support numbers of unlimited length 
     * The divisor cannot be 0 in the division operation
  2. Modulus
     * Both operands must be integers 
  3. Exponent
     * The first operand supports numbers of unlimited length 
     * The second operand must be an integer less than 10000
  4. Root
     * Both operands must be positive integers 
     * The second operand must be less than 10000
  5. Greatest common divisor
     * Both operands must be positive integers 
  6. Least common multiple
     * Both operands must be positive integers 
  > The rightmost button of the operation type is used to swap two operands
  >
  > When the switch on the right side of the [=] button is turned on, you can turn on the display of scientific notation, and then if the checkbox on the right is selected, you can specify the number of decimal places in the result in the text box on the right, which is 100 digits by default

* Random number
  * After entering the number of digits in the integer part and the decimal part in the Random area, click the [Get] button on the right side to generate the corresponding number on the right, and the maximum number of digits can be specified as 9999
* Get pi
  * After entering the number of starting digits and ending digits in the Pi field, click the [Get] button on the right to generate the number of digits corresponding to the area in pi on the right
  > The maximum number of digits can be 99,999, a maximum of 10,000 digits can be obtained each time

> The results of this tool can be quickly copied by clicking the copy button