---
title: 分析退回的訂單
description: 瞭解如何設定控制面板，提供商店回報的詳細分析。
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 退回的訂單

此主題示範如何設定控制面板，提供商店回訪的詳細分析。

![顯示退貨率與原因的詳細退貨儀表板](../../assets/detailed-returns-dboard.png)

開始之前，您必須是[Adobe Commerce](https://business.adobe.com/tw/products/magento/magento-commerce.html)客戶，且應確定貴公司使用`enterprise\_rma`資料表進行退貨。

此分析包含[進階計算資料行](../data-warehouse-mgr/adv-calc-columns.md)。

## 快速入門

要追蹤的欄

* **`enterprise_rma`**&#x200B;或&#x200B;**`rma`**&#x200B;資料表
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`**&#x200B;或&#x200B;**`rma_item_entity`**&#x200B;資料表
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

要建立的篩選器集

* **`enterprise_rma`**&#x200B;資料表
* 篩選器集名稱： `Returns we count`
* 篩選器集邏輯：
   * 預留位置 — 在這裡輸入您的自訂邏輯

* **`enterprise_rma_item_entity`**&#x200B;資料表
* 篩選器集名稱： `Returns items we count`
* 篩選器集邏輯：
   * 預留位置 — 在這裡輸入您的自訂邏輯

### 計算欄

要建立的欄

* **`enterprise_rma`**&#x200B;資料表
* **`Order's created at`**
* 選取定義： `Joined Column`
* [!UICONTROL Create Path]：
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* 選取[!UICONTROL table]： `sales_flat_order`
* 選取[!UICONTROL column]： `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 選取定義： `Joined Column`
* 選取[!UICONTROL table]： `sales_flat_order`
* 選取[!UICONTROL column]： `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`**&#x200B;是由分析人員建立，作為您`[RETURNS ANALYSIS]`票證的一部分

* **`enterprise_rma_item_entity`**&#x200B;資料表
* **`return_date_requested`**
* 選取定義： `Joined Column`
* [!UICONTROL Create Path]：
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* 選取[!UICONTROL table]： `enterprise_rma`
* 選取[!UICONTROL column]： `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`**&#x200B;是由分析人員建立，作為您`[RETURNS ANALYSIS]`票證的一部分

* **`sales_flat_order`**&#x200B;資料表
* **`Order contains a return? (1=yes/0=No)`**
* 選取定義： `Exists`
* 選取[!UICONTROL table]： `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`**&#x200B;是由分析人員建立，作為您`[RETURNS ANALYSIS]`票證的一部分
* **`Customer's previous order contains return? (1=yes/0=no)`**&#x200B;是由分析人員建立，作為您`[RETURNS ANALYSIS]`票證的一部分

>[!NOTE]
>
>如果您只想分析幾秒以解決，或幾秒以首次回應，請在要求票證時告知分析人員。

### 量度

* **傳回**
* 在&#x200B;**`enterprise_rma`**&#x200B;資料表中
* 此量度執行&#x200B;**計數**
* 在&#x200B;**`entity_id`**&#x200B;欄上
* 排序依據： **`date_requested`**
* [!UICONTROL Filter]： `Returns we count`

* **傳回的專案**
* 在&#x200B;**`enterprise_rma_item_entity`**&#x200B;資料表中
* 此量度執行&#x200B;**總和**
* 在&#x200B;**`qty_approved`**&#x200B;欄上
* 排序依據： **`return date_requested`**
* [!UICONTROL Filter]： `Returns we count`

* **傳回的專案總計值**
* 在&#x200B;**`enterprise_rma_item_entity`**&#x200B;資料表中
* 此量度執行&#x200B;**總和**
* 在&#x200B;**`Returned item total value (qty_returned * price)`**&#x200B;欄上
* 排序依據： **`return date_requested`**
* [!UICONTROL Filter]： `Returns we count`

* **訂單與退貨之間的平均時間**
* 在&#x200B;**`enterprise_rma`**&#x200B;資料表中
* 此量度執行&#x200B;**平均值**
* 在&#x200B;**`Time between order's created_at and date_requested`**&#x200B;欄上
* 排序依據： **`date_requested`**
* [!UICONTROL Filter]： `Returns we count`

>[!NOTE]
>
>在建立新報表之前，請務必[將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。

### 報表

* 傳回後有&#x200B;**重複訂購機率**
* 量度`A`： `Number of orders with returns`
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]：
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* 量度`B`： `Non-last orders with returns`
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]：
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* 公式：重複訂購機率
* [!UICONTROL Formula]： `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]： `Customer's order number`
* &#x200B;
  [!UICONTROL 圖表型別]: `Bar`

* **平均傳回時間（所有時間）**
* 量度`A`： `Avg time between order and return`
* [!UICONTROL Metric]： `Avg time between order and return`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL 圖表型別]: `Number`

* **含退貨的訂單百分比**
* 量度`A`： `Number of orders`
* [!UICONTROL Metric]： `Number of orders`

* 量度`B`： `Orders w/ return`
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]：
   * `Order contains a return? (1=yes/0=No) = 1`

* 公式：含退貨的訂單百分比
* [!UICONTROL Formula]： `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Chart Type]： `Number - % of orders with return`

* **依月份傳回的收入**
* 量度`A`： `Returned item total value`
* [!UICONTROL Metric]： `Returned item total value`

* [!UICONTROL Time period]： `All time`
* [!UICONTROL Interval]： `By month`
* &#x200B;
  [!UICONTROL 圖表型別]: `Line`

* **已退貨且不再購買的客戶**
* 量度`A`： `Number of orders with returns`
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]：
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL 群組依據]: `Customer_email`
* &#x200B;
  [!UICONTROL 圖表型別]: `Table`

* **依據專案的回訪率**
* 量度`A`： `Returned items` （隱藏）
* [!UICONTROL Metric]：傳回的專案

* 量度`B`： `Items sold` （隱藏）
* [!UICONTROL Metric]： `Number of orders`
* [!UICONTROL Filter]：

* [!UICONTROL Formula]： `Return %`
* [!UICONTROL Formula]： `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]： `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]： `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL 圖表型別]: `Table`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果可能如上述範例控制面板所示。

如果您在建立此分析時遇到任何問題，或想與Professional Services團隊互動，請[連絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)。
