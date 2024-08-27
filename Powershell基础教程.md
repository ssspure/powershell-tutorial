##### 1.数组Array 

~~~powershell
$myArr = @("Test1", "Test2", "Test3")
~~~

数组Array的创建方式

~~~powershell
$myArr.GetType()
IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                          --------
True     True     Object[]                                 System.Array

$myArr.IsFixedSize
true

$myArr[1]
Test2

$myArr[5]
$null
~~~

Array是的大小是固定的，每次增加或者减少元素，都是把之前的Array对象删除，然后创建新的Array对象，所以性能会比较差。

访问不存在的index值的时候，返回值为$null

添加元素的方式是：

- $myArr = $myArr + "Test4"
- $myArr += "Test5"



访问数组元素个数的方式是：

- $myArr.Length

- $myArr.Count

删除元素的方式是：

- $myArr = $myArr -ne "Test2"



##### 2.ArrayList

	• $myList = New-Object -TypeName System.Collections.ArrayList
ArrayList的生成方式


	• $myList.Add("Test1")：0
	• $myList.Add("Test2")：1
ArrayList添加元素的方式，添加元素的方法执行结束后，会返元素的index。
当不想返回元素index的时候，可以在前面加上[void]


	• $myList.AddRange(@("Test3", "Test4", "Test5"))
通过AddRange方法直接添加数组


	• $myList.Count
ArrayList是通过Count属性获取元素个数的，不能通过Length来获取元素个数


	• $myList.Remove("Test3")
ArrayList通过Remove方法来删除元素，但是如果指定的元素有多个的时候，只会删除第一个


	• $myList.RemoveAt(1)
ArrayList通过index删除指定元素的方法


	• $myList.RemoveRange(1,3)
ArrayList通过RemoveRange指定范围，来删除元素


三.性能比较
$myArr = @()
Measure-Command -Expression {$(0..50000).ForEach({$myArr+=$_})}
Days              : 0
Hours             : 0
Minutes           : 0
Seconds           : 35
Milliseconds      : 803
Ticks             : 358031431
TotalDays         : 0.000414388230324074
TotalHours        : 0.00994531752777778
TotalMinutes      : 0.596719051666667
TotalSeconds      : 35.8031431
TotalMilliseconds : 35803.1431


$myList = New-Object -TypeName System.Collections.ArrayList
Measure-Command -Expression {$(0..50000).ForEach({$myList.Add($_)})}
Days              : 0
Hours             : 0
Minutes           : 0
Seconds           : 0
Milliseconds      : 169
Ticks             : 1698469
TotalDays         : 1.96582060185185E-06
TotalHours        : 4.71796944444444E-05
TotalMinutes      : 0.00283078166666667
TotalSeconds      : 0.1698469
TotalMilliseconds : 169.8469

通过上面的比较，可以明显的看出ArrayList的性能要比Array好很多