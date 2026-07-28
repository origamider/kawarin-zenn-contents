---
title: "WandBを初心者が１から触ってみた"
emoji: "🐝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [wandb,Python,AI, ]
published: true
---
# はじめに
機械学習の実験管理やパフォーマンス可視化などでWandBが使われるらしく、ちょこちょこみたことがあったので、
今回はWandBで実際に可視化をしてみました。

# 対象者
- WandBを初めて触る人
- WandBの公式QuickStartから始める方

# そもそもWandBとは
Weights & Biases。機械学習で得た結果の可視化や、プロジェクトの管理などができるMLOpsチックなツールらしい。
![](/images/wandb-basic-20260728/image3.png)

# セットアップ方法
公式が出しているQuickstartをベースにセットアップ方法を説明します。([W&B Quickstart](https://docs.wandb.ai/models/quickstart))
## step1
WandB内でアカウントを作成する。
![](/images/wandb-basic-20260728/image1.png)
## step2
ユーザーアイコン->User Settings->API keysから、新しくAPI Keyの作成をする。
:::message alert
API Keyを作成後、一度だけAPI Keyが表示されます。ここでコピーしどこかしらに保存してください。(.envファイルやその他サービス)
画面を閉じるとコピーできなくなります。
:::
## step3
テスト用ディレクトリを作成する。(フォルダ名:wandb-test)

## step4
仮想環境venvを導入する。
projectごとにライブラリ、パッケージ管理は独立にしたいので、導入します。でも簡単なので安心を。
python3がなければインストールしてください。

```
python3 --version # python3があるか確認
python3 -m venv venv # venvという名前で仮想環境作成
source venv/bin/activate # 仮想環境ON!
```
なお、詳しいvenvの説明については[venv: Python 仮想環境管理](https://qiita.com/fiftystorm36/items/b2fd47cf32c7694adc2e)などを参考にしてね。

## step5
準備は完了です。あとは、[公式が出しているコード](https://docs.wandb.ai/models/quickstart)を参考にコードを書いてください。
(追記:おそらくですが、[こちら](https://docs.wandb.ai/models/quickstart)のコードですが、本来epochを使用すべきところがconfig['epochs']になってしまっています。これでも動きますが、スコアが上昇し、損失が下がるようなグラフをちゃんと作成したいのであれば、直した方がいいです。)
以下は修正版です。
```python
import wandb
import random

wandb.login()
project = "wandb-test"

config = {
    'epochs' : 10,
    'lr' : 0.01
}
with wandb.init(project=project,config=config) as run:
    offset = random.random() / 5
    print(f"lr = {config['lr']}")
    
    for epoch in range(2,config['epochs']):
        acc = 1 - 2**-epoch - random.random() / epoch - offset
        loss = 2**-epoch + random.random() / epoch + offset
        print(f"epoch={epoch}, accuracy={acc}, loss={loss}")
        run.log({"accuracy": acc, "loss": loss})

print(random.random())
```
実行後、[こちら](https://wandb.ai/home)で、自分が作成したProjectを選択すると、以下のようなダッシュボードが開きます。
![](/images/wandb-basic-20260728/image2.png)
こちらは、何回か実行した結果です。
損失および精度の可視化を勝手にやってくれています。
これを使えば、matplotlib.pyplotを使用せずとも、可視化が簡単にできるのかもしれません。

# 最後に
機械学習を今まで触ってきましたが、WandBのようなログ可視化・実験管理ツールを触ったことがなかったので、今回触れて良かったです。
なお、WandBは今回のような可視化以外にも、
LLM Applicationの評価やハイパーパラメータの最適化などもできるらしく、いつか触ってみたいと思いました！

# 参考資料
[W&B Quickstart](https://docs.wandb.ai/models/quickstart)