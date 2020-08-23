# コーディング規約 
[PEP8の日本語ドキュメント](https://pep8-ja.readthedocs.io/ja/latest/)
## コードのレイアウト
### インデント
1レベルインデントするごとに、<font color="Red">スペースを4つ</font>使う。  
行を継続する場合は、折り返された要素を縦に揃える。
```python
# 開き括弧に揃える
foo = test_function(var1, var2, var3,
                    var4, var5, var6)

# 開き括弧で改行する場合は、1インデント入れて揃える
foo = test_function(
    var1, var2, var3,
    var4, var5, var6)

# 引数とそれ以外を区別するため、スペースを4つ加える
def foo = long_long_long_function(
        var1, var2, var3,
        var4, var5, var6):
    print(var1)
    print(var2)
    print(var3)
```
if文のときは、コメントを入れる、または継続された行の条件をインデントする。  
(前者はコメントを必ず挿入する必要があるので後者で揃えた方がおそらく良い)
```python
# コメントを挿入して条件とそれ以外を区別する
if (condition1 and
    condition2):
    # コメント
    do_something()

# 継続された行の条件をインデントする
if (condition1
        and condition2)
    do_something()
```
行を継続して波括弧、ブランケット、括弧を閉じるときの記号はインデントがあってもなくても良い。
```python
# 「リストの最後の要素が置かれた行の、はじめの文字の直下」に閉じる記号を置く
my_list = [
    1, 2, 3
    4, 5, 6
    ]

# 「継続された行のはじめの文字」に合わせて閉じる記号を置く
my_lsit = [
    1, 2, 3
    4, 5, 6
]
```
### 1行の長さ
行の長さは、<font color="Red">最大79文字</font>までに制限する。(docstringやコメントは72文字)  
途中で改行するとシンタックスエラーになる場合は、バックスラッシュを使うことで複数行に分割できる。  
バックスラッシュを使うのが好ましいケースはwith文やassert文などがある。
```python
with open('/path/to/some/file/test1') as file1, \
     open('/path/to/some/file/test2') as file2:
    file2.write(file1.read())
```
### 二項演算子の改行
二項演算子を使用している行を分割する場合、演算子の前で改行する。
```python
# 演算子の前で改行する
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```
### 空行
トップレベルの関数やクラスは2行ずつ空けて定義する。  
クラス内部では、1行ずつ空けてメソッドを定義する。
```python
def test_func1():
    pass


def test_func2():
    pass


class TestClass():

    def __init(self):
        pass

    def test_func3():
        passe
```
### import文
import文は、行を分ける。from文を使用するときは、行を分けない。
```python
# ダメな例(行を分けていない)
import sys, os

# 良い例(行を分けている)
import sys
import os

# from文は例外
from subprocess import Popen, PIPE
```
import文は次の順番でグループ化し、グループの間には1行空白を入れる  
1. 標準ライブラリ
2. サードパーティに関連するもの
3. ローカルなアプリケーション/ライブラリに特有のもの
```python
import os
import sys

import numpy as np
import pandas as pd

import custom_util
```
### 引用符
単一引用符(')か二重引用符(")を使うかプロジェクトで決める。  
三重引用符で文字列を囲むときは、常に二重引用符(""")を使う。
### 式や文中の空白文字
次の場合は、余計な空白文字を使わない。
```python
# 括弧やブランケット、波括弧の初めの直後と終わりの直前
# OK
spam(ham[1], {eggs: 2})
# NG
spam( ham[ 1 ], { eggs: 2 } )

# 末尾のカンマとその後に続く閉じ括弧の間
# OK
foo = (0,)
# NG
bar = (0, )

# カンマやセミコロン、コロンの直前
# OK
if x == 4: print x, y; x, y = y, x
# NG
if x == 4 : print x , y ; x , y = y , x

# 関数呼び出しの引数リストをはじめる開き括弧の直前
# OK
spam(1)
# NG
spam (1)

# インデックスやスライスの開き括弧の直前
# OK
dct['key'] = lst[index]
# NG
dct ['key'] = lst [index]

# 代入(や他の)演算子を揃えるために、演算子の周囲に1つ以上のスペースを入れる
# OK
x = 1
y = 2
long_variable = 3
# NG
x             = 1
y             = 2
long_variable = 3
```
スライスではコロンは二項演算子のように振舞うので同じ数のスペースを置く。  
拡張スライスでは、両側に同じ数のスペースを置く。  
スライスのパラメータが省略された場合は例外でスペースも省略する。
```python
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]
```
## 命名規則
### パッケージとモジュールの名前
モジュール名は、すべて小文字の短い名前にする。  
読みやすくなるならアンダースコア使用していいが、推奨しない。　　
### クラスの名前
CapWords方式を使う。  
最初の1文字は大文字で、その後はキャメルケースを使用する。  
(例)TestClass
### 関数や変数の名前
小文字のみ使用する。必要に応じて単語をアンダースコアで区切る。  
(例)test_func
### 定数
大文字のみ使用する。単語をアンダースコアで区切る。
