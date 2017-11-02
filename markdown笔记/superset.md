# superset

#### (在python虚拟环境中_pyenv和virtualenv或者anaconda自带的conda工具_，python版本要求在3.4以上)

> conda create -n superset python=3.4
>
> source activate superset  (windows不带source)  进入环境
>
> pip install superset -i https://pypi.douban.com/simple
>
> (安装过程中可能会出现 Microsoft virtual c++10 are required问题)可以先下载在离线安装
>
> 可以再该网址http://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml，
>
> 下载文件，sasl‑0.2.1‑cp34‑cp34m‑win_amd64.whl，cp34对应的是python版本。
>
> > pip install xxxxx/sasl‑0.2.1‑cp34‑cp34m‑win_amd64.whl
>
> 仍旧是pip install的方式，后面对应文件所在的路径，简单方法是将文件拖拽到cmd窗口。
>
> 安装成功后，需要进行初始化配置，也是在命令行输入。
>
> > fabmanager create-admin --app superset
>
> 首先用命令行创建一个admin管理员账户，也是后续的登陆账号。会依次提示输入账户名，账户使用者的first name、last name、邮箱、以及确认密码。fabmanager是flask的权限管理命令，如果大家忘了密码，也能重新设立。
>
> > python superset db upgrade
>
> 初始化数据源。
>
> > python superset load_examples
>
> 载入案例数据，这里的案例数据是世界卫生组织的数据，也是上文演示的各类可视化图表，大家登陆后能够直接看到。下载速度还行。
>
> > python superset init
>
> 初始化默认的用户角色和权限。
>
> > python superset runserver
>
> 最后一步骤，启动Superset服务。因为我们是本地环境，所以在浏览器输入 http://localhost:8088 即可。在runserver后面添加 -p XXXX 可更改为其他端口。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsNhaGOGQIsFEp7wuqUJlT3CO4axfawt0OHKJl7PkMojjt2rDiax7JSSg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)


>  superset不是内部或外部命令
>
>这是命名行没有写入环境变量，在cmd中切换至superset安装目录下的bin文件夹。
>
>输入cd 路径(要带空格的)，如下图案例。如果anaconda安装在D盘，首先得输入「D:」切换系统盘，然后再CD。
>
>当目录环境变为，类似XXX\Lib\site-packages\superset\bin> 时，输入python superset db upgrade即可正确启动superset初始化，superset命令前都要有python前缀。
>
>以后每次用都要这样，并且要先进入虚拟环境
>
> superset runserver失败
>
>Superset对windows的支持并不好，正常的runserver是启动不了的，必须以开发者模式启动。
>
>> python superset runserver -d 
>
>否则会报文件缺失错误。
>
>  **Failed to start remote query on a worker**
>
>这是在建立database后，执行sql query报错。
>
>在编辑database的时候，Expose in SQL Lab和Allow Run Sync都要勾选上，下面其余的不要勾选，保留这两个就好了。
>
>  **“module" object has no attribute 'SIGALRM'**
>
>****
>
>在勾选完Expose in SQL Lab和Allow Run Sync后，windows用户可能会出现上面的一些错误。
>
>这是windows下依赖包不兼容产生的。Python的signal包只作用于linux和mac，在win是不启作用的，所以这一块在win会产生冲突于是报错。开发团队应该是不小心的。
>
>解决方法就是把相关部分的代码注释掉，这块代码的功能是超时后把query进程杀掉，注释后没大影响。大家记得就好，我测试过了。


