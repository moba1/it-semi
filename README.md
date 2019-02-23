# 情報理論と符号理論
情報理論と符号理論のゼミで作ったレジュメをまとめておくリポジトリ.

# 用意するもの
* `latexmk`
* `luatex + lualatex`
* `ams`系
* `graphicx`
* `hyperref`
* `siunitx`
* `biblatex`+`biber`

# ディレクトリ構成
`src`の下に`章/回`ごとにまとめて下さい.
```
src
 |
 |- 1章
 |  |- 第1回
 |  |- 第2回
 |  |- ...
 |  ...
 |- 2章
 |  |- ...
 |  ...
 ...
```

# 書き方
分けられた章と回ごとに`template`ディレクトリの内容物を`.latexmkrc`も含めてコピーしてきてください.
```bash
$ mkdir -p (project root)/1/1 # 第1章の第1回用のディレクトリを作成
$ cd (project root)/1/1
$ cp (project root)/template/{*,.latexmkrc} . # 必要な諸々をコピー
$ vim 色々書く
```

参考文献は書いているTeXファイルと同じディレクトリに`reference.bib`を置いて, そこに書いて下さい.
許されている書式は[公式のドキュメント](http://mirrors.ctan.org/biblio/biber/documentation/biber.pdf)を参考にして下さい.

また, `\subject`の章番号は教科書のものに合わせて下さい.

# プロジェクト全体のビルド
作業中
