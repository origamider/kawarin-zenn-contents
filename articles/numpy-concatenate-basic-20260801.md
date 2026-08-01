---
title: "numpy.concatenateについてわかりやすく"
emoji: "🍔"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [numpy, 機械学習, ニューラルネットワーク, Python]
published: True
---

# はじめに
機械学習を勉強していく中で、よく、np.concatenateが出てくる。
2つのパラメータを合成するイメージではあるが、より詳細に理解するために書きました。

# 基本的な説明と具体例
```
np.concatenate((a1, a2), axis)
```
上記が基本。意味はarray型であるa1及びa2をaxis方向に合わせるイメージ。
これに関しては具体例を見た方が絶対わかりやすい。

```python
import numpy as np
a = np.array([[1,2,3],[4,5,6]])
b = np.array([[7,8,9],[10,11,12]])
```
このようなa,bを用意する。
形状は、a,b両方とも、(2,3)である。2行3列のarray型になっている。
では早速、np.concatenateで合成してみる。

```python
c = np.concatenate((a,b),axis=0)
print(f"c.shape = {c.shape}")
print(f"c = \n{c}")
```
上記のようなコードを考える。今回はaxis=0としている。(a,b)のようにタプル型？を入力としている。とりあえず配列の列が入っていればOK。
出力は以下のようになった。
```
c.shape = (4, 3)
c = 
[[ 1  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [10 11 12]]
```
このように、axis=0と指定することで、形状は(2,3)->(4,3)のように、1次元目をベースに合成される。
結果的に、[1,2,3],[4,5,6]の後に続いて、[7,8,9],[10,11,12]が続く形になる。
続いて以下のようにaxis=1に変更する。
```python
d = np.concatenate((a,b),axis=1)
print(f"d.shape = {d.shape}")
print(f"d = \n{d}")
```
結果はこちら。
```
d.shape = (2, 6)
d = 
[[ 1  2  3  7  8  9]
 [ 4  5  6 10 11 12]]
```
今度はaxis=1と設定したため、(2,3)->(2,6)のように2次元目をベースに合成される。
結果的に、[1,2,3]の中に[7,8,9]が、[4,5,6]の中に[10,11,12]が入った形になる。

全体のコードはこちら。
```python
import numpy as np

a = np.array([[1,2,3],[4,5,6]])
b = np.array([[7,8,9],[10,11,12]])

print(f"a.shape = {a.shape}")
print(f"b.shape = {b.shape}")

c = np.concatenate((a,b),axis=0)
d = np.concatenate((a,b),axis=1)

print(f"c.shape = {c.shape}")
print(f"c = \n{c}")

print(f"d.shape = {d.shape}")
print(f"d = \n{d}")
```

# 終わりに
機械学習を勉強していると、pythonやnumpyの構文で色々わからない部分が出てきます。
行列的な操作で、入力パラメータの合成や出力の分解、特定の次元部分のみの変更、など。
今後もわからない部分が出てきたらその都度しっかり調べたいと思いました！

# 参考資料
https://numpy.org/doc/stable/reference/generated/numpy.concatenate.html
