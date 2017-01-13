# Description

プログラムのソースコードや設定ファイルの内容、コマンドの実行例などを整形して表示するためのプラグインです。  
ソースコードとして表示する内容を `<source>` と `</source>` で、設定ファイルなど通常ファイルとして表示する内容を `<file>` と `</file>` で、
コマンドの実行例として表示する内容を `<code>` と `</code>` で指定すると、それぞれの内容に合わせて出力します。

## ソースコード
ソースコードの出力は `<source>` で指定します。  
ソースコード出力が指定された内容は _source_ class の _pre_ 要素として出力します。
行番号は _lineno_ class の _span_ 要素で、自動検出するコメント部分は _comment_ class の _span_ 要素で出力します。
ソースコード中の `<`、`>`、`&` はそれぞれ自動的に `&lt;`、`&gt;`、`&amp;` に置換され、タブは4個のスペースに置換されます。
コメントを検出するために `<source>` 指定に `lang='言語'` 型式で言語の種類を _c_、_sh_、_xml_、_exrc_ から指定する事が出来ます。
_lang_ 指定が省略された場合は _c_ が仮定されます。

`<source lang='sh'>` で指示された以下のコードを

```
<source lang='sh'>
    #!/bin/sh

    # for debug
    exec 2>&1

    # get script name
    myname=${0##/*}

    # print myname
    echo ${myname}

    exit 0
</source>
```
	
この様に変換して出力します。

```
<pre class='source'>
    <span class='lineno'>  1</span><span class='comment'>#!/bin/sh</span>
    <span class='lineno'>  2</span>
    <span class='lineno'>  3</span><span class='comment'># for debug</span>
    <span class='lineno'>  4</span>exec 2&gt;&amp;1
    <span class='lineno'>  5</span>
    <span class='lineno'>  6</span><span class='comment'># get script name</span>
    <span class='lineno'>  7</span>myname=${0##/*}
    <span class='lineno'>  8</span>
    <span class='lineno'>  9</span><span class='comment'># print myname</span>
    <span class='lineno'> 10</span>echo ${myname}
    <span class='lineno'> 11</span>
    <span class='lineno'> 12</span>exit 0
</pre>
```
	
## 通常ファイル
通常ファイルは行番号を出力しない事以外はソースコード出力と同じ内容で `<file>` で指定します。  
通常ファイル出力が指定された内容は _file_ class の _pre_ 要素として出力します。

`<file lang='sh'>` で指示された以下のデータを

```
<file lang='sh'>
    #!/bin/sh

    # for debug
    exec 2>&1

    # get script name
    myname=${0##/*}

    # print myname
    echo ${myname}

    exit 0
</file>
```
	
この様に変換して出力します。

```
<pre class='file'>
    <span class='comment'>#!/bin/sh</span>
    
    <span class='comment'># for debug</span>
    exec 2&gt;&amp;1
    
    <span class='comment'># get script name</span>
    myname=${0##/*}
    
    <span class='comment'># print myname</span>
    echo ${myname}
    
    exit 0
</pre>
```
	
## コマンドライン
コマンド実行例の出力は `<code>` で指定します。  
コマンド実行例出力が指定された内容は _code_ class の _pre_ 要素として出力します。
行頭の `'# '` と `'$ ' をプロンプトとして、プロンプトが先行しない行をコマンドの出力と認識して _comment_ class の _span_ 要素で出力しますが、
`<code>` 指定に `prompt='プロンプト'` 型式で追加のプロンプトを指定す事もできます。
コマンド実行例中の `<`、`>`、`&` はそれぞれ自動的に `&lt;`、`&gt;`、`&amp;` に置換され、タブは4個のスペースに置換されます。

`<code prompt='\(gdb\)'>` で指示された以下のコマンド実行例を

```
<code prompt='\(gdb\)'>
    $ gdb -q
    (gdb) p/x 10
    $1 = 0xa
    (gdb) p/x 20
    $2 = 0x14
    (gdb) p/x $1 + $2
    $3 = 0x1e
    (gdb) p $2 - $1 / 3
    $4 = 17
    (gdb) p ($2 - $1) / 3
    $5 = 3
    (gdb) q
</code>
```
	
この様に変換して出力します。

```
<pre class='code'>
    <span class='comment'>$</span> gdb -q
    <span class='comment'>(gdb)</span> p/x 10
    <span class='comment'>$1 = 0xa</span>
    <span class='comment'>(gdb)</span> p/x 20
    <span class='comment'>$2 = 0x14</span>
    <span class='comment'>(gdb)</span> p/x $1 + $2
    <span class='comment'>$3 = 0x1e</span>
    <span class='comment'>(gdb)</span> p $2 - $1 / 3
    <span class='comment'>$4 = 17</span>
    <span class='comment'>(gdb)</span> p ($2 - $1) / 3
    <span class='comment'>$5 = 3</span>
    <span class='comment'>(gdb)</span> q
</pre>
```
	
インクルード機能は指定したファイルを読み込む機能で、既存のソースファイルを表示する際などに便利です。

`<file lang='c' include='ファイル>` で指示された場合

```
<file lang='sh' include='ファイル'>
    追加行
       :
</file>
```
	
指定されたファイルを読み込みます。

```
<pre class='file'>
    ファイルの内容
       :
    ファイルの内容
    追加行
       :
</pre>
```
	
# How to use

blosxom のプラグインディレクトリに格納して下さい。
ソースコードを `<source>` タグ、通常ファイルを `<file>` タグ、コマンドラインを `<code>` タグで指定すれば変換されます。
