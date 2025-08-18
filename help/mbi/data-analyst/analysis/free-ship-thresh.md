---
title: 免運費臨界值
description: 瞭解如何設定儀表板，以追蹤免運費運送臨界值的效能。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# 免運費

>[!NOTE]
>
>此主題包含使用原始架構和新架構的使用者端指示。 如果您在選取主工具列中的`Data Warehouse Views`後有`Manage Data`區段可用，則表示您使用新架構。

本主題將示範如何設定追蹤免運費運送臨界值績效的控制面板。 這個儀表板（如下所示）是A/B測試兩個免運費臨界值的好方法。 例如，貴公司可能不確定您應以$50或$100的價格提供免運費。 您應該針對客戶的兩個隨機子集執行A/B測試，並在[!DNL Commerce Intelligence]中執行分析。

開始之前，您想要識別兩個獨立的時段，您在此時段擁有不同的商店免運費臨界值。

![](../../assets/free_shipping_threshold.png)

此分析包含[進階計算資料行](../data-warehouse-mgr/adv-calc-columns.md)。

## 計算欄

如果您使用原始架構（例如，如果您的「`Data Warehouse Views`」功能表下沒有「`Manage Data`」選項），您希望聯絡支援團隊以建置以下欄。 在新架構上，可從`Manage Data > Data Warehouse`頁面建立這些欄。 詳細指示如下。

* **`sales_flat_order`**&#x200B;資料表
   * 此計算會以相對於您一般購物車大小的增量建立值區。 增量範圍包括5、10、50、100

* **`Order subtotal (buckets)`**&#x200B;原始架構：由分析人員建立，作為您`[FREE SHIPPING ANALYSIS]`票證的一部分
* **`Order subtotal (buckets)`**&#x200B;新架構：
   * 如上所述，這項計算會以相對於您一般購物車大小的增量建立值區。 如果您有原生小計資料行，例如`base_subtotal`，可以做為這個新資料行的基礎。 如果沒有，它可以是計算欄，其中不包含收入的送貨和折扣。

  >[!NOTE]
  >
  >「貯體」大小取決於適合您作為使用者端的尺寸。 您可以從`average order value`開始，建立一些小於或大於該數量的值區。 檢視以下計算時，您會瞭解如何輕鬆複製部分查詢、編輯查詢及建立其他值區。 範例是以50為增量完成。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`或`calculated column`，`Datatype`： `Integer`
   * [!UICONTROL Calculation]： `case when A >= 0 and A<=200 then 0 - 200`
當`A< 200`和`A <= 250`然後`201 - 250`
當`A<251`和`A<= 300`然後`251 - 300`
當`A<301`和`A<= 350`然後`301 - 350`
當`A<351`與`A<=400`然後`351 - 400`
當`A<401`與`A<=450`然後`401 - 450`
否則&#39;超過450&#39;
結束


## 量度

無新量度!!!

>[!NOTE]
>
>在建立新報表之前，請務必[將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。

## 報表

* **平均訂單值（送貨規則A**）
   * [!UICONTROL Metric]： `Average order value`

* 量度`A`： `Average Order Value`
* [!UICONTROL Time period]： `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **根據小計貯體排列的訂單數（送貨規則為A**）
   * [!UICONTROL Metric]： `Number of orders`

  >[!NOTE]
  >
  >您可以顯示`X`中的前`sorted by` `Order subtotal` `Show top/bottom` （貯體）以截斷尾端。

* 量度`A`： `Number of orders`
* [!UICONTROL Time period]： `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Column`

* 送貨規則為A **之小計訂單的**&#x200B;百分比
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * &#x200B;
     [!UICONTROL 群組依據]: `Independent`
   * [!UICONTROL Formula]： `(A / B)`
   * &#x200B;
     [!UICONTROL Format]: `%`

* 量度`A`： `Number of orders by subtotal (hide)`
* 量度`B`： `Total number of orders (hide)`
* [!UICONTROL Formula]： `% of orders`
* [!UICONTROL Time period]： `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* 小計超過送貨規則A **的訂單的**&#x200B;百分比
   * [!UICONTROL Metric]： `Number of orders`
   * &#x200B;
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]： `Number of orders`
   * &#x200B;
     [!UICONTROL 群組依據]: `Independent`

   * [!UICONTROL Formula]： `1- (A / B)`
   * &#x200B;
     [!UICONTROL Format]: `%`

* 量度`A`： `Number of orders by subtotal`
* 量度`B`： `Total number of orders (hide)`
* [!UICONTROL Formula]： `% of orders`
* [!UICONTROL Time period]： `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`


針對送貨規則B重複上述步驟與報表，並重複時間週期。

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像這個頁面頂端的影像。
