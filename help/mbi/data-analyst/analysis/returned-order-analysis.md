---
title: 分析退貨單
description: 瞭解如何設定一個儀表板，該儀表板提供對商店退貨的詳細分析。
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 退貨訂單

本主題演示了如何設定儀表板來詳細分析商店的退貨。

![](../../assets/detailed-returns-dboard.png)

開始之前，您必須是 [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 並應確保您的公司使用 `enterprise\_rma` 表格。

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 入門

要跟蹤的列

* **`enterprise_rma`** 或 **`rma`** 表
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** 或 **`rma_item_entity`** 表
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

要建立的篩選器集

* **`enterprise_rma`** 表
* 篩選器集名稱： `Returns we count`
* 篩選器集邏輯：
   * 佔位符 — 在此處輸入自定義邏輯

* **`enterprise_rma_item_entity`** 表
* 篩選器集名稱： `Returns items we count`
* 篩選器集邏輯：
   * 佔位符 — 在此處輸入自定義邏輯

### 計算列

要建立的列

* **`enterprise_rma`** 表
* **`Order's created at`**
* 選擇定義： `Joined Column`
* [!UICONTROL Create Path]:
* 
   [!UICONTROL Many]: `enterprise_rma.order_id`
* 

   [!UICONTROL One]: `sales_flat_order.entity_id`

* 選擇 [!UICONTROL table]: `sales_flat_order`
* 選擇 [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 選擇定義： `Joined Column`
* 選擇 [!UICONTROL table]: `sales_flat_order`
* 選擇 [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** 由分析師建立，作為 `[RETURNS ANALYSIS]` 票

* **`enterprise_rma_item_entity`** 表
* **`return_date_requested`**
* 選擇定義： `Joined Column`
* [!UICONTROL Create Path]:
   * 
      [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 

      [!UICONTROL One]: `enterprise_rma.entity_id`

* 選擇 [!UICONTROL table]: `enterprise_rma`
* 選擇 [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** 由分析師建立，作為 `[RETURNS ANALYSIS]` 票

* **`sales_flat_order`** 表
* **`Order contains a return? (1=yes/0=No)`**
* 選擇定義： `Exists`
* 選擇 [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** 由分析師建立，作為 `[RETURNS ANALYSIS]` 票
* **`Customer's previous order contains return? (1=yes/0=no)`** 由分析師建立，作為 `[RETURNS ANALYSIS]` 票

>[!NOTE]
>
>如果您對只分析「秒到解」或「秒到第一響應」的工作時間感興趣，請在請求票證時通知分析師。

### 度量

* **返回**
* 在 **`enterprise_rma`** 表
* 此度量執行 **計數**
* 在 **`entity_id`** 列
* 按 **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **返回的項**
* 在 **`enterprise_rma_item_entity`** 表
* 此度量執行 **和**
* 在 **`qty_approved`** 列
* 按 **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **返回的物料總值**
* 在 **`enterprise_rma_item_entity`** 表
* 此度量執行 **和**
* 在 **`Returned item total value (qty_returned * price)`** 列
* 按 **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **訂單和退貨之間的平均時間**
* 在 **`enterprise_rma`** 表
* 此度量執行 **平均**
* 在 **`Time between order's created_at and date_requested`** 列
* 按 **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

### 報告

* **返回後重複順序概率**
* 度量 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* 度量 `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* 公式：重複順序概率
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
   [!UICONTROL圖表類型]: `Bar`

* **返回的平均時間（所有時間）**
* 度量 `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 

   [!UICONTROL圖表類型]: `Number`

* **具有退貨的訂單百分比**
* 度量 `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* 度量 `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* 公式：具有退貨的訂單百分比
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **按月返回的收入**
* 度量 `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 

   [!UICONTROL圖表類型]: `Line`

* **已退貨且未再購買的客戶**
* 度量 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* 
   [!UICONTROL組依據]: `Customer_email`
* 

   [!UICONTROL圖表類型]: `Table`

* **按物料的退貨率**
* 度量 `A`: `Returned items` （隱藏）
* [!UICONTROL Metric]:返回的項

* 度量 `B`: `Items sold` （隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 

   [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
   [!UICONTROL圖表類型]: `Table`

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與上面的示例儀表板類似。

如果您在構建此分析時遇到任何問題或希望與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
