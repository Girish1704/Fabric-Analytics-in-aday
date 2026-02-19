# Microsoft Fabric - Fabric Analyst in a Day - ラボ 3

# 概要

このシナリオでは、ERP システムから取得された販売データが ADLS Gen2
に格納されています。毎日正午 (午後 12 時)
に更新されます。このデータを変換してレイクハウスに取り込み、モデルで使用する必要があります。

このデータは複数の方法で取り込むことができます。

- **ショートカット:** データへのリンクが作成されます。ビジュアル クエリ
  ビューを使用して、データを変換できます。このラボではショートカットを使用します。

- **Notebooks:**
  この方法ではコードを記述する必要があります。これは、開発者にとって使いやすい方法です。

- **データフロー (Gen2) を使用する。**Power Query やデータフロー (Gen1)
  についてはおそらくなじみがあることと思います。データフロー (Gen2)
  はその名前が示すように、新しいバージョンのデータフローです。Power
  Query とデータフロー (Gen1)
  のすべての機能に加え、データを変換して複数のデータ
  ソースに取り込む機能が追加されています。これについては以降のラボで紹介します。

- **パイプライン:** これはオーケストレーション
  ツールです。アクティビティに調整を加え、データを抽出、変換して取り込むことができます。ここではパイプラインを使用してデータフロー
  Gen2 のアクティビティを実行し、抽出、変換、取り込みを行います。

まず、ショートカットを作成して、ADLS Gen2 データ
ソースからレイクハウスにデー    
タを取り込みます。データを取り込んだら、ビジュアル クエリ
ビューを使用して、    
データを変換します。

このラボを終了すると、次のことが学べます。

- レイクハウスにショートカットを作成する方法

- ビジュアル クエリ機能を使用してデータを変換する方法

# ADLS Gen2 へのショートカット

## タスク 1: ショートカットを作成する

ショートカットは、ターゲットとなる場所へのリンクを作成するために使用されます。ショートカットを使用すると、データをレイクハウスに物理的に移すことなく、データにアクセスできます。これは、Windows
デスクトップでのショートカットの作成に似ています。

1. 画面の上部にある **lh_FAIAD**
    タブを選択し、レイクハウスに移動します。

    a. タブが表示されない場合は、ワークスペースに戻って、そこからレイクハウスを開くことができます。

2. **エクスプローラー**
    パネルで、**テーブル**の横にある**省略記号**を選択します。

3. **新しいショートカット**を選択します。

    ![](../media/Lab-03/image6.png)

4. **新しいショートカット**
    ダイアログが開きます。**外部ソース**で、**Azure Data Lake Storage
    Gen2** を選択します。

    ![](../media/Lab-03/image7.png)

5. **新しい接続 (1)** を選択します。

6. **URL** プロパティに次のリンクを入力します:
    https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales
    **(2)**:

7. [接続    ] セクションで、    [新しい接続の作成    ] **をクリックします (3)**

8. [認証の種類    ] ドロップダウンから、**Shared Access Signature (SAS)
    (4)** を選択します。

9. SAS トークンをコピーして、SAS トークン (5)
    フィールドに貼り付けます。

    - **SAS トークン:**

10. 画面右下の**次へ (6)** を選択します。

    ![](../media/Lab-03/image8.png)

11. ADLS Gen2 に接続され、左パネルにディレクトリ構造が表示されます。    
    **Delta-Parquet-Format-FY25 (1)** を展開します。

12. 以下のディレクトリ **(2)** を**選択**してから、**次へ (3)**
    を選択します。

    a. Application.Cities

    b. Application.Countries

    c. Application.StateProvinces

    d. DateDim

    e. Sales.BuyingGroups

    f. Sales.Customers

    g. Sales.InvoiceLines

    h. Sales.Invoices

    i. Warehouse.StockGroups

    j. Warehouse.StockItemStockGroups

    k. Warehouse.StockItems

    **注:** Sales.Invoices_May だけが、**選択されない**ディレクトリです。

    ![](../media/Lab-03/image9.png)

13. 名前を編集できる次のダイアログが表示されます。**Application.Cities**
    の     [アクション    ] の下にある**編集アイコン (1)** を選択します。

14. 名前を **Application.Cities から Cities に (2)** 変更します。

15. 名前の横にあるチェック マーク **(3)** を選択して、変更を保存します。

    ![](../media/Lab-03/image10.png)

