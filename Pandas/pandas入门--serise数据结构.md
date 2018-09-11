
# 1.pandas 数据结构--serise数据结构

Pandas 的数据结构主要有两种：Series（一维） 和DataFrame（二维） 


```python
import pandas as pd #pandans 导入
```

# series相关操作

Series结构是基于NumPy的ndarray结构，是一个一维的矩阵

①创建 ：pd.Series([list1]，index=[list2])//以list1、2为参数，参数为一list;index为可选参数，若不填则默认index从0开始递增；若添则index长度（list2的长度）需要与list1的长度相同


```python
s1 = pd.Series([1, 2, 3, 4, 5])
print('无index参数：
      \n',s1)
s2 = pd.Series([1, 1, 1, 1, 1], index = ['a', 'b', 'c', 'd','e'])
print('有index参数：\n',s2)
```

可以通过字典直接指定index(如下)


```python
s1 = pd.Series({'a':3,'b':4,'c':5,'f':6,'e':8})
print(s1)
```

②取数据：<br>s[index]或者s[index的list]
<br>取值操作类似于数组


```python
import numpy as np #引入numpy

v = np.random.random_sample(50) #生成一个有五十个随机数数组
s = pd.Series(v)
s1 = s[[3, 4, 7]]#取出index为3，4，7的元素存为一个新Series
s2 = s[0:5]#取出index为0-5的元素
s3 = s[23]#取出index为23的元素
print("s1\n",s1)
print("s2\n",s2)
print("s3\n",s3)
```

.head(n)和.tail(n)函数用法：
<br>取出头n行或尾n行，n为可选参数，若不填默认n取5

s = pd.Series(v)
print(s.head(3))#取出s中前三组元素
print(s.tail())#取出s中后五组元素

s.len()/求s的长度；np.shape(s)/求矩阵形状；v.unique()/出现不重复values值


```python
v = [10,3,2,1,1,1, np.nan]#nan为非数字数据
s = pd.Series(v)
print("len():",len(s))#长度
print("shape():",np.shape(s))#形状
print("count():",s.count())#数值数据长度（不包含nan）
print("unique()",s.unique() )#出现不重复values值,（转化成集合）
print("value_counts():\n",s.value_counts())#统计非重复数据的出现次数
```

③加法：相同index的value相加，若index并非共有的则该index对应value变为NaN


```python
s1=pd.Series([1,2,3,4],index=[1,2,3,4])
s2=pd.Series([1,1,1,1])
s3=s1+s2
print(s3)
```

 < 原创文章，转载请标明出处 >
