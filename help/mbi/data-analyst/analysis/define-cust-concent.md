---
title: 定義客戶集中度
description: 了解如何設定控制面板，協助您測量總收入在客戶群中的分配方式。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# 客戶集中度

在本文中，我們示範如何設定控制面板，以協助您評估總收入在客戶群中的分配方式。 了解客戶貢獻的收入百分比，並建立分段清單，以便將市場最佳化，並留住高貢獻的客戶。

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入門

首先，您必須上傳僅包含主索引鍵且值為1的檔案。 這可建立一些分析所需的計算欄。

您可以善用 [檔案上傳程式](../importing-data/connecting-data/using-file-uploader.md) 以及下方的影像，以設定檔案格式。

## 計算欄

如果您位在原始架構上(例如，如果您沒有 `Data Warehouse Views` 選項 `Manage Data` 功能表)，您會想要聯絡我們的支援團隊以建置下列欄。 在新架構上，可從 `Manage Data > Data Warehouse` 頁面。 詳細說明如下。

如果貴公司允許客戶訂購，則會作進一步區分。 若是如此，您可以忽略 `customer_entity` 表格。 如果不允許來賓訂單，請忽略 `sales_flat_order` 表格。

要建立的列

* `Sales_flat_order/customer_entity` 表格
* （輸入） `reference`
* [!UICONTROL Column type]:- `Same table > Calculation`
* [!UICONTROL Inputs]:- `entity_id`
* [!UICONTROL Calculation]:- **當A為Null時則為Null，否則為1結尾**
* [!UICONTROL Datatype]:- `Integer`

* `Customer concentration` 表格(這是您剛上傳的檔案，其編號為 `1`)
* 客戶數
* [!UICONTROL Column type]:- `Many to One > Count Distinct`
* 路徑 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選定列 —  `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* `customer_entity` 表格
* 客戶數
* [!UICONTROL Column type]:- `One to Many > JOINED_COLUMN`
* 路徑 —  `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選定列 —  `Number of customers`

* （輸入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]:- `Same table > Event Number`
* 事件擁有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`

* 客戶的收入百分位數
* [!UICONTROL Column type]:- `Same table > Calculation`
* [!UICONTROL Inputs]:- `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **當A為Null然後為Null時的大小寫(A/B)* 100結束&#x200B;**
* [!UICONTROL Datatype]:- `Decimal`

* `Sales_flat_order` 表格
* 客戶數
* [!UICONTROL Column type]:- `One to Many > JOINED_COLUMN`
* 路徑 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選定列 —  `Number of customers`

* （輸入）依客戶期限收入排名
* [!UICONTROL Column type]:- `Same table > Event Number`
* 事件擁有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`
* 篩選 —  `Customer's order number = 1`

* 客戶的收入百分位數
* [!UICONTROL Column type]:- `Same table > Calculation`
* [!UICONTROL Inputs]:- `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **當A為Null然後為Null時的大小寫(A/B)* 100結束&#x200B;**
* [!UICONTROL Datatype]:- `Decimal`

>[!NOTE]
>
>使用的百分位數甚至是客戶的分割，代表您客戶群的第X個百分位數。 每個客戶都會與一個1到100的整數相關聯，這可視為其終身收入 *排名*. 例如，如果特定客戶的客戶收入百分位數為 **5**，此客戶位於 ***第5個百分位數*** 按終身收入計算。

## 量度

* **客戶期限值總計**
* 在 `customer_entity` 表格
* 此量度會執行 **總和**
* 在 `Customer's lifetime revenue` 欄
* 由 `Customer's first order date` timestamp

## 報表

* **客戶集中度**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL分組依據]: `Independent`
* 量度 `A`: `Total customer lifetime revenue by percentile`
* 量度 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 顯示頂部/底部： `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **前10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 量度 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
   [!UICONTROL分組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **最低50%集中，只購買一次**

* 量度 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
   [!UICONTROL分組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **最下10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 量度 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
   [!UICONTROL分組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結束結果可能類似於上述範例控制面板。

如果您在建立此分析時遇到任何問題，或只是想與我們的專業服務團隊接洽， [聯絡支援](../../guide-overview.md).
