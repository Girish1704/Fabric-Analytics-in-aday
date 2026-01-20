# Microsoft Fabric - Fabric Analyst in a Day - Lab 3

![](../media/Lab-03/l3.png)

# Contents

- Introduction

- Shortcut to ADLS Gen2

  - Task 1: Create Shortcut

- Transform data using Visual Query

  - Task 2: Create Geo view using Visual Query

  - Task 3: Create Reseller view using Visual Query

  - Task 4: Create Sales view using Visual query

  - Task 5: Create Product view using Visual query

- References

# Introduction 

In our scenario, Sales Data comes from the ERP system and is stored in an ADLS Gen2. It gets updated at noon / 12 PM every day. We need to transform and ingest this data into Lakehouse and use it in our model.

There are multiple ways to ingest this data.

- **Shortcuts:** This creates a link to the data, and we can use Visual query views to transform it. We are going to use Shortcuts in this lab.

- **Notebooks:** This requires us to write code. It is a developer friendly approach.

- **Dataflow Gen2:** You are probably familiar with Power Query or Dataflow Gen1. Dataflow Gen2, as the name indicates, is the newer version of Dataflow. It provides all the capabilities of Power Query / Dataflow Gen1 with the added ability to transform and ingest data into multiple data sources. We are going to introduce this in the next couple of labs.

- **Pipeline:** This is an orchestration tool. Activities can be orchestrated to extract, transform, and ingest data. We will be using a pipeline to execute Dataflow Gen2 activity which in turn will perform extraction, transformation, and ingestion.

We will start by creating a Shortcut to ingest data into a Lakehouse from ADLS Gen2 data source. Once ingested, we are going to use Visual query views to transform it.

By the end of this lab, you will have learned:

- How to create Shortcuts in your Lakehouse

- How to transform data using the Visual query feature

# Shortcut to ADLS Gen2

## Task 1: Create Shortcut

Shortcuts are used to create a link to the target location. Shortcuts provide access to the data without needing to physically move the data into the lakehouse. This is like creating shortcuts in Windows desktop.

1. In the top of your screen select the **lh_FAIAD** tab to navigate to the Lakehouse.

    >**Note:** If you don't have a tab you can navigate back to your Workspace and open the Lakehouse from there.

2. In the **Explorer** panel, select the **ellipsis** next to
    **Tables**.

3. Select **New Shortcut.**

    ![](../media/Lab-03/image6.png)

4. **New Shortcut** dialog opens. Under **External sources**, select
    **Azure Data Lake Storage Gen2**.

    ![](../media/Lab-03/image7.png)

5. Select **New connection (1)**.

6. Enter the following link for the **URL** property: https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales **(2)**

7. Click on **Create New Connection (3)** under the Connection section

8. Select **Shared Access Signature (SAS) (4)** from the Authentication
    kind dropdown.

9. Copy the SAS token and paste it into the SAS token (5) field.

    - **SAS token:** <inject key="Sas token"></inject>

10. Select **Next (6)** on the bottom right of the screen.

    ![](../media/Lab-03/image8.png)

11. You will be connected to ADLS Gen2 with the directory structuredisplayed in the left panel. Expand **Delta-Parquet-Format-FY25 (1)**.

12. Select the following directories **(2)** and then click on
    **Next (3):**

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

    >**Note:** Sales.Invoices_May is the only directory that is **not** selected.

    ![](../media/Lab-03/image9.png)

13. You will be navigated to the next dialog where we can edit the
    names. Select the **Edit icon (1)** under Actions for
    **Application.Cities**.

14. Rename **Application.Cities to Cities (2).**

15. Select the check mark next to the name to save the change **(3)**.

    ![](../media/Lab-03/image10.png)

16. Similarly, rename the Shortcut Names as below:

    a. Application.Countries to **Countries**

    b. Application.StateProvinces to **States**

    c. DateDim to **Date**

    d. Sales.BuyingGroups to **BuyingGroups**

    e. Sales.Customers to **Customers**

    f. Sales.InvoiceLines to **InvoiceLineItems**

    g. Sales.Invoices to **Invoices**

    h. Warehouse.StockGroups to **ProductGroups**

    i. Warehouse.StockItemStockGroups to **ProductItemGroup**

    j. Warehouse.StockItems to **ProductItem**

    > **Note**: Double check the names. A typo will cause errors during the lab.

