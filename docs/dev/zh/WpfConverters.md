---
title: WpfConverters
class: heading_no_counter
keywords: Wpf, Value converter, bool, expression, method
desc: WPF使用的ValueConverter库，其中包含Bool、Number、String、Object等多种类型的值转换器
---

## 介绍
这是一个用于WPF开发的值转换库，其中包含Bool、Number、String、Object等多种类型的值转换器

**[点击查看示例代码](https://github.com/IceSkyDev/IceSky.WpfConverters.Sample)**


## 基本使用

* 添加引用

  ``` shell
  dotnet add package IceSky.WpfConverters
  ```

* 添加命名空间
  ``` xml
  xmlns:conv="clr-namespace:IceSky.WpfConverters.Converters;assembly=IceSky.WpfConverters"
  ```

* 常用转换器已经定义在资源文件中了，可以在Resources中用如下方式进行引用
  ``` xml
  <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="pack://application:,,,/IceSky.WpfConverters;component/Converters.  xaml"/>
  </ResourceDictionary.MergedDictionaries>
  ```

### 数值转换器

* NegatvieNumberConverter：负数转换器，对数值参数执行取负操作
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource NegatvieNumberConverter}}"/>
  ```
* RoundConverter：舍入转换器，对数值参数执行舍入操作，可以指定舍入模式和小数位数
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource Round2DecimalsConverter}}"/>
  ```
* NumberToBoolConverter：数值转bool转换器，0为false，非0为true
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource NumberToBoolConverter}}"/>
  ```
* NumberToRatioIntConverter：数值比例转换器，将数值参数乘以比例系数并取整，可以指定比例系数
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource NumberToDoubleIntConverter}}"/>
  ```
* RangeMapConverter：范围映射转换器，将数值从一个范围映射到另一个范围，可以指定源范围和目标范围
  ```xml
  <Border Width="{Binding Value Converter={conv:RangeMapConverter FromMin=0,FromMax=100,ToMin=100,ToMax=300}}">
  ```
* PercentConverter：百分比转换器，将数值从指定范围映射到0~100，可以指定范围最小值和最大值
  ```xml
  <TextBlock Text="{Binding Text, Converter={conv:PercentConverter Maximum=1000},StringFormat={}{0} %}"/>
  ```
* InRangeConverter：范围判断转换器，判断值是否在 [Min, Max] 区间内，可以指定是否包含起始或结束值
  ```xml
  <TextBlock Text="{Binding Text, Converter={conv:InRangeConverter Min=-100,Max=100}}"/>
  <!--Reversed-->
  <TextBlock Text="{Binding Text, Converter={conv:InRangeConverter Min=-100,Max=100,IsReversed=True}}"/>
  <!--Exclude Min-->
  <TextBlock Text="{Binding Text, Converter={conv:InRangeConverter Min=-100,Max=100,IncludeMin=False}}"/>
  ```
