# TrainTicketRails

Sample application for Rails Developers Meetup.

## Application Overview

購入する切符と乗車駅を選択し、「乗車する」ボタンをクリックします。

![screen shot 2017-07-11 at 8 13 58](https://user-images.githubusercontent.com/1148320/28044223-11b718dc-6611-11e7-87b0-844c5d1b86ee.png)

降車駅を選択し、「降車する」ボタンをクリックします。

![screen shot 2017-07-11 at 8 14 11](https://user-images.githubusercontent.com/1148320/28044228-1545f91e-6611-11e7-93a2-db613d1b6244.png)

降車可能な駅であれば、最初の画面に戻ります。

![screen shot 2017-07-11 at 8 14 16](https://user-images.githubusercontent.com/1148320/28044229-156f22e4-6611-11e7-8e6f-12f999505c52.png)

降車できない場合はエラーメッセージが表示されます。

![screen shot 2017-07-11 at 8 17 42](https://user-images.githubusercontent.com/1148320/28044283-75f91f70-6611-11e7-8c7a-00cc366c6380.png)

### 運賃表

|  |      |      |
|------|------|------|
| うめだ |      |      |
| 150  | じゅうそう |      |
| 190  | 150  | みくに |

## Procedures

回答の流れは以下のとおりです。

- このリポジトリ（upstream）を自分のアカウントにフォークする
- 開発環境をセットアップする（下記参照）
- 設問を解く（内容は後述）
- 自分のリポジトリからupstreamに対して、Pull requestを作成する

## Ruby version

- 2.4.1 (recommended)
- 2.2.2 or newer

## System dependencies

- Google Chrome (for system tests)

## Configuration

- Install ChromeDriver for system tests

```
# Mac
brew install chromedriver
```

## Database creation

```
bin/rails db:setup
```

## Database initialization

```
# Use fixtures instead of seeds.rb
bin/rails db:fixtures:load
```

## How to run the test suite

```
bin/rails test && bin/rails test:system
```

Then you see:

```
Running via Spring preloader in process 24707
Run options: --seed 28410

# Running:

.S.S.S....

Finished in 0.101604s, 98.4213 runs/s, 78.7371 assertions/s.
10 runs, 8 assertions, 0 failures, 0 errors, 3 skips

You have skipped tests. Run with --verbose for details.
Run options: --seed 41156

# Running:

Puma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:56207
Use Ctrl-C to stop
.S..S

Finished in 3.095415s, 1.6153 runs/s, 1.2922 assertions/s.
5 runs, 4 assertions, 0 failures, 0 errors, 2 skips

You have skipped tests. Run with --verbose for details.
```

## Exercises

### Ex1. Gate#exit? メソッドの実装

`test/models/gate_test.rb`を開き、`skip 'Please implement!'`の行を削除してください。（3箇所）

テストを実行し、テストが失敗することを確認してください。

```
$ bin/rails test
Running via Spring preloader in process 25108
Run options: --seed 13135

# Running:

..F

Failure:
GateTest#test_みくにで150円の切符を買って、うめだで降りる [/Users/jit/dev/sandbox/train-ticket-rails/test/models/gate_test.rb:39]:
Expected true to not be truthy.


bin/rails test test/models/gate_test.rb:37

F

Failure:
GateTest#test_同じ駅では降りられない [/Users/jit/dev/sandbox/train-ticket-rails/test/models/gate_test.rb:55]:
Expected true to not be truthy.


bin/rails test test/models/gate_test.rb:53

...F

Failure:
GateTest#test_うめだで150円の切符を買って、みくにで降りる [/Users/jit/dev/sandbox/train-ticket-rails/test/models/gate_test.rb:18]:
Expected true to not be truthy.


bin/rails test test/models/gate_test.rb:16

..

Finished in 0.105675s, 94.6298 runs/s, 104.0927 assertions/s.
10 runs, 11 assertions, 3 failures, 0 errors, 0 skips
```

テストがパスするように実装してください。

### Ex2. 画面の実装

`test/system/tickets_test.rb`を開き、「運賃が足りない場合」のテストケースにある、`skip 'Please implement!'`の行を削除してください。

システムテストを実行し、テストが失敗することを確認してください。

```
$ bin/rails test:system
Run options: --seed 48233

# Running:

SPuma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:56470
Use Ctrl-C to stop
..[Screenshot]: tmp/screenshots/failures_test_運賃が足りない場合.png

F

Failure:
TicketsTest#test_運賃が足りない場合 [/Users/jit/dev/sandbox/train-ticket-rails/test/system/tickets_test.rb:25]:
expected to find text "では降車できません。" in "TrainTicketRails 降車しました。😄 運賃 150円 190円 乗車駅 うめだ じゅうそう みくに 乗車する Image: Wikipedia"


bin/rails test test/system/tickets_test.rb:16

.

Finished in 6.378930s, 0.7838 runs/s, 0.9406 assertions/s.
5 runs, 6 assertions, 1 failures, 0 errors, 1 skips

You have skipped tests. Run with --verbose for details.
```

テストがパスするように実装してください。

### Ex3. 特殊ケースの実装

`test/system/tickets_test.rb`を開き、「すでに使用済みの切符を指定されたらトップページに移動する」のテストケースにある、`skip 'Please implement!'`の行を削除してください。

システムテストを実行し、テストが失敗することを確認してください。

```
$ bin/rails test:system
Run options: --seed 58157

# Running:

Puma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:57047
Use Ctrl-C to stop
....[Screenshot]: tmp/screenshots/failures_test_すでに使用済みの切符を指定されたらトップページに移動する.png

F

Failure:
TicketsTest#test_すでに使用済みの切符を指定されたらトップページに移動する [/Users/jit/dev/sandbox/train-ticket-rails/test/system/tickets_test.rb:31]:
expected "/tickets/1/edit" to equal "/"


bin/rails test test/system/tickets_test.rb:28



Finished in 6.378031s, 0.7839 runs/s, 1.0975 assertions/s.
5 runs, 7 assertions, 1 failures, 0 errors, 0 skips
```

テストがパスするように実装してください。

### Ex4. 最終確認＆Pull requestの作成

すべてのテストがパスすることを確認してください。

```
$ bin/rails test && bin/rails test:system
Running via Spring preloader in process 26100
Run options: --seed 13747

# Running:

..........

Finished in 0.202743s, 49.3235 runs/s, 64.1206 assertions/s.
10 runs, 13 assertions, 0 failures, 0 errors, 0 skips
Run options: --seed 27824

# Running:

Puma starting in single mode...
* Version 3.9.1 (ruby 2.4.1-p111), codename: Private Caller
* Min threads: 0, max threads: 1
* Environment: test
* Listening on tcp://0.0.0.0:57230
Use Ctrl-C to stop
.....

Finished in 3.734839s, 1.3387 runs/s, 2.1420 assertions/s.
5 runs, 8 assertions, 0 failures, 0 errors, 0 skips
```

実装が完了したら、Pull requestを作成して回答を提出してください。

### 備考

- 最後まで回答できなかった場合は、途中でギブアップして回答してもらってもOKです。
- こだわった点やアピールポイントがあれば、Pull requestのDescriptionに記述してください。

## Inquiries

何か不明な点があれば、[@jnchito](https://twitter.com/jnchito/)までご連絡ください。

## あわせて読みたい

この問題は「プロを目指す人のためのRuby入門」（2017年11月発売予定）で使用した例題がベースになっています。

[【鋭意制作中】Rubyの入門本「プロを目指す人のためのRuby入門」を執筆しています \- give IT a try](http://blog.jnito.com/entry/2017/05/30/120148)
