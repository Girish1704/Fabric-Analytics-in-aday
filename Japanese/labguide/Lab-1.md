# Microsoft Fabric - Fabric Analyst in a Day - ラボ 1

![](../media/Lab-1/lab1-04-jp.png)

# 目次

- ドキュメントの構造

- シナリオ / 問題の説明

- Power BI Desktop レポートの概要

    - タスク 1: ラボ環境で Power BI Desktop を設定する

    - タスク 2: Power BI Desktop レポートを分析する

    - タスク 3: Power Query を確認する

- 参考資料

# ドキュメントの構造

このラボでは、実行する手順だけでなく、視覚的にわかりやすいように、手順に関連するスクリーンショットも提示されます。各スクリーンショットでは、ユーザーが注目する必要のある領域が、オレンジのボックスで強調表示されて示されます。

> **注:** 製品の更新が現在進行中であるため、一部のスクリーンショットは最新の画像ではない場合があります。

# シナリオ / 問題の説明

Fabrikam, Inc. は、ノベルティ商品の卸売業者です。卸売業者である Fabrikam の顧客のほとんどは、個人に再販する会社です。Fabrikam は、専門店、スーパーマーケット、コンピューター販売店、観光名所の店など、アメリカ合衆国全土の小売顧客に販売しています。また、Fabrikam では、Fabrikam に代わって製品の販売促進を行う代理店のネットワークを通じて、他の卸売業者にも販売しています。現在、Fabrikam の顧客はすべてアメリカ合衆国に拠点を置いていますが、同社では他の国や地域への拡大を推進しようと考えています。

あなたは営業チームのデータ アナリストです。データ セットの収集、クリーニング、 解釈を行ってビジネス上の問題を解決します。また、チャートやグラフなどの視覚エフェクトをまとめたり、レポートを作成したり、それらを組織の意思決定者にプレゼンしたりもします。

データから貴重な分析情報を引き出すには、さまざまなシステムからデータを取得し、 クリーニングして、まとめてマッシュアップする必要があります。データは次のソース から取得できます。

- **販売データ:** ERP システムから取得します。データは ADLS Gen2 データベースに格納されます。毎日正午 (午後 12 時) に更新されます。

- **仕入先データ:** さまざまな仕入先から取得します。データは Snowflake データベースに格納されます。毎日真夜中 (午前 0 時) に更新されます。

- **顧客データ:** Customer Insights から取得します。データは Dataverse に格納されます。データは常に最新の状態です。

- **従業員データ:** 人事システムから取得します。エクスポート ファイルとして SharePoint フォルダーに格納されます。毎朝午前 9 時に更新されます。

  ![](../media/Lab-1/image6.jpeg)

あなたは現在、Power BI Premium で上記のソース システムからデータを取得するセマンティック モデルを構築しています。その目的は、自分のレポート作成のニーズを満たし、 エンド ユーザーにセルフ サービス機能を提供することです。モデルの更新には Power Query を使います。

**直面している課題:**

- 各種データ ソースごとに異なる更新時間に対応するには、1 日に少なくとも 3 回はデータセットを更新する必要があります。

- ソース システムで発生したすべての更新を取得するために毎回完全な更新を行う必要があるため、更新に長い時間がかかります。

- 取得元のデータ ソースでエラーが発生すると、データセットの更新が中断されます。従業員ファイルが時間どおりにアップロードされず、データセットの更新が中断されてしまうことが何度もあります。

- データ モデルに変更を加えるのに非常に長い時間がかかります。データ サイズが大きくて変換が複雑だと、Power Query によるプレビューの更新に時間がかかるためです。

- 社内標準は Mac ですが、Power BI Desktop を使用するには Windows PC が必要です。

Microsoft Fabric について聞いたあなたは、それを使って課題に対処できるかどうかを見てみることにしました。

### **Power BI Desktop レポートの概要**

Fabric の説明を始める前に、変換とモデルについて理解するために現在の Power BI Desktop のレポートを見てみましょう。

## タスク 1: ラボ環境で Power BI Desktop を設定する

1. お使いのラボ環境のデスクトップにある **Reports** フォルダー内の **FAIAD.pbix** を開
    きます。**Power BI Desktop** でファイルが開かれます。

    ![](../media/Lab-1/image7.png)

    > ### **注意:** パワー BI デスクトップの「メールアドレスを入力してください」画面で応答しなくなり、入力できない場合は、タスクバーのパワー BI アイコン **(1)** にカーソルを合わせてください。次に、余分な空白（白い）ウィンドウの **X** **(2)** をクリックして閉じます。これにより、メインのパワー BI ウィンドウが再び操作可能になります。

    ![](../media/Lab-1/lab1-04-jp1.png)

2. [メール アドレスの入力] ダイアログが表示されたら、**ユーザー名**をコピーしてダイアログの**メール** フィールドに貼り付け、**続行**を選択します。

    - メール/ユーザー名: <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-1/image8.png)

