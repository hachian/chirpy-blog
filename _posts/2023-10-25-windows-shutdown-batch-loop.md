---
title: Windowsをバッチからシャットダウンしようとすると無限ループする
date: 2023-10-25 07:42:35
categories: [life]
tags: [windows, tips]
math: false
author: hachian
---

## 現象

下図のようにシャットダウンコマンドが無限ループします。

![Alt text](/assets/img/2023-10-25-windows-shutdown-batch-loop/image.png)

以下の手順で再現することができます。

1. メモ帳を開く
1. `shutdown /s /t 0`と書いて保存
1. `shutdown.bat`という名前で保存
1. そのファイルをダブルクリックする

## 解決方法

以下の解決方法のどちらかでOKです。

### ファイル名を変える

`shutdown.bat`というファイル名を例えば`終了.bat`とすればよいです。

### コマンドを変える

どうしても名前を変えたくない場合は、終了コマンドを`shutdown /s /t 0`を`shutdown.exe /s /t 0`とすればよいです。

## 何が起こっていたのか

`shutdown`コマンドと`shutdown.bat`というファイル名が競合していることが原因でした。

コマンドの優先順位は、(実際にはほかにもルールはあると思いますが)*同一フォルダのバッチを探す*→*システムのコマンドを探す*となっています。`shutdown`コマンドが呼ばれたとき、Windowsを終了するコマンドを探索する前に、同ディレクトリにある`shutdown.bat`が呼ばれて無限ループしていることが原因でした。