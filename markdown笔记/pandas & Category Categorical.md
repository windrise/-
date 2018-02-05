## pandas & Category Categorical

* categories 与 set_categories

```python
#类别相关的方法
>>> df = pd.DataFrame({"id":[1,2,3,4,5,6],"raw_grade":['big','big','small','small','mid','mid']})
>>> df["grade"]=df["raw_grade"].astype("category")
>>> df
   id raw_grade  grade
0   1       big    big
1   2       big    big
2   3     small  small
3   4     small  small
4   5       mid    mid
5   6       mid    mid
>>> print(df["grade"])
0      big
1      big
2    small
3    small
4      mid
5      mid
Name: grade, dtype: category
Categories (3, object): [big, mid, small]
#可以看到此时类标签字符 big,mid,small ;类标签集合为[big, mid, small]
#改变类标签
>>> df["grade"].cat.categories=["very good","good","very bad"]
>>> print(df["grade"])
0    very good
1    very good
2     very bad
3     very bad
4         good
5         good
Name: grade, dtype: category
Categories (3, object): [very good, good, very bad]
#给categories赋值可以改变可以改变类别标签。赋值的时候是按照顺序进行对应的
>>> df["grade"]=df["grade"].cat.set_categories(["very bad","bad","medium","good","very good"])
>>> print(df["grade"])
0    very good
1    very good
2     very bad
3     very bad
4         good
5         good
Name: grade, dtype: category
Categories (5, object): [very bad, bad, medium, good, very good]
#改变类别标签集合，操作过后数据的标签不变，但是标签的集合变为[“very bad”, “bad”, “medium”, “good”, “very good”]

#按照类标签在标签集中的顺序排序，而不是按照类标签的字母顺序进行排序
>>> dfnew=df.sort_values(by="grade")
>>> print(dfnew)
   id raw_grade      grade
2   3     small   very bad
3   4     small   very bad
4   5       mid       good
5   6       mid       good
0   1       big  very good
1   2       big  very good

#根据标签进行分组
>>> df.groupby("grade").size()
grade
very bad     2
bad          0
medium       0
good         2
very good    2
dtype: int64

```

* `pd.Categorical`   & `pd.Categorical.codes`

```python
#将序列 列表（list） 元组（tuple） 数组（ndarray）转换成 category类型
>>> a=["ni","hao"]
>>> pd.Categorical(a)
[ni, hao]
Categories (2, object): [hao, ni]
>>> pd.Categorical(a).dtype
category
>>> x=pd.Categorical(a)
>>> x
[ni, hao]
Categories (2, object): [hao, ni]

#逻辑回归中，决策树等模型中的编码  （one-hot等）
#pd.Categorical().codes   编码
>>> a=["n","hao","a","y","ll"]
>>> pd.Categorical(a).codes
array([3, 0, 1, 4, 2], dtype=int8)
#或者
>>> pd.Categorical(a,categories=["hao","l","y","n","ll"])
[n, hao, l, y, ll]
Categories (5, object): [hao, l, y, n, ll]
    
    
 #Use copy=True to prevent such a behaviour or simply don’t reuse Categoricals:   
>>> cat = pd.Categorical([1,2,3,10], categories=[1,2,3,4,10])
>>> cat
[1, 2, 3, 10]
Categories (5, int64): [1, 2, 3, 4, 10]
>>> s = pd.Series(cat, name="cat", copy=True)
>>> s
0     1
1     2
2     3
3    10
Name: cat, dtype: category
Categories (5, int64): [1, 2, 3, 4, 10]
```