16. 同様に、ショートカット名を次のように変更します。

    a. Application.Countries から **Countries** へ

    b. Application.StateProvinces から **States** へ

    c. DateDim から **Date** へ

    d. Sales.BuyingGroups から **BuyingGroups** へ

    e. Sales.Customers から **Customers** へ

    f. Sales.InvoiceLines から **InvoiceLineItems** へ

    g. Sales.Invoices から **Invoices** へ

    h. Warehouse.StockGroups から **ProductGroups** へ

    i. Warehouse.StockItemStockGroups から **ProductItemGroup** へ

    j. Warehouse.StockItems から **ProductItem** へ

    **注:**
    名前をもう一度確認してください。入力ミスがあると、ラボの間のエラーの原因になります。

17. **作成**を選択して、ショートカットを作成します。

    ![](../media/Lab-03/image11.png)

18. すべてのショートカットがテーブルとして作成されていることに注意してください。**BuyingGroups**
    テーブルを選択し、データ
    パネルにデータのプレビューが表示されることを確認してください。

    ![](../media/Lab-03/image12.png)

次の手順では、セマンティック
モデルを作成するために、データを変換します。データを変換するためのビューを作成します。

# ビジュアル クエリを使用してデータを変換する

## タスク 2: ビジュアル クエリを使用して Geo ビューを作成する

1. SQL
    エンドポイントを使用して、**レイクハウス**にアクセスできます。これにより、    
    データに対するクエリの実行や、ビューの作成が可能になります。画面の**右上**で、    
    **レイクハウス (1) -    > SQL 分析エンドポイント (2)** を選択します。

    ![](../media/Lab-03/image13.png)

    SQL
    分析エンドポイントが表示されます。上部のナビゲーションに新しい項目が追加されました。そのタブを選択すると、レイクハウスに戻ることができます。    [エクスプローラー    ]
    パネルが変更されていることを確認してください。ビュー、ストアド
    プロシージャ、クエリなどを作成することができます。ここでは、Power Query
    のようなローコード インターフェイスを提供するビジュアル
    クエリを作成します。結果をビューとして保存します。

    最初に、Geo ビューを作成します。Geo
    ビューを作成するには、Cities、States、Countries
    の各テーブルからのデータをマージする必要があります。

2. 上部のメニューで、**新規 SQL クエリ (1)** の横にあるドロップ
    ダウンをクリックし、    
    **新規のビジュアル クエリ (2)** を選択します。

    ![](../media/Lab-03/image14.png)

3. クエリを作成するには、テーブルを     [ビジュアル クエリ    ]
    パネルに追加する必要が    
    あります。**Cities (1)**
    テーブルの横の省略記号をクリックし、**キャンバスに挿入 (2)**
    を選択します。

    ![](../media/Lab-03/image15.png)

4. **States** および **Countries**
    テーブルに対して同じ手順を繰り返します。

    次に、これらのクエリをマージする必要があります。ビジュアル クエリ
    エディターには、Power Query
    エディターを使用するためのオプションがあります。Power BI で慣れている    
    ので、これを使用しましょう。

5. **ビジュアル クエリ エディターのメニューからポップアップで開く**
    アイコンを選択し    
    ます (右側にあります)。Power Query エディターが表示されます。

    **注:**
    このアイコンがすぐに表示されない場合、右にスクロールするか、ビジュアル
    クエリ タブを再度開くことが必要な場合があります

    ![](../media/Lab-03/image16.png)

6. **Cities (1)** クエリを選択した状態で、Power Query
    エディターのリボンから**ホーム (2) -    > 結合 (3) -    > クエリのマージ
    ドロップダウン (4) -    > 新規としてクエリをマージ (5)** を選択します。

    ![](../media/Lab-03/image17.png)

7. **マージ用の左テーブル**で **Cities** を選択します。

8. **マージ用の右テーブル**で **States** を選択します。

9. 両方のテーブルから **StateProvinceID**
    列を選択します。この列を使用して結合    
    を実行します。

10. **結合の種類**として**内部**を選択します。

11. **OK** を選択します。

    ![](../media/Lab-03/image18.png)

    **マージ**という名前の新しいクエリが作成されたことを確認してください。States
    の列がいくつか必要になります。

12. **データ ビュー** (下部のパネル) で、**States** 列 (右端の列)
    の横にある**二重矢印**をク    
    リックします。

