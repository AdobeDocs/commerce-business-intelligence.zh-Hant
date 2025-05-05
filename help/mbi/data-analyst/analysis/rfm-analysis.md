---
title: 時近、頻率、貨幣(RFM)分析
description: 瞭解如何設定儀表板，讓您根據客戶造訪間隔、頻率和貨幣排名來劃分客戶。
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# RFM分析

本主題將示範如何設定儀表板，讓您依據客戶造訪間隔、頻率和貨幣排名來劃分客戶。 RFM分析是一種行銷技術，會考量客戶行為，協助您判斷外聯的分段。 它說明三個方面：

1. 客戶最近從您的商店購買的造訪間隔
1. 訪客向您購買的頻率
1. 客戶花費的金額

![](../../assets/blobid0.png)

只有在新架構上有[!DNL Adobe Commerce Intelligence] Pro計畫時（例如，如果在`Manage Data`功能表下有`Data Warehouse Views`選項），才能設定RFM分析。 可從&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;頁面建立這些資料行。 詳細指示如下。

## 快速入門

您必須先上傳只包含主索引鍵（值為1）的檔案。 這允許建立一些分析所需的計算欄。

您可以使用此[文章](../importing-data/connecting-data/using-file-uploader.md)及下方影像來格式化您的檔案。

## 計算欄

如果您的企業允許訪客訂購，則需作進一步的區分。 若是如此，您可以忽略`customer_entity`資料表的所有步驟。 如果不允許客體訂單，請忽略`sales_flat_order`資料表的所有步驟。

要建立的欄

* **`Sales_flat_order/customer_entity`**&#x200B;資料表
* `Customer's last order date`
* [!UICONTROL Column type]： `Many to one > Max`
* [!UICONTROL Pat]： `sales_flat_order.customer_id > customer_entity.entity_id`
* 已選取[!UICONTROL column]： `created_at`
* [!UICONTROL Filter]： `Orders we count`

* &#x200B;
  自客戶上次訂購日期起    秒
  * [!UICONTROL Column type]： -     「相同表格>年齡
* 已選取[!UICONTROL column]： `Customer's last order date`

* （輸入）計數參考
* [!UICONTROL Column type]： `Same table > Calculation`
* &#x200B;
  [!UICONTROL 輸入]: `entity_id`
* [!UICONTROL Calculation]： `**case when A is null then null else 1 end**`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* **計數參考**&#x200B;資料表（這是您以數字「1」上傳的檔案）
* 客戶數量
* [!UICONTROL Column type]： `Many to One > Count Distinct`
* [!UICONTROL Path]： `ales_flat_order.(input) reference > Count reference.Primary Key`或`customer_entity.(input)reference > Count Reference`。`Primary Key`
* 已選取[!UICONTROL column]： `sales_flat_order.customer_email`或`customer_entity.entity_id`

* **Customer_entity**&#x200B;表格
* 客戶數量
* [!UICONTROL Column type]： `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]： `customer_entity`。（輸入）參考資料>客戶集中度。`Primary Key`
* 已選取[!UICONTROL column]： `Number of customers`

* （輸入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]： `Same table > Event Number`
* [!UICONTROL Event owner]： `(input) reference for count`
* [!UICONTROL Event rank]： `Customer's lifetime revenue`

* 依客戶期限收入排名
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `(input) Ranking by customer lifetime revenue`，`Number of customers`
* [!UICONTROL Calculation]： `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* 客戶的貨幣分數（依百分位數）
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `(input) Ranking by customer lifetime revenue`，`Number of customers`
* [!UICONTROL Calculation]： `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* （輸入）依客戶期限訂單數排名
* [!UICONTROL Column type]： `Same table > Event Number`
* [!UICONTROL Event owner]： `(input) reference for count`
* [!UICONTROL Event rank]： `Customer's lifetime number of orders`

* 依客戶期限訂單數排名
* &#x200B;
  [!UICONTROL 欄型別]: – "相同表格>計算"
* [!UICONTROL Inputs]： - **（輸入）依客戶期限訂單數**&#x200B;排名，**客戶數**
* [!UICONTROL Calculation]： - **當A為Null然後為Null時，否則(B-(A-1))結束**
* [!UICONTROL Datatype]： — 整數