* FileSizeConverter：文件大小转换器，将整数转换为文件的字节大小
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource FileSizeConverter}}"/>
  ```
* IntToStringConverter：整数转字符串转换器，将字符串按指定分隔符分割后，返回整数指定索引的字符串，可以指定分隔符、是否删除空白、默认值
  ```xml
  <TextBlock Text="{Binding Value,Converter={conv:IntToStringConverter Source='Unknow,Active,Inactive',Default=Out of range}}" />
  ```
* InterpolateNumberConverter：数值插值转换器，指定起始值、结束值、步进值、数量中的三个来自动生成中间值列表，设置ClampToBounds=True可以将值限制在指定范围内
  ```xml
  <!--Result is 0,25,50,75,100-->
  <ListBox ItemsSource="{Binding Converter={conv:InterpolateNumberConverter Start=0, End=100, Count=5}}"/>
  <!--Result is 10,15,20,25,30-->
  <ListBox ItemsSource="{Binding Converter={conv:InterpolateNumberConverter Start=10, Step=5, Count=5}}"/>
  <!--Result is 0,-2.8,-5.6,-8.4,-10-->
  <ListBox ItemsSource="{Binding Converter={conv:InterpolateNumberConverter Start=0, End=-10, Step=-2.8, ClampToBounds=True"/>
  ```

### 布尔转换器

* InvertBoolConverter：bool取反转换器，将bool参数取反
  ```xml
  <TextBlock Text="{Binding IsChecked,Converter={conv:InvertBoolConverter}}"/>
  ```
* IsNullOrEmptyConverter：空值判断转换器，判断参数是否为空，默认为空时返回true，可以设置IsInverted=True反转判断
  ```xml
  <CheckBox IsChecked="{Binding Text,Converter={StaticResource IsNullOrEmptyConverter}}"/>
  <!--Inverted-->
  <CheckBox IsChecked="{Binding Text,Converter={StaticResource InvertedNullOrEmptyConverter}}"/>
  ```
* BoolToVisibleConverter：bool转可见性转换器，默认true=Visible，false=Collapsed，可以使用UseHidden=True来设置false=Hidden，设置IsInverted=True反转判断
  ```xml
  <Border Visibility="{Binding IsChecked, Converter={StaticResource BoolToVisibleConverter}}"/>
  <!--Inverted-->
  <Border Visibility="{Binding IsChecked, Converter={StaticResource InvertBoolToVisibleConverter}}"/>
  <!--False to Hidden-->
  <Border Visibility="{Binding IsChecked, Converter={StaticResource FalseToHiddenConverter}}"/>
  ```
* BoolToObjectConverter：bool转对象转换器，将bool参数转为任意对象，可以分别设置true和false所对应的值
  ```xml
  <TextBlock Text="{Binding IsChecked,Converter={conv:BoolToObjectConverter TrueValue=Man, FalseValue=Woman}}"/>
  <!--With null value-->
  <TextBlock Text="{Binding IsChecked,Converter={conv:BoolToObjectConverter TrueValue=运行, FalseValue=停止, NullValue=未知}}"/>
  <!--BoolToColor, True is Green, False is Red-->
  <Border Background="{Binding IsChecked Converter={StaticResource BoolToColorConverter}}"/>
  ```
* CompareToConverter：比较转换器，将参数和目标值按指定运算符进行比较，返回比较结果，可以设置IsInverted=True反转判断，比较方式包括：Equal, NotEqual, Greater, Less, GreaterOrEqual, LessOrEqual, In, NotIn, StartsWith, EndsWith, Contains
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
* MultiLogicConverter：多值逻辑转换器，默认对多个值进行And判断，可以设置UseOr=True进行Or判断
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


### 字符串转换器

* DateFormatConverter：日期格式转换器，可以按指定格式转换DateTime、DateTimeOffset、TimeSpan为字符串
  ```xml
  <TextBlock Text="{Binding Date, Converter={StaticResource StandardDateTimeConverter}}"/>
  <!--Universal format-->
  <TextBlock Text="{Binding Date, Converter={StaticResource StringFormatConverter Format={}{0:u}}}"/>
  <!--Chinese format-->
  <TextBlock Text="{Binding Date, Converter={StaticResource StringFormatConverter Format={}{0:yyyy年MM月dd日}}}"/>
  ```
* StringFormatConverter：字符串格式转换器，可以按指定格式转换字符串
  ```xml
  <!--Right align-->
  <TextBlock Text="{Binding Text, Converter={conv:StringFormatConverter Format='|{0,10}|'}}"/>
  ```
* StringCaseConverter：字符串大小写转换器，默认转为小写，可以设置ToUpper=True来转为大写
  ```xml
  <!--UpperCase-->
  <TextBlock Text="{Binding Text, Converter={StaticResource UpperCaseConverter}}"/>
  ```
* TextTruncateConverter：字符串截断转换器，将字符串按指定长度进行截断
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource Max20LengthConverter}}"/>
  ```
* MaskFormatterConverter：字符串掩码转换器，对字符串指定位置进行掩码
  ```xml
  <TextBlock Text="{Binding Text, Converter={StaticResource StringMaskConverter}}"/>
  ```
* StringToListConverter：字符串转列表转换器，将字符串按指定分隔符转为列表
  ```xml
  <ComboBox ItemsSource="{Binding Text, Converter={conv:StringToListConverter}}"/>
  ```
* StringToDictionaryConverter：字符串转字典转换器，将字符串按指定分隔符转为字典
  ```xml
  <ComboBox ItemsSource="{Binding Text, Converter={conv:StringToDictionaryConverter}}" DisplayMemberPath="Key" SelectedValuePath="Value"/>
  ```
* MultiStringConcatConverter：多个字符串连接转换器，将多个参数使用指定分隔符进行连接
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


