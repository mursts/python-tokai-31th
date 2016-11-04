==========================================
AWSでサーバレスなアプリを作った話
==========================================

| 2016.10.29 Python東海 31th
| @mursts

お前だれよ
==============================

-  みうらさとし(@mursts)
-  Python東海の管理人の1人です
-  GCPUG Nagoyaもやっています。

..   -  7/16(土)に\ `GCPUG Nagoya
..      #1 <http://gcpug-nagoya.connpass.com/event/34144/>`__

余談ですが
==============================

前回はSphinxの話をしたのにスライドをDecksetで作成したので、今回はSphinxで作成しました

私は普段AWSを触っていないので、間違えていたら教えてください。
=============================================================

サーバレス 最近良く聞くようになりました。
=========================================

サーバレスってPaaSと違うの？
==============================

サーバレス難しい。。。
==============================

さーばれす。。
==============================

- 自分でサーバ用意しなければサーバレス？
- それだったらGAE、Herokuもサーバレス？
- 詳しい話はこれを見るといいかも

- `Serverless Architecture by Naoya Ito <https://speakerdeck.com/naoya/serverless-architecture>`_

こまけえことはいいんだよ
==============================

とりあえずやってみる
==============================

サーバレスの流れにのる
==============================

作ったもの
==============================

- お昼の友

  - LINEで位置情報を送ると近場のランチのお店をピックアップしてくれます

.. image:: syokuji_blank_woman.png
   :scale: 50

使ったもの
==============================

- `Amazon API Gateway <https://aws.amazon.com/jp/api-gateway/>`_

  - LINEからのリクエストを受ける

- `AWS Lambda <https://aws.amazon.com/jp/lambda/>`_

  - API Gatewayで受けたリクエストを処理する [#f1]_

- `chalice <https://github.com/awslabs/chalice>`_

  - LambdaとAPI Gatewayを扱うのが容易になる ``Python`` [#f2]_ のフレームワーク
  - デプロイもコマンド一発でこれがないとしんどそう

- `LINE Messaging API <https://business.line.me/ja/services/bot>`_

- `ホットペッパーAPI <http://webservice.recruit.co.jp/hotpepper/>`_

--------

.. [#f1] Python 2.7、Node.js、Java 8 が使える
.. [#f2] ようやくPython登場

デモ
==============================

やったこと
==============================

.. code-block:: sh

   $ virtualenv ~/.virtualenv/chalice -p python2 # python 2.7
   $ source ~/.virtualenv/chalice/bin/activate

   $ pip install chalice

   $ chalice new-project project_name && cd project_name

   $ chalice deploy

   ここでエラー発生 # IAM consoleでユーザ作ってアクセスキーを取得した

   $ pip install awscli
   $ aws configure # AWSにアクセスするために取得したキーを設定

   $ chalice deploy

   またエラー

   # IAMでポリシーの設定
   AWSLambdaFullAccess、IAMFullAccess、AmazonAPIGatewayInvokeFullAccess、AmazonAPIGatewayAdministrator
   を設定した

   $ chalice deploy # ようやく成功

まとめ
==============================

- とりあえずサーバレスの波の端っこに乗れたのかなと思います。
- これと同じものはGAEでもHerokuでも作れます

  - 好きなものを使いましょう

- 私はGAEが好きです

宣伝1
==============================

Python Boot Camp
==============================

https://www.pycon.jp/support/bootcamp.html

- 初心者向けPythonチュートリアル
- 名古屋でもやりたいという方は声をかけてください

宣伝2
==============================

GCPUG Nagoya
==============================

http://gcpug-nagoya.connpass.com/

第2回勉強会は満席ですが、やってみたいというのがあれば声をかけてください。

以上、ありがとうございました。
==============================
