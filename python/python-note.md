## Python 学习笔记

### [Python 教程 - 廖雪峰]( http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000)
- 输入exit()并回车，就可以退出Python交互式环境
- 交互式环境下不记得函数名了，可以使用 dir 和 help 来查看
- 空值是Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。
- 如果字符串里面有很多字符都需要转义，就需要加很多\，为了简化，Python还允许用r''表示''内部的字符串默认不转义，可以自己试试：<pre>
print '\\\t\\'
\       \
print r'\\\t\\'
\\\t\\
</pre>
- Windows上也是可以“像.exe文件那样直接运行.py文件”,只需要修改环境变量PATHEXT，将.py加入就可以了：<pre>
D:\OJ\python>echo %pathext%
.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC;.py
D:\OJ\python>type hello.py
print "hello, python!"
D:\OJ\python>hello.py
hello, python!
</pre>
- [变量如何存储](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001374738264643de15c5c4abad47dd9510e3b86286acb8000)  
可以把一个变量a赋值给另一个变量b，这个操作实际上是把变量b指向变量a所指向的数据，例如下面的代码：<pre>
a = 'ABC'
b = a
a = 'XYZ'
print b
</pre>
最后一行打印出变量b的内容到底是'ABC'呢还是'XYZ'？如果从数学意义上理解，就会错误地得出b和a相同，也应该是'XYZ'，但实际上b的值是'ABC'，让我们一行一行地执行代码，就可以看到到底发生了什么事：  
执行a = 'ABC'，解释器创建了字符串'ABC'和变量a，并把a指向'ABC'，如下图：  
![](http://www.liaoxuefeng.com/files/attachments/0013871830933164ebea9bff3e24a64a1d36c0a6c7d368f000/0)  
执行b = a，解释器创建了变量b，并把b指向a指向的字符串'ABC'，如下图：  
![](http://www.liaoxuefeng.com/files/attachments/0013871831797715367a9e297944ca88f362ea3b01efaf7000/0)  
执行a = 'XYZ'，解释器创建了字符串'XYZ'，并把a的指向改为'XYZ'，但b并没有更改，如下图：  
![](http://www.liaoxuefeng.com/files/attachments/00138718324379052e7366c983442ac971699da163cacc7000/0)  
所以，最后打印变量b的结果自然是'ABC'了。
- [字符串与编码](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386819196283586a37629844456ca7e5a7faa9b94ee8000)  
ASCII编码和Unicode编码的区别：ASCII编码是1个字节，而Unicode编码通常是2个字节。（如果要用到非常偏僻的字符，就需要4个字节）。现代操作系统和大多数编程语言都直接支持Unicode。  
字母A用ASCII编码是十进制的65，二进制的01000001；  
字符0用ASCII编码是十进制的48，二进制的00110000，注意字符'0'和整数0是不同的；  
汉字中已经超出了ASCII编码的范围，用Unicode编码是十进制的20013，二进制的01001110 00101101。  
你可以猜测，如果把ASCII编码的A用Unicode编码，只需要在前面补0就可以，因此，A的Unicode编码是00000000 01000001。  
新的问题又出现了：如果统一成Unicode编码，乱码问题从此消失了。但是，如果你写的文本基本上全部是英文的话，用Unicode编码比ASCII编码需要多一倍的存储空间，在存储和传输上就十分不划算。  
所以，本着节约的精神，又出现了把Unicode编码转化为“可变长编码”的UTF-8编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。如果你要传输的文本包含大量英文字符，用UTF-8编码就能节省空间：<pre>
字符	ASCII		Unicode		UTF-8
A	01000001	00000000 	01000001	01000001
中	x		01001110 	00101101	11100100 10111000 10101101
</pre>
从上面的表格还可以发现，UTF-8编码有一个额外的好处，就是ASCII编码实际上可以被看成是UTF-8编码的一部分，所以，大量只支持ASCII编码的历史遗留软件可以在UTF-8编码下继续工作。  
搞清楚了ASCII、Unicode和UTF-8的关系，我们就可以总结一下现在计算机系统通用的字符编码工作方式：  
在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件：
![](http://www.liaoxuefeng.com/files/attachments/001387245992536e2ba28125cf04f5c8985dbc94a02245e000/0)  
Python提供了ord()和chr()函数，可以把字母和对应的数字相互转换：<pre>
ord('A')
62
chr(65)
A
</pre>
Python在后来添加了对Unicode的支持，以Unicode表示的字符串用u'...'表示，比如：<pre>
print u'中文'
中文
u'中'
u'\u4e2d'
</pre>
写u'中'和u'\u4e2d'是一样的，\u后面是十六进制的Unicode码。因此，u'A'和u'\u0041'也是一样的。  
两种字符串如何相互转换？字符串'xxx'虽然是ASCII编码，但也可以看成是UTF-8编码，而u'xxx'则只能是Unicode编码。  
把u'xxx'转换为UTF-8编码的'xxx'用encode('utf-8')方法：<pre>
u'ABC'.encode('utf-8')
'ABC'
u'中文'.encode('utf-8')
'\xe4\xb8\xad\xe6\x96\x87'
</pre>
英文字符转换后表示的UTF-8的值和Unicode值相等（但占用的存储空间不同），而中文字符转换后1个Unicode字符将变为3个UTF-8字符，你看到的\xe4就是其中一个字节，因为它的值是228，没有对应的字母可以显示，所以以十六进制显示字节的数值。len()函数可以返回字符串的长度：<pre>
len(u'ABC')
3
len('ABC')
3
len(u'中文')
2
len('\xe4\xb8\xad\xe6\x96\x87')
6
</pre>
反过来，把UTF-8编码表示的字符串'xxx'转换为Unicode字符串u'xxx'用decode('utf-8')方法：<pre>
'abc'.decode('utf-8')
u'abc'
'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
u'\u4e2d\u6587'
print '\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
中文
</pre>
由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：<pre>
 #!/usr/bin/env python
 # -*- coding: utf-8 -*-
</pre>
第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；  
第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。  
Python当然也支持其他编码方式，比如把Unicode编码成GB2312：<pre>
u'中文'.encode('gb2312')
'\xd6\xd0\xce\xc4'
</pre>
但这种方式纯属自找麻烦，如果没有特殊业务要求，请牢记仅使用Unicode和UTF-8这两种编码方式。
- [格式化输出](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386819196283586a37629844456ca7e5a7faa9b94ee8000)  
格式化整数和浮点数还可以指定是否补0和整数与小数的位数：<pre>
'%2d-%02d' % (3, 1)
' 3-01'
'%.2f' % 3.1415926
'3.14'
</pre>
如果你不太确定应该用什么，%s永远起作用，它会把任何数据类型转换为字符串：<pre>
'Age: %s. Gender: %s' % (25, True)
'Age: 25. Gender: True'
</pre>
对于Unicode字符串，用法完全一样，但最好确保替换的字符串也是Unicode字符串：<pre>
u'Hi, %s' % u'Michael'
u'Hi, Michael'
</pre>
有些时候，字符串里面的%是一个普通字符怎么办？这个时候就需要转义，用%%来表示一个%：<pre>
'growth rate: %d %%' % 7
'growth rate: 7 %'
</pre>
- [List 和 Tuple](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386819318453af120e8751ea4d2696d8a1ffa5ffdfd7000)  
当索引超出了范围时，Python会报一个IndexError错误，所以，要确保索引不要越界，记得最后一个元素的索引是len(classmates) - 1。  
如果要取最后一个元素，除了计算索引位置外，还可以用-1做索引，直接获取最后一个元素, 以此类推，可以获取倒数第2个、倒数第3个，当然，倒数第4个就越界了：<pre>
classmates = ['Michael', 'Bob', 'Tracy']
classmates[-1]
'Tracy'
classmates[-2]
'Bob'
classmates[-3]
'Michael'
classmates[-4]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
</pre>
list是一个可变的有序表，所以，可以往list中追加元素到末尾，也可以把元素插入到指定的位置，比如索引号为1的位置，要删除list末尾的元素，用pop()方法，要删除指定位置的元素，用pop(i)方法，其中i是索引位置，要把某个元素替换成别的元素，可以直接赋值给对应的索引位置：<pre>
classmates.append('Adam')
classmates
['Michael', 'Bob', 'Tracy', 'Adam']
classmates.insert(1, 'Jack')
classmates
['Michael', 'Jack', 'Bob', 'Tracy', 'Adam']
classmates.pop()
'Adam'
classmates
['Michael', 'Jack', 'Bob', 'Tracy']
classmates.pop(1)
'Jack'
classmates
['Michael', 'Bob', 'Tracy']
classmates[1] = 'Sarah'
classmates
['Michael', 'Sarah', 'Tracy']
</pre>
另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改，比如同样是列出同学的名字：<pre>
classmates = ('Michael', 'Bob', 'Tracy')
</pre>
现在，classmates这个tuple不能变了，它也没有append()，insert()这样的方法。其他获取元素的方法和list是一样的，你可以正常地使用classmates[0]，classmates[-1]，但不能赋值成另外的元素。  
不可变的tuple有什么意义？因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple。  
如果要定义一个空的tuple，可以写成()：<pre>
t = () 
t
()
</pre>
但是，要定义一个只有1个元素的tuple，如果你这么定义：<pre>
t = (1)
t
1
</pre>
定义的不是tuple，是1这个数！这是因为括号()既可以表示tuple，又可以表示数学公式中的小括号，这就产生了歧义，因此，Python规定，这种情况下，按小括号进行计算，计算结果自然是1。所以，只有1个元素的tuple定义时必须加一个逗号,，来消除歧义：<pre>
t = (1,)
t
(1,)
</pre>
来看一个“可变的”tuple：<pre>
t = ('a', 'b', ['A', 'B'])
t[2][0] = 'X'
t[2][1] = 'Y'
t
('a', 'b', ['X', 'Y'])
</pre>
这个tuple定义的时候有3个元素，分别是'a'，'b'和一个list。不是说tuple一旦定义后就不可变了吗？怎么后来又变了？别急，我们先看看定义的时候tuple包含的3个元素：  
![](http://www.liaoxuefeng.com/files/attachments/001387269705541ad608276b6f7426ca59b8c2b19947243000/0)  
当我们把list的元素'A'和'B'修改为'X'和'Y'后，tuple变为：  
![](http://www.liaoxuefeng.com/files/attachments/001387269768140c7d5ca167342402989dfc75343fe900b000/0)  
表面上看，tuple的元素确实变了，但其实变的不是tuple的元素，而是list的元素。tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向'a'，就不能改成指向'b'，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！理解了“指向不变”后，要创建一个内容也不变的tuple怎么做？那就必须保证tuple的每一个元素本身也不能变。
- [Dict 和 Set](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/0013868193482529754158abf734c00bba97c87f89a263b000)  
如果key不存在，dict就会报错，要避免key不存在的错误，有两种办法，一是通过in判断key是否存在, 二是通过dict提供的get方法，如果key不存在，可以返回None，或者自己指定的value,判断key是否存在还有其它方法，比如 has_key()：<pre>
'Thomas' in d
False
d.get('Thomas')
d.get('Thomas', -1)
-1
</pre>
要删除一个key，用pop(key)方法，对应的value也会从dict中删除：<pre>
d.pop('Bob')
75
</pre>
请务必注意，dict内部存放的顺序和key放入的顺序是没有关系的。和list比较，dict有以下几个特点：  
查找和插入的速度极快，不会随着key的增加而增加；  
需要占用大量的内存，内存浪费多。 
所以，dict是用空间来换取时间的一种方法。  
set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。要创建一个set，需要提供一个list作为输入集合：<pre>
s = set([1, 2, 3])
s
set([1, 2, 3])
</pre>
注意，传入的参数[1, 2, 3]是一个list，而显示的set([1, 2, 3])只是告诉你这个set内部有1，2，3这3个元素，显示的[]不表示这是一个list。重复元素在set中自动被过滤：<pre>
s = set([1, 1, 2, 2, 3, 3])
s
set([1, 2, 3])
</pre>
通过add(key)方法可以添加元素到set中，可以重复添加，但不会有效果, 通过remove(key)方法可以删除元素：<pre>
s.add(4)
s
set([1, 2, 3, 4])
s.add(4)
s
set([1, 2, 3, 4])
s.remove(4)
s
set([1, 2, 3])
</pre>
set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：<pre>
s1 = set([1, 2, 3])
s2 = set([2, 3, 4])
s1 & s2
set([2, 3])
s1 | s2
set([1, 2, 3, 4])
</pre>
- 函数  
比较函数cmp(x, y)，数据类型转换函数：<pre>
cmp(1, 2)
-1
cmp(2, 1)
1
cmp(3, 3)
0
int('123')
123
int(12.34)
12
float('12.34')
12.34
str(1.23)
'1.23'
unicode(100)
u'100'
bool(1)
True
bool('')
False
</pre>
函数名其实就是指向一个函数对象的引用，完全可以把函数名赋给一个变量，相当于给这个函数起了一个“别名”：<pre>
a = abs # 变量a指向abs函数
a(-1) # 所以也可以通过a调用abs函数
1
</pre>
如果没有return语句，函数执行完毕后也会返回结果，只是结果为None。return None可以简写为return。如果想定义一个什么事也不做的空函数，可以用pass语句：<pre>
def nop():
    pass
</pre>
pass语句什么都不做，那有什么用？实际上pass可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个pass，让代码能运行起来。pass还可以用在其他语句里，比如：<pre>
if age >= 18:
    pass
</pre>
缺少了pass，代码运行就会有语法错误。
如何让函数返回多个值?比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的新的坐标：<pre>
import math  
def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny  
x, y = move(100, 100, 60, math.pi / 6)
print x, y
151.961524227 70.0
</pre>
但其实这只是一种假象，Python函数返回的仍然是单一值：<pre>
r = move(100, 100, 60, math.pi / 6)
print r
(151.96152422706632, 70.0)
</pre>
原来返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。  
Python的函数定义非常简单，但灵活度却非常大。除了正常定义的必选参数外，还可以使用默认参数、可变参数和关键字参数，使得函数定义出来的接口，不但能处理复杂的参数，还可以简化调用者的代码。  
默认参数:<pre>
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
def draw_circle(0, 0, 20, linecolor=0xff0000, fillcolor=0xffff00, penwidth=5):
	pass
</pre>
有多个默认参数时，调用的时候，既可以按顺序提供默认参数，比如调用draw_circle(0, 0, 20, 0xff0000, 0xffff00)，意思是，除了0，0，20这3个必选参数外，后两个参数应用在参数linecolor和fillcolor上，penwidth参数由于没有提供，仍然使用默认值。也可以不按顺序提供部分默认参数。当不按顺序提供部分默认参数时，需要把参数名写上。比如调用draw_circle(0, 0, 20, fillcolor=0x00ff00)，意思是，fillcolor参数用传进去的值0x00ff00，其他默认参数继续使用默认值。  
默认参数很有用，但使用不当，也会掉坑里。默认参数有个最大的坑，演示如下：  
先定义一个函数，传入一个list，添加一个END再返回：<pre>
def add_end(L=[]):
    L.append('END')
    return L
</pre>
当你正常调用时，结果似乎不错：<pre>
add_end([1, 2, 3])
[1, 2, 3, 'END']
add_end(['x', 'y', 'z'])
['x', 'y', 'z', 'END']
</pre>
当你使用默认参数调用时，一开始结果也是对的,但是，再次调用add_end()时，结果就不对了：<pre>
add_end()
['END']
add_end()
['END', 'END']
add_end()
['END', 'END', 'END']
</pre>
原因解释如下：Python函数在定义的时候，默认参数L的值就被计算出来了，即[]，因为默认参数L也是一个变量，它指向对象[]，每次调用该函数，如果改变了L的内容，则下次调用时，默认参数的内容就变了，不再是函数定义时的[]了。所以，定义默认参数要牢记一点：默认参数必须指向不变对象！要修改上面的例子，我们可以用None这个不变对象来实现：<pre>
def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L
</pre>
可变参数:<pre>
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
</pre>
定义可变参数和定义list或tuple参数相比，仅仅在参数前面加了一个*号。在函数内部，参数numbers接收到的是一个tuple,调用该函数时，可以传入任意个参数，包括0个参数：<pre>
calc(1, 2)
5
calc()
0
</pre>
如果已经有一个list或者tuple，要调用一个可变参数怎么办？可以这样做：<pre>
nums = [1, 2, 3]
calc(nums[0], nums[1], nums[2])
14
</pre>
这种写法当然是可行的，问题是太繁琐，所以Python允许你在list或tuple前面加一个*号，把list或tuple的元素变成可变参数传进去,这种写法相当有用，而且很常见：<pre>
nums = [1, 2, 3]
calc(*nums)
14
</pre>
关键字参数,可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。请看示例：<pre>
def person(name, age, **kw):
    print 'name:', name, 'age:', age, 'other:', kw
</pre>
函数person除了必选参数name和age外，还接受关键字参数kw。在调用该函数时，可以只传入必选参数,也可以传入任意个数的关键字参数：<pre>
person('Michael', 30)
name: Michael age: 30 other: {}
person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
</pre>
关键字参数有什么用？它可以扩展函数的功能。比如，在person函数里，我们保证能接收到name和age这两个参数，但是，如果调用者愿意提供更多的参数，我们也能收到。试想你正在做一个用户注册的功能，除了用户名和年龄是必填项外，其他都是可选项，利用关键字参数来定义这个函数就能满足注册的需求。和可变参数类似，也可以先组装出一个dict，然后，把该dict转换为关键字参数传进去：<pre>
kw = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, city=kw['city'], job=kw['job'])
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
</pre>
当然，上面复杂的调用可以用简化的写法：<pre>
kw = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, **kw)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
</pre>
参数组合,在Python中定义函数，可以用必选参数、默认参数、可变参数和关键字参数，这4种参数都可以一起使用，或者只用其中某些，但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数和关键字参数。比如定义一个函数，包含上述4种参数：<pre>
def func(a, b, c=0, *args, **kw):
    print 'a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw
</pre>
在函数调用的时候，Python解释器自动按照参数位置和参数名把对应的参数传进去。<pre>
func(1, 2)
a = 1 b = 2 c = 0 args = () kw = {}
func(1, 2, c=3)
a = 1 b = 2 c = 3 args = () kw = {}
func(1, 2, 3, 'a', 'b')
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}
func(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
</pre>
最神奇的是通过一个tuple和dict，你也可以调用该函数：<pre>
args = (1, 2, 3, 4)
kw = {'x': 99}
func(*args, **kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'x': 99}
</pre>
所以，对于任意函数，都可以通过类似func(*args, **kw)的形式调用它，无论它的参数是如何定义的。
- 切片  
L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。即索引0，1，2，正好是3个元素。如果第一个索引是0，还可以省略：<pre>
L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
L[0:3]
['Michael', 'Sarah', 'Tracy']
L[:3]
['Michael', 'Sarah', 'Tracy']
</pre>
类似的，既然Python支持L[-1]取倒数第一个元素，那么它同样支持倒数切片，记住倒数最后一个元素的索引是-1。试试：<pre>
L[-2:]
['Bob', 'Jack']
L[-2:-1]
['Bob']
</pre>
甚至什么都不写，只写[:]就可以原样复制一个list
- [迭代](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/0013868196435255fcca20a1630446ea2dd434a7176e152000)  
list这种数据类型虽然有下标，但很多其他数据类型是没有下标的，但是，只要是可迭代对象，无论有无下标，都可以迭代，比如dict就可以迭代：<pre>
d = {'a': 1, 'b': 2, 'c': 3}
for key in d:
...     print key
...
a
c
b
</pre>
因为dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样。默认情况下，dict迭代的是key，等同于for k in d.keys()。如果要迭代value，可以用for value in d.itervalues()或for v in d.values()，如果要同时迭代key和value，可以用for k, v in d.iteritems()。  
所以，当我们使用for循环时，只要作用于一个可迭代对象，for循环就可以正常运行，而我们不太关心该对象究竟是list还是其他数据类型。那么，如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断：<pre>
from collections import Iterable
isinstance('abc', Iterable) # str是否可迭代
True
isinstance([1,2,3], Iterable) # list是否可迭代
True
isinstance(123, Iterable) # 整数是否可迭代
False
</pre>
最后一个小问题，如果要对list实现类似Java那样的下标循环怎么办？Python内置的enumerate函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身：<pre>
for i, value in enumerate(['A', 'B', 'C']):
...     print i, value
...
0 A
1 B
2 C
</pre>
上面的for循环里，同时引用了两个变量，在Python里是很常见的，比如下面的代码：<pre>
for x, y in [(1, 1), (2, 4), (3, 9)]:
...     print x, y
...
1 1
2 4
3 9
</pre>
- [列表生成式](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/00138681963899940a998c0ace64bb5ad45d1b56b103c48000)  
如果要生成[1x1, 2x2, 3x3, ..., 10x10]怎么做？<pre>
[x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
</pre>
for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方：<pre>
[x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
</pre>
还可以使用两层循环，可以生成全排列：<pre>
[m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
</pre>
运用列表生成式，可以写出非常简洁的代码。例如，列出当前目录下的所有文件和目录名，可以通过一行代码实现：<pre>
import os # 导入os模块，模块的概念后面讲到
[d for d in os.listdir('.')] # os.listdir可以列出文件和目录
['.emacs.d', '.ssh', '.Trash', 'Adlm', 'Applications', 'Desktop', 'Documents', 'Downloads', 'Library', 'Movies', 'Music', 'Pictures', 'Public', 'VirtualBox VMs', 'Workspace', 'XCode']
</pre>
for循环其实可以同时使用两个甚至多个变量，比如dict的iteritems()可以同时迭代key和value,因此，列表生成式也可以使用两个变量来生成list：<pre>
d = {'x': 'A', 'y': 'B', 'z': 'C' }
[k + '=' + v for k, v in d.iteritems()]
['y=B', 'x=A', 'z=C']
</pre>
最后把一个list中所有的字符串变成小写：<pre>
L = ['Hello', 'World', 'IBM', 'Apple']
[s.lower() for s in L]
['hello', 'world', 'ibm', 'apple']
L = ['Hello', 'World', 18, 'Apple', None]
[s.lower() for s in L]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'int' object has no attribute 'lower'
[s.lower() for s in L if isinstance(s, str)]
['hello', 'world', 'apple']
[s.lower() if isinstance(s, str) else s for s in L]
['hello', 'world', 18, 'apple', None]
</pre>
- [生成器 Generator](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/00138681965108490cb4c13182e472f8d87830f13be6e88000)  
如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器（Generator）。要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：<pre>
L = [x * x for x in range(10)]
L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
g = (x * x for x in range(10))
g
<generator object <genexpr> at 0x104feab40>
</pre>
创建L和g的区别仅在于最外层的[]和()，L是一个list，而g是一个generator。我们可以直接打印出list的每一个元素，但我们怎么打印出generator的每一个元素呢？如果要一个一个打印出来，可以通过generator的next()方法,我们讲过，generator保存的是算法，每次调用next()，就计算出下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。这种不断调用next()方法实在是太变态了，正确的方法是使用for循环，因为generator也是可迭代对象：<pre>
g.next()
0
...
g.next()
81
g.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
g = (x * x for x in range(10))
for n in g:
...     print n
...
0
1
4
9
16
25
36
49
64
81
</pre>
generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。举个简单的例子，定义一个generator，依次返回数字1，3，5：<pre>
def odd():
...     print 'step 1'
...     yield 1
...     print 'step 2'
...     yield 3
...     print 'step 3'
...     yield 5
...
o = odd()
o.next()
step 1
1
o.next()
step 2
3
o.next()
step 3
5
o.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
</pre>
可以看到，odd不是普通函数，而是generator，在执行过程中，遇到yield就中断，下次又继续执行。执行3次yield后，已经没有yield可以执行了，所以，第4次调用next()就报错。
- TBD

### [Learn Python The Hard Way](#)
- TBD

