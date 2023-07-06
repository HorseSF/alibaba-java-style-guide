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



## データベース 
* Amazon OpenSearch Service 
ダウンタイムなしで、Elasticsearch を大規模かつ簡単にデプロイ、保護、運用する完全マネージド型サービスです。Elasticsearchを利用することで、高速なデータ検索サービスを構築することが可能です。

* Amazon Quantum Ledger Database（Amazon QLDB） 
フルマネージドな台帳データベースサービスです。データの変更履歴はイミュータブルに保持され、履歴が正当であることを暗号的に検証できます。Amazon QLDBを利用すると、クレジット取引など、すべての金融取引の完全で正確なレコードを作成することができます。

* Amazon Keyspaces（またはAmazon MCS）
スケーラブルで可用性の高い、管理されたApache Cassandraと互換性のあるデータベースサービスです。 キーと値や表形式を含む大量の構造化データを保存、取得、管理することができます。Cassandra Query Language（CQL）  を使用して、アプリケーションを迅速に構築できます。Amazon KeyspacesはApache Cassandraのオープンソースと互換性があるサービスであり、そのコミュニティの更新などの恩恵を享受することができます。

* Amazon DynamoDB グローバルテーブル
複数リージョンにマルチマスターデータベースをデプロイするDynamoDBテーブルの機能です。グローバルテーブルを作成する際、そのテーブルの利用を許可する AWS リージョンを指定して複数リージョンにまたがって複数のテーブルを生成します。
DynamoDB グローバルテーブルは、グローバルにユーザーが多数いるアプリケーションに最適です。どこにいても、低レイテンシーでデータにアクセスすることができます。

## ストレージ
|管理方式|特徴|
|--|--|
|IAM　ユーザーポリシー|IAMユーザーに対してAWSリソースとしてのS3へのアクセス権限を設定|
|バケットポリシー|バケットのアクセス権をJSON設定|
|ACL|バケット/オブジェクト単位でのアクセス権限をXMLで設定することができる|
|事前署名付きURL|AWS SDKで生成した事前署名付けURLでS3オブジェクトURLにアクセスできる権利を一定期間付与する|

## EC2
* インスタンスタイプ
* * Dedicated Hostは物理的にサーバーを占有するインスタンスタイプです。Dedicated Hosts では、ライセンス条項の範囲で、ソケット単位、コア単位、または VM ソフトウェア単位の既存のライセンスを利用できます。その上で、同じAWSアカウントに属していたとしても、別のIAMグループとは物理サーバーを共有しません。
  * ハードウェア専有インスタンスはホストHWのレベルで、他のAWSアカウントに属するインスタンスから物理的に分離しますが、 同じAWSアカウントのイ ンスタンスとはHWを共有 する可能性がある
  * ベアメタルはアプリケーション基盤 となるサーバーのプロ セッサーとメモリーに直接アクセス可能なインスタンスです。 AWSの各種サービスとの 連携が可能でOSが直接下層のハードウェアにアクセス可能となります。

## AWSサポート
![image](https://github.com/HorseSF/alibaba-java-style-guide/assets/49813253/62ff88fa-d7fb-4e00-9eee-3baf862c9ecc)

## AWSの設計原則
* 7つの設計原則
* * 強固な認証基盤の整備
* * 追跡可能性の実現
* * 全レイヤーへのセキュリティ適用
* * セキュリティのベストプラクティス自動化
* * 転送中および保管中のデータの保護
* * データに人を近づけない
* * セキュリティイベントに対する準備

* AWS Well-Architected フレームワーク
* * 運用上の優秀性
* * セキュリティ
* * 信頼性
* * パフォーマンス効率
* * コスト最適化
* * 持続可能性

## 運用上の優秀性
AWS Service Catalogを利用して、AWS での使用が承認された IT サービスのカタログを作成および管理できます。この IT サービスには仮想マシンイメージ、サーバー、ソフトウェア、データベースから包括的な多層アプリケーションアーキテクチャまで、あらゆるものが含まれます。AWS Service Catalog は一般的にデプロイされた IT サービスを集中管理することができ、一貫性のあるガバナンスを実現し、コンプライアンス要件を満たすことができます。さらにユーザーは必要な承認済みの IT サービスのみをすばやくデプロイできます。AWS Service Catalog の主な利点は以下のとおりです。 
* IT サービスライフサイクルを集中管理
* 企業標準へのコンプライアンスを確保
* 従業員は承認済みの IT サービスをすばやく見つけてデプロイ可能
* ITサービスマネジメント (ITSM) /ITOM ソフトウェアに接続

## その他AWSサービス
AWS プロフェッショナルサービスは、組織がクラウドを導入するための設計とプロセスをサポートするため、AWS クラウド導入フレームワーク (AWS CAF) を作成しました。フレームワークで示されているガイダンスおよびベストプラクティスは、IT ライフサイクル全体で、組織全体にわたるクラウドコンピューティングへの包括的なアプローチを構築するのに役立ちます。

## 移行・接続
* AWS Direct Connect
オンプレミス環境ネットワークから AWSネットワーク への専用線ネットワーク接続の構築するクラウドサービスソリューションです。AWS Direct Connect を使用すると、AWS とデータセンター、オフィス、またはコロケーション環境との間にプライベート接続を確立することができます。
AWS Virtual Private Network ソリューションは、オンプレミスネットワーク、リモートオフィス、クライアントデバイス、および AWS グローバルネットワーク間に安全な接続を確立します。AWS VPN は、AWS サイト間 VPN と AWS Client VPN で構成されています。これらを組み合わせることで、ネットワークトラフィックを保護する、高可用性かつ柔軟なマネージドクラウド VPN ソリューションを提供します。

* AWS Cloud WAN
クラウド環境とオンプレミス環境間でWANを構築して、管理することができるサービスです。これを利用して、複数の拠点やネットワークにまたがるグローバルネットワークを構築することができます。Cloud WANセントラルダッシュボードを利用して、ネットワークの健全性、セキュリティ、およびパフォーマンスを監視することができます。

## IAM・認証
* AWSアカウントのルートユーザーのみ以下のタスクを実行可能です。
* * アカウントの設定を変更します。これには、アカウント名、E メールアドレス、ルートユーザーパスワード、およびルートユーザーアクセスキーが含まれます。連絡先情報、支払い通貨設定、AWS リージョンなどの他のアカウント設定はルートユーザーでなくても管理者権限で実行可能です。
* * IAM ユーザーアクセス許可を更新します。唯一の IAM 管理者が自身のアクセス許可を誤って取り消した場合は、ルートユーザーとしてサインインしてポリシーを編集し、アクセス許可を復元できます。
* * 請求情報とコスト管理コンソールへの IAM アクセスをアクティブにする
* * 特定の税金請求書を表示します。aws-portal:ViewBilling 許可を持つ IAM ユーザーは、AWS欧州から VAT 請求書を表示およびダウンロードすることができますが、AWS Inc または Amazon Internet Services Private Limited (AISPL) からは不可能です。
* * AWS アカウント を閉じます。
* * リザーブドインスタンスマーケットプレイスに出品者として登録します。
* * MFA (多要素認証)に対応するように Amazon S3 バケットを設定します。
* * 無効な仮想プライベートクラウド (VPC) ID または VPC エンドポイント ID が含まれている Amazon Simple Storage Service (Amazon S3) バケットポリシーを編集または削除します。
* * GovCloudにサインアップする。