13. パネルが開きます。選択された列が次のものだけであることを確認します。

    a. StateProvinceCode

    b. StateProvinceName

    c. CountryID

    d. SalesTerritory

14. **OK** を選択します。

    ![](../media/Lab-03/image19.png)

    次に、Countries クエリをマージする必要があります。

15. マージ クエリを選択した状態 **(1)** で、**ホーム (2) -> 結合 (3) -> クエリのマージ ドロップダウン (4) -> クエリのマージ (5)** を選択します。

    ![](../media/Lab-03/image20.png)

16.  [マージ    ] クエリ ダイアログが開きます。**マージ用の右テーブル**で
    **Countries** を選    
    択します。

17. 両方のテーブルから **CountryID**
    列を選択します。この列を使用して結合を    
    実行します。

18. **結合の種類**として**内部**を選択します。

19. **OK** を選択します。

    ![](../media/Lab-03/image21.png)

    Countries の列がいくつか必要になります。

20. **データ ビュー** (下部のパネル) で、**Countries**
    列の横にある**二重矢印**をクリックします。

21. パネルが開きます。選択された列が次のものだけであることを確認します。

    a. CountryName

    b. FormalName

    c. IsoAlpha3Code

    d. IsoNumericCode

    e. CountryType

    f. Continent

    g. Region

    h. Subregion

22. **OK** を選択します。

    **重要:** 下にスクロールし、ステップ 21 の一覧で示された 8
    つの列をすべて選択してください。次のスクリーンショットでは、UI
    の制限のため最初の 5 列のみが表示されています。

    ![](../media/Lab-03/image22.png)

    **Merge**
    テーブルのすべての列が必要なわけではありません。必要なものだけを選択して    
    ください。

23. **Merge** クエリを選択した状態 (1) で、リボンから**ホーム (2) -     >
    列の選択 (3) -    > 列の選択 (4)** を選択します。

    **注:**     [列の選択    ] オプションが表示されない場合は、    [列の管理    ]
    の下に見つかります。

    ![](../media/Lab-03/image23.png)

24. [列の選択    ] ダイアログが開きます。次の列を**オフにします**。

    a. StateProvinceID

    b. Location

    c. LastEditedBy

    d. ValidFrom

    e. ValidTo

    f. CountryID

25. **OK** を選択します。

    ![](../media/Lab-03/image24.png)

    プロセスは Power Query と類似しており、すべてのステップが、右側の
        [適用されたステップ    ] パネルとビジュアル
    ビューの両方に記録されていることを確認してください。マージ
    クエリの名前を変更し、読み込みを有効にして、このクエリからデータを読み込みましょう。

26. [クエリ    ] パネル (左) で、**マージ**
    クエリを**右クリック**します。**名前の変更**を選択し、    
    クエリの名前を **Geo** に変更します。

27. [クエリ    ] パネル (左) で、**Geo**
    クエリを**右クリック**します。**読み込みを有効にする**
    を選択し、このクエリを有効にします。

28. Cities、States、Countries
    の各クエリが**無効になっている**ことを確認します。

29. Power Query エディターの右下にある**保存**を選択します。

    ![](../media/Lab-03/image25.png)

    ビジュアル クエリ
    エディターが表示されます。ここでは、このクエリをビューとして    
    保存します。

    **注:** Power Query
    エディターを使用して実行したすべてのステップは、ビジュアル クエリ    
    エディターを使用して実行することもできます。

30. ビジュアル クエリ
    エディターのメニューから**ビューとして保存**を選択します。

    ![](../media/Lab-03/image26.png)

    [ビューとして保存    ] ダイアログが開きます。SQL
クエリが使用可能になっていることに注目してください。検証の必要がある場合は、SQL
コードを確認できます。

31. **ビュー名**に **Geo** と入力します。

32. **OK** を選択してビューを保存します。

    ![](../media/Lab-03/image27.png)

    ビューが保存されると、アラートが表示されます。

33. [エクスプローラー    ] パネル (左) で、**Views**
    を展開します。新しく作成された Geo ビューがあります。

    ![](../media/Lab-03/image28.png)

## タスク 3: ビジュアル クエリを使用して Reseller ビューを作成する

Customers テーブルと BuyingGroups テーブルをマージして、Reseller
ビューを作成しましょう。今回は、Power Query
オプションを開かずに、ビジュアル クエリを使用してビューを作成します。

