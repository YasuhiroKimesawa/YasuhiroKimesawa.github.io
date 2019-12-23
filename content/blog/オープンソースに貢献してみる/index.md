---
title: "オープンソースに貢献してみる"
date: 2019-12-23T10:07:47+06:00
draft: false

# post thumb
image: "./blog/オープンソースに貢献してみる/github_PNG20.png"

# meta description
description: "オープンソースに貢献してみる"

# taxonomies
categories: 
  - "Github"
tags:
  - "Github"
  - "オープンソース"

# post type
type: "post"
---

この記事はQiitaに書く予定の記事を先行公開しています。

ServerlessFrameworkのプラグインを修正しました。

[Lambda関数をそのままAWS Batchに乗せ換える(Python3.6限定)](https://qiita.com/YasuhiroKimesawa/items/8d7ada7cc8bddd24d60b)

https://github.com/YasuhiroKimesawa/serverless-aws-batch


ServerlessでデプロイするLambda関数をAWS Batchにソースコードをいじらずに移行するプラグインですが、いくつかバグがあったので修正しました。

ちょっと動作確認中でまだPullRequestを出していないですが、手順を残しておきましょう。

１. フォーク元のGithubに移動し、フォークボタンを押すと自分のレポジトリにフォークできます。

2. 普段どおりにローカルにCloneして適切にブランチを切って修正、自分のレポジトリにPushしましょう。

3. PushしたブランチでPullRequestを作成しましょう。ここでフォーク元を指定できます。

4. フォーク元で問題なければ取り入れてもらえるでしょう。

5. フォーク元の更新を自分のRepositoryに取り込むのは

検索するといっぱい記事が出てきますね。。。例えば、、、
[GitHubでフォーク元の差分を取り込む(@icb54615さん)](https://qiita.com/icb54615/items/3544c419a3f6fc3534fb)

6. 注意としては、フォーク元の更新を自分のレポジトリに取り込みたいので、自分のレポジトリのmasterに自分の修正を入れないことです。

よいOSSライフを！