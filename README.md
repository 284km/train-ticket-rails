# TrainTicketRails

Sample application for Rails Developers Meetup.

電車の改札口を簡易的にシミュレーションするRailsアプリケーションです。

## Application Overview

切符を購入して乗車し、目的の駅で降車する流れを以下のようにシミュレートします。

### 操作手順

購入する切符と乗車駅を選択し、「乗車する」ボタンをクリックします。

![screen shot 2017-07-11 at 8 33 11](https://user-images.githubusercontent.com/1148320/28044694-c5620494-6613-11e7-928f-cca198d66cb1.png)

降車駅を選択し、「降車する」ボタンをクリックします。

![screen shot 2017-07-11 at 8 33 19](https://user-images.githubusercontent.com/1148320/28044695-c58a7ad2-6613-11e7-88b8-13d2195b4a25.png)

降車可能な駅であれば、最初の画面に戻ります。

![screen shot 2017-07-11 at 8 33 22](https://user-images.githubusercontent.com/1148320/28044697-c595ee4e-6613-11e7-995b-3f547f0b9a1b.png)

降車できない場合はエラーメッセージが表示されます。

![screen shot 2017-07-16 at 8 20 45](https://user-images.githubusercontent.com/1148320/28243305-c075f784-69ff-11e7-84d1-7b7cdc5818fb.png)

### 運賃表

運賃は以下のようになっています。

仕様を複雑にしないよう、1区間 = 150円、2区間 = 190円で単純に固定されています。

|  |      |      |
|------|------|------|
| うめだ |      |      |
| 150  | じゅうそう |      |
| 190  | 150  | みくに |

### 駅番号

駅の並び順を明示的に表すために、このアプリケーションでは各駅に駅番号（`station_number`）を付与しています。

- うめだ = 1
- じゅうそう = 2
- みくに = 3

### 解答される方への注意事項

これはあくまで勉強会用のサンプルアプリケーションなので、ごくごく単純な仕様で実装しています。  
本番運用されることはないため、「こんな仕様も必要なのでは？」「こういうケースもありえるのでは？」といった深読みは不要です。

### 考慮不要な仕様の例

- 駅が増えたり減ったりするケース
- 運賃が変更されたり、「1区間 = 150円、2区間 = 190円」以外の運賃が登場したりするケース
- 出題内容以外の例外的な画面操作や、異常な入力値
- ユーザーの利便性を高めるためのUI改善

### 解答時の制限事項

解答時の実装方法は基本的に自由ですが、参加者の解答バリエーションが過度に増えてしまわないよう、以下の制限を設けます。

- ファイルを追加してはいけません（新しいクラスやマイグレーションを増やさない）。既存のファイルを変更するだけにしてください。
- 変更してよいファイルはモデルとコントローラのみとします。ビューやヘルパークラスは変更しないでください。
- テストコードは`skip`メソッドの行を削除する以外の変更を加えないでください（新しいテストパターンを増やさない）。
- Gemfileに新しいgemを追加しないでください。

### その他

今回のサンプルアプリケーションでは、Gateクラス（改札機クラス）に運賃が定数として埋め込まれています（`Gate::FARES`）。  
「こんなところに運賃が定義されているのは設計としておかしい！」という意見もあるかもしれませんが、これはあくまで簡易的なサンプルアプリケーションということで、スルーしてやってください 🙇

## 解答の流れ

解答の流れは以下のとおりです。

- このリポジトリ（upstream）を自分のアカウントにフォークする
- 開発環境をセットアップする（下記参照）
- 設問を解く（内容は後述）
- 自分のリポジトリからupstreamに対して、Pull requestを作成する

## 解答に利用するRubyのバージョン

2.4.1を推奨。（ただし、2.2.2以上であれば可）

## 依存する外部アプリケーション

- Google Chrome （システムテストで使用）

## 必要となるPCの設定

ChromeDriverをインストールしてください。（システムテストで使用）

```
# Macの場合
brew update
brew install chromedriver
```

ChromeDriverを自分でダウンロードして、PATHの通ったディレクトリに配置するのもOKです。

- [Downloads \- ChromeDriver \- WebDriver for Chrome](https://sites.google.com/a/chromium.org/chromedriver/downloads)

## Railsのセットアップ

このリポジトリをフォークし、ローカルにcloneしたら、次のコマンドでセットアップを実行してください。

```
bin/setup
```

セットアップを実行したらRailsを起動し、 http://localhost:3000/ にアクセスしてください。  
正常に画面が表示されればOKです。

```
rails s
```

![screen shot 2017-07-11 at 8 33 11](https://user-images.githubusercontent.com/1148320/28044694-c5620494-6613-11e7-928f-cca198d66cb1.png)

## テストコードの実行

以下のコマンドを実行し、テストコードが正常に動作することを確認してください。

```
bin/rails test && bin/rails test:system
```

次のような表示になればOKです。

```
Running via Spring preloader in process 27919
Run options: --seed 3647

# Running:

.S..S..S..

Finished in 0.067467s, 148.2206 runs/s, 118.5765 assertions/s.
10 runs, 8 assertions, 0 failures, 0 errors, 3 skips

You have skipped tests. Run with --verbose for details.
Run options: --seed 40891

# Running:

Puma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:63371
Use Ctrl-C to stop
..SS.S

Finished in 3.099099s, 1.9360 runs/s, 1.2907 assertions/s.
6 runs, 4 assertions, 0 failures, 0 errors, 3 skips

You have skipped tests. Run with --verbose for details.
```

## 問題

ここから問題が始まります。  
以下の問題文をよく読んで、解答してください。

### Ex1. 運賃の計算（下り）

`test/models/gate_test.rb`を開き、「うめだで150円の切符を買って、みくにで降りる（運賃不足）」にある`skip 'Please implement this!'`の行を削除してください。

テストを実行し、テストが失敗することを確認してください。

```
$ bin/rails test
Running via Spring preloader in process 28084
Run options: --seed 58060

# Running:

..S...F

Failure:
GateTest#test_うめだで150円の切符を買って、みくにで降りる（運賃不足） [/Users/jit/dev/sandbox/train-ticket-rails/test/models/gate_test.rb:18]:
Expected true to not be truthy.


bin/rails test test/models/gate_test.rb:16

..S

Finished in 0.058427s, 171.1537 runs/s, 154.0384 assertions/s.
10 runs, 9 assertions, 1 failures, 0 errors, 2 skips

You have skipped tests. Run with --verbose for details.
```

テストがパスするように実装してください。

### Ex2. 運賃の計算（上り）

`test/models/gate_test.rb`を開き、「みくにで150円の切符を買って、うめだで降りる（運賃不足）」にある`skip 'Please implement this!'`の行を削除してください。

Ex1と同じ要領で実装してください。

### Ex3. 同じ駅で降りる場合

`test/models/gate_test.rb`を開き、「同じ駅では降りられない」にある`skip 'Please implement this!'`の行を削除してください。

Ex1と同じ要領で実装してください。

### Ex4. 画面の実装

`test/system/tickets_test.rb`を開き、「運賃が足りない場合」と「同じ駅で降りる場合」のテストケースにある、`skip 'Please implement this!'`の行を削除してください。（計2箇所）

システムテストを実行し、テストが失敗することを確認してください。

```
Run options: --seed 13045

# Running:

Puma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:63717
Use Ctrl-C to stop
[Screenshot]: tmp/screenshots/failures_test_運賃が足りない場合.png

F

Failure:
TicketsTest#test_運賃が足りない場合 [/Users/jit/dev/sandbox/train-ticket-rails/test/system/tickets_test.rb:25]:
expected to find text "降車駅 では降車できません。" in "TrainTicketRails 降車しました。😄 切符 150円 190円 乗車駅 うめだ じゅうそう みくに 乗車する Image: Wikipedia"


bin/rails test test/system/tickets_test.rb:16

S...[Screenshot]: tmp/screenshots/failures_test_同じ駅で降りる場合.png

F

Failure:
TicketsTest#test_同じ駅で降りる場合 [/Users/jit/dev/sandbox/train-ticket-rails/test/system/tickets_test.rb:37]:
expected to find text "降車駅 では降車できません。" in "TrainTicketRails 降車しました。😄 切符 150円 190円 乗車駅 うめだ じゅうそう みくに 乗車する Image: Wikipedia"


bin/rails test test/system/tickets_test.rb:28



Finished in 9.524030s, 0.6300 runs/s, 0.8400 assertions/s.
6 runs, 8 assertions, 2 failures, 0 errors, 1 skips

You have skipped tests. Run with --verbose for details.
```

テストがパスするように実装してください。

### Ex5. 特殊ケースの実装

`test/system/tickets_test.rb`を開き、「すでに使用済みの切符を指定されたらトップページに移動する」のテストケースにある、`skip 'Please implement this!'`の行を削除してください。

Ex4と同じ要領で実装してください。

### Ex6. 最終確認＆Pull requestの作成

すべてのテストがパスすることを確認してください。

```
$ bin/rails test && bin/rails test:system
Running via Spring preloader in process 28528
Run options: --seed 4005

# Running:

..........

Finished in 0.067580s, 147.9728 runs/s, 192.3646 assertions/s.
10 runs, 13 assertions, 0 failures, 0 errors, 0 skips
Run options: --seed 10018

# Running:

Puma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:64152
Use Ctrl-C to stop
......

Finished in 4.652693s, 1.2896 runs/s, 2.5792 assertions/s.
6 runs, 12 assertions, 0 failures, 0 errors, 0 skips
```

実装が完了したら、Pull requestを作成して解答を提出してください。

### 備考

- 最後まで回答できなかった場合は、途中でギブアップして提出してもらってもOKです。
- こだわった点やアピールポイントがあれば、Pull requestのDescriptionに記述してください。

## お問い合わせ

何か不明な点があれば、[@jnchito](https://twitter.com/jnchito/)までご連絡ください。

## あわせて読みたい

この問題は「プロを目指す人のためのRuby入門」（2017年11月発売予定）で使用した例題がベースになっています。

[【鋭意制作中】Rubyの入門本「プロを目指す人のためのRuby入門」を執筆しています \- give IT a try](http://blog.jnito.com/entry/2017/05/30/120148)

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

