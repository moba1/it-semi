# 情報理論と符号理論
情報理論と符号理論のゼミで作ったレジュメをまとめておくリポジトリ.

## 運用上の注意点
`master`にプッシュする際は`/doc`ディレクトリが含まれていないように。

PRがでると、Travis CIが起動して、ビルド、gh-pagesブランチにプッシュするまで自動でやってくれる。
CIでビルドされた資料を見たけば、[ここ](https://moba1.github.io/it-semi)に接続すると見られる。

## ディレクトリ構成
`src`ディレクトリの下に`n`(第`n`回の意味)というディレクトリがあって、そこの下に各回の資料がビルドのための`Makefile`とともに置いてある。
```
src/
 ├─ 1/
 │  ├─ hoge.pdf
 │  ├─ hoge.tex
 │  ├─ hoge.bib
 │  └─ Makefile
 │
 ├─ 2/
 │  ├─ fuga.pdf
 │  ├─ fuga.tex
 │  └─ Makefile
 ┆
```

## `template`の中身
1. `Makefile`
   * `TEX_COMPILER`: TeXコンパイラを指定する(デフォルト`uplatex`)
   * `DVI_COMPILER`: DVIファイルのコンパイラを指定する(デフォルト`dvipdfmx`)
   * `MAIN_TEX_FILE`: コンパイルする起点となるTeXファイルのパス(デフォルト`main.tex`)
   * `MAX_REPEAT`: `latexmkrc`を利用しない場合に使用される。この回数分だけコンパイルする(デフォルトは3回)
   * もし、LuaLaTeXやXeLaTeXなどの直接PDFを吐くLaTeXエンジンを`latexmk`で利用する場合は、各回の資料ごとの`Makefile`の`latexmk`を利用している部分を
      ```bash
      # -pdflatex にエンジン名を指定する
      latexmk -pdflatex=lualatex -pdf $(MANI_TEX_FILE);
      ```
     と変更すればOK
1. `main.tex`: コンパイルする際の起点となるTeXファイル

## 資料の用意方法
```bash
$ cd クローン先
$ bin/create.bash 回数 # 回数には自分の担当した輪読第n回の`n`を指定。たとえば`1`とか
```
これで、`template`ディレクトリから`src/n`へ必要なファイルが移動される。
もし、`latexmkr`を利用するのであれば、`create.bash`に`-l`オプションを渡せばいい:
```bash
$ bin/create.bash -l 回数
```

## PRの出し方
1. このリポジトリをフォークしてクローン
1. 資料を書く
1. `git checkout -b '適当なブランチ名'`
1. `git add`する
1. `git push origin HEAD`

## 全資料のビルド方法
全ての資料をビルドする場合は
```bash
$ cd クローン先
$ make
```
でOK。
これで`プロジェクトルート/doc`へビルド済みのPDFが用意される。

逆に言えば、ここに書いた`Makefile`を利用したシステムに沿わないと、全資料をビルドできなくなる。
全資料をビルドできるようにするには、次の条件を満たす必要がある:

* 資料をビルドするディレクトリ(例えば`src/1`など)には常に`Makefile`を置いておく
* `doc`へPDFを移動するようにする
* 各資料があるディレクトリ(`src`直下の`src/1`など)におく`Makefile`は`make clean`できるようにする

## 全資料のクリーンアップ
次のコマンドで生成物、中間ファイルを削除できる。
```bash
$ cd クローン先
$ make clean
```
