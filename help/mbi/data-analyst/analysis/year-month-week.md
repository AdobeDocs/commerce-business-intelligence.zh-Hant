---
title: 每年、每月和每週報告
description: 瞭解如何輕鬆查看隨時間變化的趨勢並更改您可能希望比較的時段的透視。
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 期間報告

>[!NOTE]
>
>本主題包含使用原始體系結構和新體系結構的客戶端的說明。 你在 [新架構](../../administrator/account-management/new-architecture.md) 如果你有 [!DNL _Data Warehouse視圖_] 選擇後 [!DNL Manage Data] 的上界。

報表生成器使您可以輕鬆查看隨時間的變化趨勢，並更改要比較的時段的透視。 本主題演示了如何設定儀表板以更深入地查看級別，以便您能夠建立每週、每月和每年分析的報表。

![](../../assets/Wow__mom__yoy.png)

在開始之前，您應更詳細地查看瀏覽透視 [這裡](../../tutorials/using-visual-report-builder.md) 和獨立時間選項 [這裡](../../tutorials/time-options-visual-rpt-bldr.md)。

此分析包含 [高級計算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 計算列

* **`Sales_flat_order`** 表
* **原始體系結構：** 以下列由分析員建立，作為 `[YoY WoW MoM ANALYSIS]` 票
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **新體系結構：** 下面列出的SQL，其中顯示了如何建立此計算的示例
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A, &#39;h24&#39;)**

      ![](../../assets/new-arch-create-calc.png)

## 度量

沒有。

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

* **YoY圖表**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]:前100%排序依據 **`created_at (month-day)`***

* 度量 `A`: `This year`
* 度量 `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
   [!UICONTROL Chart Type]: `Line`

* **MoM圖表**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 時間選項： `Time range (Custom)`: `2 months ago to 1 month ago`

   * 顯示頂部/底部：前100%排序依據 **`created_at (day of month)`***

* 度量 `A`:本月*
* 度量 `B`:上個月*
* [!UICONTROL Time period]:一個月前
* 
   [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
   [!UICONTROL Chart Type]: Line

* **鎢圖表**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]:前100%排序依據 `created_at (day of week)`

* 度量 `A`: `This week`
* 度量 `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
   [!UICONTROL Chart Type]: `Line`

* **DoD圖表**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]:前100%排序依據 `created_at (hour of day)`

* 度量 `A`: `Today`
* 指標B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
   [!UICONTROL Chart Type]: `Line`

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與此頁頂部的影像類似。
