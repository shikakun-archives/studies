## Chapter1

### reset.cssとnormalize.css

歴史的には、reset.cssが生まれてみんな使っていたが、ちょっと過激すぎないか (*1) ということで、normalize.cssが生まれた。

最近のCSSフレームワークはまず、normalize.cssを読みこんで、そこから組み立てるものが多いように感じる (*2) 。

> ###### *1
>
> 全称クラスタ (`*`) にスタイルを指定するとすべての html 要素に適用されるので、ちょっとヘルシーじゃないんじゃないの、という意味です。

> ###### *2
>
> 例えば、 CSS フレームワークの Twitter Bootstrap では 2011 年にリリースされていた v1.4.0 では [Reset CSS](https://github.com/twbs/bootstrap/blob/f92759b36db43e782e4235f1f214ac5851383f9b/lib/reset.less) を利用していましたが、最新の v3.3.6 では [normalize.css](https://github.com/twbs/bootstrap/blob/81df608a40bf0629a1dc08e584849bb1e43e0b7a/less/normalize.less) を利用しています。
>
> Reset CSS と normalize.css は以下の URL からダウンロードできます。圧縮されていない normalize.css を読むと、どういったブラウザ間の差異をなくすためにこのスタイルシートを指定しているのか、という理由が書いてあるのでおもしろいです。
>
> * reset.css
>   * [CSS Tools: Reset CSS](http://meyerweb.com/eric/tools/css/reset/)
> * normalize.css
>   * [Normalize.css: Make browsers render all elements more consistently.](https://necolas.github.io/normalize.css/)

## Chapter 2

### 横幅はどう指定するのがいいのか。

headerやfooterをパーセンテージ、メインやサイドバーをpxで指定するのってなんかもやもやするけど、そういうもの。

それはどういうデザインにするかによるんじゃないだろうか。

パーセンテージで指定することってあんまりないかも。たとえば中にバナーなんかがはいるときには、パーセンテージ指定しているとどういう大きさのものを作ればいいかわからなくなるよね。また、ブラウザの大きさってだいたい決まってるので、それにあわせて幅を決めることが多いように感じる。

### metaタグの順番とOGPタグについて

metaの順番って本当に意味がある？ない？

OGPタグは、SNSサイトがHTMLの先頭nバイトしかみないようなケースもあるようだ。なので、OGPはなるべく上にしたりしてる。

OGPタグはメディア側にキャッシュされてしまう。たとえば、下書き状態のものをFacebookに投稿してしまったりすると、一回facebook側のキャシュ

### main要素使ってる？

どこまでmainなのか難しい。sidebarはmainに入るのか？sidebarの中のコンテンツに依存する？

検索エンジンのクローラーが、main要素があればそれをコンテンツの内容の判断に使っているかもしれないがわからない。microformatsとGoogle気持ちを伝えるという方法もあったよね。

### marginプロパティの順番の覚え方

先頭が上でそこから時計回りと覚えればよい。

### clearfix

afterの疑似要素でclearfixするのはちょっと古い。今の主流は `overflow: hidden` bourbon ではとても議論されている (*3)

clearfixハックは時代によって変わってきているので、時代にあわせられるようにしておくのがよい。たとえば、SCSSの場合はmixinにしておいていつでも変えられるようにしておくのがよいのではないかと思っている。

なぜ `overflow: hidden` でclearfixできるのか？ブラウザがそういう風になっているから？

`overflow: hidden` でやる場合は、likeJavaScriptで要素が追加されたときに、親要素の

> ###### *3
>
> うろおぼえの知識で適当に話してしまいましたが、 Bourbon のコードを見ると `&::after` の疑似要素で実装されていました。あれ…？
>
> * https://github.com/thoughtbot/bourbon/blob/master/core/bourbon/addons/_clearfix.scss
>
> 2013年の記事ですが、 clearfix の仕組みや歴史については以下のページで大変詳しく解説されています。
>
> * [floatを解除する手法のclearfix と 次世代のレイアウトの話｜Web Design KOJIKA17](http://kojika17.com/2013/06/clearfix-2013.html)
>
> この記事を読むと、もともと clear プロパティを指定したからっぽの要素を最後に追加することで clearfix を実現していたのを、疑似要素で代用するようになったということでした。
>
> また、`overflow: hidden;` を指定するとなぜ clearfix 相当のことができるのかというと、overflow プロパティに visible 以外の値が指定されていると、中にある float プロパティが指定されている要素の高さも算出してくれるようになるから、ということでした（結局ブラウザがそういう風になっているから、という理由ではありますが…）。

### overflowプロパティってそもそもなんなの？

コンテンツが枠からはみ出したときにどう表示されるかを指定する。以下の4つがある。

- hidden: 隠す
- auto: ブラウザ依存
- scroll: スクロールバーがでる
- visible: はみでてもいいから見せる

visibleの場合は、枠が拡張されるわけではなくて中身がはみ出るだけ。ただ、古いIEでは枠が拡張してしまうという問題があった。

### box-sizingについて

「HTMLはアンパン」だという説明を聞いたことがある。

餡がコンテンツ、パンがpadding、皮がborder。アンパンとアンパンの間がmargin。

`box-sizing: border-box` を指定すると、widthとheightがアンパンの皮までになる。`border-box` じゃない場合は、餡の部分だけがwidthとheightになる。IE8から使えるが、Androidの2系はベンダープレフィックスがいる。(ベンダープレフィックスってわかるかな？)

`*` に付けるのはよくないんじゃないだろうか。レイアウトが崩れたときになぜ崩れたのかがわかりにくいし、box-sizing の意味を理解して、必要な要素につけてほしい。

### rem

まず、こういう解釈でよいかという話。

以前、デバイス(スマホ、タブレット、PC)でフォントサイズは変えていい(変えたほうがいい)んじゃないかという議論があった。

デバイスによってベースのフォントサイズを絶対指定して、各要素やセレクタをremで指定する、という考えでいいのか？

それに答えるために、まずはremが生まれた背景をまず説明する。

アクセシビリティの観点からフォントサイズはパーセンテージで指定しようブームがあった。が、パーセンテージ指定は親要素から相対的な大きさなので、同じパーセンテージでも、親要素によってフォントの大きさが変わってしまう問題があった。

html要素のフォントサイズをパーセンテージで指定して、それ以外をremで指定するようにすればよいのではという流れになっている。

rem指定は、IE9と10だとショートハンドプロパティだと効かないけど、それ以外はいけるので今からやるならremでいい。

### アクセスビリティとブラウザのズーム機能

最近のブラウザは、ズーム機能をフォントサイズを変えるのではなく画面自体の拡大で実現していたりする。そうすると、pxが指定されていてもズームができる。

フォントサイズが大きくなっても崩れないように確認をしているか？

していないことが多い。ただ、日常的にフォントサイズを変更するような人がメンバーにいると、その人が勝手に確認していたりする。

上記のようにブラウザの拡大機能がどう実現されているかで、そもそも確認が必要なのか？という話もある。

### remをフォントサイズ以外で使うことの是非

remをheightやwidthで使うのはOKなのか？

文字を対象にしたスタイルなのであれば指定していいのでは。たとえば3文字分の大きさとか。

モダンなCSSフレームワークは全部remだったりするけど、まだremでレイアウトした経験がないので、本当にそれでいいかは自身がない。

## Chapter 2

### url('') のシングルクォーテーションについて

Googleのスタイルガイドでは省略せよと言っている (*4) 。

Webデザインの文脈では、CSSは人間が読むんだから、チームで読みやすいほうがいい。

最適化はminifyでやりましょう。

> ###### *4
>
> Google が「省略せよと言っている」ところは、ここです。
>
> * [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.xml?showone=CSS_Quotation_Marks#CSS_Quotation_Marks)
>
> 日本語訳もされています。2012年? の話ですが、参考になるかもしれません！
>
> * [「Google HTML/CSS Style Guide」を適当に和訳してみた | REFLECTDESIGN](http://re-dzine.net/2012/05/google-htmlcss-style-guide/)

### background-attachment

[background-attachment－スタイルシートリファレンス](http://www.htmq.com/style/background-attachment.shtml) これの下にでてくる犬。

### box-shadow

影は画像で切り出すのかCSSで実現するのか？

IE8以下に対応しないといけない場合は画像にしないといけない、そうじゃなければCSSのほうがよいと思う。微妙な色見を変えたり、深さを変えたり簡単なので。角丸も同様。

### logoはbackground-imageにするべきか

10年前のインターネットでは文字を画像にしたいときに、Googleが画像だと読んでくれないんじゃないかという不安な人がいて、CSSで9999px横に飛ばすというテクニックが横行していた。ただ、これはよく悪用されていたのでGoogle八分されていった。それだけではなく、9999とばすのはパフォーマンス的によくないのではないかという問題もあるので、最近は100%とばすのが主流。

著者は、やましい気持ちがないならやってもいいんじゃないか？というとのこと。

shikakun的には、image要素とaltでいいんじゃないかと思う。

あまり適切じゃなさそうなbackground-image、インターネットにはよくあるんだけど、なぜみんなやるのか？ (*5)

- なにかに恐れている
- ちょっとテクニックを使って仕事した気になる

ということじゃないだろうか。

> ###### *5
>
> この話のあと、そういえば CSS スプライトとかの理由もあるな… と思いました。
>
> アイコンフォントや HTTP2？の時代？では、こういうテクニックはいらなくなるのかもしれません？

### マージンの相殺はなぜそういう仕組みなのか

HTMLは文章のマークアップなのだ。たとえば、連続したpの間にmarginが2倍空くのはおかしいと思う。そういうところからマージンの相殺があるのでは。

マージンの相殺があるからpaddingでマージンをとりたがる人がいるが、それもありだと思う。

### 連続した要素の間をいいかんじにあける

その昔、last-childが使えなかったときは困っていたんだが、2016年、last-childセレクタがあるのでそれでいいと思う。

### activeというクラス名について

これは2年前の話である (*6) 。

`nav-item__active` とか `nav-item--active` のような名前にして、対象と状態を区別(?組合せる?)するほうがよいとされている。メンテナンスもしやすい。(ヒント: BEM)

> ###### *6
>
> 個人の主観によるものです。ただ、`.active` といった名前をカジュアルに指定していると、どこかで汚染された値がガンガン上書きされて表示が崩れるといった事故がなんども起こっているので、僕は書きません。
>
> BEM (MindBEMding) については、過去に勉強会を開催したときの資料があるので、よろしければご覧ください！
>
> * [100年後も崩れないCSS勉強会 · 第2回「コンポーネント」](http://pepabo.github.io/css/component/)

### inline-block

実は世界はアンパンだけではなかったのだ。インライン要素にはパンがないのだ。

インラインとして横に並べることも簡単だし、ブロックのようにpaddingとmarginもある、そういうのがinline-block。ただ、これによって世界は壊されてしまった。

たとえば、本書のような使い方をすると、改行がテキストをしてあつかわれてしまうので、微妙に空白があいたりする。そのハックとして、親要素のfont-sizeを0にするハックがある。

じゃあなんでfloatにしないのか？中央によせるのが難しいのだ。これをしたいときに、inline-blockを使ってしまう。

ただ、2016年にはFlexboxがある！あるにはあるが、今もまともに使える状態ではな…2017年はFlexbox元年である。

スマホオンリーであれば、Flexboxが十分実用に耐えうる。

### 詳細度について

[100年後も崩れないCSS勉強会 · 第1回「詳細度」](http://pepabo.github.io/css/specificity/) を読めばすべてがわかる。

全部クラスにするのか、というのはチームで合意をとればどっちでもいいのでは。

## 角丸

IE8のない今、2016年はCSSで。

## transition

transitionはIE10から。ふわっとしてほしいと思ってIE8や9を使ってる人なんているのだろうか。なので気にせずCSSでやっちゃう。

どうしてもふわっとしたいときは、jQueryでやるが、うまく作らないとホバーを高速に繰替えすとバグることがあるので注意。

## 宿題

- インライン要素にpaddingはあるのか？ (*7)
- background-imageを使いたくなる具体的なユースケースは？

> ###### *7
>
> inline 要素でも padding や margin を指定すると反映されます。ただし、上下の指定など一部のプロパティは無視される場合もあります。個人的には padding や margin を指定するときは、block または inline-block 要素にするようにしています（inline 要素、つまり文字に、ここで話しているパンにあたるものがあるなんて気持ち悪いし…）。でも、ぜひいろいろ試してみてください！