3. [Microsoft Azure にサインインする] タブにログイン画面が表示されます。次のメール アドレス/ユーザー名を入力して、**次へ**をクリックします。

    - メール/ユーザー名: <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-1/image9.png)

4. 次に、以下の**一時アクセス パス**を入力して、**サインイン**をクリックします。

    - 一時アクセス パス: <inject key="AzureAdUserPassword"></inject>

      ![](../media/Lab-1/image10.png)

5. **すべてのアプリにサインインしたままにする**ダイアログが開きます。**OK** を選択します。

    ![](../media/Lab-1/image11.png)

6. **準備が完了しました。** ダイアログが開きます。**完了**を選択します。

    これで Power BI Desktop が開きます。

## タスク 2: Power BI Desktop レポートを分析する

以下のレポートでは、Fabrikam の売上を分析しています。ページの左上に KPI が一覧表示されています。残りのビジュアルは、担当地域、製品グループ、リセラー会社ごとの時系列に沿った売上を強調しています。

![](../media/Lab-1/image12.jpeg)

> **注:** このトレーニングでは、Fabric で利用できるツールを使ったデータの取得、変換、モデリングに焦点を当てています。レポートの作成やナビゲーションには焦点を当てません。数分かけてレポートを理解してから、次のステップに進みましょう。

1. 営業担当地域別にデータを分析してみましょう。**Sales Territory の New England** (散布図) ビジュアルを選択します。売上の推移からわかるように、New England ではリセラー Tailspin Toys が Wingtip Toys よりも多くの売上をあげています。Sales YoY% の縦棒グラフを見ると、過去 1 年間の Wingtip Toys の売上成長率が低く、四半期ごとに減少していることがわかります。第 3 四半期で少し回復したものの、第 4 四半期で再び下がりました。

    ![](../media/Lab-1/image13.jpeg)

2. これを Rocky Mountain の担当地域と比較してみましょう。**Sales Territory の Rocky Mountain**
    (散布図) ビジュアルを選択します。Sales YoY% の縦棒グラフを見ると、Wingtip Toys の売上は、2 回の四半期で低かった後 2023 年の第 4 四半期で急激に増えていることがわかります。

    ![](../media/Lab-1/image14.jpeg)

3. **Sales Territory の Rocky Mountain** を選択して、フィルターを外します。

4. 画面の下部中央にある散布図ビジュアル (Sales 別の Sales Orders) から、右上の外れ値を選択します (第 4 象限)。Margin % は 52% であり、平均の 50% を上回っていることがわかります。また、2023 年の最後 2 回の四半期では、Sales YoY% が増加しています。

    ![](../media/Lab-1/image15.jpeg)

5. 散布図ビジュアルで外れ値のリセラーを選択して、**フィルターを外します**。

6. 製品グループとリセラー別に製品の詳細を取得してみましょう。Product Group および ResellerCompany による Sales の横棒グラフのビジュアルから、**Tailspin Toys の Packaging Materials バーを右クリック**し、ダイアログから**ドリルスルー -> Product Detail** を選択します。

    ![](../media/Lab-1/image16.png)

7. 製品の詳細を提供するページに移動します。今後の注文もいくつかあることがわか
    ります。

8. このページの確認が完了したら、ページの左上にある **Ctrl + 戻る矢印**をクリックして売上レポートに戻ります。

    ![](../media/Lab-1/image17.png)

9. 自由にレポートをさらに分析してみてください。準備ができたら、モデル ビューを見てみましょう。左パネルで、**モデル ビュー アイコン**を選択します。

    ![](../media/Lab-1/image18.png)

10. Sales と PO という 2 つのファクト テーブルがあることがわかります。

    a. Sales データの粒度は、Date、Reseller、Product、People 別です。Date、Reseller、Product、People が Sales につながっています。

    b. PO データの粒度は、Date、Product、People 別です。Date、Product、People が PO につながっています。

    c. Product ごとの Supplier データがあります。Supplier は Product につながっ ています。

    d. Geo ごとの Reseller の場所データがあります。Geo は Reseller につながっ ています。

    e. Reseller ごとの Customer 情報があります。Customer は Reseller につながっ ています。

## タスク 3: Power Query を確認する

1. Power Query を調べてデータ ソースについて理解しましょう。リボンから**ホーム -> データの変換**を選択します。

    ![](../media/Lab-1/image19.png)

2. Power Query ウィンドウが開きます。リボンから**ホーム -> データ ソース設定**を選
    択します。[データ ソース設定] ダイアログが開きます。一覧をスクロールしていくと、問題の説明で述べたように 4 つのデータ ソースがあることがわかります。

    - Snowflake

    - SharePoint

    - ADLS Gen2

    - Dataverse