17. Select **Create** to create the Shortcut.

    ![](../media/Lab-03/image11.png)

18. Notice all the Shortcuts are created as Tables. Select **BuyingGroups** table and notice we can see a preview of the data in the data panel.

    ![](../media/Lab-03/image12.png)

The next step is to transform the data, so we can create a semantic model. We are going to create views to transform the data.

# Transform data using Visual Query

## Task 2: Create Geo view using Visual Query

1. We can access the Lakehouse using a SQL endpoint. This provides the ability to query the data and create views. On the **top right** of the screen, select **Lakehouse (1) -\> SQL analytics endpoint (2)**.

    ![](../media/Lab-03/image13.png)

    You will be navigated to SQL analytics endpoint. You have a new item now in your top navigation and can move back to the Lakehouse by selecting
    that tab. Notice the Explorer panel has changed. You now can create views, stored procedures, queries and more. We are going to create a visual query as it provides a low code, like Power Query, interface. We
    will save the result as a view.

    We will start by creating a Geo view. We need to merge data from the Cities, States and Countries tables to create the Geo view.

2. From the top menu, click the drop down next to **New SQL query (1)** and then select **New visual query (2)**.

    ![](../media/Lab-03/image14.png)

3. To build a query, we need to add tables to the Visual Query panel. Click on the ellipsis next to the **Cities (1)** table and select **Insert into canvas (2).**

    ![](../media/Lab-03/image15.png)

4. Repeat the same steps for the **States** and **Countries** tables.

    Next, we need to merge these queries. The visual query editor comes with the option to use Power Query editor. Let's use this, since we are familiar with this because of Power BI.

5. **From the menu in Visual query editor**, select the **Open in popup** icon (towards the right). You will be navigated to Power Query editor.
    
    >**Note:** You may have to scroll to the right or re-open your visual query tab if you do not immediately see this icon.

    ![](../media/Lab-03/image16.png)

6. With **Cities (1)** query selected, from the Power Query editor ribbon, select **Home (2) -> Combine (3) -> Merge queries dropdown (4) -> Merge queries as new (5)**. Merge queries dialog opens.

    ![](../media/Lab-03/image17.png)

7. In the **Left table for merge**, select **Cities**.

8. In the **Right table for merge**, select **States**.

9. Select **StateProvinceID** columns from both the tables. We are going to join using this column.

10. Select **Inner** as the **Join kind**.

11. Select **OK.**

    ![](../media/Lab-03/image18.png)

    Notice a new query called **Merge** has been created. We need a few columns from States.

12. In the **Data view** (bottom panel), click on the **double arrow** next to the **States** column (last column to the right).

13. A panel opens. Ensure that the only selected columns are the
    following:

    a. StateProvinceCode

    b. StateProvinceName

    c. CountryID

    d. SalesTerritory

14. Select **OK**.

    ![](../media/Lab-03/image19.png)

15. We need to merge Countries query now. With the Merge query selected **(1)**, select **Home (2) -> Combine (3) -> Merge queries dropdown (4) -> Merge queries (5)**.

    ![](../media/Lab-03/image20.png)

16. Merge query dialog opens. In the **Right table for merge**, select **Countries**.

17. Select **CountryID** columns from both the tables. We are going to join using this column.

18. Select **Inner** as the **Join kind**.

19. Select **OK.**

    ![](../media/Lab-03/image21.png)

    We need a few columns from Countries.

20. In the **Data view** (bottom panel), click on the **double arrow** next to the **Countries** column.

21. A panel opens. Ensure that the only selected columns are the following:

    a. CountryName

    b. FormalName

    c. IsoAlpha3Code

    d. IsoNumericCode

    e. CountryType

    f. Continent

    g. Region

    h. Subregion

22. Select **OK**.

    >**Important:** Make sure to scroll down and select all eight columns listed in step 21. The screenshot below only displays the first 5 columns due to a UI limitation.

    ![](../media/Lab-03/image22.png)

    We do not need all the columns in the **Merge** table. Make sure to only select those that we need.

23. With **Merge** query selected (1), from the ribbon select **Home (2) -> Choose columns (3) -> Choose columns (4)**.

    >**Note:** If the Choose columns option is not visible, you can find it under Manage columns.

    ![](../media/Lab-03/image23.png)

