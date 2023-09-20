---
title: Quarto環境構築
date: 2023-09-20 21:59:38
categories: [tech]
tags: [quarto, document, conda, vscode, python, jupyter]
math: false
author: hachian
---

[Quarto](https://quarto.org/)を使えば、`Python`と`Markdown`で科学技術文章を作成することができます。

この記事では、Quartoの環境構築方法について説明します。Windowsにて、*vscode*と*conda*コマンド(Anaconda, Miniconda環境)を使った構築方法を説明します。

通常のインストール方法は[公式ページ](https://quarto.org/)をご覧ください。

## Quarto CLIのインストール

[Quarto CLI](https://quarto.org/docs/get-started/)をインストールします。

インストールが完了すると、`quarto`コマンドが使用可能になります。`quarto -v`でバージョンを確認すると以下の画像のようになります。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image.png)

## Visual Studio Codeの拡張機能をインストール

Visual Studio Codeを起動し、左側の拡張機能を選択もしくはショートカットキー<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd>を押下します。

検索欄にて*quarto*などと検索し、Quarto拡張機能を探します。インストールボタンをクリックしてインストールします。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-1.png)

## condaコマンドを用いたQuartoの環境構築

[公式ページ](https://quarto.org/docs/projects/virtual-environments.html#using-conda)のUsing condaを参考にしています。

まず、Quartoプロジェクトを作成するフォルダを作ります。私は`C:\00_work\python\quarto`というフォルダを作成し、そこで作業しました。

`Anaconda Prompt`を立ち上げ、以下のコマンドを入力し、先ほど作成したフォルダに移動します。

```bash
cd C:\00_work\python\quarto
```

下記画像のように、<kbd>Win</kbd>を押し、`Anaconda`などと検索すると`Anaconda Prompt`を見つけることができるでしょう。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-2.png)

以下のコマンドで新規の仮想環境を作ります。

```bash
conda create -p env python
```

`-p`オプションはあまり見かけませんが、仮想環境フォルダのパスを指定するオプションです。この場合、`C:\00_work\python\quarto\env`フォルダに仮想環境が作成されます。作成時のスクリーンショットは以下の通りです。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-3.png)

> 普段、condaコマンドで仮想環境を作成する場合は`-n`オプションを用いて`conda create -n 【環境名】 python`のようにします。この場合、`C:\Users\【ユーザ名】\Ainiconda3\envs\【環境名】`に仮想環境が作成されますが、今回はQuartoで使用する都合上、ワークスペース内に仮想環境を作成しています。
{: .prompt-tip }

### 仮想環境に必要なライブラリをインストール

仮想環境ができたら、アクティベートします。例えば、以下のコマンドを実行するように促されると思います。仮想環境ができた旨のメッセージの最後のほうに記載されています。

```bash
conda activate C:\00_work\python\quarto\env
```

アクティベートが完了すると、Anaconda Promptの`(base)`となっていた部分が`(env)`に変わると思います。私の環境で試した画像は以下です。(見た目をカスタマイズしているため、一致するわけではないことをご承知ください。)

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-4.png)

続いて、[公式の指示通り](https://quarto.org/docs/projects/virtual-environments.html#using-conda)、必要なライブラリをインストールします。`jupyter`, `pandas`, `matplotlib`が必要なようです。以下のコマンドでインストールできます。

```bash
conda install jupyter pandas matplotlib 
```

Anaconda Promptはいったん閉じてしまって大丈夫です。

## Visual Studio Codeの設定

Visual Studio Codeを起動し、`C:\00_work\python\quarto`をワークスペースとします。右クリックコンテキストメニューに登録してあると、添付画像のようにvscodeを開くことができるので楽です。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-6.png)

<kbd>F1</kbd>もしくは<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>を押下し、コマンドパレットを開きます。`python interpreter`などと検索し、*Python: インタープリターを選択*をクリックします。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-5.png)

インタープリターとして、先ほど作成した環境を選びます。この記事の通りに作成している場合、`.\env\python.exe`というパスになっています。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-7.png)

設定できたら[Quarto公式のテスト](https://quarto.org/docs/get-started/hello/vscode.html#render-and-preview)を実行してみます。`hello.qmd`という名前の新しいファイルを作成し、リンクからコピーしたテスト用のコードを貼り付けます。

再びコマンドパレットを開き、`render`などと検索し、`Quarto: Render`を選択します。

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-8.png)

![Alt text](/assets/img/2023-09-20-quarto-vscode-conda/image-9.png)

上記画像のようにエディタの右側にQuartoのプレビューが表示されれば環境構築は完了となります。

### ModuleNotFoundErrorが出る場合

`Quarto: Render`した際に、`ModuleNotFoundError`が出る場合があります。一番なりやすいエラーは以下だと思います。

```bash
ModuleNotFoundError: No module named 'nbformat'
```

このエラーが出た場合、エラーメッセージの終わりにある通り、`activate`がちゃんとできていない可能性が高いです。エラーメッセージの当該部分を引用します。

> There is an unactivated Python environment in env. Did you forget to activate it?

このエラーに遭遇したら、この記事の通り設定できているか、もう一度インタープリターの設定を確認して見てください。場合によってはVisual Studio Codeの再読み込みや再起動、PC自体の再起動が必要かもしれません。