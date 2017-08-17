### python常用

> python join（）
>
> str.join(sequence)       #sequence 要连接的元素序列     #返回值：返回通过制定字符连接序列中元素后生成的新字符串
>
> ```
> #!/usr/bin/python
>
> str = "-";
> seq = ("a", "b", "c"); # 字符串序列
> print str.join( seq );
>
> ```



> 输出： a-b-c
>


> 
>
> python 3中只有unicode str，所以把decode方法去掉了。你的代码中，f1已经是unicode str了，不用decode。
>
> 如果文件内容不是unicode编码的，要先以二进制方式打开，读入比特流，再解码。
>
> ```
> /tmp/ python3
> Python 3.2.3 (default, Feb 20 2013, 14:44:27) 
> [GCC 4.7.2] on linux2
> Type "help", "copyright", "credits" or "license" for more information.
> >>> f1 = open("unicode.txt", 'r').read()
> >>> print(f1)
> 寒冷
>  
> >>> f2 = open("unicode.txt", 'rb').read() #二进制方式打开
> >>> print(f2)
> b'\xe5\xaf\x92\xe5\x86\xb7\n'
> >>> f2.decode()
> '寒冷\n'
> >>> f1.decode()
> Traceback (most recent call last):
>   File "<stdin>", line 1, in <module>
> AttributeError: 'str' object has no attribute 'decode'
> >>> 
> ```


> 
>
> open方法返回的是一个文件对象
> 而使用read方法后，返回的是一个包含文件内容的字符串
> 可以用readlines，这个返回的是列表
>
> 即为  open(FileName, 'r').read() 和open(FileName, 'r')区别