3. **閉じる** を選択して [データ ソース設定] ダイアログを閉じます。

    ![](../media/Lab-1/image20.png)

4. 左側の [クエリ] パネルでは、各クエリがデータ ソースごとにグループ化されていることがわかります。

5. **DataverseData** フォルダーには、BabyBoomer、GenX、GenY、GenZ という 4 つの異なるクエリで使用できる Customer データが含まれています。これら 4 つのクエリをアペンドして、Customer クエリを作成します。

6. クエリ ウィンドウから **Customer** クエリをクリックします。このクエリを選択するには、Dataverse の資格情報を再入力する必要があります。**資格情報の編集**をクリックします。

    ![](../media/Lab-1/image21.png)

7. **サインイン**をクリックしてアカウントにログインします。

    ![](../media/Lab-1/image22.png)

8. **ユーザー名**と**パスワード**を入力することで、Dataverse データ ソースの資格情報を入力できます。資格情報は以下で提供します。終わったら、**接続**を選択します。

    - メール/ユーザー名: <inject key="AzureAdUserEmail"></inject>

    - パスワード: <inject key="AzureAdUserPassword"></inject>

9. クエリ ウィンドウから **ADLS Base Folder** クエリをクリックします。このクエリを選択すると、資格情報を求められます。**資格情報の編集**をクリックします。

    ![](../media/Lab-1/image23.png)

10. ADLS データ ソースの場合、**Shared Access Signature (SAS)** オプションを選択し、下記の **SAS トークン**を入力します。

    - **SAS** トークン: <inject key="Sas token"></inject>

    ![](../media/Lab-1/image24.png)

11. **ADLSData** フォルダーには複数のディメンション (Geo、Product、Reseller、Date) があることがわかります。Sales ファクトもあります。

    - **Geo ディメンション**は、Cities、Countries、States の各クエリからのデータをマージすることで作成されます。

    - **Product ディメンション**は、Product Groups と Product Item Group のクエリからのデータをマージすることで作成されます。

    - **Reseller ディメンション**は、BuyingGroup クエリを使ってフィルター処
    理されます。

    - **Sales ファクト**は、InvoiceLineItems と Invoice のクエリをマージするこ
    とで作成されます。

12. Snowflake データ ソースの場合は、クエリ ウィンドウから **SupplierCategories** クエリを選択します。このクエリを選択すると、資格情報の入力を求められます。**資格情報の編集**をクリックします。

    ![](../media/Lab-1/image25.png)

13. 下記の **Snowflake ユーザー名**と **Snowflake パスワード**を入力します。これらの資格情報を使用して Snowflake にあるすべてのテーブルを Snowflake に接続し、 **[接続]** を選択します。

    - **Snowflake ユーザー名:** <inject key="SnowFlake Username" enableCopy="false" />

    - **Snowflake パスワード:** <inject key="SnowFlake Password" enableCopy="false" />

        > **注:** 上で示した資格情報を使用した Snowflake への接続で問題が発生する場合は、以下で示すバックアップ資格情報を使用してください。

    - **Snowflake ユーザー名:** SNOWFLAKE_BACKUP

    - **Snowflake パスワード:** 8UpfRpExVDXv2AC1

14. **SnowflakeData** フォルダーには、Supplier ディメンションと PO (Order / Spend) ファクトが含まれていることがわかります。

    - **Supplier ディメンション**は、Suppliers クエリと SupplierCategories クエリをマージすることで作成されます。

    - **PO ファクト**は、PO と PO Line Items のクエリをマージすることで作成されます。

15. SharePoint データ ソースの場合は、クエリ ウィンドウから **People** クエリを選択します。このクエリを選択すると、資格情報の入力を求められます。**資格情報の編集**をクリックします。

    ![](../media/Lab-1/image26.png)

16. **Microsoft アカウント** オプションを選択し、**サインイン**をクリックします。下記のユーザー名とパスワードを入力し、[接続] を選択します。

    - **メール/ユーザー名:** <inject key="AzureAdUserEmail"></inject>

    - **パスワード:** <inject key="AzureAdUserPassword"></inject>

      ![](../media/Lab-1/image27.png)

17. **SharepointData** フォルダーには People ディメンションが含まれていることがわかります。

    ![](../media/Lab-1/image28.png)

    これで、私たちが何を扱っているかがわかりました。以降のラボでは、Dataflow Gen2 を使って同様の Power Query を作成し、レイクハウスを使ってモデリングを行います。

# 参考資料

Fabric Analyst in a Day (FAIAD) では、Microsoft Fabric で使用できる主要な機能の一部をご紹介します。サービスのメニューにあるヘルプ (?) セクションには、いくつかの優れたリソースへのリンクがあります。

![](../media/Lab-1/image29.png)

Microsoft Fabric の次のステップに役立つリソースをいくつか以下に紹介します。

