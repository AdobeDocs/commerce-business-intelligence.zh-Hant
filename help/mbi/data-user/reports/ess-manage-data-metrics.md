---
title: 建立量度
description: 了解如何使用量度建立圖表。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 建立量度

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md).

簡言之，量度就是測量。 在SQL和資料庫結構中，度量類似於在變數時段內儲存的查詢。

在 [!DNL MBI]，您可以將量度用於 [建立圖表](../../data-user/reports/ess-rpt-build-visual.md). 例如，量度 `revenue` 是訂購的總量。 量度 `average customer revenue per order` 是客戶每筆訂單的平均花費。

在報表中使用時，量度可依指定時段分析，並 [篩選或分段](../../best-practices/segment-filter.md) 不同類別。 請考慮分析按性別分組的平均客戶收入，在此例中， `average customer revenue per order` 是量度，性別是群組。

## 定義量度 {#define}

1. 若要建立新量度，請按一下 **[!UICONTROL Data** > **Metrics]**.

1. 按一下 **[!UICONTROL Create New Metric]**.

1. 從下拉式清單中，按一下包含您要用於量度的原生或計算欄的表格。

1. 為量度命名。

   我們建議您一個名稱，一看就能告訴您量度是什麼。 例如： `Average Order Revenue`.

1. 下一步是定義量度的用途。 使用下拉式功能表，定義量度的操作， `operation` 欄和 `date` 維度：

   * 選擇操作：
      * `Count`  — 此操作會計算資料表中的列數
      * `Max` - Max返回特定資料列的最大值
      * `Min` - Min會傳回特定資料欄的最小值
      * `Sum`  — 此操作會加總特定資料欄的值
      * `Average`  — 此操作計算資料列值的平均值
      * `Count Distinct Value`  — 這會計算特定資料欄中的唯一值數
      * `Median`  — 此操作計算資料列值的中位數
      * `First and Third Quartiles`  — 這些操作分別計算資料列值的第25和第75百分位
      * `Tenth and Ninetieth Percentiles`  — 這些操作分別計算資料列值的第10和第90個百分位數
   * 選擇要對執行操作的列。 例如，如果您想要找出總收入，則要對 `order total` 欄。

      如果您正在編輯現有量度，您也可以 [變更量度的操作表格](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) 在本節中。

   * 選擇可用來分析量度趨勢的日期維度。 例如， `order date`.


## 新增篩選器 {#filters}

此 `Filter` 區段可讓您建立新篩選器或套用 [儲存的篩選集](../../data-user/reports/ess-manage-data-filters.md) 至量度。

為我們的 `average order revenue` 量度中，我們不想加入在設定商店時可能已執行的任何測試訂單，這會導致錯誤的結果。 我們可以套用篩選器集，從資料集中移除這些訂單。 建立篩選器後，篩選器將套用至使用此量度建立的所有圖表。

此 `Filter Logic` 區段可讓您進一步定義量度的行為。

* &quot;\[&quot;`A`\]或\[`B`「\]」將允許滿足篩選器「\[」的任何資料`A`\]或\[`B`\]
* &quot;\[&quot;`A`\]和\[`B`「\]」將僅允許滿足兩個篩選器「\[」的資料`A`\]和\[`B`\]
* &quot;(\[`A`\]和\[`B`\])或\[`C`「\]」將僅允許同時滿足兩個篩選器的資料\[`A`\]和\[`B`\]或滿足篩選器\[`C`單獨

## 新增Dimension {#dimensions}

此 [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 區段顯示所有可用的資料維度，以供篩選或分組之用；依預設，所有可用的資料欄都會列為維度。 繼續我們的範例，如果我們想依轉介來源劃分收入，我們可以在此執行此操作。

除了將所有可用資料欄列為維度外， [!DNL MBI] 也會猜測哪些欄可分組。 *對報表資料進行分段或分組*，欄必須標示為可群組。

## 結束 {#finish}

除了定義量度的運作方式，您也可以在 `User Rights` 區段。 同時 `Admin` 使用者可存取所有量度，您必須勾選適當群組旁的方塊，以指出可使用此量度的使用者。

如果您正在編輯現有量度，可以在 `Dependent Charts` 區段。

變更會自動儲存，而您的量度現在可正常運作。
