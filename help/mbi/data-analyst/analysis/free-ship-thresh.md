---
title: 免費裝運閾值
description: 瞭解如何設定跟蹤免費發運閾值效能的儀表板。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 免費運輸

>[!NOTE]
>
>本主題包含使用原始體系結構和新體系結構的客戶端的說明。 如果您擁有 `Data Warehouse Views` 選擇後 `Manage Data` 的上界。

本主題演示如何設定跟蹤免費發運閾值效能的儀表板。 下面顯示的此儀表板是A/Btest兩個免費發運閾值的絕佳方法。 例如，您的公司可能不確定您應該以50美元還是100美元的價格提供免費送貨服務。 您應執行客戶的兩個隨機子集的A/Btest，並執行以下分析： [!DNL Commerce Intelligence]。

在開始之前，您需要確定兩個單獨的時間段，在這些時間段中，您對商店的免費發運閾值有不同的值。

![](../../assets/free_shipping_threshold.png)

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 計算列

如果您位於原始體系結構上(例如，如果您沒有 `Data Warehouse Views` 選項 `Manage Data` 菜單)，您希望聯繫支援團隊以構建以下列。 在新體系結構上，可以從 `Manage Data > Data Warehouse` 的子菜單。 詳細說明如下。

* **`sales_flat_order`** 表
   * 此計算將建立相對於您的典型購物車大小增量的購物車。 這可以從增量（包括， 5、10、50、100）開始

* **`Order subtotal (buckets)`** 原始體系結構：由分析師建立，作為 `[FREE SHIPPING ANALYSIS]` 票
* **`Order subtotal (buckets)`** 新體系結構：
   * 如上所述，此計算會建立相對於您的典型購物車大小增量的購物車。 如果有本機小計列，如 `base_subtotal`，可用作此新列的基礎。 否則，它可以是從收入中排除發運和折扣的計算列。
   >[!NOTE]
   >
   >「儲存桶」大小取決於作為客戶端適合您的內容。 你可以從 `average order value` 並建立一些小於或大於此數的桶。 查看下面的計算時，您將看到如何輕鬆複製部分查詢、編輯查詢以及建立附加儲存桶。 該示例以50為增量完成。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`或 `calculated column`。 `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
何時 `A< 200` 和 `A <= 250` 然後 `201 - 250`
何時 `A<251` 和 `A<= 300` 然後 `251 - 300`
何時 `A<301` 和 `A<= 350` 然後 `301 - 350`
何時 `A<351` 和 `A<=400` 然後 `351 - 400`
何時 `A<401` 和 `A<=450` 然後 `401 - 450`
否則「超過450」結束



## 度量

沒有新的指標！!!

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **發運規則A的平均訂單值**
   * [!UICONTROL Metric]: `Average order value`

* 度量 `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **按發運規則A的小計時段列出的訂單數**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >通過顯示頂部，可以切斷尾端 `X` `sorted by` `Order subtotal` （桶） `Show top/bottom`。

* 度量 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **按發運規則A的小計列出的訂單百分比**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL組依據]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* 度量 `A`: `Number of orders by subtotal (hide)`
* 度量 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`

* **小計超過發運規則A的訂單百分比**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL組依據]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* 度量 `A`: `Number of orders by subtotal`
* 度量 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


對發運B和發運規則B的期間重複上述步驟和報表。

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與此頁頂部的影像類似。
