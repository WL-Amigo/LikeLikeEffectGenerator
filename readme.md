 いいねボタン風エフェクトアニメジェネレータ
============================================

[Webアプリはこちらから (Web App is available here)](http://wl-amigo.github.io/LikeLikeEffectGenerator/)

(twitter's Like-like GIF animation generator)

Twitterのいいねボタンを押した時っぽいGIFアニメを、好きな画像から生成出来るWebアプリです。

This is a web application generates GIF animation like twitter's Like button, from any image you like.

(This documentation is written in Japanese. At the moment, There is no English version of documentation. Sorry.)



 動作環境
----------

本アプリは、以下の環境で動作することを確認しています。

 * FireFox (44.0.2) on Ubuntu 14.04 LTS
 * Google Chrome (49.0.2623.75 (64-bit)) on Ubuntu 14.04 LTS


 使い方
--------

1. 「ここに使いたい画像をドラッグ＆ドロップ！」と書かれた場所に、生成元の画像ファイルをドラッグ＆ドロップします。(もしくは、その場所をクリックするとファイル選択画面が開きます)
2. 「生成！」ボタンを押します。しばらく待つと、生成結果のGIFアニメが表示されます。
3. 「GIFアニメをダウンロード」ボタンを押すと、生成したGIFアニメをダウンロード出来ます(表示されているGIFアニメを 右クリック->名前を付けて保存 でも大丈夫です)。また、ページ下部にある「連番PNGをZIPでダウンロード」ボタンを押すと、生成されたGIFアニメの元になっている連番PNG(減色前)をZIPで固めたものをダウンロード出来ます(おまけでエフェクトのみのSVGファイルも入ってます)。


 設定可能なパラメータについて
------------------------------

ページ中央にある設定についての説明です。

### 「出現画像」

 * **出力サイズ(px)** : 生成するGIFアニメの1辺のピクセル数を指定します。大きいと生成にそれなりに時間がかかりますので注意して下さい。横にある「出力サイズを確認する」ボタンで、出力されるGIFの縦横サイズを確認出来ます(既にGIFアニメを生成していた場合、これを実行すると破棄されてしまいますのでご注意下さい)。
 * **画像を円形にトリミングする** : 入力された画像を先に円形にトリミング(切り抜き)してからGIFアニメを生成します。動作としては、まず入力画像の長辺を1辺の長さとする正方形の画像を生成し、その中央に入力画像を配置します(入力画像が正方形だった場合は何も起こりません)。その後、その画像いっぱいの正円で切り抜きを行います。
 * **押されてない時風の画像を付加する** : 入力画像を、透明度を維持したまま灰色に塗りつぶした画像を用意し、それをGIFアニメの最初の方に表示させます。この処理は画像の透明度に依存しますので、透明度が設定されていない画像ではうまく行きません(四角い灰色の画像が表示されてしまいます)。
 * **画像拡大時に補完しない** : 生成されるGIFのサイズが入力された画像サイズよりも大きい時に行われる入力画像の拡大出力において、補間を行わないようにします( = 最近傍法で拡大します)。ドット絵などを使用して生成する時にオススメです。(一部ブラウザは対応していない可能性があります。PC版FireFox, Chromeでは利用可能です)


### 「弾ける大きな丸のエフェクト」

いいねボタンを押した直後に出てくる「弾ける大きな丸」の色を指定できます。色は「出現時の色」->「消滅時の色」と線形に変化します。


### 「飛び散る小さい丸のエフェクト」

いいねボタンを押して、ハートマークと共に出てくる「飛び散る小さい丸」の色を指定できます。

 * **色の付け方** : 「虹色」か「指定色」が選べます。「虹色」の場合は、時計回りに虹色になるように自動で設定します。「指定色」の場合は、「色1(早く消える方)」と「色2(遅く消える方)」で指定した色を使用します。


### 「高度な設定」

あまり使われ無さそうな特殊な設定です。

 * **クオンタイズ品質** : GIFアニメの生成に使用している [jsgif](https://github.com/antimatter15/jsgif) 内で使用されている [NeuQuant](https://github.com/devongovett/neuquant) に与える quality 値です(1 〜 30)。小さいほどクオンタイズ(減色)の品質が上がります(元の画像との誤差平均が小さくなる)が、計算にものすごい時間が掛かります。通常は10で問題ありません。


 利用したライブラリ
--------------------

 * [jQuery](https://jquery.com/)
 * [canvg](https://github.com/gabelerner/canvg) : SVGからcanvasを得るために使用
 * [jsgif](https://github.com/antimatter15/jsgif) : 連番canvasからのGIFアニメの生成(但し、NeuQuantによるパレットの生成をグローバルパレットのみに限定するために改造したものを使用)
 * [filer](https://github.com/ebidel/filer.js/) : data-urlからのblobの取得(ユーティリティ部分のみを抜き出して使用)
 * [FileSaver](https://github.com/eligrey/FileSaver.js/) : blobのダウンロードボタンの実装に使用
 * [jszip](https://stuk.github.io/jszip/) : 連番canvasと連番SVGをzipに固めるのに使用
 * [Tiny Color Picker](http://www.dematte.at/tinyColorPicker/) : 色指定でカラーピッカーを利用可能にするために使用


 ライセンス
------------

本ソフトウェアは MITライセンス の下でライセンスされています。従って、**著作権表記とライセンス文をソフトウェア付近の参照可能な場所に設置する** こと(例えば、公開リポジトリの中など)を条件に、本ソフトウェアを元に新たなソフトウェアを作ることなどを全面的に認めます。

より詳細には、本リポジトリ内の LICENSE をご覧ください。