24. Choose columns dialog opens. **Uncheck** the following columns.

    a. StateProvinceID

    b. Location

    c. LastEditedBy

    d. ValidFrom

    e. ValidTo

    f. CountryID

25. Select **OK**.

    ![](../media/Lab-03/image24.png)

    Notice the process is like Power Query, we have all the steps recorded both in the Applied Steps panel on the right and the visual view. Let's rename Merge query and Enable load, so that the data is loaded from this query.

26. **Right-click** on the **Merge** query in the Queries (left) panel. Select **Rename** and rename the query to **Geo**.

27. **Right-click** on the **Geo** query in the Queries (left) panel. Select **Enable Load** to enable this query.

28. Make sure that the Cities, States and Countries queries are **disabled**.

29. Select **Save**, found in the bottom right of the power query editor.

    ![](../media/Lab-03/image25.png)

    We will be navigated to the Visual query editor. Let's now save this query as a view.

    >**Note:** All the steps we performed using Power Query editor can be performed using Visual query editor as well.

30. From the Visual query editor menu select **Save as view**.

    ![](../media/Lab-03/image26.png)

    Save as view dialog opens. Notice the SQL query is available. You can review it if you want to verify the SQL code.

31. Enter **Geo** as **View name**.

32. Select **OK** to save the view.

    ![](../media/Lab-03/image27.png)

    You will get an alert once the view is saved.

33. In the Explorer (left) panel, expand **Views.** We have the newly created Geo view.

    ![](../media/Lab-03/image28.png)

## Task 3: Create Reseller view using Visual Query

Let's create the Reseller view which is created by merging Customers
table with the BuyingGroups table. This time around we will create the
view using Visual query without opening the Power Query option.

1. From the top menu, click the drop down next to **New SQL query (1)** and then select **New visual query (2)**.

2. To build a query, we need to add tables to the Visual Query panel. Click on the ellipsis next to the **BuyingGroups (1)** table and select **Insert into canvas (2)**.

    ![](../media/Lab-03/image29.png)

3. Repeat the same steps for the **Customers** table.

4. **Select the Customers** query. When selected, Customers will have a "**+**" sign after Table (this indicates we are adding a step after Table. If you do not see the **"+"** sign after table, you may have selected a different step. Select Table and you will be good to go).

5. From the Visual query menu, select **Combine -\> Merge queries**.

    ![](../media/Lab-03/image30.png)

    The Merge dialog opens with Customers selected as the top table.

6. In the **Right table for merge**, select **BuyingGroups**.

7. Select **BuyingGroupID** columns from both the tables. We are going to join using this column.

8. Select **Inner** as the **Join kind**.

9. Select **OK**.

    ![](../media/Lab-03/image31.png)

10. In the **Data view** (bottom panel), click on the **double arrow** next to the **BuyingGroups** column (last column to the right) to select the columns we need from BuyingGroups.

11. A panel opens. **Select the** **BuyingGroupName** column.

12. Select **OK**.

    ![](../media/Lab-03/image32.png)

    We do not need all the columns in our Customer table. Let's select only those we need.

13. From the Visual query menu, select **Manage columns -\> Choose columns**.

    ![](../media/Lab-03/image33.png)

14. Choose columns dialog opens. **Select** the following columns.

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

15. Select **OK**.

    ![](../media/Lab-03/image34.png)

16. Let's rename BuyingGroupName column. In the **Data view, double-click on BuyingGroupName** column header to make it editable.

17. **Rename** the column to **ResellerCompany**.

    ![](../media/Lab-03/image35.png)

    Notice the Customer table has all the steps documented. Now let's save this view.

18. We need to save the Customers query as it has all the steps. We need to Enable load. Select the **ellipsis** in the **Customers** query box.

19. Make sure **Enable load** is checked.

    ![](../media/Lab-03/image36.png)

    >**Note**: The **Customer** box should have a blue border, if enable load is checked.

20. From the Visual query menu, select **Save as view**.

    ![](../media/Lab-03/image37.png)

    Save as view dialog opens. Notice the SQL query is available. You can
    review it, if you select it.

21. Enter **Reseller** as **View name**.

22. Select **OK** to save the view.

    ![](../media/Lab-03/image38.png)

    You will get an alert once the view is saved.

23. In the Explorer (left) panel, expand **Views.** We have the newly created Reseller view.

    ![](../media/Lab-03/image39.png)