* 客戶的頻率分數（依百分位數）
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `(input) Ranking by customer lifetime number of orders`，`Number of customers`
* [!UICONTROL Calculation]： `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* 自客戶上次訂購日期起的秒數排名
* [!UICONTROL Column type]： `Same table > Event Number`
* [!UICONTROL Event owner]： `(input) reference for count`
* [!UICONTROL Event rank]： `Seconds since customer's last order date`

* 客戶的造訪間隔分數（依百分位數）
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `(input) Ranking by customer lifetime number of orders`，`Number of customers`
* [!UICONTROL Calculation]： `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* 客戶的造訪間隔分數（依百分位數）
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `Customer's recency score (by percentiles)`，`Customer's frequency score (by percentiles)`，`Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]： `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* &#x200B;
  [!UICONTROL 資料型別]: String

* **計數參考**&#x200B;資料表
* [!UICONTROL Number of customers]： `(RFM > 0)`
* [!UICONTROL Column type]： `Many to One > Count Distinct`
* [!UICONTROL Path]： `sales_flat_order.(input) reference > Customer Concentration. Primary Key`或`customer_entity.(input)reference > Customer Concentration.Primary Key`
* 已選取[!UICONTROL column]： `sales_flat_order.customer_email`或`customer_entity.entity_id`
* [!UICONTROL Filter]： `Customer's RFM score (by percentile)`不等於000

* **Customer_entity**&#x200B;表格
* [!UICONTROL Number of customers]： `(RFM > 0)`
* [!UICONTROL Column type]： `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]： `customer_entity.(input) reference > Customer Concentration.Primary Key`
* 已選取[!UICONTROL column]： - `Number of customers`

* 客戶的造訪間隔分數`(R+F+M)`
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： - `Customer's recency score (by percentiles)`， `Customer's frequency score (by percentiles)`， `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]： `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* （輸入）依客戶的整體RFM分數排名
* [!UICONTROL Column type]： `Same table > Event Number`
* [!UICONTROL Event owner]： `(input) reference for count`
* [!UICONTROL Event rank]： `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]： `Customer's RFM score (by percentile)`不等於000

* 依客戶的整體RFM分數排名
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `(input) Ranking by customer's overall RFM score`，`Number of customers (RFM > 0)`
* [!UICONTROL Calculation]： `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

* 客戶的RFM群組
* [!UICONTROL Column type]： `Same table > Calculation`
* [!UICONTROL Inputs]： `(input) Ranking by customer lifetime revenue`，`Number of customers`
* [!UICONTROL Calculation]： `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* &#x200B;
  [!UICONTROL 資料型別]: `Integer`

>[!NOTE]
>
>使用的百分位數是客戶的偶數拆分（例如，20%區間會傳回1-5）。 如果您有自訂方式來權衡這些專案，請在提交票證時告知分析人員。

## 量度

沒有新量度！

>[!NOTE]
>
>在建立新報表之前，請務必[將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。

## 報表

* 按RFM群組&#x200B;**客戶**
* 量度`A`： `New customers`
* [!UICONTROL Metric]： `New customers`
* [!UICONTROL Filter]： `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* [!UICONTROL Group by]： `Customer's RFM group`
* &#x200B;
  [!UICONTROL 群組依據]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **具有5個造訪間隔分數的客戶**
* 量度`A`： `New customers`
* [!UICONTROL Metric]： `New customers`
* [!UICONTROL Filter]： `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* 隱藏圖表
* &#x200B;
  [!UICONTROL 群組依據]: `Email`
* [!UICONTROL Group by]： `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **具有一個造訪間隔分數的客戶**
* 量度`A`： `New customers`
* [!UICONTROL Metric]： `New customers`
* [!UICONTROL Filter]： `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* 隱藏圖表
* &#x200B;
  [!UICONTROL 群組依據]: `Email`
* [!UICONTROL Group by]： `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像上面的範例儀表板，但三個產生的表格只是您可執行的客戶細分型別的範例。
