---
title: 年度、每月和每週報告
description: 瞭解如何輕鬆檢視一段時間內的趨勢，並變更您想比較之時間期間的觀點。
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 特定時段的報告

>[!NOTE]
>
>此主題包含使用原始架構和新架構的使用者端指示。 如果您從主工具列選取[後有](../../administrator/account-management/new-architecture.md)Data Warehouse檢視&#x200B;[!DNL _區段可用，即表示_]&#x200B;新架構[!DNL Manage Data]。

Report Builder可讓您輕鬆檢視一段時間的趨勢，以及變更您想比較之時段的觀點。 本主題將示範如何設定控制面板，以更深入的方式讓您建立每週、每月、每年和每月的報表。

![顯示逐周、逐月和逐年比較的儀表板](../../assets/Wow__mom__yoy.png)

開始之前，您應該檢閱更詳細的探索觀點[這裡](../../tutorials/using-visual-report-builder.md)和獨立的時間選項[這裡](../../tutorials/time-options-visual-rpt-bldr.md)。

此分析包含[進階計算資料行](../data-warehouse-mgr/adv-calc-columns.md)。

## 計算欄

* **`Sales_flat_order`**&#x200B;資料表
* **原始架構：**&#x200B;以下資料行是由分析人員建立為您`[YoY WoW MoM ANALYSIS]`票證的一部分
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **新架構：** SQL如下所列，其中包含如何建立此計算的範例像片
   * `created_at (month-day)` [!UICONTROL Calculation]： **to_char(A， &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]： **to_char(A， &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]： **to_char(A， &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]： **to_char(A， &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]： &#x200B;** to_char(A， &#39;hh24&#39;)**
     ![在Data Warehouse Manager中建立計算資料行介面](../../assets/new-arch-create-calc.png)

## 量度

無。

>[!NOTE]
>
>在建立新報表之前，請務必[將所有新欄新增為量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。

## 報表

* **YoY圖表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * [!UICONTROL Time options]： `Time range (Custom)`： `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]：前100%依&#x200B;**`created_at (month-day)`**&#x200B;排序*

* 量度`A`： `This year`
* 量度`B`： `Last year`
* [!UICONTROL Time period]： `1 year ago to 0 years ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `created_at (month-day)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **MoM圖表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * 時間選項： `Time range (Custom)`： `2 months ago to 1 month ago`

   * 顯示前/後：前100%依&#x200B;**`created_at (day of month)`**&#x200B;排序*

* 量度`A`：本月*
* 量度`B`：上個月*
* [!UICONTROL Time period]：一個月前至0個月前
* &#x200B;
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]： `created_at (day of month)`
* &#x200B;
  [!UICONTROL Chart Type]: Line

* **WoW圖表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * [!UICONTROL Time options]： `Time range (Custom)`： `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]：前100%依`created_at (day of week)`排序

* 量度`A`： `This week`
* 量度`B`： `Last week`
* [!UICONTROL Time period]： `1 week ago to 0 weeks ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `created_at (day of week)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **DoD圖表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * [!UICONTROL Time options]： `Time range (Custom)`： `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]：前100%依`created_at (hour of day)`排序

* 量度`A`： `Today`
* 量度B： `Yesterday`
* [!UICONTROL Time period]： `1 day ago to 0 days ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `created_at (hour of day)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像這個頁面頂端的影像。
