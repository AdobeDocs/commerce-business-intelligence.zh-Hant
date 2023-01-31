---
title: 視覺效果Report Builder中的視覺效果選項
description: 了解如何使用視覺化Report Builder中的視覺化選項。
exl-id: e42a004e-28e3-4484-bb5a-b58c810b23e0
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 0%

---

# 視覺效果選項

為指定資料集選擇正確的視覺效果是分析過程的關鍵環節。 每個資料集都有一個故事要講述，但該故事的效果以其視覺影響和可讀性來強調。

此 [!DNL MBI] `Visual Report Builder` 提供12個不同的視覺效果選項，各有各自的優點和使用案例。 本文探討 [!DNL MBI]，包括必要的報表設定（若適用），以及使用案例的範例。 以下是MBI中的視覺效果：

* `Scalar`
* `Table`
* `Line`
* `Bar`
* `Stacked Bar`
* `Column`
* `Stacked Column`
* `Pie`
* `Area`
* `Funnel`
* `Scatter plot`
* `Bubble`
* `Heatmap`

## `Scalar`

`Scalar` 報表會顯示為單一數值。 這通常用來顯示收入或訂單等關鍵量度的「所有時間」值，或透過兩個不同的標量報表比較收入與預算的依日計算。 在以下範例中，這只會顯示指定報告間隔的訂單總數：

![](../../assets/blobid0.png)

若要將報表儲存為標量，請配置篩選器和時間設定，然後按一下 **[!UICONTROL Save]** 或 **[!UICONTROL Update]** 在報表的右上角。 在 `Type` 下拉式清單，選擇數字：量度名稱，將報表儲存為左側列顯示的值。

![](../../assets/blobid1.png)

**需求**:

* `Time interval`: `None`
* `Group by`: `None`
* 僅限一個量度

## `Table`

正如名字所暗示的， `table` 報表非常適合用於顯示表格詳細資訊。 當需要在單一報表中依值或量度顯示大量群組時，表格通常是最佳方式。 以下是「客戶詳細資料」表格，顯示依客戶電子郵件分組的訂單和收入：

![](../../assets/blobid2.png)

與標量報表類似，您可以按一下 **[!UICONTROL Save]** 或 **[!UICONTROL Update]** 在報告建立工具中，選取 `Type` 下拉式清單。

![](../../assets/blobid3.png)

**需求：**

* 雖然沒有報表設定需求，但請務必注意，表格上限為3500列。 如果您的資料集包含超過3500列，您需要篩選結果以縮小範圍，或將結果匯出至 `.csv` 或 `Excel` 以查看完整資料集。

## `Line`

`Line` 圖表是比較相似度量同類群組效能的最佳選擇。 例如，分析同一時段內兩個地區的收入，或比較已履行訂單中逐年的增長，如下所示：

![](../../assets/blobid0.png)

新增至報表的每個量度和公式都以其自己的行表示。 在比較單位和比例相似的量度時，請務必清除 `Multiple Y-Axes` 來顯示相同比例的所有量度。

若要將報表儲存為折線圖，請調整報表 `Type` to `Chart`，然後從報告建立工具中選取適當的視覺效果，如下所示：

![](../../assets/blobid1.png)

**需求：**

* 無

## `Bar`

`Bar` 圖表會以一系列水準長條來顯示資料，最適合依值來顯示有限量度或群組的整體效能。 例如，長條圖可用來比較依商店列出的收入：

![](../../assets/blobid2.png)

每個不重複的量度、分組依據和時間間隔組合都會顯示為其專屬列。 如果您有兩個量度，其中一個 `group by`，包含三個不同 `group by` 值，您的報表會顯示6個不同的長條。

若要將報表儲存為長條圖，請調整報表 `Type` to `Chart` ，然後選取 `Bar` 選項，如下所示：

![](../../assets/blobid3.png)

**需求：**

* 無

## `Stacked Bar`

`Stacked bar` 圖表與其長條圖組相似，具有顯示每個長條的比例劃分的額外功能。 通常，堆疊長條圖是以兩個或多個量度和單一組依據來設定，因此每個長條代表依值分割的不重複群組。

例如，以下報表有兩個相同的收入量度：一個篩選了首次訂購，另一個篩選了重複訂購。 依商店分組後，您會看到每個商店的總收入貢獻（以橫條的總寬度表示），以及每個商店的首次與重複收入劃分：

![](../../assets/blobid4.png)

請確定 `Multiple Y-Axes` 設定如上所示的報表時，此欄位會取消勾選方塊。

若要將報表儲存為堆疊長條圖，請調整報表 `Type` to `Chart` ，然後從報告建立工具中選取堆疊長條圖選項：

![](../../assets/blobid5.png)

**需求：**

* 無

## `Column`

`Column` 圖表將每個資料點表示為垂直欄，通常比水準長條圖視覺效果更適合顯示時間趨勢資料。 由於每個獨特度量和依組合分組都以其自己的一系列長條表示，因此欄報表通常最適合具有三個或更少量度的報表，或透過包含1-3個依值分組的單一群組的一個量度。

在以下範例中，我們顯示兩個收入量度，一個是初次篩選收入，另一個是重複收入，並隨著月份進行趨勢分析：

![](../../assets/blobid6.png)

欄報表可透過變更報表來儲存 `Type` to `Chart`，並選取欄視覺效果選項：

![](../../assets/blobid7.png)

**需求：**

* 無

## `Stacked Column`

