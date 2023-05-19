---
title: 定義客戶集中度
description: 瞭解如何設定控制面板，以幫助您衡量總收入在客戶群中的分配方式。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# 客戶集中度

本主題演示了如何設定控制面板，以幫助您衡量總收入在客戶群中的分配方式。 瞭解客戶貢獻的收入百分比是多少，並建立細分清單，以便為您的高貢獻客戶提供最佳市場和留住他們。

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 入門

您首先需要上載一個只包含一個主鍵的檔案，該主鍵的值為1。 這允許為分析建立一些必要的計算列。

您可以使用 [檔案上載程式](../importing-data/connecting-data/using-file-uploader.md) 和下面的影像來格式化檔案。

## 計算列

如果您位於原始體系結構上(例如，如果您沒有 `Data Warehouse Views` 選項 `Manage Data` )，您希望與支援團隊聯繫以構建以下列。 在新體系結構上，可以從 `Manage Data > Data Warehouse` 的子菜單。 詳細說明如下。

如果您的企業允許客人訂單，則會作進一步的區分。 如果是，可忽略 `customer_entity` 的子菜單。 如果不允許來賓訂單，請忽略 `sales_flat_order` 的子菜單。

要建立的列

* `Sales_flat_order/customer_entity` 表
* （輸入） `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]:- **如果A為null，則為null，則為1結尾**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` 表(這是您上傳的檔案，其編號 `1`)
* 客戶數
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* 路徑 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選定列 —  `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* `customer_entity` 表
* 客戶數
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* 路徑 —  `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選定列 —  `Number of customers`

* （輸入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件級別 —  `Customer's lifetime revenue`

* 客戶的收入百分比
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **如果A為空，則為空，則為空(A/B)* 100結束&#x200B;**
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` 表
* 客戶數
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* 路徑 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選定列 —  `Number of customers`

* （輸入）按客戶生命週期收入排名
* [!UICONTROL Column type]: – `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件級別 —  `Customer's lifetime revenue`
* 篩選器 —  `Customer's order number = 1`

* 客戶的收入百分比
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **如果A為空，則為空，則為空(A/B)* 100結束&#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>使用的百分位數甚至是客戶的分解，表示客戶群的Xth百分位數。 每個客戶都與一個介於1到100之間的整數相關聯，該整數可以視為其生存期收入 *秩*。 例如，如果特定客戶的客戶收入百分點是 **5**，此客戶在 ***第五百分位*** 以終生收入計算。

## 度量

* **客戶生存期總值**
* 在 `customer_entity` 表
* 此度量執行 **和**
* 在 `Customer's lifetime revenue` 列
* 按 `Customer's first order date` 時間戳

## 報告

* **客戶集中度**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL組依據]: `Independent`
* 度量 `A`: `Total customer lifetime revenue by percentile`
* 度量 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 顯示頂部/底部： `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **最高10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 度量 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
   [!UICONTROL組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **最低50%的濃度，僅一次購買**

* 度量 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
   [!UICONTROL組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **底部10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 度量 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
   [!UICONTROL組依據]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與上面的示例儀表板類似。

如果您在構建此分析時遇到任何問題，或者只想與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
