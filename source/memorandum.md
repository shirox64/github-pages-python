# 備忘録

## インストール方法(Mac)
1.homebrewのインストール
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
2.Python3インストール
```
brew install python
```
3.Python3確認
```
python3 -v
```

## Pythonの真偽値の定義
* 偽であると定義されている定数: NoneとFalse
* 数値型におけるゼロ: 0, 0.0, 0j(複素数), Decimal(0), Fraction(0, 1)
* 空のシーケンスまたはコレクション: '', (), [], {}, set(), range(0)
* 上記以外のオブジェクトはすべてTrue判定

## 多重ループ回避
```python
years = range(2010, 2013)
integers = range(1, 3)
chars = ('a', 'b', 'c')

for year, i, char in [(year, i, char) for year in years for i in integers for char in chars]:
  print(year, i, char)
```

## json標準出力
```python
import json
JSON_SAMPLE = '{"_meta": {"hash": {"sha256": "hash"}, "pipfile-spec": 6, "requires": {"python_version": "3.6"}, "sources": [{"name": "pypi", "url": "https://pypi.python.org/simple", "verify_ssl": true } ] } }'
data = json.loads(JSON_SAMPLE)
print(json.dumps(data, indent=2))
```

## jsonファイル出力
```python
test_file_path = '/XXX/YYY/ZZZ/'
result = json.loads(json.dumps(output_graph))
with open(test_file_path + 'result.json', 'w') as f:
    json.dump(result,f,indent=2,ensure_ascii=False)
```
※日本語含む場合 ensure_ascii=Falseを指定

## Noneの比較
None との比較に == や != を利用しない。 is や is not を利用する。

## Pythonはすべて参照渡し
※参照渡しでも書き換え可能なオブジェクトとcなオブジェクトが存在する。
* ミュータブルオブジェクト(書き換え可能)
list, set, dict など
* イミュータブルオブジェクト(書き換え不可能)
int, float, str, tuple など


## pandasパフォーマンス維持のためのTIPS
行に対するループとDataFrame.applyは使わない。  
pandas.DataFrameは内部的に同じ型の列をまとめてnp.ndarrayとして保持している。  
列ごとに連続したデータを持つことになるため、行に対するループには向かない。  
DataFrame.iterrows でのループの際には 異なる型を持つ列の値を Series として取り出すため、そのインスタンス化にも時間がかかる。  
numpyを使った方が断然早い！！！  
参考サイト : https://kunai-lab.hatenablog.jp/entry/2018/04/08/134924  
applyメソッドも使用を避ける

## if __name__ == '__main__':の下はグローバルスコープ
if __name__ == '__main__':の下で宣言した変数は、すべてグローバル変数になる！！  
main関数でくるむことによってグローバルスコープの名前空間は汚染されない。またmain関数でくるむことにより、main処理を冒頭に書けるのでコードの見通しがよくなる。
```Python
import sys

def main(args):
    for arg in args:
      print(arg)

if __name__ == '__main__':
    main(sys.argv[1:])
```