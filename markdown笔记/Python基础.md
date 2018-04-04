#Python基础

* pip 安装包

  > 1、pip install ...
  >
  > 国内镜像源：
  >
  > > 清华: https://pypi.tuna.tsinghua.edu.cn/simple 
  > >
  > > 豆瓣: http://pypi.douban.com/simple/
  > >
  > > 阿里: http://mirrors.aliyun.com/pypi/simple/  
  >
  > 2、手动指定安装源
  >
  > pip install xx -i http://pypi.douban.com/simple 
  >
  > 3、全局指定安装源
  >
  > windows在user目录下新建pip文件夹，进入pip文件夹新建pip.ini，加入以下内容即可。
  >
  > >[global]
  > >index-url = https://pypi.tuna.tsinghua.edu.cn/simple

* conda安装

  > 1、 conda install ...
  >
  > 2、更换国内源（目前只有清华的）
  >
  > >​    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  > >​    conda config --set show_channel_urls yes
  >
  > 3、 conda remove ...



## 人生苦短我用Python

> 应用： 网络爬虫、 数据分析挖掘、数据可视化、web开发、机器学习

写程序：

> 命令行、IDLE、Jupyter。。。
>
> 交互式和文件（python a.py）

输入输出：

> ```python
> name=input()
> print('hello,',name,'It's nice')
> ```
>
> 

* jupyter-notebook

  > 1.打开 cmd ，输入命令 jupyter notebook --generate-config，将生成 jupyter_notebook_config.py文件
  >
  > 2.在C:\Users\Administrator\.jupyter 中的文件找到文件 jupyter_notebook_config.py
  >
  > 3.用记事本打开找到 # The directory to use for notebooks and kernels.
  > 修改这一句c.NotebookApp.notebook_dir = u' 
  >
  > 为c.NotebookApp.notebook_dir = u'E:\\jupyternotebook'

  使用博客： http://blog.csdn.net/liuyanlin610/article/details/76231958/

* 基本数据类型

  * 整数(int)、浮点数(float)、复数(complex)  运算（`**`  幂运算）

    type(223)、isinstance(233,int)、isinstance(233,float)、


  * 字符串(string)

    [以**单引号**或**双引号**括起来的任意文本，比如 ‘abc',"xyz"],请注意，`''`或`""`本身只是一种表示方式，不是字符串的一部分，因此，字符串`'abc'`只有`a`，`b`，`c`这3个字符。如果`'`本身也是一个字符，那就可以用`""`括起来，比如`"I'm OK"`包含的字符是`I`，`'`，`m`，空格，`O`，`K`这6个字符。

    转移字符`\`  比如`\n`换行，等等

    上面是在交互式命令行内输入，注意在输入多行内容时，提示符由`>>>`变为`...`，提示你可以接着上一行输入，注意`...`是提示符，不是代码的一部分;  Python里面的

  * 布尔值(bool)    运算（and,or,not） 不可以与 `0/1` 互换    `>` `<` `=` 运算得到布尔值

    ```python
    True and True 

    5>3 and 2>9

    ```

  * 空值 `None` 不是0，一个特殊的空值

  * 变量 

   >a=3    #不用声明，自动默认
   >
   >ab='nihao'
   >
   >ac=True
   >
   >print(type(a)) ...

  这种变量本身类型不固定的语言称之为**动态语言** ，与之相对的是**静态语言** （java： int a=0;）

  ```python
  a = 'ABC'
  b = a
  a = 'XYZ'
  print(b)
  ```
  分析：
  执行a = 'ABC'，解释器创建了字符串'ABC'和变量a，并把a指向'ABC'
  执行b = a，解释器创建了变量b，并把b指向a指向的字符串'ABC'
  执行a = 'XYZ'，解释器创建了字符串'XYZ'，并把a的指向改为'XYZ'，但b并没有更改


  ```
  ```
自行查看廖雪峰python3教程基本内容
  ​

  ​