---
title: 營銷ROI
description: 瞭解如何設定跟蹤渠道分析的控制板 — 包括按市場活動和聚合的ROI。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 營銷ROI

>[!NOTE]
>
>本主題包含使用原始體系結構和新體系結構的客戶端的說明。 你在 [新架構](../../administrator/account-management/new-architecture.md) 在從主工具欄中選擇「管理資料」後，「Data Warehouse視圖」部分可用。

如果你在線上廣告上花錢，你希望跟蹤你在這方面花的錢的回報，並就進一步的投資做出資料驅動的決策。 本主題演示了如何設定跟蹤渠道分析的控制面板 — 包括按市場活動和匯總的ROI。

![](../../assets/Marketing_dashboard_example.png)

在開始之前，您要連接 [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md)。 [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) 並引入任何額外的線上廣告支出資料。 此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 統一表

**原始體系結構：** 把你的開支從各種渠道匯集起來，比如 [!DNL Facebook Ads] 或 [!DNL Google Adwords],Adobe建議建立 **統一表** 你所有廣告費的。 您需要一個分析師來完成此步驟。 如果你沒有， [提出支援請求](../../guide-overview.md#Submitting-a-Support-Ticket) 和主題 `[MARKETING ROI ANALYSIS]`，分析員將建立此表。

**新體系結構：** 您可以按照中的示例 [此分析庫](../../data-analyst/data-warehouse-mgr/create-dw-views.md) 主題。 統一表現在稱為新體系結構上的Data Warehouse視圖。

## 計算列

要建立的列

* **`Consolidated Digital Ad Spend`** 表
* **`Campaign name`** 由Adobe分析師建立，作為 **[營銷ROI分析]** 票

**原始和新體系結構：**

* **`sales_flat_order`** 表
   * **`Order's GA campaign`**
      * 選擇定義： `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * 選擇 [!UICONTROL table]: `ecommerce####`
      * 選擇 [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * 選擇定義：聯接列
      * 選擇 [!UICONTROL table]: `ecommerce####`
      * 選擇 [!UICONTROL column]: `medium`
      * [!UICONTROL Path]:sales_flat_order.increment_id = e-commerce####.transactionId
   * **`Order's GA source`**
      * 選擇定義：聯接列
      * 選擇 [!UICONTROL table]: `ecommerce####`
      * 選擇 [!UICONTROL column]: `source`
      * [!UICONTROL Path]:sales_flat_order.increment_id = e-commerce####.transactionId ^



* **`customer_entity`** 表
* **`Customer's first order GA campaign`**
   * 選擇定義： `Max`
   * 選擇 [!UICONTROL table]: `sales_flat_order`
   * 選擇 [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 選擇定義： `Max`
   * 選擇 [!UICONTROL table]: `sales_flat_order`
   * 選擇 [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]:sales_flat_order.customer_id = customer_entity.entity.id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 選擇定義： `Max`
   * 選擇 [!UICONTROL table]: `sales_flat_order`
   * 選擇 [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** 表
* **`Customer's first order GA campaign`**
   * 選擇定義： `Joined Column`
   * 選擇 [!UICONTROL table]: `customer_entity`
   * 選擇 [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 選擇定義：聯接列
   * 選擇 [!UICONTROL table]: `customer_entity`
   * 選擇 [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 選擇定義： `Joined Column`
   * 選擇 [!UICONTROL table]: `customer_entity`
   * 選擇 [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## 度量

* **廣告支出**
* 在 **`Consolidated Digital Ad Spend`** 表
* 此度量執行 **和**
* 在 **`adCost`** 列
* 按 **`date`** 時間戳

* **廣告印象**
* 在 **`Consolidated Digital Ad Spend`** 表
* 此度量執行 **和**
* 在 **`Impressions`** 列
* 按 **`Month`** 時間戳

* **廣告點擊**
* 在 **`Consolidated Digital Ad Spend`** 表
* 此度量執行 **和**
* 在 **`adClicks`** 列
* 按 **`Month`** 時間戳

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **廣告花費（所有時間）**
   * [!UICONTROL Metric]:廣告支出

* 度量 `A`:廣告支出
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **廣告客戶收購（始終）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選器邏輯：([`A`] 或 [`B`] 或 [`C`])和 [`D`]

* 度量 `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **廣告ROI**
   * [!UICONTROL Metric]:廣告支出

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選器邏輯：([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]:平均生命週期收入
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選器邏輯：([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* 度量 `A`: `Ad Spend (hide)`
* 度量 `B`: `Ad customer acquisitions (hide)`
* 度量 `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **按GA介質排序的訂單**
   * 

      [!UICONTROL度量]: `Orders`

* 度量 `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **按市場活動列出的廣告投資回報率**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選器邏輯：([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]:平均生命週期收入
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選器邏輯：([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]:訂單的平均生存期數
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選器邏輯：([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* 度量 `A`: `Ad Spend` （隱藏）
* 度量 `B`: `Ad customer acquisitions`
* 度量 `C`: `Average LTV`
* 度量 `D`: `Average lifetime # of orders`
* 
   [!UICONTROL公式]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* 度量 `H`: `adClicks`
* 度量 `I`: `Impressions`
* 
   [!UICONTROL公式]: `CTR`
* 
   [!UICONTROL公式]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 
   [!UICONTROL組依據]: `campaign` (將「客戶的第一訂單」市場活動用於非廣告支出表指標)
* 

   [!UICONTROL Chart Type]: `Table`

如果您在構建此分析時遇到任何問題，或者只想與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

### 相關

* [UTM標籤的最佳做法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [如何 [!DNL Google Analytics] UTM歸因工作？](../analysis/utm-attributes.md)
