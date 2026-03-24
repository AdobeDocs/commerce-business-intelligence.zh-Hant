---
title: 定義客戶集中度
description: 瞭解如何設定儀表板，協助您評估總收入如何在客戶群間分配。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/kayq-ci-AiHHgNoaX09h6dqKQX14MudLvEqFmos3hQE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 0%

---

# 客戶集中度

此主題示範如何設定儀表板，協助您測量總收入在客戶群之間的分配方式。 瞭解客戶貢獻了多少百分比的收入，並建立分段清單以將市場最佳化並留住貢獻最多的客戶。

此分析包含[進階計算資料行](../data-warehouse-mgr/adv-calc-columns.md)。

## 快速入門

您必須先上傳只包含主索引鍵（值為1）的檔案。 這允許建立一些分析所需的計算欄。

您可以使用[檔案上傳程式](../importing-data/connecting-data/using-file-uploader.md)及下列影像來格式化您的檔案。

## 計算欄

如果您使用原始架構（例如，如果您的「`Data Warehouse Views`」功能表下沒有「`Manage Data`」選項），您想要聯絡支援團隊以建置以下欄。 在新架構上，可從`Manage Data > Data Warehouse`頁面建立這些欄。 詳細指示如下。

如果您的企業允許訪客訂購，則需作進一步的區分。 若是如此，您可以忽略`customer_entity`資料表的所有步驟。 如果不允許客體訂單，請忽略`sales_flat_order`資料表的所有步驟。

要建立的欄

* `Sales_flat_order/customer_entity`資料表
* （輸入） `reference`
* [!UICONTROL Column type]： - `Same table > Calculation`
* [!UICONTROL Inputs]： - `entity_id`
* [!UICONTROL Calculation]： - **當A為null然後null時，則為1結束**
* [!UICONTROL Datatype]： - `Integer`

* `Customer concentration`資料表（這是您以數字`1`上傳的檔案）
* 客戶數量
* [!UICONTROL Column type]： - `Many to One > Count Distinct`
* 路徑 — `sales_flat_order.(input) reference > Customer Concentration.Primary Key`或`customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選取的資料行 — `sales_flat_order.customer_email`或`customer_entity.entity_id`

* `customer_entity`資料表
* 客戶數量
* [!UICONTROL Column type]： - `One to Many > JOINED_COLUMN`
* 路徑 — `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選取的資料行 — `Number of customers`

* （輸入） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]： - `Same table > Event Number`
* 事件擁有者 — `Number of customers`
* 事件排名 — `Customer's lifetime revenue`

* 客戶的收入百分位數
* [!UICONTROL Column type]： - `Same table > Calculation`
* [!UICONTROL Inputs]： - `(input) Ranking by customer lifetime revenue`， `Number of customers`
* [!UICONTROL Calculation]： - **當A為Null然後為Null時，則為(A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]： - `Decimal`

* `Sales_flat_order`資料表
* 客戶數量
* [!UICONTROL Column type]： - `One to Many > JOINED_COLUMN`
* 路徑 — `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選取的資料行 — `Number of customers`

* （輸入）依客戶期限收入排名
* [!UICONTROL Column type]： - `Same table > Event Number`
* 事件擁有者 — `Number of customers`
* 事件排名 — `Customer's lifetime revenue`
* 篩選器 — `Customer's order number = 1`

* 客戶的收入百分位數
* [!UICONTROL Column type]： - `Same table > Calculation`
* [!UICONTROL Inputs]： - `(input) Ranking by customer lifetime revenue`， `Number of customers`
* [!UICONTROL Calculation]： - **當A為Null然後為Null時，則為(A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]： - `Decimal`

>[!NOTE]
>
>使用的百分位數是甚至分段的客戶，代表客戶群的第X個百分位。 每個客戶都與1到100的整數相關聯，這可以視為其期限收入&#x200B;*排名*。 例如，如果特定客戶的客戶收入百分位數為&#x200B;**5**，則就期限收入而言，此客戶在所有客戶中屬於&#x200B;***第五個百分位***。

## 量度

* **總客戶期限值**
* 在`customer_entity`資料表中
* 此量度執行&#x200B;**總和**
* 在`Customer's lifetime revenue`欄上
* 依`Customer's first order date`時間戳記排序

## 報表

* **客戶集中度**
* [!UICONTROL Metric]： `Total customer lifetime value`
* [!UICONTROL Filter]： `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]： `Total customer lifetime value`
* [!UICONTROL Filter]： `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL 群組依據]: `Independent`
* 量度`A`： `Total customer lifetime revenue by percentile`
* 量度`B`： `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Customer's revenue percentile`
* 顯示頂端/底部： `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **前10%濃度**
* [!UICONTROL Filter]： `Customer's revenue percentile <= 10`

* 量度`A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* &#x200B;
  [!UICONTROL 群組依據]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **僅一次購買最下層50%的濃度**

* 量度`A`： `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]：

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* &#x200B;
  [!UICONTROL 群組依據]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **後10%濃度**
* [!UICONTROL Filter]： `Customer's revenue percentile > 90`

* 量度`A`： `Total customer lifetime revenue`
* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* 隱藏圖表
* &#x200B;
  [!UICONTROL 群組依據]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果可能如上述範例控制面板所示。

如果您在建立此分析時遇到任何問題，或只是想與專業服務團隊互動，請[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
