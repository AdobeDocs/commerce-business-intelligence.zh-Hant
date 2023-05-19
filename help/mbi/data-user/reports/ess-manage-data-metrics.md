---
title: 建立度量
description: 瞭解如何使用度量建立圖表。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 建立度量

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md)。

度量是度量。 在SQL和資料庫結構中，度量類似於在變數期間儲存的查詢。

在 [!DNL Commerce Intelligence]，您可以使用度量 [建立圖表](../../data-user/reports/ess-rpt-build-visual.md)。 例如，度量 `revenue` 是訂單總數。 度量 `average customer revenue per order` 是每個訂單的平均客戶支出。

在報告中使用時，可以在指定的時間段內分析度量， [過濾或分段](../../best-practices/segment-filter.md) 不同類別。 考慮分析按性別分組的平均客戶收入 — 在本例中， `average customer revenue per order` 是指標，性別是組。

## 定義度量 {#define}

1. 要建立度量，請按一下 **[!UICONTROL Data** > **Metrics]**。

1. 按一下 **[!UICONTROL Create New Metric]**。

1. 從下拉清單中，按一下包含要用於度量的本機列或計算列的表。

1. 命名您的度量。

   Adobe推薦一個名稱，它一目瞭然地告訴您度量是什麼。 例如： `Average Order Revenue`。

1. 下一步是定義度量的功能。 使用下拉菜單，定義度量的操作， `operation` 列和 `date` 維：

   * 選擇一個工序：
      * `Count`  — 此操作計算資料表中的行數
      * `Max` - Max返回特定資料列的最大值
      * `Min`  — 最小值返回特定資料列的最小值
      * `Sum`  — 此操作將匯總特定資料列的值
      * `Average`  — 此操作計算資料列值的平均值
      * `Count Distinct Value`  — 這將計算特定資料列中唯一值的數量
      * `Median`  — 此操作計算資料列值的中值
      * `First and Third Quartiles`  — 這些操作分別計算資料列值的第25和第75百分位
      * `Tenth and Ninetieth Percentiles`  — 這些操作分別計算資料列值的第10和第90百分位
   * 選擇一列以執行操作。 例如，如果要查找總收入，您將對 `order total` 的雙曲餘切值。

      如果正在編輯現有度量，還可以 [更改度量的操作表](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) 的下界。

   * 選擇可用於趨勢度量的日期維。 比如說， `order date`。


## 添加篩選器 {#filters}

的 `Filter` 部分允許您建立篩選器或應用 [已保存的篩選器集](../../data-user/reports/ess-manage-data-filters.md) 你的指標。

對於 `average order revenue` metric，您不希望包括在設定商店時可能已執行的任何test訂單 — 這將給我們不準確的結果。 可以應用篩選器集以從資料集中刪除這些訂單。 建立篩選器後，它將應用於使用此度量構建的所有圖表。

的 `Filter Logic` 節是可進一步定義度量應如何運行的位置。

* &quot;\[&quot;`A`\或\[`B`「\]」允許滿足篩選器\[的任何資料`A`\]或\[`B`\]
* &quot;\[&quot;`A`\]和\[`B`\]」僅允許滿足兩個篩選器\[的資料`A`\]和\[`B`\]
* &quot;(\[`A`\]和\[`B`\])或\[`C`\]」僅允許同時滿足篩選器\[的資料`A`\]和\[`B`\]或滿足篩選器\[`C`\]單獨

## 添加Dimension {#dimensions}

的 [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 部分顯示所有可用的資料維以進行篩選或分組；預設情況下，所有可用資料列都作為維列出。 繼續本示例，如果要按推薦來源劃分收入，可以在此處執行此操作。

除將所有可用資料列列為維外， [!DNL Commerce Intelligence] 猜測哪些列可分組。 *對報表資料進行分段或分組*，列必須標籤為可組。

## 完成 {#finish}

除了定義度量的行為方式外，還可以在 `User Rights` 的子菜單。 同時 `Admin` 用戶有權訪問所有度量，您必須通過選中相應組旁邊的框來指示可以使用此度量的用戶。

如果正在編輯現有度量，則可以查看在中使用此度量的圖表清單（以及其所有者） `Dependent Charts` 的子菜單。

更改將自動保存，您的度量現在可以繼續。
