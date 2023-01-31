---
title: 商務流失率
description: 了解如何產生和分析您的商務流失率。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 流失率

在本主題中，我們示範如何計算 **流失率** 為 **商務客戶**. 與SaaS或傳統訂閱公司不同，商務客戶通常沒有具體的 **&quot;混合事件&quot;** 來顯示這些客戶不應再計入您的作用中客戶。 因此，下列指示可讓您根據客戶自上次訂購以來經過的確定時間量，將客戶定義為「已處理」。

![](../../assets/Churn_rate_image.png)

許多客戶想要協助您開始概念化 **時間範圍** 應根據其資料使用。 如果您想使用歷史客戶行為來定義此 **流失時間範圍**，請熟悉 [定義流失](../analysis/define-cust-churn.md) 文章。 接著，您可以在下列指示中，使用流失率公式中的結果。

## 計算欄

要建立的列

* **`customer_entity`** 表格
* **`Customer's last order date`**
   * 選取 [!UICONTROL definition]: `Max`
   * 選擇 [!UICONTROL table]: `sales_flat_order`
   * 選擇 [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * 選取 [!UICONTROL definition]: `Age`
   * 選擇 [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>一定要 [將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 量度

* **新客戶（按首次訂購日期）**
   * 我們數

>[!NOTE]
>
>此量度可能已存在於您的帳戶中。

* 在 **`customer_entity`** 表格
* 此量度會執行 **計數**
* 在 **`entity_id`** 欄
* 由 **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **新客戶（按上次訂購日期）**
   * 我們數

>[!NOTE]
>
>此量度可能已存在於您的帳戶中。

* 在 **`customer_entity`** 表格
* 此量度會執行 **計數**
* 在 **`entity_id`** 欄
* 由 **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>一定要 [將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **流失率**
   * [!UICONTROL Metric]:新客戶（按首次訂購日期）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 客戶上次訂購日期後的秒數>= [你自定義的對顧客的封鎖&#x200B;]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *量度 `A`:`New customers cumulative`*
* *量度 `B`:`Churned customers by last order date`*
* *量度 `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

以下是一些常見的月份>秒轉換，但google提供其他值，包括您可能要尋找的任何自訂值的周>秒轉換。

| **月** | **秒** |
|---|---|
| 3 | 777.6萬 |
| 6 | 1555.2萬 |
| 9 | 2332.8萬 |
| 12 | 3110.4萬 |

編譯所有報表後，您可以視需要在控制面板上組織報表。 結束結果可能類似於上述範例控制面板。
