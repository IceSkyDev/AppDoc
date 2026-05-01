---
title: WpfConverters
class: heading_no_counter
keywords: Wpf, Value converter, bool, expression, method
desc: A ValueConverter library used in WPF, includes value converters for various types such as Bool, Number, String, Object, etc.
---

## Introduce
A ValueConverter library used in WPF, includes value converters for various types such as Bool, Number, String, Object, etc.

**You can view samples at the following path: [IceSky.WpfConverters.Sample](https://github.com/IceSkyDev/IceSky.WpfConverters.Sample)**


## Basic Usage

* Add reference

  ``` shell
  dotnet add package IceSky.WpfConverters
  ```

* Add namespace
  ``` xml
  xmlns:conv="clr-namespace:IceSky.WpfConverters.Converters;assembly=IceSky.WpfConverters"
  ```

* Common converters have already been defined in the resource file and can be referenced in Resources in the following way
  ``` xml
  <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="pack://application:,,,/IceSky.WpfConverters;component/Converters.  xaml"/>
  </ResourceDictionary.MergedDictionaries>
  ```

### Number Converter

* NegatvieNumberConverter: Perform negation operation on numeric parameters
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource NegatvieNumberConverter}}"/>
  ```
* RoundConverter: Perform rounding operations on numeric parameters, allowing the specification of rounding mode and decimal places
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource Round2DecimalsConverter}}"/>
  ```
* NumberToBoolConverter: 0 is false, not 0 is true
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource NumberToBoolConverter}}"/>
  ```
* NumberToRatioIntConverter: Multiply numeric parameters by a ratio and round off, you can specify the scale ratio
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource NumberToDoubleIntConverter}}"/>
  ```
* RangeMapConverter: Map a value from one range to another, specifying the source range and the target range
  ```xml
  <Border Width="{Binding Value Converter={conv:RangeMapConverter FromMin=0,FromMax=100,ToMin=100,ToMax=300}}">
  ```
* PercentConverter: Map the numerical value from a specified range to 0~100, allowing the minimum and maximum values of the range to be specified
  ```xml
  <TextBlock Text="{Binding Text, Converter={conv:PercentConverter Maximum=1000},StringFormat={}{0} %}"/>
  ```
* InRangeConverter: Determine whether a value is within the [Min, Max] range, and you can specify whether to include the start or end value
  ```xml
  <TextBlock Text="{Binding Text, Converter={conv:InRangeConverter Min=-100,Max=100}}"/>
  <!--Reversed-->
  <TextBlock Text="{Binding Text, Converter={conv:InRangeConverter Min=-100,Max=100,IsReversed=True}}"/>
  <!--Exclude Min-->
  <TextBlock Text="{Binding Text, Converter={conv:InRangeConverter Min=-100,Max=100,IncludeMin=False}}"/>
  ```
