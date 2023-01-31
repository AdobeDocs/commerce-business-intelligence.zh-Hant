---
title: 使用「顯示頂端/底端」功能排序資料
description: 了解如何使用「顯示頂端/底部」功能來排序資料。
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 使用 `Show Top/Bottom` 功能

您可以在 `Visual Report Builder` 而不是建立分析。 例如，您可以建立報表來顯示您的贏取和行銷管道的價值，但您也可以建立報表，只顯示前五名表現者。 同樣地，您也可以建立報表來重新調整行銷工作，顯示哪些州產生的收入最多。

在同時使用 `Group By` 和 `Time Interval of None`. 當這兩個元素都在報表中時， `Show Top/Bottom` 功能會顯示在圖表預覽上方。 此功能可讓您根據您設定的參數，查看上（最高到最低）和下（最低到最高）資料點。

![在「視覺化」Report Builder中顯示「上/下」功能。](../../assets/Show_Top_Bottom.png)

## 如何使用？ {#how}

按一下 **[!UICONTROL Show Top/Bottom link]**，則會顯示一個視窗，您可在其中設定顯示和排序參數。 文本框中的數字可以是整數(如 `5`)或 `ALL`. 接著，您可以選擇依量度或群組來排序報表。

例如，如果想要顯示帶來最多收入的五個反向連結來源，以下是我們的操作方式：

1. 新增 `Revenue` 量度。

1. 新增 `Group By` 依反向連結來源分段量度。

1. 設定 `Time Interval` to `None`.

1. 在 `Show Top/Bottom` 設定，將顯示設定為 `5` 因此，報表中只會包含前5個總收入金額的反向連結來源。

>[!NOTE]
>
>因為報表沒有 `Time Interval`，值（在此例中為前5個反向連結來源）可能會隨時間而變更。 如果一個反向連結來源的收入超過另一個，來源顯示的順序將會變更。

## 使用多個量度呢？ {#multiplemetrics}

當報表中有多個量度時，使用此功能會變得複雜，因為每個量度只能依本身或其中一個群組排序。

假設我們用 `Revenue` 和 `Number of orders` 量度，依反向連結來源分組。 `Revenue` 只能依 `Revenue` 或轉介來源和 `Number of orders` 只能依 `Number of orders` 或轉介來源。

這表示，當我們 `Revenue` 從上 `5` 產生轉介來源的收入，我們無法同時依排名最前的 `5` 產生轉介來源的收入。 簡言之：有多個量度時，最好依群組排序每個量度。

以下是圖表範例，我們將 `Revenue` 量度本身而非群組。 如您所見，不依群組排序量度會建立奇怪（且最終無助）的報表：

![奇怪而無益的報告結果。](../../assets/strange-report-results.png)

如果我們已依群組排序這兩個量度，圖表會如下所示：

![依群組排序兩個量度。](../../assets/sort-metrics-by-grouping.png)

## 預設值排序方式為何？ {#defaultsorting}

只有一個量度包含在 `Group by` 和 `Time Interval` of `None`，預設順序為 `Visual Report Builder` 是根據量度顯示排名最前的值。 在此情況下， `Show Top/Bottom` 如果此功能符合您的需求，則可能不需要此功能。

在此示例中，我們將查看我們的銷售代表已關閉了多少機會。 此表格會根據量度自動從最高到最低排序，在此情況下 `Won Opportunities`.

![依量度排序。](../../assets/Ordered_by_metric.png)

不過，新增第二個量度時，預設會根據分組排序頂端。 新增量度和群組後，預設的排序會依據第一個群組、第二個群組等。

![按分組排序。](../../assets/Ordered_by_grouping.png)

## 包裝 {#wrapup}

我們在文章的開頭提到過，但我們再次說：雖然我們介紹了一些基本示例，但此功能有許多有趣的用途。

想想我們以前的銷售代表和銷售機會示例。 移除 `Time Interval`，套用 `Group By`，並根據分組對資料進行排序，使我們能夠詳細了解每個代表贏得的機會數量。 此外，使用 `Show Top/Bottom` 讓我們找出表現最佳的人。
