python中的zip,map，filter,reduce,lambda函数的使用

* lambda

  > lambda函数也叫做匿名函数,省去了命名。冒号前面是参数可以有多个，用逗号隔开，冒号右边是返回值。
  >
  > 1、 `def f(x): `
  >
  > ​	  `return x**2`
  >
  > 相当于 `g = lambda x: x**2`
  >
  > 2、`foo =[2,18,9,22] `
  >
  > ​	  print(list( filter(lambda x: x%3 ==0,foo) )
  >
  > 3、
  >
  > `b = lambda x: lambda y : x+y`
  >
  > `a=b(3)`
  >
  > `a(2)`
  >
  > 5
  >
  > `(b(2))(2)`
  >
  > 4

* filter  python内置函数

  > filter()函数用于过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表。两个参数。filter(function, iterable) 第一个为函数，第二个为序列（可迭代的），序列中每个参数传递给函数进行判断，然后返回True 或者False，最后将返回TRUE的元素放到新的列表中。
  >
  > ​

* map（map(function, iterable,...)）

  > map()函数会根据提供的函数对指定序列做映射。iterable，一个或多个序列。
  >
  > python 2.x返回列表   python 3.x 返回迭代器
  >
  > ![map](D:\picture\map.jpg)
  >
  > 提供了两个列表，对相同位置的列表数据进行相加
  >
  > \>\>\>map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
  >
  > [3, 7, 11, 15, 19]
  >
  > ​

* reduce (reduce (function,iterable[,initializer]))

  > reduce函数会对参数序列中的元素进行累积
  >
  > 函数将一个数据集合（链表，元组等）的所有数据进行下列操作：用传给reduce中的函数function（有两个参数）先对集合中的第1,2个元素进行操作，得到的结果再与第三个数据用function函数运算，最后得到一个结果
  >
  > ![reduce](D:\picture\reduce.png)
  >
  > \>\>\> reduce(lambda x,y:x+y,[1,2,3,4,5])
  >
  > 15

* zip()  python 的内建函数。

  > 它接受一系列可迭代的对象作为参数，将对象中对应的元素打包成一个个tuple（元组），然后返回由这些tuples组成的list（列表）。若传入参数的长度不等，则返回list的长度和参数中长度最短的对象相同。利用*号操作符，可以将list unzip（解压）
  >
  > ```python 
  > >>> a = [1,2,3]
  > >>> b = [4,5,6]
  > >>> c = [4,5,6,7,8]
  > >>> zipped = zip(a,b)
  > [(1, 4), (2, 5), (3, 6)]
  > >>> zip(a,c)
  > [(1, 4), (2, 5), (3, 6)]
  > >>> zip(*zipped)
  > [(1, 2, 3), (4, 5, 6)]
  >
  > #遍历字典
  > doc_dict={'title':[], 'link':[]}
  > for title,link in zip(doc_dict['title'],doc_dict['link']):
  >     print(title)
  >     print(link)
  > 	
  > ```



* 函数式编程

除了上面的内容外还有

print( [ x%3 for x in range(6) ])  #[0,1,2,0,1,2]

