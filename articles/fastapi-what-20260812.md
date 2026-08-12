---
title: "FastAPIってなに？何ができるの。需要は。"
emoji: "📑"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [FastAPI, Python]
published: true
---
# はじめに
いろんなところでFastAPIという言葉を聞くが、そもそもFastAPIってなんなのか、何ができるのかが気になったので、初心者が軽く調べた結果を書きました。

# FastAPIとは
Pythonのフレームワーク。簡単にAPIを構築できるらしい。
フレームワークはライブラリのようなもの。人間が書いた、開発を楽にできるようにする専用のコード群。
詳しくは、[【定義】フレームワークとは何か](https://qiita.com/tamahassam/items/bf3755639bc9394bbee8)等で確認してくれ。
APIについては、[APIの仕組みとは？メリットや連携の事例を初心者向けにわかりやすく解説](https://data.wingarc.com/what-is-api-16084)を参考にすると良い。
簡単に自分のイメージを書くなら、
FastAPIを使用することで、開放されているendpointにアクセスすれば特定の処理が走る、みたいな仕組みを簡単に作れる。
なお、非同期処理も可能である。
つまり重い処理があった時(DBアクセス、LLM回答待ち)に、それを一旦待たずに次に進めるのである。

# 最後に
とりあえず軽く調べただけですが、思い出せました。
実際にFastAPIを使ってフルスタック開発してみたいですね。

# 参考資料
https://qiita.com/Hashimoto-Noriaki/items/6dbefe8068dbfe2c236d
https://data.wingarc.com/what-is-api-16084
