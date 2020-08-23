# NumPy

## NumPyとは
NumPyは科学技術計算に特化したサードパーティ製パッケージで配列や行列を効率よく扱える。

## インポート
```Python
# NumPyのインポート
import numpy as np
```

## 1次元配列
```Python
# 1次元配列作成
array_1d = np.array([1, 2, 3])

array_1d
# array([1, 2, 3])

print(array_1d)
# [1, 2, 3]

type(array_1d)
# numpy.ndarray

array_1d.shape
# (3,)
```

## 2次元配列
```Python
# 2次元配列作成
array_2d = np.array([[1, 2, 3], [4, 5, 6]])

array_2d
# array([[1, 2, 3],
#        [4, 5, 6]])

print(array_2d)
# [[1, 2, 3]
#  [4, 5, 6]]

array_2d.shape
# (2, 3)
```

## 変形
``` Python
array1 = np.array([1, 2, 3, 4, 5, 6])
array1
# array([1, 2, 3, 4, 5, 6])

# 1次元配列を2次元配列に変形
array2 = array1.reshape((2, 3))
array2
# array([[1, 2, 3],
#        [4, 5, 6]])

# 変形する要素数が合わない場合は、エラーになる
array3 = array1.reshape((3, 4))
# ValueError: cannot reshape array of size 6 into shape (3,4)

# 1次元配列に戻す *参照を渡す
array4 = array2.ravel()
array4
# array([1, 2, 3, 4, 5, 6])

# 1次元配列に戻す *コピーを返す
array5 = array2.flatten()
# array([1, 2, 3, 4, 5, 6])
```

## データ型
### データ型一覧
下記の表は、numpyのデータ型の一覧です。

|データ型|型コード|説明|
|:---|:--:|:---|
|int8	    |i1	    |符号あり8ビット整数型|
|int16	    |i2	    |符号あり16ビット整数型|
|int32	    |i4	    |符号あり32ビット整数型|
|int64	    |i8	    |符号あり64ビット整数型
|uint8	    |u1	    |符号なし8ビット整数型|
|uint16	    |u2	    |符号なし16ビット整数型|
|uint32	    |u4	    |符号なし32ビット整数型|
|uint64	    |u8	    |符号なし64ビット整数型|
|float16	|f2	    |半精度浮動小数点型（符号部1ビット、指数部5ビット、仮数部10ビット）|
|float32	|f4	    |単精度浮動小数点型（符号部1ビット、指数部8ビット、仮数部23ビット）|
|float64	|f8	    |倍精度浮動小数点型（符号部1ビット、指数部11ビット、仮数部52ビット）|
|float128	|f16	|四倍精度浮動小数点型（符号部1ビット、指数部15ビット、仮数部112ビット）|
|complex64	|c8	    |複素数（実部・虚部がそれぞれfloat32）|
|complex128	|c16	|複素数（実部・虚部がそれぞれfloat64）|
|complex256	|c32	|複素数（実部・虚部がそれぞれfloat128）|
|bool	    |?	    |ブール型（True or False）|
|unicode	|U	    |Unicode文字列|
|object	    |O	    |Pythonオブジェクト型|

### データ型の指定
``` Python
# データ型を指定しない場合は、自動で設定される
array1 = np.array([1, 2, 3])
array1.dtype
# dtype('int32')

# データ型を指定は、下記の3パターンがあります
# 1. np.int16
array2 = np.array([1, 2, 3], dtype=np.int16)
# 2. 文字列'int16'
array2 = np.array([1, 2, 3], dtype='int16')
# 3. 型コードの文字列'i2'
array2 = np.array([1, 2, 3], dtype='i2')

array2.dtype
# dtype('int16')

# 配列作成後にデータ型を変更
array2.astype(np.float16)
# array([1, 2, 3], dtype=float16)
```

## インデックスとスライス
``` Python
array1 = np.array([1, 2, 3])
array1[0]
# 1
array1[1:]
# array([2, 3])
array1[-1]
# 3

array2 = np.array([[1, 2, 3], [4, 5, 6]])
array2[0]
# array([1, 2, 3])
array2[1, 0]
# 4
array2[:, 2]
# array([3, 6])
array2[1, :]
# array([4, 5, 6])
array2[0, 1:]
# array([2, 3])
arary2[:, [0, 2]]
# array([[1, 3],
#        [4, 6]])
```

## データ再代入
``` Python
array1 = np.array([1, 2, 3])
array1[2] = 4
array1
# array([1, 2, 4])

array2 = np.array([[1, 2, 3], [4, 5, 6]])
array2[1, 2] = 7
array2
# array([[1, 2, 3],
#        [4, 5, 7]])

array2[:, 2] = 8
array2
# array([[1, 2, 8],
#        [4, 5, 8]])
```

## 深いコピー(copy)
コピーには浅いコピーと深いコピーがあるのでしっかり理解する必要があります。
特にPython標準のリストではスライスした結果はコピーが渡されますが、NumPyではスライスした結果は参照が渡されるので注意。
``` Python
a1 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

# 浅いコピー
b1 = a1
# b1とa1の参照先が同じなのでb1を変更するとa1も変わる
b1[:, 2] = 9
b1
# array([[1, 2, 9],
#        [4, 5, 9],
#        [7, 8, 9]])
a1
# array([[1, 2, 9],
#        [4, 5, 9],
#        [7, 8, 9]])

# 深いコピー
b1 = a1.copy()
# b1には新しいオブジェクトが作成されているので変更してもa1に影響はない
b1[:, 2] = 9
b1
# array([[1, 2, 9],
#        [4, 5, 9],
#        [7, 8, 9]])
a1
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])
```

