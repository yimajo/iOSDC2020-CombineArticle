# 図解で整理するCombineフレームワークの全体像

<img src="https://github.com/yimajo/iOSDC2020-CombineArticle/blob/master/combine_overview.svg">

## はじめに

AppleはWWDC19にてCombineフレームワークを発表しました。このフレームワークによりリアクティブプログラミングおよび宣言的なコーディングが可能になります。本記事ではそのかんたんな概要とCombineの全体像を示します。

## リアクティブプログラミングって？

まずはリアクティブプログラミングの説明として、コード1に手続き型のコードがリアルタイムに変更される値に対応していない例を示します。
次のコード2ではリアクティブプログラミングによりリアルタイムに変更される値に対応している例です。
iOSアプリ開発ではそもそもリアルタイムに値の変化を検知する仕組みとして、従来から様々なイベント通知手段が用意されてはいます。しかしこれを他プラットフォームで利用されるような一般化されたリアクティブプログラミング仕様であるReactive Streamsをベースとした公式フレームワークで行えることがCombineのメリットなわけです。

## Publisher

要素をイベントとして通知する概念を示したものがPublisherです。このPublisherという名前はReactiveStreams仕様そのままであり、その仕様に沿っていないRxSwiftではObservableに相当します。

## Subscriber

Publisherのイベントを処理する役割としてプロトコルとして用意されています。直接Subscriberを利用するよりも、Publisherのプロトコルエクステンションとしてイベントを処理するsinkメソッドなどが用意されており、Subscriberを間接的に利用することが多いはずです。このSubscriberという名前についてもReactiveStreams仕様をベースとしています。RxSwiftには同様の概念としてObserverが存在します。

## Subscription 

SubscriberからPublisherへ通知を制御するために存在しており、ReactiveStreams仕様にあるバックプレッシャーを実現することができます。RxSwiftには存在しません。

## Publishers

Mapなどのオペレーターが利用する様々な型がPublishersとして列挙されています。Publisherに準拠しており、オペレーターはストリームを処理し列挙されているそれぞれの型へ変換します。

## Subject

外部からイベントを発生させられる自由度が高いPublisherです。2つのSubjectが用意されておりCurrentValueSubjectは初期値を持ちます。

## Subscribers

Subscriberとして機能する型の名前空間として用意されています。

## おわりに

SwiftUIが開発の全盛となっても、@PublishedなどのプロパティラッパーによりCombineを意識しない方法が用意されているため、Combineをなるべく使わないという手もあります。しかし、アプリの仕様は日々複雑になるものであり、そういった際にCombineをより深く知りたくなった際、本記事が役に立つ日があるかもしれません。

## 参考

- tobi462
   - https://twitter.com/tobi462/status/1272755992447442945
- Getting Started with Combine - Shai Mishali - App Builders 2020
  - https://youtu.be/R7KgBgvQJ0c