- ブログ記事で [Microsoft Fabric の GA に関するお知らせ](https://aka.ms/Fabric-Hero-Blog-Ignite23)の全文を確認する

- [ガイド付きツアー](https://aka.ms/Fabric-GuidedTour)を通じて Fabric を探索する

- [Microsoft Fabric の無料試用版](https://aka.ms/try-fabric)にサインアップする

- [Microsoft Fabric の Web サイト](https://aka.ms/microsoft-fabric)にアクセスする

- [Fabric の学習モジュール](https://aka.ms/learn-fabric)で新しいスキルを学ぶ

- [Fabric の技術ドキュメント](https://aka.ms/fabric-docs)を参照する

- [Fabric の作業開始に関する無料の e-book](https://aka.ms/fabric-get-started-ebook) を読む

- [Fabric コミュニティ](https://aka.ms/fabric-community)に参加し、質問の投稿やフィードバックの共有を行い、他のユーザーから学びを得る

より詳しい Fabric エクスペリエンスのお知らせに関するブログを参照してください。

- [Fabric の Data Factory エクスペリエンスに関するブログ](https://aka.ms/Fabric-Data-Factory-Blog)

- [Fabric の Synapse Data Engineering エクスペリエンスに関するブログ](https://aka.ms/Fabric-DE-Blog)

- [Fabric の Synapse Data Science エクスペリエンスに関するブログ ](https://aka.ms/Fabric-DS-Blog)

- [Fabric の Synapse Data Warehousing エクスペリエンスに関するブログ ](https://aka.ms/Fabric-DW-Blog)

- [Fabric の Synapse Real-Time Analytics エクスペリエンスに関するブログ](https://aka.ms/Fabric-RTA-Blog)

- [Power BI のお知らせに関するブログ](https://aka.ms/Fabric-PBI-Blog)

- [Fabric の Data Activator エクスペリエンスに関するブログ ](https://aka.ms/Fabric-DA-Blog)[Fabric の管理とガバナンスに関するブログ](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Fabric の OneLake に関するブログ](https://aka.ms/Fabric-OneLake-Blog)

- [Dataverse と Microsoft Fabric の統合に関するブログ](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation.All rights reserved.

このデモ/ラボを使用すると、次の条件に同意したことになります。

このデモ/ラボで説明するテクノロジまたは機能は、ユーザーのフィードバックを取得し、学習エクスペリエンスを提供するために、Microsoft Corporation によって提供されます。 ユーザーは、このようなテクノロジおよび機能を評価し、Microsoft にフィードバックを提供するためにのみデモ/ラボを使用できます。それ以外の目的には使用できません。このデモ/ラボまたはその一部を、変更、コピー、配布、送信、表示、実行、再現、発行、ライセンス、著作物の作成、転送、または販売することはできません。

複製または再頒布のために他のサーバーまたは場所にデモ/ラボ (またはその一部) をコピーまたは複製することは明示的に禁止されています。

このデモ/ラボは、前に説明した目的のために複雑なセットアップまたはインストールを必要としないシミュレーション環境で潜在的な新機能や概念などの特定のソフトウェア テクノロジ/製品の機能を提供します。このデモ/ラボで表されるテクノロジ/概念は、フル機能を表していない可能性があり、最終バージョンと動作が異なることがあります。また、そのような機能や概念の最終版がリリースされない場合があります。物理環境でこのような機能を使用するエクスペリエンスが異なる場合もあります。

**フィードバック。** このデモ/ラボで説明されているテクノロジ、機能、概念に関するフィードバックを Microsoft に提供する場合、ユーザーは任意の方法および目的でユーザーのフィードバックを使用、共有、および商品化する権利を無償で Microsoft に提供するものとします。また、ユーザーは、フィードバックを含む Microsoft のソフトウェアまたはサービスの特定部分を使用したり特定部分とインターフェイスを持ったりする製品、テクノロジ、サービスに必要な特許権を無償でサード パーティに付与します。ユーザーは、フィードバックを含めるために Microsoft がサード パーティにソフトウェアまたはドキュメントをライセンスする必要があるライセンスの対象となるフィードバックを提供しません。これらの権限は、本契約の後も存続します。

Microsoft Corporation は、明示、黙示、または法律上にかかわらず、商品性のすべての保証および条件、特定の目的、タイトル、非侵害に対する適合性など、デモ/ラボに関するすべての保証および条件を拒否します。Microsoft は、デモ/ラボから派生する結果、出力の正確さ、任意の目的に対するデモ/ラボに含まれる情報の適合性に関して、いかなる保証または表明もしません。

**免責事項**

このデモ/ラボには、Microsoft Power BI の新機能と機能強化の一部のみが含まれています。一部の機能は、製品の将来のリリースで変更される可能性があります。このデモ/ラボでは、新機能のすべてではなく一部について学習します。
