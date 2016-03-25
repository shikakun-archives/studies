# フロントの奥深さに触れる〜Frontend Meetup Tokyo vol.1 (2016/03/24)

* [フロントの奥深さに触れる〜Frontend Meetup Tokyo vol.1 - connpass](http://frontend.connpass.com/event/28369/)

主催の日本経済新聞電子版の紹介からスタート、PV は月間 3 億とのこと。

## small画面でも、BIG画面でも、今すぐ使えるレスポンシブ活用術

[:memo: 資料](http://www.slideshare.net/ourmaninjapan/small-screenbigscreen)

ダニエル・デイビスさん @ourmaninjapan

* DuckDuckGo で働いてる。オフィスはなくて全員リモート。
* 最近 [ONEILL](http://us.oneill.com/) のサイトをこっそりレスポンシブデザインにした。
* コンバージョン・流通が上がった。収入は 40% あがった。
* KPI の内訳を見ると、モバイルが上がるのはあたりまえだけど、デスクトップも上がってた。
* デスクトップでもウィンドウ小さくしてインターネットしてる人がいる。モバイルにやさしくすると、デスクトップにもやさしくなる。
* モバイルは、iPhone のことじゃない。次のデバイスは予想できない。車の窓がデバイスになってたりするし、iPhone だって新しい機種がどんなデザインかわからない。モバイルがスマートフォンだとしても、スクリーンの大きさはばらばらだ。
* モバイルユーザーは、動いてるわけじゃない。布団で寝転がりながら Wi-Fi 繋いで見てるかもしれないし、パソコンでも外出先で 3G 回線にデザリングしてるかも、こんなときはパソコンだってモバイルとも言える。
* テレビは離れて見るものだから、文字の大きさがスマホやパソコンと違う。人間の指の大きさと、マウスカーソルの大きさ。矢印キーで操作してるかも。

#### レスポンシブ 10 TIPS

1. viewport を指定しろ
  * `device-width` にしよう。
  * `userscarable=no` はやめて。ピンチできなくなるだろが。
2. Media Query つかおう
  * ブレークポイントはコンテンツの大きさにあわせると吉。
3. コンテンツは 1 カラムで
4. 画像は `max-width: 100%;` 指定しとけ。
5. いらないコンテンツは隠せ
  * でも表示できるようにしとけ。
6. HTML5 で書け
  * とくに input type はメッチャ増えた (autofocus, email, number...) ので、最適なやつにしよう。
7. `:hover` あるところ `:focus` も指定しろ
8. エフェクトは JavaScript より CSS でやろう
  * ベンダープレフィックスつけるときは最後につけないやつ忘れずにね。
9. JavaScript もいいよ
  * おもしろ API もあるよ。バッテリー API、ネットワーク接続 API、光センサー API...
  * ただし、ネットワーク接続 API はローカルルータまでの話なので注意。
10. 画像もレスポンシブ化しよう
  * 祝 iOS 対応! これからは `picture` 要素の時代です。
  * [Chrome のサンプル](http://googlechrome.github.io/samples/picture-element/) がかわいい。

## Building a reusable web component system at the FT

[:memo: 資料](https://speakerdeck.com/triblondon/building-a-reusable-component-system-at-the-ft)

アンドリューさん @triblondon

顔がすごく小さい。 M&M のチョコを色で分けたいぐらい整理整頓好き。

FT のサイトはいろんなのがめっちゃある。その長い歴史のなかで、だんだん複雑になってきて、求められるものが変わってきた。

1. 多くのデバイスで閲覧できること。デバイスだけでなく、ウェブサービス（Flipboard や Facebook の Instant Article など）もある。
2. UX。
3. パフォーマンス。

たとえば FT には 4 つの画像ギャラリーが存在していたし、オーバーレイ（モーダルウィンドウ）を閉じるボタンの実装もいろんなのがあった。

この複雑さを、標準化することで解決したい。それを、コンポーネント単位でアプローチしていくことにした。

まず [ビルドプロセス](https://github.com/Financial-Times/origami-build-tools) を決める。それからコードルールを決めた。

あとは [Origami](http://origami.ft.com/) の説明。すごいなぁ…。

ビルドは 20〜30 秒かかる、でもキャッシュの仕組みがあるので問題ない。

WebComponents 大好きだからやりたいけど polyfill 必要なのでまだ時期尚早。ブラウザのシェアが 50% を超えたら導入して、残りの 50% のために polyfill を用意しようと思ってる。

## リンク

* [フロントの奥深さに触れる〜Frontend Meetup Tokyo vol.1 #frontendmt に行ってきたメモ - console.lealog();](http://lealog.hateblo.jp/entry/2016/03/24/194048)
