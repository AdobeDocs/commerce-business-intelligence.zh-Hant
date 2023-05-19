---
title: 商業流失
description: 瞭解如何生成和分析您的Commerce流失率。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# 流失率

本主題演示如何計算 **流失率** 為 **商業客戶**。 與SaaS或傳統訂閱公司不同，商業客戶通常沒有具體的 **&quot;攪拌事件&quot;** 向您顯示他們不應再指望您的活躍客戶。 因此，下面的說明允許您根據客戶自上次訂購以來經過的確定時間量將客戶定義為「已變更」。

![](../../assets/Churn_rate_image.png)

許多客戶希望幫助他們開始概念化 **時間** 他們應該根據自己的資料使用。 如果要使用歷史客戶行為來定義此 **攪動時間**，您可能希望熟悉 [定義流動](../analysis/define-cust-churn.md) 主題。 然後，您可以使用以下說明中的流失率公式中的結果。

## 計算列

要建立的列

* **`customer_entity`** 表
* **`Customer's last order date`**
   * 選擇 [!UICONTROL definition]: `Max`
   * 選擇 [!UICONTROL table]: `sales_flat_order`
   * 選擇 [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * 選擇 [!UICONTROL definition]: `Age`
   * 選擇 [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 度量

* **新客戶（按第一訂單日期）**
   * 計數的客戶

>[!NOTE]
>
>此度量可能存在於您的帳戶中。

* 在 **`customer_entity`** 表
* 此度量執行 **計數**
* 在 **`entity_id`** 列
* 按 **`Customer's first order date`** 時間戳
* [!UICONTROL Filter]:

* **新客戶（按最後訂單日期）**
   * 計數的客戶

   >[!NOTE]
   >
   >此度量可能存在於您的帳戶中。

* 在 **`customer_entity`** 表
* 此度量執行 **計數**
* 在 **`entity_id`** 列
* 按 **`Customer's last order date`** 時間戳
* [!UICONTROL Filter]:

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **流失率**
   * [!UICONTROL Metric]:新客戶（按第一訂單日期）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 自客戶上次訂單日期後的秒數>= [您自定義的對於教堂式顧客的隔離&#x200B;]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
      [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 

      [!UICONTROL Format]: Percentage

* *度量 `A`:`New customers cumulative`*
* *度量 `B`:`Churned customers by last order date`*
* *度量 `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

下面是一些常見的月份>秒轉換，但google提供了其他值，包括您可能正在查找的任何自定義值的周>秒轉換。

| **月** | **秒** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與上面的示例儀表板類似。