1. 上部のメニューで、**新規 SQL クエリ (1)** の横にあるドロップ
    ダウンをクリックし、    
    **新規のビジュアル クエリ (2)** を選択します。

2. クエリを作成するには、テーブルを     [ビジュアル クエリ    ]
    パネルに追加する必要が    
    あります。**BuyingGroups (1)**
    テーブルの横の省略記号をクリックし、**キャンバスに挿入 (2)**
    を選択します。

    ![](../media/Lab-03/image29.png)

3. **Customers** テーブルに対して同じ手順を繰り返します。

4. **Customers** クエリを選択します。Customers
    を選択すると、テーブルの後に     "+    " 記号が表示されます
    (これは、テーブルの後にステップを追加することを示しています。テーブルの後に
    **    "+    "**
    記号が表示されない場合は、別のステップを選択している可能性があります。    [テーブル    ]
    を選択すれば、続行できます)。

<!-- -->

5. ビジュアル クエリのメニューから**結合 -    >
    クエリのマージ**を選択します。

    ![](../media/Lab-03/image30.png)

    [マージ    ] ダイアログが開き、Customers
が最上位のテーブルとして選択されています。

6. **マージ用の右テーブル**で **BuyingGroups** を選択します。

7. 両方のテーブルから **BuyingGroupID**
    列を選択します。この列を使用して結合を    
    実行します。

8. **結合の種類**として**内部**を選択します。

9. **OK** を選択します。

    ![](../media/Lab-03/image31.png)

10. **データ ビュー** (下部のパネル) で、**BuyingGroups** 列 (右端の列)
    の横にある**二重矢印**をクリックして、BuyingGroups
    から必要な列を選択します。

11. パネルが開きます。**BuyingGroupName** 列を**選択**します。

12. **OK** を選択します。

    ![](../media/Lab-03/image32.png)

    Customer
    テーブルのすべての列が必要なわけではありません。必要な列だけを選択してください。

13. ビジュアル クエリのメニューから**列の管理 -    >
    列の選択**を選択します。

    ![](../media/Lab-03/image33.png)

14. [列の選択    ] ダイアログが開きます。次の列を**選択**します。

    a. ResellerID

    b. ResellerName

    c. PostalCityID

    d. PhoneNumber

    e. FaxNumber

    f. WebsiteURL

    g. DeliveryAddressLine1

    h. DeliveryAddressLine2

    i. DeliveryPostalCode

    j. PostalAddressLine1

    k. PostalAddressLine2

    l. PostalPostalCode

    m. BuyingGroupName

15. **OK** を選択します。

    ![](../media/Lab-03/image34.png)

16. BuyingGroupName 列の名前を変更しましょう。**データ ビューで
    BuyingGroupName    
    列ヘッダーをダブルクリック**して、編集可能にします。

17. 列を **ResellerCompany** という**名前に変更**します。

    ![](../media/Lab-03/image35.png)

    Customer
    テーブルには、すべてのステップが記録されていることを確認してください。    
    次に、このビューを保存しましょう。

18. すべてのステップがあるため、Customers
    クエリを保存する必要があります。読み込みを有効にする必要があります。**Customers**
    クエリ ボックスの**省略記号**を選択します。

19. **読み込みを有効にする**がオンになっていることを確認します。

    ![](../media/Lab-03/image36.png)

    **注:**     [読み込みを有効にする    ] がオンになっていると、**Customer**
    ボックスが青の境界線で囲まれます。

20. ビジュアル クエリ
    エディターのメニューから**ビューとして保存**を選択します。

    ![](../media/Lab-03/image37.png)

    [ビューとして保存    ] ダイアログが開きます。SQL
クエリが使用可能になっていることに注目してください。選択すると、そのクエリを確認することができます。

21. **ビュー名**に **Reseller** と入力します。

22. **OK** を選択してビューを保存します。

    ![](../media/Lab-03/image38.png)

    ビューが保存されると、アラートが表示されます。

23. [エクスプローラー    ] パネル (左) で、**Views**
    を展開します。新しく作成された Reseller    
    ビューがあります。

    ![](../media/Lab-03/image39.png)

## タスク 4: ビジュアル クエリを使用して Sales ビューを作成する

InvoiceLineItems と Invoices のテーブル、および Reseller
ビューをマージして、Sales ビューを作成しましょう。このクエリは Power BI
Desktop
にあります。詳細エディターからコードをコピーします。ただし、コードをコピーする前に、ビジュアル
クエリを使用してマージ
テーブルを作成する必要があります。これは、ビジュアル
クエリでは空のクエリを作成できないためです。この方法を試してみましょう。

