#### 直接运行py文件
1. 第一行加上 `#!/user/bin/env python`
2. 添加可执行属性 `chmod a+x hello.py`

#### 基本输入输出
 `raw_input`,`print`

#### python跳出n层循环的方式
1.自定义异常
2.封装成函数，使用`return`
3.for else

#### 内置数据类型
1.list和tuple是Python内置的有序集合，一个可变，一个不可变。根据需要来选择使用它们。
2.if else;if elif else;
#### 函数定义
Python的函数具有非常灵活的参数形态，既可以实现简单的调用，又可以传入非常复杂的参数。

默认参数一定要用不可变对象，如果是可变对象，运行会有逻辑错误！

要注意定义可变参数和关键字参数的语法：

*args是可变参数，args接收的是一个tuple；

**kw是关键字参数，kw接收的是一个dict。

以及调用函数时如何传入可变参数和关键字参数的语法：

可变参数既可以直接传入：func(1, 2, 3)，又可以先组装list或tuple，再通过\*args传入：func(*(1, 2, 3))；

关键字参数既可以直接传入：func(a=1, b=2)，又可以先组装dict，再通过\*\*kw传入：func(**{'a': 1, 'b': 2})。

使用\*args和\**kw是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。

####其他
1.默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.itervalues()，如果要同时迭代key和value，可以用for k, v in d.iteritems()。