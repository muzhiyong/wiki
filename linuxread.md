

概述：read命令 -d[输入结束字符，默认结束符是换行] -p("提示语句") -n[字符个数] -t(等待时间) -s(不回显) -a [数组名]

1、基本读取

read命令接收标准输入（键盘）的输入，或其他文件描述符的输入（后面在说）。得到输入后，read命令将数据放入一个标准变量中。下面是read命令
的最简单形式::

```
#!/bin/bash
echo -n "Enter your name:" //参数-n的作用是不换行，echo默认是换行
read name //从键盘输入
echo "hello $name,welcome to my program" //显示信息
exit 0 //退出shell程序。
```
由于read命令提供了-p参数，允许在read命令行中直接指定一个提示。

所以上面的脚本可以简写成下面的脚本::

```
#!/bin/bash
read -p "Enter your name:" name
echo "hello $name, welcome to my program"
exit 0
```

在上面read后面的变量只有name一个，也可以有多个，这时如果输入多个数据，则第一个数据给第一个变量，第二个数据给第二个变量，如果输入数据个数过多，则最后所有的值都给第一个变量。如果太少输入不会结束。

在read命令行中也可以不指定变量.如果不指定变量，那么read命令会将接收到的数据放置在环境变量REPLY中。


例如::

`read -p "Enter a number"`

环境变量REPLY中包含输入的所有数据，可以像使用其他变量一样在shell脚本中使用环境变量REPLY.

2、计时输入.

使用read命令存在着潜在危险。脚本很可能会停下来一直等待用户的输入。如果无论是否输入数据脚本都必须继续执行，那么可以使用-t选项指定一个计时器。
-t选项指定read命令等待输入的秒数。当计时满时，read命令返回一个非零退出状态;

```
#!/bin/bash
if read -t 5 -p "please enter your name:" name
then
echo "hello $name ,welcome to my script"
else
echo "sorry,too slow"
fi
exit 0
```

除了输入时间计时，还可以设置read命令计数输入的字符。当输入的字符数目达到预定数目时，自动退出，并将输入的数据赋值给变量。

```
#!/bin/bash
read -n1 -p "Do you want to continue [Y/N]?" answer
case $answer in
Y | y)
echo "fine ,continue";;
N | n)
echo "ok,good bye";;
*)
echo "error choice";;
esac
exit 0
```

该例子使用了-n选项，后接数值1，指示read命令只要接受到一个字符就退出。只要按下一个字符进行回答，read命令立即
接受输入并将其传给变量。无需按回车键。

3、默读（输入不显示在监视器上）

有时会需要脚本用户输入，但不希望输入的数据显示在监视器上。典型的例子就是输入密码，当然还有很多其他需要隐藏的数据。

-s选项能够使read命令中输入的数据不显示在监视器上（实际上，数据是显示的，只是read命令将文本颜色设置成与背景相同的颜色）。

```
#!/bin/bash
read -s -p "Enter your password:" pass
echo "your password is $pass"
exit 0
```

4、读文件
最后，还可以使用read命令读取Linux系统上的文件。

每次调用read命令都会读取文件中的"一行"文本。当文件没有可读的行时，read命令将以非零状态退出。

读取文件的关键是如何将文本中的数据传送给read命令。

最常用的方法是对文件使用cat命令并通过管道将结果直接传送给包含read命令的while命令

例子::

```
#!/bin/bash
count=1 //赋值语句，不加空格
cat test | while read line //cat 命令的输出作为read命令的输入,read读到的值放在line中
do
echo "Line $count:$line"
count=$[ $count + 1 ] //注意中括号中的空格。
done
echo "finish"
exit 0
```

5、更改结束符

-d[character] 指定结束输入的字符 d--delimiter分隔符，界定符

就是读取输入，直到某个字符出现为止，而不是转行结束。当然，“某个字符”不算进去。

测试结果：

1, 指定是某个字符后，回车也被读进去，而不会因回车结束

2, -dstr 不会到str结束，是s结束，所以人家才说是character

3, -dx str ;# str变量转了n行+输入字符 ; echo $str 并不会把转行输出来，要echo "$str" 才会转行。

6、数组输入

把输入内容按分隔符(空格或者跳格之类)分配给数组，连续的空格也算为1个分割。

输入后，数组规格跟c语言一样,用var[n]的格式表示，下标从0开始，

直接echo $var 的效果等于echo ${var[0]}

当echo 数组带下标的时候，记得加{}表达，比如echo ${a[1]}

定义数组变量： read -a arr 就可以了; read -a arr[1] 出错。

但是你直接 read arr[1] 是允许的，就是直接赋值数组某个元素。