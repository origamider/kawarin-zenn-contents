---
title: "[Python]pipとuvの違いってなに"
emoji: "🐕"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [pip,uv,Python]
published: true
---

# はじめに
よくPythonを触っていると、pip install や uv run などを見かけます。
結局、pipとuvの違いをちゃんと説明できるようにしたいと思い、記事にしました。

# uvとpipの違い
pipはPython製のPythonパッケージマネージャーで、パッケージのversion管理をメインにできるもの。
uvはRust製のPythonパッケージマネージャーで、パッケージのversion管理の他に仮想環境も作ることができるもの。
uvはpipよりも高速にインストールできるらしい。Rust特有の並列処理能力を活かしているとのこと。

具体的なコマンドイメージ
```python
pip install numpy
```
pipを使用し、numpyをインストールしているシーン。
ただ、仮想環境構築はpipでは提供されていない。
```Python
python -m venv [環境名] # 仮想環境作成
source [環境名]/bin/activate # 仮想環境ON
deactivate # 仮想環境Off
```
上記のような形で仮想環境は別途作成する形になっている。

ただ、uvは仮想環境作成も提供されているらしい。
```python
uv venv
```
これを実行することで、.venvフォルダが作成される。これは仮想環境venv。
```python
uv pip install numpy
```
実行するとvenv仮想環境内にnumpyがインストールされる。
```python
uv init
```
をすると、プロジェクトが作成される。uvを使ったPythonの管理がしやすい環境のProjectってこと。
以下のような構成で作成される。
![](/images/pip-uv-basic-20260807/image1.png)
```python
uv add numpy
```
を実行すると、pyproject.tomlというPythonパッケージ管理系ファイルのdependencies(依存系)にnumpyが追加されるよ。
```python
uv sync
```
これを実行すると、.venvフォルダとpyproject.tomlに書かれている依存関係を同期させる。

従来だと、他人のgithub上のprojectをローカルで実行する際に、
```python
pip install -r requirements.txt
```
をしていたけど、それが、uv syncで正確に行けるってことだね。

# 最後に
uvとpipの違いがある程度わかりました。uvを使えば、pipとは違って仮想環境作成およびパッケージの高速インストールの両方ができるので、uvを使えば良さそうですね。

# 参考資料
https://paiza.jp/works/knowledge/article-python-uv-kn#h1e3f7b0f00