## Task 4: Create Sales view using Visual query

Let's create the Sales view, which is created by merging the tables
InvoiceLineItems and Invoices with the Reseller view. We have this query
in Power BI Desktop. We will copy the code from the Advanced Editor. But
before copying the code, we need to create a merge table using Visual
query as creating a blank query is not possible in Visual query. Let's
give this method a try.

1. From the top menu, click the drop down next to **New SQL query** and then select **New visual query**.
    
    ![](../media/Lab-03/image40.png)

2. From the **Explorer -> Table** section, we need to add tables to the Visual Query panel. Click on the ellipsis next to the **InvoiceLineItems** table and select **Insert into canvas**.

3. Repeat the same steps for the **Invoices** table.

4. From the **Explorer -> Views** section, we need to add tables to the Visual Query panel. Click on the ellipsis next to the **Reseller** table and select **Insert into canvas**.

5. From the Visual query editor, select the **Open in popup** to open Power Query editor.

    ![](../media/Lab-03/image41.png)

6. With **InvoiceLineItems** query selected, from the ribbon select **Home (2) -> Combine (3) -> Merge queries dropdown (4) -> Merge queries as new (5).** Merge queries dialog opens.

    ![](../media/Lab-03/image42.png)

7. In the **Left table for merge**, select **InvoiceLineItems**.

8. In the **Right table for merge**, select **Invoices**.

9. Select **InvoiceID** columns from both the tables. We are going to join using this column.

10. Select **Inner** as the **Join kind**.

11. Select **OK**.

    ![](../media/Lab-03/image43.png)

    We are going to copy code from Power BI Desktop and paste it using the Advanced Editor.

12. If you have not already opened it, open **FAIAD.pbix** located in the **Reports** folder on the desktop of your lab environment.

13. From the ribbon select **Home -> Transform data**. Power Query window opens. As you have noticed in the earlier lab, queries in the left panel are organized by data source.

    ![](../media/Lab-03/image44.png)

14. From the left **Queries** panel, under the **ADLSData** **(1)** folder, select **Sales (2)** query.

15. From the ribbon select **Home -> Advanced Editor (3)** and the Advanced Editor dialog will open.

    ![](../media/Lab-03/image45.png)

    >**Note:** If you're unable to find the Advanced Editor, you can access it under **Home -\> Query -\> Advanced Editor**.

