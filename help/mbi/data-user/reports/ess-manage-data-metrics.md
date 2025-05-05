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
>需要[管理員許可權](../../administrator/user-management/user-management.md)。

量度是一種測量。 在SQL和資料庫結構中，量度就像變數期間的預存查詢。

在[!DNL Commerce Intelligence]中，您可以使用量度來[建立圖表](../../data-user/reports/ess-rpt-build-visual.md)。 例如，量度`revenue`是訂單總數。 量度`average customer revenue per order`是平均客戶每筆訂單花費的金額。

在報表中使用時，可以在指定的時段內分析量度，並依不同類別篩選或分段[&#128279;](../../best-practices/segment-filter.md)。 請考慮分析依性別分組的平均客戶收入 — 在此案例中，`average customer revenue per order`是量度，而性別是分組。

## 定義量度 {#define}

1. 若要建立量度，請按一下&#x200B;**[!UICONTROL Data** > **Metrics]**。

1. 按一下&#x200B;**[!UICONTROL Create New Metric]**。

1. 從下拉式清單，按一下包含您要用於量度之原生或計算欄的表格。

1. 為您的量度命名。

   Adobe會推薦可以讓您一眼就知道該量度是什麼的名稱。 例如： `Average Order Revenue`。

1. 下一步是定義量度的功能。 使用下拉式功能表，定義量度的作業、`operation`欄及`date`維度：

   * 選擇作業：
      * `Count` — 此作業會計算資料表中的列數
      * `Max` - Max會傳回特定資料欄的最大值
      * `Min` - Min會傳回特定資料欄的最小值
      * `Sum` — 此作業會加總特定資料欄的值
      * `Average` — 此作業會計算資料欄值的平均值
      * `Count Distinct Value` — 這會計算特定資料欄中值的唯一數目
      * `Median` — 此作業會計算資料欄值的中位數
      * `First and Third Quartiles` — 這些作業會分別計算資料欄值的第25個百分位和第75個百分位
      * `Tenth and Ninetieth Percentiles` — 這些作業會分別計算資料欄值的第10個百分位和第90個百分位

   * 選擇要對其執行作業的欄。 例如，如果您想要尋找總收入，可在`order total`欄上執行加總作業。

     如果您正在編輯現有的量度，也可以在此區段中[變更量度的作業表格](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md)。

   * 選擇可用來分析量度趨勢的日期維度。 例如，`order date`。

## 新增篩選器 {#filters}

`Filter`區段可讓您建立篩選器或將[儲存的篩選器集](../../data-user/reports/ess-manage-data-filters.md)套用至您的量度。

對於`average order revenue`量度，您不想包含任何設定商店時可能完成的測試訂單 — 這會提供不準確的結果。 可套用篩選集，以從資料集中移除這些訂單。 建立篩選器後，該篩選器將套用至使用此量度建立的所有圖表。

`Filter Logic`區段可讓您進一步定義量度應有的行為。

* 「\[`A`\]或\[`B`\]」允許任何滿足篩選器\[`A`\]或\[`B`\]的資料
* 「\[`A`\]和\[`B`\]」只允許同時符合篩選器\[`A`\]和\[`B`\]的資料
* 「（\[`A`\]和\[`B`\]） OR \[`C`\]」僅允許同時滿足篩選器\[`A`\]和\[`B`\]的資料，或僅滿足篩選器\[`C`\]的資料

## 新增Dimension {#dimensions}

[`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)區段會顯示所有可用於篩選或分組的資料維度；依預設，所有可用的資料欄都會列為維度。 繼續此範例，如果您想依反向連結來源劃分收入，可在此執行。

除了以維度形式列出所有可用的資料欄之外，[!DNL Commerce Intelligence]還會猜測哪些欄是可分組的。 *若要將報表*&#x200B;上的資料分段或分組，欄必須標示為可分組。

## 正在完成 {#finish}

除了定義量度的行為方式，您還可以在`User Rights`區段中設定許可權層級。 雖然`Admin`使用者可存取所有量度，但您必須勾選適當群組旁的方塊，指出可使用此量度的使用者。

如果您正在編輯現有的量度，可以在`Dependent Charts`區段中檢視使用此量度的圖表清單（以及擁有圖表的人員）。

變更會自動儲存，您的量度現已準備就緒。
