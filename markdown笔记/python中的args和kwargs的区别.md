# python中的`*args`和`**kwargs`的区别

* `*args`

  > 用来将参数打包成tuple给函数体调用
  >
  > ```python
  > def function(arg,*args):
  >     print（arg,args,type(args)）
  >    
  > function(1,2,3,4,5)
  > #result
  > 1 （2,3,4,5） <class 'tuple'>
  >
  > ```
  >
  > ​

* `**kwargs` 

  > 打包关键字参数成dict给函数体调用
  >
  > ```python
  > def func(arg,*args,**kwargs):
  >     print(arg,args,kwargs,type(kwargs))
  >     
  > func(1,2,3,4,5,a=3)
  > #result
  > 1 (2, 3, 4, 5) {'a': 3} <class 'dict'>
  > ```
  >
  > ​