* FileSizeConverter: Convert an integer to the file's byte size
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource FileSizeConverter}}"/>
  ```
* IntToStringConverter: Split the string by the specified separator, return the string at the specified integer index. You can specify the separator, whether to trim whitespace, and the default value
  ```xml
  <TextBlock Text="{Binding Value,Converter={conv:IntToStringConverter Source='Unknow,Active,Inactive',Default=Out of range}}" />
  ```
* InterpolateNumberConverter: Specify three of the start value, end value, step value, and quantity to automatically generate a list of interpolate. Setting ClampToBounds=True can restrict the values within the specified range
  ```xml
  <!--Result is 0,25,50,75,100-->
  <ListBox ItemsSource="{Binding Converter={conv:InterpolateNumberConverter Start=0, End=100, Count=5}}"/>
  <!--Result is 10,15,20,25,30-->
  <ListBox ItemsSource="{Binding Converter={conv:InterpolateNumberConverter Start=10, Step=5, Count=5}}"/>
  <!--Result is 0,-2.8,-5.6,-8.4,-10-->
  <ListBox ItemsSource="{Binding Converter={conv:InterpolateNumberConverter Start=0, End=-10, Step=-2.8, ClampToBounds=True"/>
  ```

### Bool Converter

* InvertBoolConverter: Invert the bool parameter
  ```xml
  <TextBlock Text="{Binding IsChecked,Converter={conv:InvertBoolConverter}}"/>
  ```
* IsNullOrEmptyConverter: Determine whether the parameter is empty. Returns true by default when it is empty. You can set IsInverted=True to invert the result
  ```xml
  <CheckBox IsChecked="{Binding Text,Converter={StaticResource IsNullOrEmptyConverter}}"/>
  <!--Inverted-->
  <CheckBox IsChecked="{Binding Text,Converter={StaticResource InvertedNullOrEmptyConverter}}"/>
  ```
* BoolToVisibleConverter: Default true = Visible, false = Collapsed. You can use UseHidden=True to set false = Hidden, and set IsInverted=True to invert the result
  ```xml
  <Border Visibility="{Binding IsChecked, Converter={StaticResource BoolToVisibleConverter}}"/>
  <!--Inverted-->
  <Border Visibility="{Binding IsChecked, Converter={StaticResource InvertBoolToVisibleConverter}}"/>
  <!--False to Hidden-->
  <Border Visibility="{Binding IsChecked, Converter={StaticResource FalseToHiddenConverter}}"/>
  ```
* BoolToObjectConverter: Convert a bool parameter to any object, allowing you to set the TrueValue and FalseValue
  ```xml
  <TextBlock Text="{Binding IsChecked,Converter={conv:BoolToObjectConverter TrueValue=Man, FalseValue=Woman}}"/>
  <!--With null value-->
  <TextBlock Text="{Binding IsChecked,Converter={conv:BoolToObjectConverter TrueValue=运行, FalseValue=停止, NullValue=未知}}"/>
  <!--BoolToColor, True is Green, False is Red-->
  <Border Background="{Binding IsChecked Converter={StaticResource BoolToColorConverter}}"/>
  ```
* CompareToConverter: Compare the parameter and the target value using the specified operator, return the comparison result, and you can set IsInverted=True to reverse the result. Operator include: Equal, NotEqual, Greater, Less, GreaterOrEqual, LessOrEqual, In, NotIn, StartsWith, EndsWith, Contains
  ```xml
  <!-- >10 is true-->
  <TextBlock Text="{Binding Text,Converter={conv:CompareToConverter TargetValue=10,Operator=Greater}}"/>
  <!--Inverted, >10 is false-->
  <TextBlock Text="{Binding Text,Converter={conv:CompareToConverter TargetValue=10,Operator=Greater,IsInverted=True}}"/>
  <!-- StartsWith 'a' is true-->
  <TextBlock Text="{Binding Text,Converter={conv:CompareToConverter TargetValue=a,Operator=StartsWith}}"/>
  <!--Contains 'a' or 'A' is true-->
  <TextBlock Text="{Binding Text,Converter={conv:CompareToConverter TargetValue=a,Operator=Contains,IgnoreCase=True}}"/>
  <!--'12' or 'ab' or 'at' is true-->
  <TextBlock Text="{Binding Text,Converter={conv:CompareToConverter TargetValue='12, ab, at',Operator=In}}"/>
  ```
* MultiLogicConverter: By default, multiple values are evaluated using AND. You can set UseOr=True to evaluate using OR.
  ```xml
  <Button>
    <Button.IsEnabled>
      <MultiBinding Converter="{conv:MultiLogicConverter}">
        <Binding Path="IsChecked" ElementName="Chk1"/>
        <Binding Path="IsChecked" ElementName="Chk2"/>
        <Binding Path="IsChecked" ElementName="Chk3"/>
      </MultiBinding>
    </Button.IsEnabled>
  </Button>
  <!--Use or-->
  <MultiBinding Converter="{conv:MultiLogicConverter UseOr=True}">
   ...
  </MultiBinding>
  ```


### String Converter

* DateFormatConverter: Can convert DateTime, DateTimeOffset, TimeSpan to string in a specified format
  ```xml
  <TextBlock Text="{Binding Date, Converter={StaticResource StandardDateTimeConverter}}"/>
  <!--Universal format-->
  <TextBlock Text="{Binding Date, Converter={StaticResource StringFormatConverter Format={}{0:u}}}"/>
  <!--Chinese format-->
  <TextBlock Text="{Binding Date, Converter={StaticResource StringFormatConverter Format={}{0:yyyy年MM月dd日}}}"/>
  ```
* StringFormatConverter: Can convert string in a specified format
  ```xml
  <!--Right align-->
  <TextBlock Text="{Binding Text, Converter={conv:StringFormatConverter Format='|{0,10}|'}}"/>
  ```
* StringCaseConverter: Defaults to lowercase, can set ToUpper=True to convert to uppercase
  ```xml
  <!--UpperCase-->
  <TextBlock Text="{Binding Text, Converter={StaticResource UpperCaseConverter}}"/>
  ```
* TextTruncateConverter: Truncate the string to the specified length
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource Max20LengthConverter}}"/>
  ```
