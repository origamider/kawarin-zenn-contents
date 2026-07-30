---
title: "Softmax単体の逆伝播を計算グラフで導出する【ゼロつく2】"
emoji: "💬"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [ニューラルネットワーク,Python,誤差逆伝播法,ディープラーニング]
published: True
---
# はじめに
```python
def backward(self, dout):
        dx = self.out * dout
        sumdx = np.sum(dx, axis=1, keepdims=True)
        dx -= self.out * sumdx
        return dx
```
早速だが、これは、ゼロから作るDeep Learning2で使われている、Softmax層の逆伝播コード(Numpy)である。
よくあるSoftmax + Cross Entropyを組み合わせたものではなく、Softmaxのみのパターンで、
実装コードがなにこれ状態だったので、それをサポートするための記事を書きたいと思いました。

# 対象読者
- Softmax単体の逆伝播コードを理解したい方

# 説明
## 基本説明
Softmax関数の定義は以下のような形です。

$$
    y_{i} = \frac{e^{x_{i}}}{\sum_{i} e^{x_{i}}}\\
    Y = (y1,y2,..,yn) = softmax(X)
$$

ここから計算グラフを図示すると以下のようになります。
![](/images/softmax-backward-20260730/image1.png)

最初に逆伝播の結果を表示します。
![](/images/softmax-backward-20260730/image2.png)

なお、dxは、$\frac{dLoss}{dx}$を表すとする。

$x_{i}$に対し、$y_{i}(dy_{i} - \sum_{i}{y_{i}dy_{i}})$ が逆伝播となる。
```
dx = self.out * dout
```
で、$y_{i}dy_{i}$ を計算し、
```
sumdx = np.sum(dx, axis=1, keepdims=True)
```
で、$\sum_{i}{y_{i}dy_{i}}$ を計算、
```
dx -= self.out * sumdx
```
最後にこれをすることで、ようやく$y_{i}(dy_{i} - \sum_{i}{y_{i}dy_{i}})$ が求められる。

## 各ノードと逆伝播
ここでは軽く各ノードごとの逆伝播を記載する。詳しくはネットで調べるとわかると思う。

- 掛け算ノード
ここでは行列積ではなく、ただの要素同士の掛け算(アダマール積)を表す。
逆伝播はz = xyとすると、
$$\frac{dL}{dz} = y\frac{dL}{dz}$$
つまり、上流から流れてきた勾配ともう片方の数値の掛け算でできる。

- 割り算(inverse)ノード
$y = \frac{1}{x}$とすると、
$$\frac{dL}{dx} = -\frac{dL}{dy}x^{-2}$$

- 足し算ノード
基本的には上流からの勾配がそのまま流れる。

- expノード
$y = e^x$とすると、
$$\frac{dL}{dx} = e^x\frac{dL}{dy}$$

## その他重要点
あるノードから分散して進む場合、逆伝播は、それぞれの勾配を足したものになる。
言葉で言ってもわかりにくいので今回の例で説明する。
割り算(inverse)ノードの出力を見てほしい。それぞれ$e^{x_{1}}dy_{1}$ ,$e^{x_{2}}dy_{2}$, $e^{x_{3}}dy_{3}$が出力されている。
ここで、割り算ノードの、上流から流れる勾配は、3つの出力を合わせた、
T = $e^{x_{1}}dy_{1} + e^{x_{2}}dy_{2} + e^{x_{3}}dy_{3}$となる。

# 最後に
ぜろつく2でsoftmax単体の逆伝播コードが使われていたが、その導出方法が書かれていなかったため、今回記事にしました。
ここら辺の逆伝播の理解がかなり深まりました。

# 参考資料
[斎藤 康毅「ゼロから作るDeep Learning❷ー自然言語処理編」](https://www.oreilly.co.jp/books/9784873118369/)