`Stacked column` 報表幾乎與直欄圖相同，但類似的欄會互相堆疊在一起，使得總高度代表值的總和。 以有限數量的量度或群組格將堆疊的欄再次視覺化效果最佳。

使用與 `Column` 上節中，含有兩個收入量度（首次篩選並重複）的報表，會以堆疊欄的視覺效果呈現如下所示：

![](../../assets/blobid8.png)

同樣，重要的是 `Multiple Y-Axes` 以堆疊欄視覺效果顯示多個量度時，會清除核取方塊。

若要將報表儲存為堆疊欄，請設定報表 `Type` to `Chart` ，然後選取 `stacked column` 選項：

![](../../assets/blobid9.png)

**需求：**

* 無

## `Pie`

`Pie` 圖表最適合顯示具有一個或多個組的單個度量，或顯示不具有組的多個度量。 無論是哪種情況，時間間隔都必須設定為無，才能在餅圖中顯示資料。 在以下範例中，單一訂單量度會依商店名稱分組，以依商店顯示訂單劃分：

![](../../assets/blobid10.png)

若要將報表儲存為圓形圖，請設定報表 `Type` to `Chart` ，然後選取 `pie` 選項，如下所示：

![](../../assets/blobid11.png)

**需求：**

* `Time interval`: `None`
* 下列其中一項：
   * `Single metric with one or more group bys`
   * `Multiple metrics with no group bys`

## `Area`

`Area` 圖表幾乎與堆疊的直欄圖相同，但直欄會連續顯示。 與堆疊的欄類似，區域圖最好以有限數量的群組或量度視覺化。

以 `stacked column` 區段中，下方的報表透過區域圖視覺效果顯示首次與重複收入的比較：

![](../../assets/blobid12.png)

若要將報表儲存為區域圖，請調整 `Type` to `Chart` 並選擇區域選項：

![](../../assets/blobid13.png)

**需求：**

* 無

## `Funnel`

`Funnel` 圖表最適合於將轉換視覺化為預期事件序列。 幾個範例包括分析銷售漏斗中潛在的收入，從銷售機會到結案交易，或測量客戶在第一次和第二次訂購、第二次和第三次訂購之間的下降，以此類推。 後者的範例如下所示：

![](../../assets/blobid4.png)

在漏斗報表中，漏斗的指定步驟的相對值會由步驟的高度反映，而步驟的顯示順序則由報表設定決定。 設定漏斗報表有兩種方式：

* `Single metric with one group by`: — 由組的「顯示頂部/底部」設定確定的步驟順序。 依預設，漏斗步驟會從最大值到最小值依序顯示，但您也可以依名稱將它們依字母順序排序。

* `Multiple metrics with no group by`: — 由量度新增至報表的順序所決定的步驟順序。

若要將報表儲存為漏斗圖，請調整報表 `Type` to `Chart` 並在report builder中選取適當的視覺效果。

![](../../assets/blobid5.png)

**需求：**

* `Time interval`: `None`
* 下列其中一項：
   * `Single metric with one group by`
   * `Multiple metrics with no group by`

## `Scatter plot`

A `scatter plot` 可用來檢查量度與兩個不同變數的關係，以便輕鬆識別關聯和離群值。 此類型的視覺效果最適合搭配數值維度使用，請嘗試搭配「訂購」量度及 `Customer's lifetime number of coupons` 和 `Customer's lifetime revenue` 維度，了解抵用券使用與收入的關聯。 您可以選擇散布圖是否有趨勢線：

![](../../assets/scatter-plot-1.png)

![沒有趨勢線](../../assets/scatter-plot-2.png)

![](../../assets/scatter-plot-3.png)

![使用趨勢線](../../assets/scatter-plot-4.png)

**需求：**

選項1:

* 二 `metrics`
* 一 `group by`
* `Time interval`: `None`

選項2:

* 二 `metrics`
* 否 `group by`
* 設定 `time interval`

## `Bubble` 圖表

A `bubble` 圖表最多可顯示四個資料維度，其中 `X` 和 `Y` 軸指定氣泡的位置， `Z` 軸是泡泡的大小，通過包含兩個組，可以向泡泡添加顏色。 當您想要在單一圖表中繪製多個資料維度時，最適合使用此類型的視覺效果。

例如，下圖顯示依特定贏取來源（泡泡顏色）和狀態（特定顏色的各種泡泡）分組的客戶數量（泡泡大小），根據總收入和平均期限訂單繪製。

![](../../assets/bubble-1.png)

下圖顯示依贏取來源（泡泡顏色）和狀態（特定顏色的各種泡泡）分組的客戶數量（泡泡大小），根據平均期限值和總收入繪製。

![](../../assets/bubble-2.png)

**單系列氣泡圖要求：**

選項1

* 三 `metrics`
* 一 `group by`
* `Time interval`: `None`

選項2

* 三 `metrics`
* 否 `group by`
* 設定 `time interval`

**多系列氣泡圖要求：**

* 三 `metrics`
* 二 `group by`
* `Time interval`: `None`

## `Heatmap`

使用 `heatmaps` 視覺化資料中的熱點。 例如，熱度圖可指出您經常從何處獲得較高的音量。 將此資料視覺化可協助您調整庫存水準，以確保在這些尖峰期間滿足需求。

下列熱圖會以整體方式，依一週中的某天（小時）顯示數週內的訂單。

![](../../assets/heat-map.png)<!--{: width="650"}-->

**需求：**

選項1

* 一 `metric`
* 二 `group by`
* `Time interval`: `None`

選項2

* 一 `metric`
* 一 `group by`
* 設定 `time interval`
