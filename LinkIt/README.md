# Description

エントリーデータ中の '[' と ']' で指示された URL文字列/画像ファイル/動画ファイルをリンクに置換します。

## URL 文字列

`[http://URL文字列 タイトル]` を

```
<a href='http://URL文字列' target='_blank'>タイトル</a>
```

に置換します。
タイトルが省略された場合は URL がそのまま使用されます。

## 画像ファイル

ファイルの拡張子が "jpg"、"jpeg"、"gif"、 "png" の場合画像ファイルと認識します。
ImageMagick を呼び出して 表示用のサムネイルファイルを自動で作成した上で、

`[画像ファイル キャプション]` を

```
<div class='snapimg'>
	<div class='images'>
		<a href='画像ファイル' rel='lightbox[エントリーデータ]'><img class='images' src='サムネイルファイル' alt='Image: 画像ファイル'></a>
	</div>
</div>
<br clear='all'>
<div class='caption'>キャプション</div>
```

に置換します。
キャプションが省略された場合はファイル名がそのまま使用されます。

## 動画ファイル

ファイルの拡張子が "mov" の場合動画ファイルと認識します。

`[動画ファイル 幅]` を

```
<div class='snapimg'>
	<div class='images'>
		<video controls width='幅'>
			< source src='動画ファイル'>
		</video>
	</div>
</div>
<br clear='all'>
```

に置換します。
幅が省略された場合は "width= " は出力されません。

# How to use

blosxom のプラグインディレクトリに格納して下さい。
画像ファイルの格納ディレクトリはデフォルトでは entries/images ですが、
変更する場合は `$imagedir` を変更して下さい。
