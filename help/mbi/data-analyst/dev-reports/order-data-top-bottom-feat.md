---
title: 使用「顯示頂部/底部」功能對資料排序
description: 瞭解如何使用「顯示頂部/底部」功能對資料進行排序。
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# 使用 `Show Top/Bottom` 特徵

您可以在 `Visual Report Builder` 比分析時間的趨勢更好。 例如，您可以構建一個報告來顯示您的收購和市場營銷渠道的價值，但您也可以構建一個只顯示前五名執行者的報告。 同樣，您可以通過建立顯示哪些州生成了最多收入的報告來重新調整營銷工作。

此類資料排序和排序可以在同時使用 `Group By` 和 `Time Interval of None`。 當這兩個元素都在報告中時， `Show Top/Bottom` 圖表預覽上方顯示功能。 此功能允許您根據您設定的參數查看頂部（最高到最低）和底部（最低到最高）資料點。

![在可視Report Builder中顯示頂部/底部功能。](../../assets/Show_Top_Bottom.png)

## 我怎麼用？ {#how}

按一下 **[!UICONTROL Show Top/Bottom link]** 來設定顯示和排序參數。 文本框中的數字可以是整數(如 `5`)或 `ALL`。 接下來，您可以選擇按度量或按分組對報表進行排序。

例如，如果要顯示帶來最多收入的五個推薦來源，您就是這樣做的：

1. 添加 `Revenue` 度量。

1. 添加 `Group By` 按引用源分段度量。

1. 設定 `Time Interval` 至 `None`。

1. 在 `Show Top/Bottom` 設定，將顯示設定為 `5` 因此，只有前五個總收入額的推薦來源才包括在報告中。

>[!NOTE]
>
>因為報告沒有 `Time Interval`，值（在本例中為前五個引用源）可隨時間變化。 如果一個推薦來源在收入方面超過另一個來源，則來源顯示的順序將發生更改。

## 使用多個指標呢？ {#multiplemetrics}

當報告中有多個度量時，使用此功能會變得複雜，因為每個度量只能按其自身或其中一個分組進行排序。

假設你和他們 `Revenue` 和 `Number of orders` 度量，按引用源分組。 `Revenue` 只能按 `Revenue` 或推薦來源 `Number of orders` 只能按 `Number of orders` 或推薦來源。

這意味著，當你可以 `Revenue` 從頂部 `5` 生成收入的參考來源，您不能同時按頂層顯示訂單數 `5` 創收的推薦來源。 簡言之：當存在多個度量時，最佳選擇是按分組對每個度量進行排序。

下面是對 `Revenue` 按本身而不是按分組來度量。 正如您所看到的，不按分組對度量進行排序會生成一個奇怪（而且最終毫無幫助）的報告：

![奇怪而無益的報告結果。](../../assets/strange-report-results.png)

如果您按分組對兩個指標進行排序，則圖表將如下所示：

![按分組對兩個度量進行排序。](../../assets/sort-metrics-by-grouping.png)

## 預設情況下，值如何排序？ {#defaultsorting}

當報告中只包含一個度量時 `Group by` 和 `Time Interval` 共 `None`，在 `Visual Report Builder` 即根據度量顯示頂值。 在這個例子中， `Show Top/Bottom` 如果這符合您的需要，則可能不需要功能。

此示例將介紹您的銷售代表已關閉的機會數。 此表根據度量自動從最高到最低排序，在此情況下 `Won Opportunities`。

![按度量排序。](../../assets/Ordered_by_metric.png)

但是，當添加第二個度量時，預設值是根據分組對頂部進行排序。 隨著度量和分組的添加，預設排序基於第一分組，然後是第二分組等。

![按分組排序。](../../assets/Ordered_by_grouping.png)

## 收尾 {#wrapup}

雖然此處介紹了一些基本功能，但此功能有許多有趣的用途。

請考慮以前的銷售代表和機會示例。 刪除 `Time Interval`，應用 `Group By`，並且根據分組對資料進行排序使我們能夠詳細瞭解每個銷售代表贏得的機會數量。 另外，使用 `Show Top/Bottom` 讓我們瞭解誰是表現最好的人。
