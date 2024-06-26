---
title: 建立量度
description: 瞭解如何使用量度建立圖表。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 建立量度

>[!NOTE]
>
>需要 [管理員許可權](../../administrator/user-management/user-management.md).

量度是一種測量。 在SQL和資料庫結構中，量度就像變數期間的預存查詢。

在 [!DNL Commerce Intelligence]，您可將量度用於 [建立圖表](../../data-user/reports/ess-rpt-build-visual.md). 例如，量度 `revenue` 是訂單總數。 量度 `average customer revenue per order` 是客戶每筆訂單的平均花費。

在報表中使用量度時，可依指定時段分析量度並 [篩選或分段](../../best-practices/segment-filter.md) 依不同類別。 考慮分析依性別分組的平均客戶收入 — 在此案例中， `average customer revenue per order` 是量度，而性別是群組。

## 定義量度 {#define}

1. 若要建立量度，請按一下 **[!UICONTROL Data** > **Metrics]**.

1. 按一下 **[!UICONTROL Create New Metric]**.

1. 從下拉式清單，按一下包含您要用於量度之原生或計算欄的表格。

1. 為您的量度命名。

   Adobe會推薦可以讓您一眼就知道該量度是什麼的名稱。 例如： `Average Order Revenue`.

1. 下一步是定義量度的功能。 使用下拉式功能表，定義量度的操作， `operation` 欄和 `date` 維度：

   * 選擇作業：
      * `Count`  — 此作業會計算資料表格中的列數
      * `Max`  — 最大值會傳回特定資料欄的最大值
      * `Min` - Min會傳回特定資料欄的最小值
      * `Sum`  — 此作業會加總特定資料欄的值
      * `Average`  — 此作業會計算資料欄值的平均值
      * `Count Distinct Value`  — 這會計算特定資料欄中的唯一值數量
      * `Median`  — 此作業會計算資料欄值的中值
      * `First and Third Quartiles`  — 這些作業會分別計算資料欄值的第25個百分位和第75個百分位
      * `Tenth and Ninetieth Percentiles`  — 這些作業會分別計算資料欄值的第10個百分位和第90個百分位

   * 選擇要對其執行作業的欄。 例如，如果您想找出總收入，您可以對 `order total` 欄。

     如果您正在編輯現有量度，您也可以 [變更量度的作業表格](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) 在本節中。

   * 選擇可用來分析量度趨勢的日期維度。 例如， `order date`.

## 新增篩選器 {#filters}

此 `Filter` 區段可讓您建立篩選器或套用 [儲存的篩選器集](../../data-user/reports/ess-manage-data-filters.md) 至您的量度。

對於 `average order revenue` 量度，您不會想要包含設定商店時可能完成的任何測試訂單，因為這會提供不準確的結果。 可套用篩選集，以從資料集中移除這些訂單。 建立篩選器後，該篩選器將套用至使用此量度建立的所有圖表。

此 `Filter Logic` 區段是您進一步定義量度行為方式的地方。

* &quot;\[`A`\]或\[`B`\]」允許滿足篩選條件的任何資料\[`A`\]或\[`B`\]
* &quot;\[`A`\]和\[`B`\]」只允許同時符合兩個篩選器的資料\[`A`\]和\[`B`\]
* &quot;(\[`A`\]和\[`B`\])或\[`C`\]」只允許同時滿足這兩個篩選器的資料\[`A`\]和\[`B`\]，或滿足篩選器\[`C`\]單獨使用

## 新增Dimension {#dimensions}

此 [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 區段會顯示用於篩選或群組的所有可用資料維度；依預設，所有可用資料欄都會列為維度。 繼續此範例，如果您想依反向連結來源劃分收入，可在此執行。

除了以維度形式列出所有可用的資料欄之外， [!DNL Commerce Intelligence] 猜測哪些欄可分組。 *若要在報表上將資料分段或分組*，欄必須標示為可群組。

## 正在完成 {#finish}

除了定義量度的行為方式外，您也可以在 `User Rights` 區段。 當 `Admin` 使用者有權存取所有量度，您必須勾選適當群組旁的方塊，指出可使用此量度的使用者。

如果您正在編輯現有的量度，可以在以下位置檢視使用此量度的圖表清單（以及擁有圖表的人員）： `Dependent Charts` 區段。

變更會自動儲存，您的量度現已準備就緒。