### 对象转换器
* NullOrEmptyToObjectConverter：空转对象转换器，将空值转为指定对象，可以设置IsInverted=True反转判断
  ```xml
  <TextBlock Text="{Binding Text,Converter={conv:NullOrEmptyToObjectConverter EmptyValue=is empty}}" 
           Foreground="{Binding Text,Converter={conv:NullOrEmptyToObjectConverter EmptyValue=Red, NonEmptyValue=Green}}"
           FontWeight="{Binding Text,Converter={conv:NullOrEmptyToObjectConverter EmptyValue=Bold,NonEmptyValue=Normal}}"/>
  ```
* NullOrEmptyToInvisibleConverter：空转不可见转换器，默认将空值转为Collapsed，可以使用UseHidden=True来设置空值=Hidden，设置IsInverted=True反转判断
  ```xml
  <Button Visibility="{Binding Text, Converter={StaticResource NullOrEmptyToHiddenConverter}}"/>
  ```
* InvertVisibilityConverter：Visibility反转转换器，默认将Visible转为Collapsed，可以使用UseHidden=True来设置转为Hidden
  ```xml
  <Border Visibility="{Binding Visibility,Converter={StaticResource InvertVisibilityConverter}}"/>
  ```
* EqualsToBoolConverter：相等转bool转换器，使用Equals和目标值比较，若相等则为true，可以设置IsInverted=True反转判断
  ```xml
  <!--Text=0 is true-->
  <TextBlock Text="{Binding Text,Converter={StaticResource IsZeroConverter}}"/>
  <!--SelectedIndex!=2 is true-->
  <TextBlock Text="{Binding SelectedIndex,Converter={conv:EqualsToBoolConverter TargetValue={t:Int 2},IsInverted=True}}"/>
  ```
* SwitchConverter：分支转换器，可以设置字典类型的分支条件进行匹配，支持忽略大小写
  ```xml
  <!-- SwitchConverter use Cases from another converter -->
  <TextBlock Text="{Binding Text,Converter={conv:SwitchConverter Cases={conv:ConverterProperty FromConverter={conv:StringToDictionaryConverter Source='a=1,b=2,c=3'}},IgnoreCase=True,DefaultValue=0}}"/>
  ```
* WhenThenConverter：条件转换器，可以在Xaml文件中定义条件，根据条件返回结果
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
* StringMappingConverter：字符串映射转换器，按字符串进行分隔映射，转换结果为字符串
  ```xml
  <TextBlock Text="{Binding Text,Converter={conv:StringMappingConverter MappingString='1=⏳,2=✅,3=🚚,4=📦,5=❌', DefaultValue=-}}"/>
  ```
* IndexToObjectConverter：索引转对象转换器，转换对象列表中的指定索引
  ```xml
  <!--Define list in resource-->
  <x:Array Type="sys:String" x:Key="StringSource">
    <sys:String>first</sys:String>
    <sys:String>second</sys:String>
    <sys:String>third</sys:String>
  </x:Array>
  <TextBlock Text="{Binding SelectedIndex,Converter={conv:IndexToObjectConverter OptionList={StaticResource StringSource},DefaultValue=-}}"/>
  ```
* TypeCastConverter：类型转换器，将参数转为目标类型，可以指定转换失败的默认值
  ```xml
  <conv:TypeCastConverter x:Key="tc" TargetType="sys:Int16" DefaultValue="{t:Int 2}"/>
  ```
* EnumToListConverter：枚举转列表转换器，默认使用枚举名称作为列表值，可以使用UseDescription=True指定使用描述作为列表值，使用ExcludeValue指定要排除的枚举值，多个可以用','分隔
  ```xml
  <ComboBox ItemsSource="{Binding Source={x:Type local:TestEnum}, Converter={conv:EnumToListConverter UseDescription=True, ExcludeValue='0,2'}}"/>
  ```
* EnumToDictionaryConverter：枚举转字典转换器，字典的Key为枚举的值，默认使用枚举名称作为字典的Value，可以使用UseDescription=True指定使用描述作为字典的Value，使用ExcludeValue指定要排除的枚举值，多个可以用','分隔
  ```xml
  <ComboBox ItemsSource="{Binding Source={x:Type local:TestEnum}, Converter={conv:EnumToDictionaryConverter UseDescription=True}}" DisplayMemberPath="Value" SelectedValuePath="Key"/>
  ```


### 颜色转换器

* ColorAutoConverter：颜色转换器，支持String、Color和Brush三者的互相转换
  ```xml
  <Border Background="{Binding Text, Converter={StaticResource ColorAutoConverter}}"/>
  ```
