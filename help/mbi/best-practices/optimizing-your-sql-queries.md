---
title: 優化SQL查詢
description: 瞭解如何優化SQL查詢。
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# 優化SQL查詢

的 [!DNL SQL Report Builder] 允許您在任何給定時間查詢和迭代這些查詢。 當您需要修改查詢而無需等待更新週期完成，然後才能實現您建立的列或報告需要更新時，此功能非常有用。

在執行查詢之前， [[!DNL Commerce Intelligence] 估計其成本](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html)。 成本考慮執行查詢所需的時間長度和資源數。 如果該成本被認為過高或返回的行數超過 [!DNL Commerce Intelligence] 限制，查詢失敗。 用於查詢 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)Adobe建議您編寫盡可能最簡化的查詢。

## 使用SELECT或選擇所有列

選擇所有列不能進行及時、易於執行的查詢。 使用 `SELECT *` 運行可能需要相當長的時間，尤其是如果表具有許多列。

因此，Adobe建議您避免使用 `SELECT *` 盡可能只包括您需要的列：

| **不是這樣……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## 使用完全外連接

外連接選擇要連接的兩個表的全部，這增加了查詢的計算成本。 這意味著您的查詢需要更長的時間才能運行，並且更有可能失敗，因為返回結果可能需要的時間超過執行限制。

不要使用此類型的連接，應考慮使用內部連接或左連接。 僅當表之間存在列匹配時，內部連接才返回結果(例如， `order_id` 都存在於 `customers` 和 `orders` )的正平方根。 左連接返回左（第一個）表中的所有結果以及右（第二個）表中的匹配結果。

查看如何重寫FULL OUTER JOIN查詢：

| **不是這樣……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

除了使用的JOIN類型外，這些查詢在所有方面都是相同的。

## 使用多個連接

雖然您可以在查詢中包括多個聯接，但請記住，這可能會推高查詢的成本。 為避免達到成本閾值，Adobe建議盡可能避免多個連接。

## 使用篩選器

盡可能使用篩選器。 `WHERE` 和 `HAVING` 子句篩選結果，並僅提供您真正想要的資料。

## 在JOIN子句中使用篩選器

如果在執行聯接時使用篩選器，請確保將其應用於聯接中的兩個表。 即使是冗餘的，這也降低了查詢的計算成本並減少了執行時間。

| **不是這樣……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## 使用運算子

在編寫查詢時，請考慮盡可能使用「最便宜」運算子。 每個查詢都有計算成本，計算成本由構成查詢的函式、運算子和篩選器決定。 一些算子需要的計算量較少，這使得它們比其他算子更便宜。

比較運算子（>、&lt;、=等）是最便宜的，後面是 [比如。 SIMILAR TO和POSIX運算子](https://www.postgresql.org/docs/9.5/functions-matching.html) 最貴的運營商。

## 使用EXISTS與IN

使用 `EXISTS` 與 `IN` 取決於您嘗試返回的結果類型。 如果您只對單個值感興趣，請使用 `EXISTS` 子句 `IN`。 `IN` 與逗號分隔值清單一起使用，這增加了查詢的計算成本。

當 `IN` 查詢運行時，系統必須首先處理子查詢( `IN` )，然後根據在 `IN` 的雙曲餘切值。 `EXISTS` 效率要高得多，因為查詢不必多次運行 — 檢查查詢中指定的關係時會返回true/false值。

簡單地說：系統在使用 `EXISTS`。

| **不是這樣……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## 使用ORDER BY

`ORDER BY` 是SQL中的一個昂貴函式，可以顯著提高查詢的成本。 如果您收到錯誤消息，指出查詢的EXPLAIN成本過高，請嘗試消除任何 `ORDER BY`從查詢中輸入。

這不是說 `ORDER BY` 不能使用 — 只是應在必要時使用。

## 使用GROUP BY和ORDER BY

在某些情況下，此方法與您嘗試的操作不符。 一般規則是，如果您使用 `GROUP BY` 和 `ORDER BY`，則應按相同順序將列置於兩個子句中。 例如：

| **不是這樣……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## 包裝

學習編寫SQL的最佳方法是嘗試和錯誤。 要查找最適合您的報告，請嘗試僅使用SQL編輯器重新建立幾個報告。
