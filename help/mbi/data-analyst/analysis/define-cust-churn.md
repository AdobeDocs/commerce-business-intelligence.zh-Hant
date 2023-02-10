---
title: 定義客戶流失
description: 了解如何設定控制面板，協助您定義交易式客戶的流失率。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 交易客戶流失

在本文中，我們示範如何設定控制面板，以協助您定義交易式客戶的流失率。

![](../../assets/churn-deashboard.png)

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 計算欄

要建立的列

* `customer_entity` 表格
* `Customer's lifetime number of orders`
* 選取定義： `Count`
* 選取 [!UICONTROL table]: `sales_flat_order`
* 選取 [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]:sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* 我們計算的訂單

* `sales_flat_order` 表格
* `Customer's lifetime number of orders`
* 選取定義：連結列
* 選取 [!UICONTROL table]: `customer_entity`
* 選取 [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 選取定義： `Age`
* 選取 [!UICONTROL column]: `created_at`

* **`Customer's order number`** 將由分析師建立，作為 **[定義流失]** 票證
* **`Is customer's last order`** 將由分析師建立，作為 **[定義流失]** 票證
* **`Seconds since previous order`** 將由分析師建立，作為 **[定義流失]** 票證
* **`Months since order`** 將由分析師建立，作為 **[定義流失]** 票證
* **`Months since previous order`** 將由分析師建立，作為 **[定義流失]** 票證

## 量度

無新量度！

>[!NOTE]
>
>一定要 [將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **初始重複順序概率**
* 量度A:所有重複的訂單
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 量度B:所有時間訂購
* [!UICONTROL Metric]:訂單數

* [!UICONTROL Formula]:初始重複順序概率
* 
   [!UICONTROL公式]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **自訂單後，重複訂單機率已指定月份**
* 量度A:按上次訂單後的月重複訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 量度B:自訂單（隱藏）以來的最後訂單（按月）
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 量度C:所有重複訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL分組依據]: `Independent`

* 量度D:所有上次訂購（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL分組依據]: `Independent`

* [!UICONTROL Formula]:初始重複順序概率
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

初始重複訂單概率報表代表重複訂單總計/訂單總計。 每個訂單都是重複訂單的機會；重複階數是實際執行的次數。

我們使用的公式可簡化為（X個月後發生的重複訂單總計）/（至少X個月的訂單總計）。 它向我們顯示，過去，由於訂單已過X個月，因此使用者有Y%的機會下另一份訂單。

在您建置控制面板後，我們最常收到的問題是：如何使用此方法來判斷流失率臨界值？

**這個問題沒有「一個正確的答案」。** 不過，建議您找出折線超過初始重複機率一半之數值的點。 這是我們可以說的「如果使用者要重複下訂單，他們現在可能已經完成了」的地方。 最終，目標是選擇從「保留」切換為「重新啟用」工作有意義的臨界值。

編譯所有報表後，您可以視需要在控制面板上組織報表。 結束結果可能看起來像頁面頂端的影像

如果您在建立此分析時遇到任何問題，或只是想與我們的專業服務團隊接洽， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
