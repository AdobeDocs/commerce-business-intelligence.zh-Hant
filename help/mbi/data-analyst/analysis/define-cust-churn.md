---
title: 定義客戶流失
description: 瞭解如何設定儀表板，幫助您為事務性客戶定義流失。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 事務性客戶流失

本主題演示了如何設定儀表板，幫助您為事務性客戶定義流失。

![](../../assets/churn-deashboard.png)

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 計算列

要建立的列

* `customer_entity` 表
* `Customer's lifetime number of orders`
* 選擇定義： `Count`
* 選擇 [!UICONTROL table]: `sales_flat_order`
* 選擇 [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]:sales_flat_order.customer_id = customer_entity.entity.id
* [!UICONTROL Filter]:
* 盤點的訂單

* `sales_flat_order` 表
* `Customer's lifetime number of orders`
* 選擇定義：聯接列
* 選擇 [!UICONTROL table]: `customer_entity`
* 選擇 [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 選擇定義： `Age`
* 選擇 [!UICONTROL column]: `created_at`

* **`Customer's order number`** 由分析師建立，作為 **[定義流失]** 票
* **`Is customer's last order`** 由分析師建立，作為 **[定義流失]** 票
* **`Seconds since previous order`** 由分析師建立，作為 **[定義流失]** 票
* **`Months since order`** 由分析師建立，作為 **[定義流失]** 票
* **`Months since previous order`** 由分析師建立，作為 **[定義流失]** 票

## 度量

沒有新的指標！

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **初始重複階概率**
* 指標A:全時重複訂單
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 指標B:全時訂單
* [!UICONTROL Metric]:訂單數

* [!UICONTROL Formula]:初始重複階概率
* 
   [!UICONTROL公式]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **自訂單以來給定月份的重複訂單概率**
* 指標A:自上一訂單（隱藏）起按月重複訂單
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 指標B:自訂單（隱藏）以來按月列出的最後訂單
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 度量C:全時重複訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL組依據]: `Independent`

* 度量D:全時上次訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL組依據]: `Independent`

* [!UICONTROL Formula]:初始重複階概率
* 
   [!UICONTROL公式]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* 顯示top.bottom:前24個類別，按類別名稱排序

* 

   [!UICONTROL Chart type]: `Line`

初始重複訂單概率報表表示總重複訂單/總訂單。 每次訂單都是重複訂單的機會；重複次數是實際重複次數的子集。

您使用的公式簡化為（X個月後發生的重複訂單總數）/（至少X個月的訂單總數）。 它向我們顯示，從訂單開始算起已有X個月，因此用戶進行另一訂單的機率為Y%。

一旦您構建了儀表板，最常見的問題就是：如何使用此參數來確定流失閾值？

**對此，沒有&quot;一個正確的答案&quot;。** 但是，Adobe建議找到行與初始重複概率率的一半值交叉的點。 在這個點，你可以說&quot;如果用戶要重複訂單，他們現在可能已經做了。&quot; 最終，目標是選擇從「保留」轉為「重新激活」的合理的閾值。

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與頁面頂部的影像類似

如果您在構建此分析時遇到任何問題，或者只想與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
