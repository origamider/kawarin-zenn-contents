---
title: "ZennCliで初めてのZenn投稿をしてみた"
emoji: "🔖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Zenn, 記事, zenncli]
published: false
---
## はじめに
これからZennでいろんな技術系の記事を投稿したいと思っていたので、手始めにZennCliを使ってVsCodeから記事投稿をしてみたいと思います。

## ZennとGithubの連携
まず初めにZennとGithubを連携します。
[ZennとGithubを連携する方法](https://zenn.dev/eguchi244_dev/articles/github-zenn-linkage-20230501)が大変参考になりました。

# Repositoryを作る
自分のGithubアカウントから、Repositoryタブを押し、Zenn用のrepositoryを作成する。
repository名は"kawarin-zenn-contents"とした。
結果はこちら。
![](/images/article-1/スクリーンショット1.png)

# Zenn側からRepositoryの連携をする
Zennの自分のアカウントアイコンから"GitHubからのデプロイ"を押し、リポジトリの連携をしましょう。
Githubの認証画面が出たら、"Only select repositories"からZenn用のRepositoryを選択し認証してください。
認証が正常にできると、Zennからは以下のように見えると思います。
![](/images/article-1/スクリーンショット2.png)

# ローカルにGithubのRepositoryをクローンする
作成したRepositoryをローカルで扱えるようにするため、クローンしましょう。
![](/images/article-1/スクリーンショット3.png)
該当のrepositoryを押すと、上記のような画面があると思うので、そこから自分のgitURLをコピーし、以下のように実行してください。(自分のワークスペースで)
```
git clone https://github.com/************.git
```
すると実行したカレントディレクトリに作られます。

# ZennCliをインストールする
そもそもCliとは、Command Line Interfaceの略で、ターミナル上でコマンドを入力して色々できる。
今回はZennCliを使うことで、ローカル環境で記事作成やプレビューができるようになります。
公式サイトを見ればできると思います。
https://zenn.dev/zenn/articles/install-zenn-cli

前提としてNode.js14以上がマストらしい。
```
node -v
```
で確認してください。
その後、
```
npm init --yes # 初期化設定
npm install zenn-cli # zenn-cliを導入
npx zenn init # 諸々の設定(README.mdや.gitignoreなどが作られる)
```
をすればOK。
なお、ZennCliのアップデート方法は以下のような感じ。
```
npm install zenn-cli@latest
```
定期的にすると良いかも。

# 記事作成方法
```
npx zenn new:article --slug "ファイル名"
```
でarticles内にmarkdown形式のファイルが作成される。
ファイル名はユニーク意識で。
あとは作成されたファイルの中に、markdown形式で記事を書きましょう。
公式が出しているmarkdown記法一覧が参考になります。
https://zenn.dev/zenn/articles/markdown-guide

# 投稿方法