16. **Select code from Line 3** (#!"Expanded Invoice" ...) all the way through to the last line of code.

17. **Right-click** and select **Copy**.

18. Select **Cancel** to close Advanced Editor.

    ![](../media/Lab-03/image46.png)

19. **Navigate back to the browser** where you have the Power Query Editor open.

20. Make sure you have **Merge** query selected.

21. From the ribbon select **Home -\> Advanced Editor**. Advanced Editor dialog opens.

    ![](../media/Lab-03/image47.png)

    >**Note:** If you're unable to find the Advanced Editor, you can access it under **Home -\> Query -\> Advanced Editor**.

22. At the **end of line 2 add a comma** (Source = Table.NestedJoin(InvoiceLineItems, {"InvoiceID"}, Invoices, {"InvoiceID"}, "Invoices", JoinKind.Inner)**,**

23. Click **Enter** to start a new line.

24. Enter **Ctrl+V** on your keyboard to paste the code you copied from
    Power BI Desktop.

    >**Note**: If you are working in the lab environment, please select the **ellipsis (...)** on the top right of the screen. Use the slider to **enable** **VM Native Clipboard**. Select OK in the dialog. Once done pasting the queries you can disable this option.

    ![](../media/Lab-03/image48.png)

    ![](../media/Lab-03/image49.png)

25. Highlight the last two lines of code (in Source) and **delete** it.

26. Select **OK** to save the changes.

    ![](../media/Lab-03/image50.png)

    If it is easier, delete all the code in the Advanced Editor and paste
    the below code into Advanced Editor.

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

27. You will be navigated back to the Power Query Editor. In the left, Queries panel, **double-click on Merge** query to rename it.

28. **Rename** Merge query to **Sales**.

29. Right-click on Sales query and select **Enable load** to enable the query to be loaded.

    ![](../media/Lab-03/image51.png)

30. Select **Save** to Save and Close the Power Query dialog. You will be navigated to the Visual query editor.

31. From the Visual query menu, select **Save as view**. Save as view dialog opens. Notice the SQL query is available. You can review it, if you choose it.

32. Enter **Sales** as **View name (1)**.

33. Select **OK (2)** to save the view.

    ![](../media/Lab-03/image52.png)

    You will get an alert once the view is saved.

34. In the Explorer (left) panel, expand **Views.** We have the newly created Sales view.

    ![](../media/Lab-03/image53.png)

## Task 5: Create Product view using Visual query

Let's create the Product view, which is created by merging
**ProductItem**, **ProductItemGroup** and **ProductGroups** tables. To move things along, we are going to copy code into Advanced Editor.

1. From the top menu, click the drop-down next to **New SQL query (1)** and then select **New visual query (2).**

    ![](../media/Lab-03/image54.png)

2. From Explorer section, we need to add tables to the Visual Query panel. Click on the ellipsis next to the **ProductItem (1)** table and select **Insert into canvas (2)**.

    ![](../media/Lab-03/image55.png)

3. Repeat the same steps for the **ProductItemGroup** and **ProductGroups** tables.

4. From the Visual query editor, select the **Open in popup** to open Power Query editor.

    ![](../media/Lab-03/image56.png)

5. With **ProductItem** query selected **(1)**, from the ribbon select **Home (2) -\> Combine (3) -\> Merge queries dropdown (4) -\> Merge queries as new (5).** Merge dialog opens.

    ![](../media/Lab-03/image57.png)

6. In the **Left table for merge**, select **ProductItem**.

7. In the **Right table for merge**, select **ProductItemGroup**.

8. Select **StockItemID** columns from both the tables. We are going to join using this column.

9. Select **Left outer** as the **Join kind**.

10. Select **OK.** New Merge query is created.

    ![](../media/Lab-03/image58.png)

11. With Merge query selected, from the ribbon, select **Home -\> Advanced editor**. Advanced editor dialog opens.

    ![](../media/Lab-03/image59.png)

    >**Note:** If you're unable to find the Advanced Editor, you can access it under **Home -\> Query -\> Advanced Editor**.

12. **Select all the code** in Advanced editor and **delete** it.

13. **Paste** the below code into Advanced editor.

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

14. Select **OK** to close Advanced Editor. You will be navigated back to Power Query editor.

    ![](../media/Lab-03/image60.png)

15. In the Queries panel on the left, **double-click on Merge** query to rename it.

16. **Change the name** of the Merge query to **Product**.

17. Right-click on Product query and select **Enable load** to enable the query to be loaded.

18. Select **Save** to Save and Close the Power Query dialog. You will be navigated to Visual query.

    ![](../media/Lab-03/image61.png)

19. From the Visual query menu, select **Save as view**. Save as view dialog opens. Notice the SQL query is available. You can review it, if you choose it.

20. Enter **Product** as **View name**.

21. Select **OK** to save the view.

    ![](../media/Lab-03/image62.png)

    You will get an alert once the view is saved.

22. In the Explorer (left) panel, expand **Views.** We have the newly created Product view.

    ![](../media/Lab-03/image63.png)

We have transformed the data from ADLS Gen2 data source. In this lab, we learned how to create shortcuts and explored various options for using visual query views to transform data.

In the next lab, we will learn how to use Dataflow Gen2 and create Shortcut to another Lakehouse.

# References

Fabric Analyst in a Day (FAIAD) introduces you to some of the key functions available in Microsoft Fabric. In the menu of the service, the Help (?) section has links to some great resources.

![](../media/Lab-03/image64.png)

Here are a few more resources that will help you with your next steps with Microsoft Fabric.

- See blog to read the full [Microsoft Fabric GA announcement](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Explore Fabric through the [Guided Tour](https://aka.ms/Fabric-GuidedTour)

- Sign up for the [Microsoft Fabric free trial](https://aka.ms/try-fabric)

- Visit the [Microsoft Fabric website](https://aka.ms/microsoft-fabric)

- Learn new skills by exploring the [Fabric Learning modules](https://aka.ms/learn-fabric)

- Explore the [Fabric technical documentation](https://aka.ms/fabric-docs)

- Read the [free e-book on getting started with Fabric](https://aka.ms/fabric-get-started-ebook)

- Join the [Fabric community](https://aka.ms/fabric-community) to post your questions, share your feedback, and learn from others

Read the more in-depth Fabric experience announcement blogs:

- [Data Factory experience in Fabric blog](https://aka.ms/Fabric-Data-Factory-Blog)

- [Synapse Data Engineering experience in Fabric blog](https://aka.ms/Fabric-DE-Blog)

- [Synapse Data Science experience in Fabric blog](https://aka.ms/Fabric-DS-Blog)

- [Synapse Data Warehousing experience in Fabric blog](https://aka.ms/Fabric-DW-Blog)

- [Synapse Real-Time Analytics experience in Fabric blog](https://aka.ms/Fabric-RTA-Blog)

- [Power BI announcement blog](https://aka.ms/Fabric-PBI-Blog)

- [Data Activator experience in Fabric blog](https://aka.ms/Fabric-DA-Blog)

- [Administration and governance in Fabric blog](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)

- [Dataverse and Microsoft Fabric integration blog](https://aka.ms/Dataverse-Fabric-Blog)

© 2025 Microsoft Corporation. All rights reserved.
By using this demo/lab, you agree to the following terms:

The technology/functionality described in this demo/lab is provided by
Microsoft Corporation for purposes of obtaining your feedback and to
provide you with a learning experience. You may only use the demo/lab
to evaluate such technology features and functionality and provide
feedback to Microsoft. You may not use it for any other purpose. You
may not modify, copy, distribute, transmit, display, perform,
reproduce, publish, license, create derivative works from, transfer,
or sell this demo/lab or any portion thereof.

COPYING OR REPRODUCTION OF THE DEMO/LAB (OR ANY PORTION OF IT) TO ANY
OTHER SERVER OR LOCATION FOR FURTHER REPRODUCTION OR REDISTRIBUTION IS
EXPRESSLY PROHIBITED.

THIS DEMO/LAB PROVIDES CERTAIN SOFTWARE TECHNOLOGY/PRODUCT FEATURES
AND FUNCTIONALITY, INCLUDING POTENTIAL NEW FEATURES AND CONCEPTS, IN A
SIMULATED ENVIRONMENT WITHOUT COMPLEX SET-UP OR INSTALLATION FOR THE
PURPOSE DESCRIBED ABOVE. THE TECHNOLOGY/CONCEPTS REPRESENTED IN THIS
DEMO/LAB MAY NOT REPRESENT FULL FEATURE FUNCTIONALITY AND MAY NOT WORK
THE WAY A FINAL VERSION MAY WORK. WE ALSO MAY NOT RELEASE A FINAL
VERSION OF SUCH FEATURES OR CONCEPTS. YOUR EXPERIENCE WITH USING SUCH
FEATURES AND FUNCITONALITY IN A PHYSICAL ENVIRONMENT MAY ALSO BE
DIFFERENT.

**FEEDBACK**. If you give feedback about the technology features,
functionality and/or concepts described in this demo/lab to Microsoft,
you give to Microsoft, without charge, the right to use, share and
commercialize your feedback in any way and for any purpose. You also
give to third parties, without charge, any patent rights needed for
their products, technologies and services to use or interface with any
specific parts of a Microsoft software or service that includes the
feedback. You will not give feedback that is subject to a license that
requires Microsoft to license its software or documentation to third
parties because we include your feedback in them. These rights survive
this agreement.

MICROSOFT CORPORATION HEREBY DISCLAIMS ALL WARRANTIES AND CONDITIONS
WITH REGARD TO THE DEMO/LAB, INCLUDING ALL WARRANTIES AND CONDITIONS
OF MERCHANTABILITY, WHETHER EXPRESS, IMPLIED OR STATUTORY, FITNESS FOR
A PARTICULAR PURPOSE, TITLE AND NON-INFRINGEMENT. MICROSOFT DOES NOT
MAKE ANY ASSURANCES OR REPRESENTATIONS WITH REGARD TO THE ACCURACY OF
THE RESULTS, OUTPUT THAT DERIVES FROM USE OF DEMO/ LAB, OR SUITABILITY
OF THE INFORMATION CONTAINED IN THE DEMO/LAB FOR ANY PURPOSE.

**DISCLAIMER**

This demo/lab contains only a portion of new features and enhancements
in Microsoft Power BI. Some of the features might change in future
releases of the product. In this demo/lab, you will learn about some,
but not all, new features.