* ColorToTupleConverter：颜色转Tuple转换器，支持RGB和HSL两种方式，默认为RGB模式，可以设置ToHsl=True指定为HSL模式
  ```xml
  <TextBlock Text="{Binding Text,Converter={StaticResource Color2RgbConverter}}"/>
  ```
* ValueToRangeColorConverter：值转范围颜色转换器，可以将数值按比例转为指定颜色范围中间的颜色，可以设置ToHsl=True指定为HSL模式，默认值为：0~100对应红色到绿色
  ```xml
  <Border Background="{Binding Value, Converter={StaticResource DefaultValueToRangeRgbConverter}}"/>
  ```
* BrightnessConverter：颜色亮度转换器，将颜色按指定系数调整亮度，默认系数为0.5
  ```xml
  <Border Background="{Binding Text, Converter={conv:BrightnessConverter Factor=0.2}}"/>
  ```
* InterpolateColorConverter：颜色插值转换器，指定起始、结束颜色和数量自动生成中间颜色列表，默认为RGB模式，可以设置UseHsl=True指定为HSL模式
  ```xml
  <!--RGB mode-->
  <ItemsControl ItemsSource="{Binding Converter={conv:InterpolateColorConverter StartValue=Red,EndValue=Green,Count=10}}"/>
  <!--HSL mode-->
  <ItemsControl ItemsSource="{Binding Converter={conv:InterpolateColorConverter StartValue=Blue,EndValue=Orange,Count=10,UseHsl=True}}">
  ```
* ValuesToColorConverter：将三个或四个数值转为颜色，第四个数值表示不透明度，默认为RGB模式，可以设置ToHsl=True指定为HSL模式
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

### 表达式转换器
ExpressionConverter，使用‘#’作为变量占位符，可以将字符串参数放在单引号中，支持的运算包括：
* 四则运算：支持+、-、×、÷、%（取模）运算
  ```xml
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#+2'}}"/>
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#/4'}}"/>
  <TextBlock Text="{Binding Text,Converter={conv:ExpressionConverter Formula='#%5'}}">
  ```
* 逻辑运算：支持And、Or、Not运算
  ```xml
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula=# and true}}"/>
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula=# or false}}"/>
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula=not #}}">
  <TextBlock Text="{Binding IsChecked,Converter={conv:ExpressionConverter Formula='iif(#,\'yes\',\'no\')'}}">
  ```
* 比较运算：支持>、<、>=、<=、<>、=，>和<在xaml中需要用&gt;和&lt;进行转义
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
* 字符串运算：支持Len(expression)、Trim(expression)、Substring(expression, start, length)、和IIF(expression, truevalue, falsevalue)等方法
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


### 方法转换器
MethodConverter，可以使用实例方法、静态方法或扩展方法进行转换，可以用ParameterStr来指定方法参数，多个参数用','分隔，设置IgnoreCase=True可以指定方法名不区分大小写
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


### 链式转换器
库中所有的转换器都支持链式转换，包含FromConverter参数可以指定使用其他转换器作为输入
  ```xml
  <!-- Triple rounding and to currency -->
  <TextBlock Text="{Binding Text, Converter={conv:StringFormatConverter Format={}{0:C}, FromConverter={conv:NumberToRatioIntConverter Ratio=3}}}"/>
  <!-- SwitchConverter use Cases from another converter -->
  <TextBlock Text="{Binding Text,Converter={conv:SwitchConverter Cases={conv:ConverterProperty FromConverter={conv:StringToDictionaryConverter Source='1=⏳,2=✅,3=🚚,4=📦,5=❌'}}}}"/>
  <!-- Calculate the sin value after convert the angle to radians -->
  <TextBlock Text="{Binding Value, Converter={conv:MethodConverter TargetType={x:Type sys:Math},MethodName=Sin, FromConverter={conv:MethodConverter TargetType={x:Type ext:NumberExtensions},MethodName=ToRadians}}}"/>
  ```

### 类型化参数标记扩展
此库中包含了基本数据类型的类型化参数标记扩展，可以作为在XAML中写入原始类型值的简写，其中包括了基本的数值类型、Char、String、Bool、Date、Time、DateTime、TimeSpan、DateTimeOffset、Guid、Enum、EnumValues、Point、Size、Rect、Vector、Color、HSLColor、Brush、StringList、IntList、DoubleList,使用时需要添加命名空间：

  ``` xml
  xmlns:t="clr-namespace:IceSky.WpfConverters;assembly=IceSky.WpfConverters"
  ```
  
  * 使用示例
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