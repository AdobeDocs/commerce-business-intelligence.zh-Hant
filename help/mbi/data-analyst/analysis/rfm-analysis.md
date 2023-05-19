---
title: 頻率、頻率、貨幣(RFM)分析
description: 瞭解如何設定控制板，使您能夠按客戶的近期、頻率和貨幣排名對客戶進行細分。
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# RFM分析

本主題演示了如何設定儀表板，使您能夠按客戶的近期、頻率和貨幣排名對客戶進行細分。 RFM分析是一種營銷技術，它將客戶行為考慮在內，以幫助您確定外聯細分。 它涉及三個方面：

1. 瞭解客戶最近從您的商店購買的時間
1. 他們從你那裡購買的頻率
1. 客戶支出的貨幣

![](../../assets/blobid0.png)

只有在具有 [!DNL Adobe Commerce Intelligence] 針對新體系結構進行專業規劃(例如，如果您 `Data Warehouse Views` 選項 `Manage Data` )的正平方根。 這些列可從 **[!DNL Manage Data > Data Warehouse]** 的子菜單。 詳細說明如下。

## 入門

您首先需要上載一個只包含一個主鍵的檔案，該主鍵的值為1。 這允許為分析建立一些必要的計算列。

你可以使用 [文章](../importing-data/connecting-data/using-file-uploader.md) 和下面的影像來格式化檔案。

## 計算列

如果您的企業允許客人訂單，則會作進一步的區分。 如果是，可忽略 `customer_entity` 的子菜單。 如果不允許來賓訂單，請忽略 `sales_flat_order` 的子菜單。

要建立的列

* **`Sales_flat_order/customer_entity`** 表
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* 已選擇 [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       自客戶上次訂單日期以來的秒數
   * [!UICONTROL Column type]:- &quot;相同表>年齡
* 已選擇 [!UICONTROL column]: `Customer's last order date`

* （輸入）計數引用
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL輸入]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [!UICONTROL資料類型]: `Integer`

* **計數引用** 表（這是您上傳的檔案，編號為「1」）
* 客戶數
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` 或 `customer_entity.(input)reference > Count Reference`。 `Primary Key`
* 已選擇 [!UICONTROL column]: `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* **客戶實體** 表
* 客戶數
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.（輸入）參考>客戶集中。 `Primary Key`
* 已選擇 [!UICONTROL column]: `Number of customers`

* （輸入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* 按客戶生存期收入排名
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL資料類型]: `Integer`

* 客戶的貨幣分數（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL資料類型]: `Integer`

* （輸入）按客戶生存期訂單數排序
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* 按客戶生存期訂單數排序
* 
   [!UICONTROL列類型]: – "同一表>計算"
* [!UICONTROL Inputs]:- **（輸入）按客戶生存期訂單數排序**。 **客戶數**
* [!UICONTROL Calculation]:- **如果A為null，則為空，則結束(B-(A-1))**
* [!UICONTROL Datatype]: — 整數

* 客戶的頻率分數（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL資料類型]: `Integer`

* 自客戶上次訂單日期以來按秒排序
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* 客戶的收入分數（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL資料類型]: `Integer`

* 客戶的收入分數（按百分比）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [!UICONTROL資料類型]: String

* **計數引用** 表
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 已選擇 [!UICONTROL column]: `sales_flat_order.customer_email` 或 `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 不等於000

* **客戶實體** 表
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* 已選擇 [!UICONTROL column]:- `Number of customers`

* 客戶的收入分數 `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [!UICONTROL資料類型]: `Integer`

* （輸入）按客戶總體RFM得分排序
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 不等於000

* 按客戶的總RFM得分排名
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL資料類型]: `Integer`

* 客戶的RFM組
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [!UICONTROL資料類型]: `Integer`

>[!NOTE]
>
>使用的百分位數甚至會分解客戶（例如，返回1-5的20%時段）。 如果您有自定義的方式想對這些票證進行加重，請在提交票證時告知分析師。

## 度量

沒有新的指標！

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **按RFM分組劃分的客戶**
* 度量 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* [!UICONTROL Group by]: `Customer's RFM group`
* 
   [!UICONTROL組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **具有五個最近分的客戶**
* 度量 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* 隱藏圖表
* 
   [!UICONTROL組依據]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **具有一個最近分的客戶**
* 度量 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* 隱藏圖表
* 
   [!UICONTROL組依據]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與上面的示例儀表板相似，但三個生成的表只是您可以執行的客戶細分類型的示例。
