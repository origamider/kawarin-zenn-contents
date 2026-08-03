---
title: "[Python] Anacondaチートシート 〜よく使うコマンド集〜"
emoji: "👌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Anaconda,チートシート,Python]
published: true
---

# はじめに
AnacondaというPythonのパッケージ管理や仮想環境作成ができるサービスを使う機会があったため、公式ドキュメントベースでよく使うコマンド集をまとめました。

# チートシート
|コマンド|説明|
|-|-|
|conda info -e|全ての環境を表示。eはenvironmentのe。|
|conda create --name [仮想環境名]|指定した名前で仮想環境を作成|
|conda activate [仮想環境名]|指定した仮想環境をONにする|
|conda deactivate|仮想環境OFF|
|conda --version|condaのversion表示|
|conda update --name base conda|標準環境下のcondaを最新にする|
|conda list|現在いる環境のインストール済みのpackageを表示|
|conda list [パッケージ名]|現在いる環境の指定したパッケージ情報を表示|
|conda update --all|現在いる環境のインストール済みのpackageを全て更新|
|conda install [パッケージ名]|現在いる環境で指定したパッケージをインストール|
|conda uninstall [パッケージ名]|現在いる環境で指定したパッケージをアンインストール|
|conda remove --name [仮想環境名] --all|指定した仮想環境を削除する|

# さいごに
適宜こちらのチートシートを参考にしながらanacondaの操作に慣れればいいなと思っています。

# 参考資料
https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html