> 
>
> ![img](http://mmbiz.qpic.cn/mmbiz_jpg/9WoCz1BTJSgfxKlHXgoE0ddHNtbZpnDradDXz3wn4TSqrwfAFaJ71fZJs00I47icpG0Pq5L9tVtdgfibmB37z1IA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1)
>
> 


> 如上图，把signal所在行都注释，下面再加一个pass就好了，粗糙了点，没太大影响。文件在superset/utils.py下，代码中间部分。
>
> 其他一些小问题都是细节的，比如防火墙屏蔽，比如SQL读取的时候数据类型报错，这个可以靠调试解决。      
>
>   使用
>
> 先别急着使用，因为Superset是英文，我们先把它汉化了。Superset自身支持语言切换。
>
> 进入到Superset所在目录文件，按我之前的步骤，应该在anaconda/envs/superset/lib/python3.4/site-packages/superset中，路径视各位情况可能有差异。
>
> 在目录下有一个叫config.py的文件，打开它，找到Setup default language这一行，修改变量。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsibp4AgZxt5oXjiaufXuMWryTFZNYicOW7VSj1V6YCEVLv5XHDt6iaGASMg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> BABEL_DEFAULT_LOCALE调整为zh，这样界面默认为中文。languages字典中zh前面的注释#去掉。保存后退出。
>
> 接下来还是在Superset的目录下新创建文件夹，按translations/zh/LC_MESSAGES的路径依次创建三个。Superset官网提供了汉化包，在最大的同性交友网站github上下载，目录为：
>
> https://github.com/apache/incubator-superset/blob/master/superset/translations/zh/LC_MESSAGES/messages.mo
>
> 网址路径有点长，下载后把mo文件放在LC_MESSAGES文件下。清除浏览器的缓存，重新登陆localhost。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBszmKvPOxLVvbPej4x8tTW6icbLm2CQM4PEXkenoiaEuNPrEATeyib8cY6w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 搞定！
>
> 需要注意的是，它并非完全汉化，而是汉化了superset相关的部分。部分文字被写入在flask app的文件中，汉化起来比较麻烦。
>
> Superset分为多个模块，安全模块是账号管理相关，包括角色列表，视图权限控制，操作日志等。管理模块没什么用，主要是设计元素。
>
> 数据源可以访问和连接数据库，切片是各类数据可视化，均是单图；看板即为Dashboard，是切片的集合，Superset提供了三个初始案例，SQL工具箱是数据查询平台。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsqjTp1VF0VCloVdMgsfFeJYVA9V4iazVqlHfPbTLNicPjmnrw026CjqOQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 麻雀虽小，五脏俱全，对于大部分中小型的企业，Superset足以应付数据分析工作。
>
> 先学习连接数据库，这里以我电脑中的数据库为准，如果大家学习过早前的教程，那么数据库中都应该有数据分析师的练习数据，我这里不重复了，可以看历史文章。也可用自带的卫生数据照着练习。
>
> Superset使用了sqlalchemy框架，使用前需要安装数据库驱动程序，先退出runserver，进入superset虚拟环境，安装Python中的MySQL驱动程序。
>
> >  pip install pymysql
>
> MySQL的驱动程序很多，除了pymysql，还有mysqlclient等。安装好后，进入数据源，新建一个database连接。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsFKQ8Cq7sNeKnVXX4aQqBXzszk8fibTpmnFosYuU6QwEyfcib6xUhkicjA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 在SQLAlchemy URL中加入数据库的地址，格式为:
>
> > mysql+pymysql://root:xxxx@localhost:3306/qin?charset=utf8
>
> mysql是数据库类型，pymysql是驱动程序，表示用pymysql连接mysql数据库，+号不能省略。
>
> 另外，root是数据库登陆账号,xxxx为密码，这个按大家自己设立的来。localhost是数据库地址，因为我的是本地环境，所以localhost即可，也可以是127.0.0.1。3306是端口，一般默认这个。qin是需要连接的数据库，也是我自己设的名字。后面带参数charset=utf8，表示编码，因为表里面有中文。
>
> 其他数据库的连接大同小异，图中绿色的连接是相关教程。
>
> 如果大家在公司网络，拥有内网访问数据库的权限，也可以尝试连接，应该是可以的，这样就能在个人电脑上实行敏捷的BI分析。
>
> 格式命名好后，点击测试，出现seems ok，表示成功访问。在选项下面还有个Expose in SQL Lab，允许我们在SQL工具箱查询，要打上勾。
>
> 进入到SQL工具箱，左边选择table为DataAnalyst。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBszhiawXbpPSXg60F0belAXwHcHdErNYiba1aZe02ficrWhryU3VU3nmMEw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 直接出来了数据库的数据预览。连查询平台的颜值都那么高。大家的SQL技能应该都很不错，有兴趣可以在这里练习一下，语法和MySQL一致。其他数据库则是其他数据库的语法。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsucdvpgIQaAy036RUu1LicAibQuwVLKlgO38KAAKry2o0Q6icS3iaL85wUw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 执行一段SQL语句，它支持下载为CSV，我没试过支持最大文件的大小，但作为日常的查询平台是绰绰有余了。
>
> 选择Visualize，进入切片绘图模式。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsMerYEaa3qS0tiaAA4gFRwyoYGwNp5ia5Mlvdy9RKrIgvticXD6nyPO39w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 这里自动匹配支持的图表选项，包括Bar Chart条形图，Pir Chart饼图等。下面的选项是定义维度，我们将city，education，postitionName，salary，workYear都勾选为维度。agg_func是聚合功能，这里将职位ID求和，改成count()，点击生成图表。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsvkeH4pfTfrhqOWCFhoiaDHySo4GJ7hPFqYz6DibSMMF4npbxYER3E6Nw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 这里按城市生成了各职位ID求和获得的条形图，也就是不同城市的分析师人数。
>
> 左边Chart Options可以调整分析需要的维度。Metrics是分析的度量，这里是count(positionId)，Series是条形图中的类别，Breakdowns可以认为是分组或者分桶。这里将Series改成workYear，Breakdowns改成city，点击Query执行。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsE7XPiae5eXhLtgtB7U9Fhy1bOLhXdVfAkkenCKB5eqWzwJ8cD7lrhBQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 条形图变更为按工作年限和城市细分的多维条形图。点击Stacked Bars，则切换成堆积柱形图。操作不难。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBspurkK9ja3FQLeLN7CURAv3JlbMb7jiamTAjkf2qHPtFVUgRia3xMRe2Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 左侧的选项栏还有其他功能，这里就不多做介绍了，和市面上常见的BI没有多大区别，琢磨一下也就会了。
>
> Superset支持的图表很丰富，如果具备开发能力，也能以D3和Flask为基础做二次开发。Airbnb官方也会不断加入新的图表。不同图表，其左侧的操作选项也不同。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsPzCRWKSzg8tsvzL7IUy3lM5tzm5vPF7fs67Qphq80RXFkjgXRSK96A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 上图是以数据分析师职位名称为基础绘制的词云图，生成的速度会比较慢。我们选择save保存。完成的图表均存放在切片下。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBs3NNic5ZdxA4qPdCb7A5EjYV3BKNTQL8ZQwAorcgQL8jCriaSPnrhfqmQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> Dashboard通过多个切片组合完成，每个切片连接不同的数据源，这是BI的基本逻辑。进入看板界面，新建一个Dashboard。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBsj0MpwgNmIwa2Rl9DGvqRYJlE0pSdVZd8ghX3tIv8HpiaMlhOSZT5u1Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 设置看板相应的配置选项，因为我偷懒了，所以只做了两个切片，大家有兴趣可以继续增加。其他选项忽略，都是自动生成的。点击save，到这一步，BI最重要的Dashboard就完成了。
>
> 浏览一下最终的成果吧。
>
> ![img](http://mmbiz.qpic.cn/mmbiz_png/9WoCz1BTJSjwoEXTc7ovVDuyib7JV4icBs4rddL7sZtCUCSIBuUnmCtvIPvvNbyQfQ0QFQ1n5X6lSs5ibBbibJg2iag/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)
>
> 关于Superset的新手教学结束了，要是部署到公司，账号和权限多研究下。它和市面上的其他BI没有太多区别，不过它是我们用Python从零到有一手建立，这个感觉可比用Excel爽不少。虽然我的演示以单机版为主，将其建立在linux服务器上大同小异。
>
> 从零开始搭建到现在，排除掉下载花费的时间，大家可以计算是不是真的只用一个小时就搭建好一个数据分析平台？没骗你们吧。
>
> 通过搭建Superset，数据分析新手对BI应该也有一个大概的了解，市面上的BI大同小异，只是侧重点不同。在Superset的基础上，往底层完成埋点采集和数据ETL，往上拓展报表监控，CRM等，这些也有不少开源软件可用。至于机器学习，以及Hadoop和Spark更是一个大生态，把这些都算上，则是真正完整的大数据分析平台了。
>
> Superset也有缺陷，它使用的是ORM框架，虽然它能连接众多的数据库，但是它有一个关系映射过程，将SQL数据转化为Python中的对象，这也造成它在大数据量的处理效率不如专业的BI软件。在使用SQL工具箱时，应该尽量避免超大表之间的关联，以及复杂的group by。
>
> 我个人的建议是，它只是一款轻量级的BI，复杂的数据关联，应该在ETL过程中完成，Superset只需要执行最终结果表的读取即可。它足够支撑TB级别的数据源读取。技术比较成熟的团队，也能尝试将Superset和Kylin整合，这样OLAP的能力又能上一个台阶。
>
> 另外，Superset中的表都是独立的，所以多图表间的复杂联动并不支持，仅支持过滤，这点比较可惜。不知道Airbnb后续会不会支持。
>
> 好消息是，这个开源项目一直在更新，github什么也有很多新的功能特性待开发，比如dashboard上加入tab切换栏等。可以star一下关注。

摘自：https://mp.weixin.qq.com/s/u5KO6Dw9slbF6CJOoQd_Jg  和

https://mp.weixin.qq.com/s/LPQNuizvmzyyoNjUnrwE4A