1. 上部のメニューで、**新規 SQL クエリ**の横にあるドロップ
    ダウンをクリックし、**新規のビジュアル クエリ**を選択します。

    ![](../media/Lab-03/image40.png)

2. **エクスプローラー -    > Table** セクションから、    [ビジュアル クエリ    ]
    パネルにテーブルを追加する必要があります。**InvoiceLineItems**
    テーブルの横の省略記号をクリックし、**キャンバスに挿入**を選択します。

3. **Invoices** テーブルに対して同じ手順を繰り返します。

4. **エクスプローラー -    > Views** セクションから、    [ビジュアル クエリ    ]
    パネルにテーブルを追加する必要があります。**Reseller**
    テーブルの横の省略記号をクリックし、**キャンバスに挿入**を選択します。

5. ビジュアル クエリ エディターで、**ポップアップで開く**を選択して
    Power Query エディターを開きます。

    ![](../media/Lab-03/image41.png)

6. **InvoiceLineItems** クエリを選択した状態で、リボンから次のように選択します: **ホーム (2) -> 結合 (3) -> クエリのマージ ドロップダウン (4) -> 新規としてクエリをマージ (5)。**    [マージ    ] ダイアログが開きます。

    ![](../media/Lab-03/image42.png)

7. **マージ用の左テーブル**で **InvoiceLineItems** を選択します。

8. **マージ用の右テーブル**で **Invoices** を選択します。

9. 両方のテーブルから **InvoiceID**
    列を選択します。この列を使用して結合を実行します。

10. **結合の種類**として**内部**を選択します。

11. **OK** を選択します。

    ![](../media/Lab-03/image43.png)

    Power BI Desktop
    からコードをコピーし、詳細エディターを使用して貼り付けます。

12. まだ開いていない場合は、お使いのラボ環境のデスクトップにある
    **Reports** フォルダー内の **FAIAD.pbix** を開きます。

13. リボンから**ホーム -    > データの変換**を選択します。Power Query
    ウィンドウが開きます。前のラボで確認したように、左パネルのクエリはデータ
    ソースごとに整理され    
    ています。

    ![](../media/Lab-03/image44.png)

14. 左の**クエリ** パネルの **ADLSData** **(1)** フォルダーにある
    **Sales (2)** クエリを選択します。

15. リボンから**ホーム -    > 詳細エディター (3)**
    を選択します。    [詳細エディター    ]    
    ダイアログが開きます。

    ![](../media/Lab-03/image45.png)

    **注:** 詳細エディターが見つからない場合は、**ホーム     > クエリ -    >
    詳細エディター**からアクセスできます。

