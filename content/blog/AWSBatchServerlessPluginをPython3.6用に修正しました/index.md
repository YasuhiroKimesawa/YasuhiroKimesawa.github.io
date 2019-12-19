---
title: "Lambda関数をそのままAWS Batchに乗せ換える(Python3.6限定)"
date: 2019-12-16T10:07:47+06:00
draft: false

# post thumb
image: "./images/featured-post/post-5.jpg"

# meta description
description: "Lambda関数をそのままAWS Batchに乗せ換える(Python3.6限定)"

# taxonomies
categories: 
  - "AWS"
  - "serverless"
tags:
  - "AWS"
  - "Lambda"
  - "AWSBatch"

# post type
type: "featured"
---

この記事はQiitaに書こうと思っている記事を先行で公開しています。

Serverlessでサービスを展開していると、どうしてもRDBを使いたくなったり、どこかでバッチ処理をしたくなったりしますよね。

RDBについては、RDS ProxyがLambdaから使用可能になりそうでいい兆しですね。

[Amazon RDS Proxy](https://aws.amazon.com/jp/rds/proxy/)

バッチ処理についてはかつてからAWS Batchというのが用意されています。

これはECRに用意したDockerを使って処理を実行できる環境です。Queueも用意されているのでかなり自由なバッチ設計ができると思います。

さて、Serverlessで環境を構築している場合、まず選択肢として、AWSBatchよりもLambdaを考えると思います。

StepFunctionやQueue、S3などのイベント、並行処理を駆使して構築する場合もあるでしょう。

ただ、Lambdaの実行制限は現状15分でそれを超える場合は何か手を考えなくてはいけません。

処理を分割する、並行処理を考える等あると思いますが、選択肢としてAWS Batchへの移行も入ってくるかと。


しかし、問題はECR上にDockerを用意しなくてはいけない点です。


AWS Batchを使用する場合、Lambdaで使っているソースコードをわざわざDockerに乗せて、ECRのレポジトリに突っ込まなくてはいけない。

これは非常に面倒臭いです。


そこでServerlessFrameworkを使っている場合限定ですが、いいPluginを見つけました。


[serverless-aws-batch](https://github.com/justinram11/serverless-aws-batch)

※　ただしこちらは不具合が多いので注意。。。


このプラグインはServerlessFrameworkからデプロイする際に、Lambdaで使用するソースをそのままDockerに乗せ、ECRにPushしてくれて、
Batchの設定まで行ってくれる夢のようなPluginです。

イベントや環境変数もそのまま使えます(Batchを起動するLambdaが自動で作られ、イベントや環境変数の設定も引き継がれる)。
serverless.ymlをちょっと書き換えるだけで全部構築してくれます。

ただ、先の大元のPluginはちょっとバグが多かったので、せめてPython3.6で動くように手を入れたものがこちらになります。

[serverless-aws-batch](https://github.com/YasuhiroKimesawa/serverless-aws-batch/tree/revert-2-revert-1-bugfix/various_bugfix)

※ 大元をForkしてまだプルリクを出していないのですが、取り込まれたらリンクを修正します。

使い方はGithubのReadmeに詳しく書いてあります。
基本serverless.ymlでiamにbatchを許可するのと、該当のfunctionにbatchの項目を付け足すだけで済むはずです。

ぜひ使ってみてください＼(^o^)／

Python3.6以外では動く保証はないですが、同じような修正をすればいけると思うので、ForkしてPRしてもらえればいいかと思います。

あらためて、大元のjustinram11さんありがとうございます！ナイスアイデアです！