* MaskFormatterConverter: Mask a specified position of the string
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource StringMaskConverter}}"/>
  ```
* StringToListConverter: Convert a string into a list using a specified separator
  ```xml
  <ComboBox ItemsSource="{Binding Text, Converter={conv:StringToListConverter}}"/>
  ```
* StringToDictionaryConverter: Convert a string to a dictionary using the specified separator
  ```xml
  <ComboBox ItemsSource="{Binding Text, Converter={conv:StringToDictionaryConverter}}" DisplayMemberPath="Key" SelectedValuePath="Value"/>
  ```
* MultiStringConcatConverter: Join multiple parameters using a specified separator
  ```xml
  <TextBlock>
    <TextBlock.Text>
      <MultiBinding Converter="{conv:MultiStringConcatConverter Separator=', '}">
        <Binding ElementName="txtStr1" Path="Text"/>
        <Binding ElementName="txtMaskStr" Path="Text"/>
      </MultiBinding>
    </TextBlock.Text>
  </TextBlock>
  ```


### Object Converter
* NullOrEmptyToObjectConverter: Convert empty value to a specified object, you can set IsInverted=True to reverse the judgment
  ```xml
  <TextBlock Text="{Binding Text,Converter={conv:NullOrEmptyToObjectConverter EmptyValue=is empty}}" 
           Foreground="{Binding Text,Converter={conv:NullOrEmptyToObjectConverter EmptyValue=Red, NonEmptyValue=Green}}"
           FontWeight="{Binding Text,Converter={conv:NullOrEmptyToObjectConverter EmptyValue=Bold,NonEmptyValue=Normal}}"/>
  ```
* NullOrEmptyToInvisibleConverter: By default, empty value are converted to Collapsed. You can use UseHidden=True to set empty value to Hidden, and set IsInverted=True to invert the judgment
  ```xml
  <Button Visibility="{Binding Text, Converter={StaticResource NullOrEmptyToHiddenConverter}}"/>
  ```
* InvertVisibilityConverter: By default, Visible is converted to Collapsed. You can use UseHidden=True to set it to Hidden
  ```xml
  <Border Visibility="{Binding Visibility,Converter={StaticResource InvertVisibilityConverter}}"/>
  ```
* EqualsToBoolConverter: Use Equals to compare with the target value; if equal, it is true. You can set IsInverted=True to invert the judgment
  ```xml
  <!--Text=0 is true-->
  <TextBlock Text="{Binding Text,Converter={StaticResource IsZeroConverter}}"/>
  <!--SelectedIndex!=2 is true-->
  <TextBlock Text="{Binding SelectedIndex,Converter={conv:EqualsToBoolConverter TargetValue={t:Int 2},IsInverted=True}}"/>
  ```
* SwitchConverter: You can use dictionary types to set branch conditions for matching, supporting IgnoreCase
  ```xml
  <!-- SwitchConverter use Cases from another converter -->
  <TextBlock Text="{Binding Text,Converter={conv:SwitchConverter Cases={conv:ConverterProperty FromConverter={conv:StringToDictionaryConverter Source='a=1,b=2,c=3'}},IgnoreCase=True,DefaultValue=0}}"/>
  ```
* WhenThenConverter: You can define conditions in the Xaml file and return result based on the conditions
  ```xml
  <!--Resource-->
  <conv:WhenThenConverter x:Key="StatusSwitchConverter" DefaultValue="未知状态">
    <conv:WhenThenConverter.Cases>
      <conv:SwitchCase When="Active" Then="激活"/>
      <conv:SwitchCase When="Inactive" Then="未激活"/>
    </conv:WhenThenConverter.Cases>
  </conv:WhenThenConverter>
  <TextBlock Text="{Binding Text,Converter={StaticResource StatusSwitchConverter}}"/>
  ```
* StringMappingConverter: Map by string separation, the conversion result is a string
  ```xml
  <TextBlock Text="{Binding Text,Converter={conv:StringMappingConverter MappingString='1=⏳,2=✅,3=🚚,4=📦,5=❌', DefaultValue=-}}"/>
  ```
* IndexToObjectConverter: Convert the specified index in the object list
  ```xml
  <!--Define list in resource-->
  <x:Array Type="sys:String" x:Key="StringSource">
    <sys:String>first</sys:String>
    <sys:String>second</sys:String>
    <sys:String>third</sys:String>
  </x:Array>
  <TextBlock Text="{Binding SelectedIndex,Converter={conv:IndexToObjectConverter OptionList={StaticResource StringSource},DefaultValue=-}}"/>
  ```
* TypeCastConverter: Convert the parameter to the target type, and you can specify a default value if the conversion fails
  ```xml
  <conv:TypeCastConverter x:Key="tc" TargetType="sys:Int16" DefaultValue="{t:Int 2}"/>
  ```
* EnumToListConverter: By default, the enum name is used as the list value. You can use UseDescription=True to specify using the description as the list value, and use ExcludeValue to specify the enum values to be excluded. Multiple values can be separated by ','
  ```xml
  <ComboBox ItemsSource="{Binding Source={x:Type local:TestEnum}, Converter={conv:EnumToListConverter UseDescription=True, ExcludeValue='0,2'}}"/>
  ```
* EnumToDictionaryConverter: The dictionary's key is the value of the enum. By default, the enum name is used as the dictionary's value. You can use UseDescription=True to specify using the description as the dictionary's value, and use ExcludeValue to specify enum values to exclude, with multiple values separated by ','
  ```xml
  <ComboBox ItemsSource="{Binding Source={x:Type local:TestEnum}, Converter={conv:EnumToDictionaryConverter UseDescription=True}}" DisplayMemberPath="Value" SelectedValuePath="Key"/>
  ```


### Color Converter

* ColorAutoConverter: Supports mutual conversion among String, Color, and Brush
  ```xml
  <Border Background="{Binding Text, Converter={StaticResource ColorAutoConverter}}"/>
  ```
* ColorToTupleConverter: Supports RGB and HSL modes, default is RGB mode, can set ToHsl=True to specify HSL mode
  ```xml
  <TextBlock Text="{Binding Text,Converter={StaticResource Color2RgbConverter}}"/>
  ```
* ValueToRangeColorConverter: You can convert numerical values proportionally to colors within a specified range. You can set ToHsl=True to specify HSL mode. The default is: 0~100 corresponds to red to green
  ```xml
  <Border Background="{Binding Value, Converter={StaticResource DefaultValueToRangeRgbConverter}}"/>
  ```
* BrightnessConverter: Adjust the brightness of the color according to the specified factor, with the default factor being 0.5
  ```xml
  <Border Background="{Binding Text, Converter={conv:BrightnessConverter Factor=0.2}}"/>
  ```
* InterpolateColorConverter: Automatically generate a list of interpolate colors by specifying the starting color, ending color, and quantity. The default is RGB mode, and you can set UseHsl=True to specify HSL mode
  ```xml
  <!--RGB mode-->
  <ItemsControl ItemsSource="{Binding Converter={conv:InterpolateColorConverter StartValue=Red,EndValue=Green,Count=10}}"/>
  <!--HSL mode-->
  <ItemsControl ItemsSource="{Binding Converter={conv:InterpolateColorConverter StartValue=Blue,EndValue=Orange,Count=10,UseHsl=True}}">
  ```
* ValuesToColorConverter: Convert three or four values to a color, the fourth value represents opacity, default is RGB mode, can set ToHsl=True to specify HSL mode
  ```xml
  <TextBlock>
    <TextBlock.Text>
      <MultiBinding Converter="{conv:ValuesToColorConverter IsHsl=True}">
        <Binding ElementName="sldH" Path="Value"/>
        <Binding ElementName="sldS" Path="Value"/>
        <Binding ElementName="sldL" Path="Value"/>
        <Binding ElementName="sldA" Path="Value"/>
      </MultiBinding>
    </TextBlock.Text>
  </TextBlock>
  ```

### Expression Converter
Using '#' as a variable placeholder, string parameters can be placed in single quotes, and the supported operations include: 
* Arithmetic operations: supports +, -, ×, ÷, % (Mod) operations
  ```xml
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#+2'}}"/>
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#/4'}}"/>
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#%5'}}">
  ```
* Logic operations: Supports And, Or, Not operations
  ```xml
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula=# and true}}"/>
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula=# or false}}"/>
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula=not #}}">
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula='iif(#,\'yes\',\'no\')'}}">
  ```
* Comparison operations: Support >, <, >=, <=, <>, =. > and < need to be escaped as &gt; and &lt; in XAML
  ```xml
  <!-- >2 -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula=#>2}}"/>
  <!-- <=3 -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='# &lt;=3'}}"/>
  <!-- <>5 -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula=# &lt;&gt;5}}"/>
  <!-- >=60 && <=100 -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='# &gt;= 60 AND # &lt;= 100'}}"/>
  ```
* String operations: Supports methods such as Len(expression), Trim(expression), Substring(expression, start, length), and IIF(expression, truevalue, falsevalue)
  ```xml
  <!-- Len -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='len(\'#\')'}}"/>
  <!-- Trim -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='trim(\'#\')'}}"/>
  <!-- Concat -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#+\'abc\''}}"/>
  <!-- Substring -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='substring(\'#\',2,3)'}}"/>
  <!-- IIF -->
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='iif(#>5,\'是\', \'否\')'}}"/>
  ```


### Method Converter
You can use instance methods, static methods, or extension methods for conversion. You can use ParameterStr to specify method parameters, separate multiple parameters with ',', and set IgnoreCase=True to make the method name case-insensitive.
  ```xml
  <!-- ToUpper -->
  <TextBlock Text="{Binding Text, Converter={conv:MethodConverter MethodName=ToUpper}}"/>
  <!-- Replace -->
  <TextBlock Text="{Binding Text, Converter={conv:MethodConverter MethodName=Replace,ParameterStr='a,b'}}"/>
  <!-- Static method: Math.Abs -->
  <TextBlock Text="{Binding Text, Converter={conv:MethodConverter TargetType={x:Type sys:Math}, MethodName=abs, IgnoreCase=True}}"/>
  <!-- Custom string extension method: ExtractDigits -->
  <TextBlock Text="{Binding Text, Converter={conv:MethodConverter TargetType={x:Type ext:StringExtensions},MethodName=ExtractDigits}}"/>
  ```


### Chain Mode
All converters in the library support chained conversion, and the FromConverter parameter can specify using another converter as input
  ```xml
  <!-- Triple rounding and to currency -->
  <TextBlock Text="{Binding Text, Converter={conv:StringFormatConverter Format={}{0:C}, FromConverter={conv:NumberToRatioIntConverter Ratio=3}}}"/>
  <!-- SwitchConverter use Cases from another converter -->
  <TextBlock Text="{Binding Text,Converter={conv:SwitchConverter Cases={conv:ConverterProperty FromConverter={conv:StringToDictionaryConverter Source='1=⏳,2=✅,3=🚚,4=📦,5=❌'}}}}"/>
  <!-- Calculate the sin value after convert the angle to radians -->
  <TextBlock Text="{Binding Value, Converter={conv:MethodConverter TargetType={x:Type sys:Math},MethodName=Sin, FromConverter={conv:MethodConverter TargetType={x:Type ext:NumberExtensions},MethodName=ToRadians}}}"/>
  ```

### Type Parameter Markup Extension
This library contains type markup extensions for basic data types, which can serve as shorthand for writing primitive type values in XAML, including basic numeric types, Char, String, Bool, Date, Time, DateTime, TimeSpan, DateTimeOffset, Guid, Enum, EnumValues, Point, Size, Rect, Vector, Color, HSLColor, Brush, StringList, IntList, DoubleList, you need to add namespace when using it: 

  ``` xml
  xmlns:t="clr-namespace:IceSky.WpfConverters;assembly=IceSky.WpfConverters"
  ```
  
  * Usage example
    ```xml
    <Slider Value="{t:Double 5}"/>
    <TextBlock Text="{Binding Source={t:Enum local:TestEnum,Option1}}"/>
    <ComboBox ItemsSource="{t:EnumValues local:TestEnum}"/>
    <ComboBox ItemsSource="{t:IntList '1,2,3'}"/>
    <TextBlock Text="{Binding Source={t:Point 10,20}}"/>
    <TextBlock Text="{Binding Source={t:Size 100,200}}"/>
    <TextBlock Text="{Binding Source={t:Rect 0,0,100,100}}"/>
    <TextBlock Text="{Binding Source={t:Vector 5,10}}"/>
    <Ellipse Fill="{t:Brush red}"/>
    <Ellipse Fill="{t:Brush {t:Color 200,100,100,0.5}}"/>
    <Ellipse Fill="{t:Brush {t:HSLColor 180,1,0.5,0.5}}"/>
    ```