# alibaba-java-style-guide
* [前言](README.md)
* [编程规约](c1/README.md)
    * [(一) 命名规约](c1/s1.md)
    * [(二) 常量定义](c1/s2.md)
    * [(三) 格式规约](c1/s3.md)
    * [(四) OOP规约](c1/s4.md)
    * [(五) 集合处理](c1/s5.md)
    * [(六) 并发处理](c1/s6.md)
    * [(七) 控制语句](c1/s7.md)
    * [(八) 注释规约](c1/s8.md)
    * [(九) 其他](c1/s9.md)
* [异常日志](c2/README.md)
    * [(一) 异常处理](c2/s1.md)
    * [(二) 日志处理](c2/s2.md)
* [MySQL规约](c3/README.md)
    * [(一) 建表规约](c3/s1.md)
    * [(二) 索引规约](c3/s2.md)
    * [(三) SQL规约](c3/s3.md)
    * [(四) ORM规约](c3/s4.md)
* [工程规约](c4/README.md)
    * [(一) 应用分层](c4/s1.md)
    * [(二) 二方库规约](c4/s2.md)
    * [(三) 服务器规约](c4/s3.md)
* [安全规约](c5/README.md)

#### ELB/Auto Scaling
##### Elastic Load Balancing（ELB）
ELB配下の負荷分散先リソースのことを「ターゲット」といい、一つのELB配下で管理されるターゲットの集合を「ターゲットグループ」といいます。ターゲットにはEC2などのインスタンスや、IPアドレス、Lambda関数が指定でき、それらをまとめたターゲットグループ単位に負荷分散を行います。なお、AZ障害時の影響を少なくするためにも、ターゲットはマルチAZ（複数のAZに配置する構成）にするのが一般的です。

##### ELBの種類
* Application Load Balancer（ALB）
  ALBはレイヤー7（アプリケーション層）で負荷分散を行います。ALBではHTTP、HTTPSをサポートしています。また、WebSocketや、同一インスタンス内の複数ポートへの負荷分散、ホストベースやパスベース、URLクエリ文字列でのルーティングに対応しています。
* * ALBが対応している主なルーティング
  * ホストベース
    ホストベースのルーティングとは、クライアントがリクエストした接続先URLのFQDNに従ってルーティングできる機能のことです。
  * パスベース
    パスベースのルーティングとは、クライアントがリクエストした接続先URLのパスに従ってルーティングできる機能のことです。
  * URLクエリ文字列
    URLクエリ文字列でのルーティングとは、クライアントがリクエストした接続先URLのクエリ文字列に従ってルーティングできる機能のことです。
* Network Load Balancer（NLB）
  NLBはレイヤー4（トランスポート層）で負荷分散を行います。NLBではTCP、UDP、TLSをサポートしています。また、WebSocketや、同一インスタンス内の複数ポートへの負荷分散に対応しています。
* Classic Load Balancer（CLB）
  CLBはレイヤー7（アプリケーション層）およびレイヤー4（トランスポート層）で負荷分散を行います。CLBではHTTP、HTTPS、TCP、SSL/TLSをサポートしています。CLBはALBやNLBより古いサービスでパフォーマンスが劣るため、基本的にはALBやNLBの利用が推奨されています。

##### ELBの機能
* ヘルスチェック
* アクセスログ
  ELBに送信されるリクエストを記録しログをAmazon S3に保存します。記録されたログはトラフィックの分析やコンプライアンスの監査に利用できます。アクセスログには、クライアントのアクセス日時、接続元IPアドレス、ポート番号、ステータスコードなどクライアントの接続情報が記録されます。
* ELB自身のスケーリング
  ELBにはリクエスト数の増減に応じてELB自身が自動的にスケーリングする機能があります。リクエスト数が増加したらELB自身を自動的にスケールアウト（追加）し、リクエスト数が減少したらスケールイン（削除）して元の状態に戻ります。
* リダイレクト
  ALBには、ALBに送られてきたリクエストを別のURLにリダイレクトする機能があります。例えば、ユーザーから「http://www.example.com」（HTTP）へ送られたリクエストを「https://www.example.com」（HTTPS）に変換することで、セキュアな通信が可能になります。HTTPのリクエストをHTTPSに変換するには、ALBでHTTPリスナーを作成し、HTTPSへリダイレクトするルールを設定します。
* ELB経由の暗号化通信
  ELB経由でクライアントとターゲット間の通信を暗号化させるには、暗号化する通信の範囲とサーバー証明書（SSL/TLS証明書）の配置によって3つの方法があります。サーバー証明書とは、ユーザーとの通信をHTTPSで暗号化するとともに、ドメイン（ping-t.com など）の使用権を確認してアクセス先のサーバーが本物であるという証明する電子証明書のことです。ELB経由の暗号化通信に利用するサーバー証明書は、AWS Certificate Manager（SSL/TLS証明書を管理するサービス）で管理されている証明書を利用できます。
  * クライアントとELB間の通信を暗号化する
    * ELBにサーバー証明書を導入する
      クライアントとELB間で通信を暗号化し、ELBとターゲット間は平文の通信（暗号化されていない通信）を行う方法です。クライアントとELB間での通信の暗号化・復号をELBが行うため、ターゲットに暗号化・復号による負荷が発生しません。すべてのELBが対応しています。
  * クライアントとターゲット間の通信を暗号化する
    * ELBとターゲットにサーバー証明書を導入する
      クライアントとELB間、ELBとターゲット間で別の暗号化通信を行う方法です。暗号化接続はELBが終端となり、ELBから別の暗号化接続を確立して通信します。ELB、ターゲットに暗号化・復号による負荷がかかりますが、クライアントからターゲットまでの通信すべてを暗号化できます。ALB、CLBが対応しています。
    * ターゲットにサーバー証明書を導入する
      ELBでは暗号化・復号せず、直接クライアントとターゲット間で暗号化通信を行う方法です。ターゲットに暗号化・復号による負荷が発生しますが、ELBによる暗号化・復号の遅延を発生させずに通信全てを暗号できます。NLB、CLBが対応しています。
* SNIを利用したELB経由の暗号化通信
  SNI（Server Name Indication）は、暗号化通信で使用するサーバー証明書をパブリックIPアドレスではなくドメイン名によって判断する技術です。SNIに対応したELBに複数のサーバー証明書を導入すると、ELBが宛先ドメイン名から適切なサーバー証明書を判断してサーバーへ通信を転送します。SNIはALBとNLBが対応しています。
##### Auto Scaling 
* シンプルスケーリング
  1つのメトリクス（CPU使用率などシステムのパフォーマンスに関するデータ）に対する1つのしきい値に基づいて、インスタンスを増減します。
  例：300秒間の平均CPU使用率が50％を超えたら、インスタンスを1台追加する

* ステップスケーリング
  1つのメトリクスに対する複数のしきい値に基づいて、インスタンスの増減を段階的に行います。
  例：300秒間の平均CPU使用率が50％を超えたらインスタンスを1台追加し、90％を超えたら2台追加する

* ターゲット追跡スケーリング
  1つのメトリクスが指定した目標値になるように、インスタンスを増減します。増減するインスタンス数はAWS側で調整されます。
  例：平均CPU使用率を30％に維持する

#### Lambda/API Gateway
#### ECS/Fargate
