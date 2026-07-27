---
title: "Node.jsって結局なんなの"
emoji: "🐕"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [nodejs,JavaScript]
published: true
---
# はじめに
Web開発でNext.jsなどを使う際、Node.jsが必要だと言われる。
"Node.jsはJavaScriptの実行環境である"と言われても、"JavaScriptの実行環境"がそもそもようわからん。なんとなく環境構築でNode.jsを入れ、npxだかnpmだかのコマンドを使っていい感じにしているが、これらをいいかげん理解したかったので、今回を機にちゃんと理解してみようと思います。

# 対象者
- 「npm,npxコマンド」とNode.jsの関係性が知りたい人
- Node.jsって結局なんなのかを知りたい人
- 「JavaScriptの実行環境」の意味を知りたい人

# 手始めにNode.jsとは。
Node.jsはJavaScriptの実行環境である。
よく、pythonやC言語などを実行する際、以下のようにコンパイル等をしますよね。
```python
python main.py
```
```
gcc main.c
```
これと同じように、Node.jsがあることで、
```javascript
node hello.js
```
のように実行できます。このようにターミナル上でJavaScriptを実行できる環境(プログラム)のことを指します。
そもそもの流れとして、
従来はJavaScriptはブラウザ上でしか実行できませんでした。
Chromeなどのブラウザの中にJavaScript専用の実行エンジンがあったからです。
ただ、JavaScriptを使ってサーバーの構築やOSアクセス(ファイルの読み書きなど？)をするために、Node.jsが作られました。
ちなみに余談ですが、Node.jsをインストールしていれば、どこかしらに必ずファイルがあるはずです。

# npm,npxコマンドとNode.jsの関係
## npmとは。
JavaScriptのパッケージ管理ツールで、ライブラリのインストールや、依存関係・バージョン管理などをコマンドベースでできる。
npm = Node Package Managerと書かれている記事が多々見られたが、実際は「npm is not an acronym」の再起表現らしい?
詳しくは(これ)[https://zenn.dev/ryuu/articles/what-npm-means]がおすすめ。面白い。
```
npm init -y
```
はプロジェクト作成のコマンド。package.jsonが作成される。
```
npm install dayjs
```
ここにdayjsと呼ばれるライブラリをインストールしてみると、package.jsonに
```
"dependencies": {
    "dayjs": "^1.11.21"
}
```
が追加される。

## npxとは。
インストール済み Or 未インストールのモジュールを実行するツール。
Next.jsの環境構築で最初に以下のような形でprojectを作成しますよね。
```
npx create-next-app kawarin-test
```
これですが、実は、next.jsがgithubで公開しているパッケージ([こちら](https://github.com/vercel/next.js/tree/canary/packages/create-next-app))を実行しています。
つまり、create-next-appというパッケージを実行しているのです。
詳しいnpxとnpmの違いについては[【Node.js入門】npmとnpxの違い](https://zenn.dev/uniformnext/articles/c68ea2bb6cbe00)を参考にするといいでしょう。

## Node.jsとの関係性
Node.jsはJavaScriptを動かす実行環境であり、npmはNode.jsにデフォルトで入っているパッケージ管理コマンド、
npxは一時的にモジュールの実行ができるコマンドだと認識しています。

## 終わりに
ここら辺がある程度理解できたので気持ちが良いです。ただ、より厳密に理解しようとすると、ブラウザの仕組みやJavaScriptエンジンなどを詳細に理解する必要が出てきて、大変なので、今回はここまででとどめておきます(笑)
間違っている箇所がございましたら、指摘していただけると幸いです！


# 参考資料
[Next.jsの環境構築を初心者向けにわかりやすく](https://zenn.dev/retasusan/articles/5bdc8c443f2e71)
[Node.jsとはなにか？なぜみんな使っているのか？](https://qiita.com/non_cal/items/a8fee0b7ad96e67713eb)
[プログラミング初心者のための JavaScript と Node.js の歴史、それを踏まえた勉強方法](https://zenn.dev/mizchi/articles/3789a101dae388d98159)
[【Node.js入門】npmとnpxの違い](https://zenn.dev/uniformnext/articles/c68ea2bb6cbe00)
