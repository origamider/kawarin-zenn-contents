---
title: "[MacOS/Apple Silicon] Docker環境構築方法"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Python,Docker]
published: true
---

# はじめに
Dockerを使用すると、自分の作成したWebアプリを丸ごとデプロイでき、どこでも誰でも同じ環境が使える点で良いらしい。
自分の作成したWebアプリを誰でも問題なく使えるようにするため、Dockerの導入を記事にする。

# 対象環境
MacOS。AppleSiliconM3。

# セットアップ方法
## step1(任意)
```code
softwareupdate --install-rosetta
```
現時点だと、特定のオプショナルコマンドを実行する際に、Rosetta 2が必要になるらしい。
Rosetta 2を使用することで、AppleSilicon搭載Macの環境で、Intel系プログラムを実行できるとのこと。
installは任意。

## step2
[release notes](https://docs.docker.com/desktop/release-notes/)から最新のDocker.dmgをダウンロード。

## step3
Docker.dmgをダブルクリックし、Docker iconをApplication フォルダに移す。
下記のように表示される。
![](/images/docker-setup-20260804/image1.png)

## step4
FinderからApplicationフォルダを開き、ダブルクリックする。

## step5
記載された指示に従って進める。簡単な承認と、アカウント作成が求められるはず。
できたら以下のような画面になる。
![](/images/docker-setup-20260804/image2.png)


## step6
```
docker run hello-world
```
正常にdockerがインストールされているかを確認。
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```
みたいなメッセージが出ればOK。

## 最後に
簡単にDockerのセットアップ方法を記載しました。誰かの役に立てれれば幸いです。

# 参考資料
https://docs.docker.com/desktop/setup/install/mac-install/
