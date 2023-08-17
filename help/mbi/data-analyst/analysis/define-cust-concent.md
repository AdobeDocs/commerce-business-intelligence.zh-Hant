---
title: 定義客戶集中度
description: 瞭解如何設定儀表板，協助您評估總收入如何在客戶群間分配。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# 客戶集中度

此主題示範如何設定儀表板，協助您測量總收入在客戶群之間的分配方式。 瞭解客戶貢獻了多少百分比的收入，並建立分段清單以將市場最佳化並留住貢獻最多的客戶。

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 快速入門

您必須先上傳只包含主索引鍵（值為1）的檔案。 這允許建立一些分析所需的計算欄。

您可以使用 [檔案上傳程式](../importing-data/connecting-data/using-file-uploader.md) 和下圖來格式化您的檔案。

## 計算欄

如果您使用原始架構(例如，如果您沒有 `Data Warehouse Views` 下的選項 `Manage Data` 選單)，您想要聯絡支援團隊以建置以下欄。 在新架構上，這些欄可從以下網址建立： `Manage Data > Data Warehouse` 頁面。 詳細指示如下。

如果您的企業允許訪客訂購，則需作進一步的區分。 如果是，您可以忽略的所有步驟 `customer_entity` 表格。 如果不允許來賓訂單，請忽略的所有步驟 `sales_flat_order` 表格。

要建立的欄

* `Sales_flat_order/customer_entity` 表格
* （輸入） `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]： - **A為null然後為null的情況，否則1結束**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` 表格(這是您上傳的檔案，編號為 `1`)
* 客戶數量
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* 路徑 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key` 或 `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選取的欄 —  `sales_flat_order.customer_email` 或 `customer_entity.entity_id`

* `customer_entity` 表格
* 客戶數量
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* 路徑 —  `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選取的欄 —  `Number of customers`

* （輸入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`

* 客戶的收入百分位數
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]： - **當A為null然後為null時的情況，否則(A/B)* 100個結尾&#x200B;**
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` 表格
* 客戶數量
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* 路徑 —  `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選取的欄 —  `Number of customers`

* （輸入）依客戶期限收入排名
* [!UICONTROL Column type]: – `Same table > Event Number`
* 事件所有者 —  `Number of customers`
* 事件排名 —  `Customer's lifetime revenue`
* 篩選 —  `Customer's order number = 1`

* 客戶的收入百分位數
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]： - **當A為null然後為null時的情況，否則(A/B)* 100個結尾&#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>使用的百分位數是甚至分段的客戶，代表客戶群的第X個百分位。 每個客戶都與1到100的整數相關聯，這可以視為其期限收入 *排名*. 例如，如果特定客戶的客戶收入百分位數為 **5**，此客戶位於 ***第五個百分位數*** 終身收入的所有客戶中。

## 量度

* **客戶期限值總計**
* 在 `customer_entity` 表格
* 此量度會執行 **Sum**
* 在 `Customer's lifetime revenue` 欄
* 排序依據： `Customer's first order date` timestamp

## 報表

* **客戶集中度**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
  [！UICONTROL群組依據]: `Independent`
* 量度 `A`： `Total customer lifetime revenue by percentile`
* 量度 `B`： `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 顯示頂端/底端： `100% of Customer's revenue percentile Name`
* 
  [!UICONTROL Chart type]: `Line`

* **前10%集中**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 量度 `A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
  [！UICONTROL群組依據]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **僅需一次購買即可達到最低50%的集中度**

* 量度 `A`： `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
  [！UICONTROL群組依據]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **底部10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 量度 `A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* 
  [！UICONTROL群組依據]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果可能如上述範例控制面板所示。

如果您在建立此分析時遇到任何問題，或只是想與Professional Services團隊互動， [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
