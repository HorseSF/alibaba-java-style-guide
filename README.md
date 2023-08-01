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

### データベース
#### RDS/Aurora
##### 特徴
* データベースインスタンスとストレージが分離したアーキテクチャ
* 複数のデータコピーと自動修復機能などによるストレージの高い耐障害性
* レプリカインスタンスの自動フェイルオーバーによる高可用性
* 最大64TBまでスケール可能な拡張性
* Aurora Auto Scalingによる負荷の自動調整
* データベースのクローンを高速作成
##### Amazon Aurora Global Database（Aurora グローバルデータベース）
Auroraグローバルデータベースは、Auroraデータベースを複数のリージョンにまたがって運用できるサービスです。例えば、東京リージョンで稼働しているデータベースを大阪リージョンにも配置できるということです。Auroraグローバルデータベースを使用しても、ユーザーは複数のリージョンのデータベースを管理する必要はありません。データはプライマリとして稼働しているメインのリージョンからセカンダリリージョンへレプリケートされます。

#### Redshift
データウェアハウス（DWH：Data WareHouse）とは、複数のシステムからデータを収集・統合・蓄積し、分析に使用するデータベースです。蓄積したデータは、例えば時系列や顧客のデータに基づいて分析され、結果はシステム効率化や経営改善などの意思決定に利用されます。このように、大容量データを分析し経営に役立てることを「BI：Business Intelligence」といい、RedshiftはBIの分野で活用されています。
