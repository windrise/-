## pandas索引

iloc 索整型索引
loc 索引字符串索引
ix 是 iloc 和 loc的合体

例如：
import pandas as pd
index_loc = ['a','b']
index_iloc = [1,2]
data = [[1,2,3,4],[5,6,7,8]]

columns = ['one','two','three','four']
df1 = pd.DataFrame(data=data,index=index_loc,columns=columns)
df2 = pd.DataFrame(data=data,index=index_iloc,columns=columns)

### df1 用.loc['a']可以正确检索，但用.iloc['a']则会报错





print(df1.loc['a'])
#-------------------
one 1
two 2
three 3
four 4
Name: a, dtype: int64
#-------------------

### 相反，df2 用.iloc[10]可以正确检索，但用.loc[10]则会报错



print(df2.loc[1])
#-------------------
one 1
two 2
three 3
four 4
Name: 10, dtype: int64
#-------------------

# .ix则在两个df里都可以通用
df1.ix['a']
df2.ix[1]
可以检索字符串型索引，也可以索引整型索引。