## 数列を返す
``` Python
np.arange(10)
# array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

np.arange(1, 7)
# array([1, 2, 3, 4, 5, 6])

np.arange(1, 7, 2)
# array([1, 3, 5])
```

## 配列の結合
### 水平方向に結合
水平方向に結合するには、np.hstack()またはnp.concatenate()関数を使用します。
``` Python
a1 = np.arange(4).reshape(2, 2)
# array([[0, 1],
#        [2, 3]])

a2 = np.arange(4, 8).reshape(2, 2)
# array([[4, 5],
#        [6, 7]])

a3 = np.hstack((a1, a2))
# array([[0, 1, 4, 5],
#        [2, 3, 6, 7]])

a4 = np.concatenate((a1, a2), axis=1)
# array([[0, 1, 4, 5],
#        [2, 3, 6, 7]])
```

### 垂直方向に結合
垂直方向に結合するには、np.vstack()またはnp.concatenate()関数を使用します。
``` Python
a1 = np.arange(4).reshape(2, 2)
# array([[0, 1],
#        [2, 3]])

a2 = np.arange(4, 8).reshape(2, 2)
# array([[4, 5],
#        [6, 7]])

a3 = np.vstack((a1, a2))
# array([[0, 1],
#        [2, 3],
#        [4, 5],
#        [6, 7]])

a4 = np.concatenate((a1, a2), axis=0)
# array([[0, 1],
#        [2, 3],
#        [4, 5],
#        [6, 7]])
```

### 奥行き方向に結合
奥行き方向に結合するには、np.dstack()関数を使用します。
``` Python
a1 = np.arange(4).reshape(2, 2)
# array([[0, 1],
#        [2, 3]])

a2 = np.arange(4, 8).reshape(2, 2)
# array([[4, 5],
#        [6, 7]])

a3 = np.dstack((a1, a2))
# array([[[0, 4],
#         [1, 5]],
#        [[2, 6],
#         [3, 7]]])
```

### 新しい列として結合
np.column_stack()関数を使用して、1次元の配列を新しい列として結合することができます。
``` Python
a1 = np.arange(6).reshape(2, 3).T
# array([[0, 3],
#        [1, 4],
#        [2, 5]])

a2 = np.arange(6, 9)
# array([6, 7, 8])

a3 = np.column_stack((a1, a2))
# array([[0, 3, 6],
#        [1, 4, 7],
#        [2, 5, 8]])
```

### 新しい行として結合
np.row_stack()関数を使用して、1次元の配列を新しい行として結合することができます。
``` Python
a1 = np.arange(6).reshape(3, 2)
# array([[0, 1],
#        [2, 3],
#        [4, 5]])

a2 = np.array([6, 7])
# array([6, 7])

a3 = np.row_stack((a1, a2))
# array([[0, 1],
#        [2, 3],
#        [4, 5],
#        [6, 7]])
````

## 統計関数
### 和
sum()関数はそれぞれ、配列の要素の和を計算します。
引数に何も指定していない場合は、全ての要素に対して演算が適用されます。
各列の合計を求めるためにはaxis=0を、各行の合計を求めるためにaxis=1を指定します。
``` Python
a1 = np.arange(1, 6)
# array([1, 2, 3, 4, 5])

a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a1.sum(), a2.sum()
# (15, 45)

a2.sum(axis=0)
# array([12, 15, 18])
```

### 積
prod()関数は、配列の要素の積を計算します。引数はsumと同様です。
``` Python
a1 = np.arange(1, 6)
# array([1, 2, 3, 4, 5])

a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a1.prod(), a2.prod()
# (120, 362880)

a2.prod(axis=1)
# array([6, 120, 504])
```

### 累積和
累積和を求めるには、cumsum()関数を使用します。
``` Python
a1 = np.arange(1, 6)
# array([1, 2, 3, 4, 5])

a1.cumsum()
# array([ 1,  3,  6, 10, 15])

a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.cumsum()
# array([ 1,  3,  6, 10, 15, 21, 28, 36, 45])

a2.cumsum(axis=0)
# array([[ 1,  2,  3],
#        [ 5,  7,  9],
#        [12, 15, 18]])
```

### 累積積
累積積を求めるには、cumprod()関数を使用します。
``` Python
a1 = np.arange(1, 6)
# array([1, 2, 3, 4, 5])

a1.cumprod()
# array([  1,   2,   6,  24, 120])

a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.cumprod()
# array([     1,      2,      6,     24,    120,    720,   5040,  40320,
#        362880])

a2.cumprod(axis=1)
# array([[  1,   2,   6],
#        [  4,  20, 120],
#        [  7,  56, 504]])
```

### 平均
平均を求めるには、mean()関数を使用します。
``` Python
a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.mean(axis=1)
# array([2., 5., 8.])
```

### 標準偏差
標準偏差を求めるには、std()関数を使用します。
``` Python
a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.std(axis=1)
# array([0.81649658, 0.81649658, 0.81649658])
```

### 分散
分散を求めるには、var()関数を使用します。
``` Python
a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.var(axis=1)
# array([0.66666667, 0.66666667, 0.66666667])
```

### 最小
``` Python
a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.min()
# 1

a2.min(axis=1)
# array([1, 4, 7])
```

### 最大
``` Python
a2 = np.arange(1, 10).reshape(3, 3)
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])

a2.max()
# 9

a2.max(axis=1)
# array([3, 6, 9])
```