16. **3 行目 (#    "Expanded Invoice    " ...)**
    から最後のコード行までのコードを選択します。

17. **右クリック**して**コピー**を選択します。

18. **キャンセル**を選択して詳細エディターを閉じます。

    ![](../media/Lab-03/image46.png)

19. Power Query エディターが開いている**ブラウザーに戻ります**。

20. **マージ** クエリが選択されていることを確認してください。

21. リボンから**ホーム -    >
    詳細エディター**を選択します。    [詳細エディター    ] ダイアロ    
    グが開きます。

    ![](../media/Lab-03/image47.png)

22. **2 行目の末尾にコンマを追加します** (Source =
    Table.NestedJoin(InvoiceLineItems, {    "InvoiceID    "}, Invoices,
    {    "InvoiceID    "},     "Invoices    ", JoinKind.Inner),

23. **Enter** を押して、新しい行を開始します。

24. キーボードで **Ctrl+V** を押して、Power BI Desktop
    からコピーしたコードを貼
    り付けます。

    **注:** ラボ環境で作業している場合は、画面の右側にある**省略記号
    (    ...)** を選択してください。スライダーを使用して **VM ネイティブ
    クリップボード**を**有効**にします。ダイアログで     [OK    ]
    を選択します。クエリの貼り付けが済んだら、このオプションを無効にしてかまいません。

    ![](../media/Lab-03/image48.png)

    ![](../media/Lab-03/image49.png)

25. コードの最後の 2 行 (ソース内) を強調表示して**削除**します。

26. **OK** をクリックして変更を保存します。

    ![](../media/Lab-03/image50.png)

    簡単に行うには、詳細エディターですべてのコードを削除し、次のコードを詳細エディ
    ターに貼り付けます。

    ```
    let
    Source = Table.NestedJoin(InvoiceLineItems, {"InvoiceID"}, Invoices, {"InvoiceID"}, "Invoices", JoinKind.Inner),
        #"Expanded Invoice" = Table.ExpandTableColumn(Source, "Invoices", {"CustomerID", "BillToCustomerID", "SalespersonPersonID", "InvoiceDate"}, {"CustomerID", "BillToCustomerID", "SalespersonPersonID", "InvoiceDate"}),
        #"Removed Other Columns" = Table.SelectColumns(#"Expanded Invoice",{"InvoiceLineID", "InvoiceID", "StockItemID", "Quantity", "UnitPrice", "TaxRate", "TaxAmount", "LineProfit", "ExtendedPrice", "CustomerID", "SalespersonPersonID", "InvoiceDate"}),
        #"Renamed Columns" = Table.RenameColumns(#"Removed Other Columns",{{"CustomerID", "ResellerID"}}),
        #"Merged Queries" = Table.NestedJoin(#"Renamed Columns", {"ResellerID"}, Reseller, {"ResellerID"}, "Customer", JoinKind.Inner),
        #"Added Custom" = Table.AddColumn(#"Merged Queries", "Sales Amount", each [ExtendedPrice] - [TaxAmount]),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Sales Amount", type number}}),
        #"Removed Columns" = Table.RemoveColumns(#"Changed Type",{"Customer"})
    in
        #"Removed Columns"
    ```

27. Power Query エディターに戻ります。左側の     [クエリ    ]
    パネルで、**マージ クエリをダブルクリック**して、名前を変更します。

28. マージ クエリを **Sales** という**名前に変更**します。

29. Sales
    クエリを右クリックし、**読み込みを有効にする**を選択して、クエリが読み込まれるようにします。

    ![](../media/Lab-03/image51.png)

30. **保存**を選択してクエリを保存し、Power Query
    ダイアログを閉じます。ビジュアル クエリ エディターが表示されます。

31. ビジュアル クエリ
    エディターのメニューから**ビューとして保存**を選択します。    [ビューとして保存    ]
    ダイアログが開きます。SQL
    クエリが使用可能になっていることに注目してください。選択すれば、そのクエリを確認することができます。

32. **ビュー名 (1)** に **Sales** と入力します。

33. **OK (2)** を選択してビューを保存します。

    ![](../media/Lab-03/image52.png)

    ビューが保存されると、アラートが表示されます。

34. [エクスプローラー    ] パネル (左) で、**Views**
    を展開します。新しく作成された Sales ビューがあります。

    ![](../media/Lab-03/image53.png)

## タスク 5: ビジュアル クエリを使用して Product ビューを作成する

**ProductItem**、**ProductItemGroup**、**ProductGroups**
の各テーブルをマージして、Product
ビューを作成しましょう。作業を進めるために、コードを詳細エディターにコピーします。

1. 上部のメニューで、**新規 SQL クエリ (1)** の横にあるドロップ
    ダウンをクリックし、    
    **新規のビジュアル クエリ (2)** を選択します。

    ![](../media/Lab-03/image54.png)

2.  [エクスプローラー    ] セクションから、    [ビジュアル クエリ    ]
    パネルにテーブルを追加する必要があります。**ProductItem (1)**
    テーブルの横の省略記号をクリックし、**キャンバスに挿入 (2)**
    を選択します。

    ![](../media/Lab-03/image55.png)

3. **ProductItemGroup** および **ProductGroups**
    テーブルに対して同じ手順を繰り返します。

4. ビジュアル クエリ エディターで、**ポップアップで開く**を選択して
    Power Query エディターを開きます。

    ![](../media/Lab-03/image56.png)

5. **ProductItem** クエリを選択した状態 **(1)**
    で、リボンから**ホーム (2) -    > 結合 (3) -    > クエリのマージ
    ドロップダウン (4) -    > 新規としてクエリをマージ (5)** を選択します。
    を選択します。    [マージ    ] ダイアログボックスが開きます。

    ![](../media/Lab-03/image57.png)

6. **マージ用の左テーブル**で **ProductItem** を選択します。

7. **マージ用の右テーブル**で **ProductItemGroup** を選択します。

8. 両方のテーブルから **StockItemID**
    列を選択します。この列を使用して結合を実行します。

9. **結合の種類**で**左外部**を選択します。

10. **[OK    ] を選択します。** 新しいマージ クエリが作成されます。

    ![](../media/Lab-03/image58.png)

11. マージ クエリを選択した状態で、リボンから**ホーム -    >
    詳細エディター**を選択します。    [詳細エディター    ]
    ダイアログが開きます。

    ![](../media/Lab-03/image59.png)

    **注:** 詳細エディターが見つからない場合は、**ホーム     > クエリ -    >
    詳細エディター**からアクセスできます。

12. **詳細エディターのコードをすべて選択し、削除します**。

13. 次のコードを詳細エディターに**貼り付けます**。

    ```
    let
       Source = Table.NestedJoin(ProductItem, {"StockItemID"}, ProductItemGroup, {"StockItemID"}, "ProductItemGroup", JoinKind.LeftOuter),
       #"Expanded ProductItemGroup" = Table.ExpandTableColumn(Source, "ProductItemGroup", {"StockGroupID"}, {"StockGroupID"}),
       #"Merged queries" = Table.NestedJoin(#"Expanded ProductItemGroup", {"StockGroupID"}, ProductGroups, {"StockGroupID"}, "ProductGroups", JoinKind.LeftOuter),
       #"Expanded ProductGroups" = Table.ExpandTableColumn(#"Merged queries", "ProductGroups", {"StockGroupName"}, {"StockGroupName"}),
       #"Choose columns" = Table.SelectColumns(#"Expanded ProductGroups", {"StockItemID", "StockItemName", "SupplierID", "Size", "IsChillerStock", "TaxRate", "UnitPrice", "RecommendedRetailPrice", "TypicalWeightPerUnit", "StockGroupName"})
    in
       #"Choose columns"
    ```

14. **OK** を選択して詳細エディターを閉じます。Power Query
    エディターに戻ります。

    ![](../media/Lab-03/image60.png)

15. 左側の     [クエリ    ] パネルで、**マージ
    クエリをダブルクリック**して、名前を変更します。

16. マージ クエリの名前を **Product** に**変更**します。

17. Product
    クエリを右クリックし、**読み込みを有効にする**を選択して、クエリが読み込まれるようにします。

18. **保存**を選択してクエリを保存し、Power Query
    ダイアログを閉じます。ビジュアル クエリが表示されます。

    ![](../media/Lab-03/image61.png)

19. ビジュアル クエリ
    エディターのメニューから**ビューとして保存**を選択します。    [ビューとして保存    ]
    ダイアログが開きます。SQL
    クエリが使用可能になっていることに注目してください。選択すれば、そのクエリを確認することができます。

20. **ビュー名**に **Product** と入力します。

21. **OK** を選択してビューを保存します。

    ![](../media/Lab-03/image62.png)

    ビューが保存されると、アラートが表示されます。

22. [エクスプローラー    ] パネル (左) で、**Views**
    を展開します。新しく作成された Product ビューがあります。

    ![](../media/Lab-03/image63.png)

ADLS Gen2
データソースからデータを変換しました。このラボでは、ショートカットの作成方法を学習し、ビジュアル
クエリ
ビューを使用してデータを変換するためのさまざまなオプションを確認しました。

次のラボでは、データフロー (Gen2)
の使用方法と別のレイクハウスへのショートカットの作成方法を学習します。

# 参考資料

Fabric Analyst in a Day (FAIAD) では、Microsoft Fabric
で使用できる主要な機能の一部をご紹介します。サービスのメニューにあるヘルプ
(?) セクションには、いくつかの優れたリソースへのリンクがあります。

![](../media/Lab-01/image28.png)

Microsoft Fabric
の次のステップに役立つリソースをいくつか以下に紹介します。

- ブログ記事で [Microsoft Fabric の GA
  に関するお知らせ](https://aka.ms/Fabric-Hero-Blog-Ignite23)の全文を確認する

- [ガイド付きツアー](https://aka.ms/Fabric-GuidedTour)を通じて Fabric
  を探索する

- [Microsoft Fabric
  の無料試用版](https://aka.ms/try-fabric)にサインアップする

- [Microsoft Fabric の Web
  サイト](https://aka.ms/microsoft-fabric)にアクセスする

- [Fabric
  の学習モジュール](https://aka.ms/learn-fabric)で新しいスキルを学ぶ

- [Fabric の技術ドキュメント](https://aka.ms/fabric-docs)を参照する

- [Fabric の作業開始に関する無料の
  e-book](https://aka.ms/fabric-get-started-ebook) を読む

- [Fabric
  コミュニティ](https://aka.ms/fabric-community)に参加し、質問の投稿やフィードバックの共有を行い、他のユーザーから学びを得る

より詳しい Fabric
エクスペリエンスのお知らせに関するブログを参照してください。

- [Fabric の Data Factory
  エクスペリエンスに関するブログ](https://aka.ms/Fabric-Data-Factory-Blog) 

- [Fabric の Synapse Data Engineering
  エクスペリエンスに関するブログ](https://aka.ms/Fabric-DE-Blog) 

- [Fabric の Synapse Data Science
  エクスペリエンスに関するブログ ](https://aka.ms/Fabric-DS-Blog)

- [Fabric の Synapse Data Warehousing
  エクスペリエンスに関するブログ ](https://aka.ms/Fabric-DW-Blog)

- [Fabric の Synapse Real-Time Analytics
  エクスペリエンスに関するブログ](https://aka.ms/Fabric-RTA-Blog)

- [Power BI のお知らせに関するブログ](https://aka.ms/Fabric-PBI-Blog)

- [Fabric の Data Activator
  エクスペリエンスに関するブログ ](https://aka.ms/Fabric-DA-Blog)[Fabric
  の管理とガバナンスに関するブログ](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Fabric の OneLake に関するブログ](https://aka.ms/Fabric-OneLake-Blog)

- [Dataverse と Microsoft Fabric
  の統合に関するブログ](https://aka.ms/Dataverse-Fabric-Blog)

© 2025 Microsoft Corporation.All rights reserved.

このデモ/ラボを使用すると、次の条件に同意したことになります。

このデモ/ラボで説明するテクノロジまたは機能は、ユーザーのフィードバックを取得し、学習エクスペリエンスを提供するために、Microsoft
Corporation によって提供されます。
ユーザーは、このようなテクノロジおよび機能を評価し、Microsoft
にフィードバックを提供するためにのみデモ/ラボを使用できます。それ以外の目的には使用できません。このデモ/ラボまたはその一部を、変更、コピー、配布、送信、表示、実行、再現、発行、ライセンス、著作物の作成、転送、または販売することはできません。

複製または再頒布のために他のサーバーまたは場所にデモ/ラボ
(またはその一部) をコピーまたは複製することは明示的に禁止されています。

このデモ/ラボは、前に説明した目的のために複雑なセットアップまたはインストールを必要としないシミュレーション環境で潜在的な新機能や概念などの特定のソフトウェア
テクノロジ/製品の機能を提供します。このデモ/ラボで表されるテクノロジ/概念は、フル機能を表していない可能性があり、最終バージョンと動作が異なることがあります。また、そのような機能や概念の最終版がリリースされない場合があります。物理環境でこのような機能を使用するエクスペリエンスが異なる場合もあります。

**フィードバック。** このデモ/ラボで説明されているテクノロジ、機能、概念に関するフィードバックを
Microsoft
に提供する場合、ユーザーは任意の方法および目的でユーザーのフィードバックを使用、共有、および商品化する権利を無償で
Microsoft に提供するものとします。また、ユーザーは、フィードバックを含む
Microsoft
のソフトウェアまたはサービスの特定部分を使用したり特定部分とインターフェイスを持ったりする製品、テクノロジ、サービスに必要な特許権を無償でサード
パーティに付与します。ユーザーは、フィードバックを含めるために Microsoft
がサード
パーティにソフトウェアまたはドキュメントをライセンスする必要があるライセンスの対象となるフィードバックを提供しません。これらの権限は、本契約の後も存続します。

Microsoft Corporation
は、明示、黙示、または法律上にかかわらず、商品性のすべての保証および条件、特定の目的、タイトル、非侵害に対する適合性など、デモ/ラボに関するすべての保証および条件を拒否します。Microsoft
は、デモ/ラボから派生する結果、出力の正確さ、任意の目的に対するデモ/ラボに含まれる情報の適合性に関して、いかなる保証または表明もしません。

**免責事項**

このデモ/ラボには、Microsoft Power BI
の新機能と機能強化の一部のみが含まれています。一部の機能は、製品の将来のリリースで変更される可能性があります。このデモ/ラボでは、新機能のすべてではなく一部について学習します。
