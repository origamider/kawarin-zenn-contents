---
title: "[機械学習]Sumノードの逆伝播についてわかりやすく"
emoji: "🍕"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [機械学習,誤差逆伝播法,Python,ニューラルネットワーク]
published: True
---

# はじめに
ゼロから作るDeep Learning2のコードのSumノードの逆伝播のコードの理解が浅かったため、
わかりやすく説明できるようにしました。
ちなみに該当コードは以下の部分です。(N,T,H)の形状であるtがSumノードを通し、(N,T)形状のsに変換される例です。
```
dt = ds.reshape(N, T, 1).repeat(H, axis=2)
```

# 対象読者
- ぜろつく2の逆伝播の理解をしたい方
- 行列のある方向の合計をするSumノードの逆伝播を理解したい方

# 数式ベースの説明
今回はわかりやすく２次元で考えます。

$$
\boldsymbol{a}=
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1T} \\
a_{21} & a_{22} & \cdots & a_{2T} \\
\vdots & \vdots & \ddots & \vdots \\
a_{N1} & a_{N2} & \cdots & a_{NT}
\end{pmatrix}
\in \mathbb{R}^{N\times T}
$$

$$
\boldsymbol{s}=
\begin{pmatrix}
s_1 \\ s_2 \\ \vdots \\ s_N
\end{pmatrix}
=
\begin{pmatrix}
\sum_{j=1}^{T} a_{1j} \\[6pt]
\sum_{j=1}^{T} a_{2j} \\[6pt]
\vdots \\[6pt]
\sum_{j=1}^{T} a_{Nj}
\end{pmatrix}
\in \mathbb{R}^{N}
$$

ここでは入力をa、出力をsとします。
数式ベースで理解がしにくい方には以下のような形をイメージしてもらえればわかりやすいかと思います。

```
[[1,2,3],[4,5,6]] --sum--> [6,15]
# 形状変化: (2,3) -> (2,)
```

そして早速、sumノードの逆伝播の結論をいいます。

$$
\frac{\partial L}{\partial \boldsymbol{a}}=
\begin{pmatrix}
\dfrac{\partial L}{\partial s_1} & \dfrac{\partial L}{\partial s_1} & \cdots & \dfrac{\partial L}{\partial s_1} \\[10pt]
\dfrac{\partial L}{\partial s_2} & \dfrac{\partial L}{\partial s_2} & \cdots & \dfrac{\partial L}{\partial s_2} \\[10pt]
\vdots & \vdots & \ddots & \vdots \\[10pt]
\dfrac{\partial L}{\partial s_N} & \dfrac{\partial L}{\partial s_N} & \cdots & \dfrac{\partial L}{\partial s_N}
\end{pmatrix}
\in \mathbb{R}^{N\times T}
$$

まず具体的に、$\frac{\partial L}{\partial a_{11}}$ を考えます。
ここで自分も理論的に証明ができない部分で申し訳ありませんが、
以下のようになります。

$$
\frac{\partial L}{\partial a_{11}} = 
\frac{\partial L}{\partial s_{1}}\frac{\partial s_{1}}{\partial a_{11}} + 
\cdots 
+ \frac{\partial L}{\partial s_{N}}\frac{\partial s_{N}}{\partial a_{11}} 
$$

直感的なイメージとしては、$a_{11}$がそれぞれのsへ影響を及ぼしているために、勾配は、 
$\frac{\partial L}{\partial s}\frac{\partial s}{\partial a_{11}}$ の総和になるものだと理解しています。
詳しくは、連鎖律で調べると良いでしょう。

ここで $s_{1} = a_{11}+a_{12}+\cdots+a_{1T}$ となるため、
$\frac{\partial s_{1}}{\partial a_{11}} = 1, \frac{\partial s_{2}}{\partial a_{11}}=\cdots=\frac{\partial s_{N}}{\partial a_{11}} = 0$ となります。
つまり、

$$
\frac{\partial L}{\partial a_{11}} = \frac{\partial L}{\partial s_{1}}
$$
となります。
同様に考えると、

$$
\frac{\partial L}{\partial a_{ij}} = \frac{\partial L}{\partial s_{i}}
$$
となります。
ここで重要なのは、j行目は関係なく、i行目のaの勾配については、全て $\frac{\partial L}{\partial s_{i}}$ になるという点です。

よって、

$$
\frac{\partial L}{\partial \boldsymbol{a}}=
\begin{pmatrix}
\dfrac{\partial L}{\partial s_1} & \dfrac{\partial L}{\partial s_1} & \cdots & \dfrac{\partial L}{\partial s_1} \\[10pt]
\dfrac{\partial L}{\partial s_2} & \dfrac{\partial L}{\partial s_2} & \cdots & \dfrac{\partial L}{\partial s_2} \\[10pt]
\vdots & \vdots & \ddots & \vdots \\[10pt]
\dfrac{\partial L}{\partial s_N} & \dfrac{\partial L}{\partial s_N} & \cdots & \dfrac{\partial L}{\partial s_N}
\end{pmatrix}
\in \mathbb{R}^{N\times T}
$$

が理解できたと思います！

つまり、
形状(N,T)のaがsumノードで形状(N,)のsに変換される場合、
逆伝播 $\frac{\partial L}{\partial a}$ は、$\frac{\partial L}{\partial s}$ のaxis=1方向(2次元)にコピーすればいいということがわかります。

同様に今回の例を考えると、
形状(N,T,H)のaがsumノードで形状(N,T)のsに変換される場合、
逆伝播 $\frac{\partial L}{\partial a}$ は、$\frac{\partial L}{\partial s}$ のaxis=2方向(3次元)にコピーすればいいと理解できます。

この説明なら、
```
da = ds.reshape(N, T, 1).repeat(H, axis=2)
```
のコードもなんとなく理解できると思います。

# 最後に
機械学習の逆伝播について、コードだけを見てもなかなか理解できないことが多いです。
数式ベースで具体例から考えれば、自分の中で腑に落ちました。

# 参考資料
[斎藤 康毅「ゼロから作るDeep Learning❷ー自然言語処理編」](https://www.oreilly.co.jp/books/9784873118369/)