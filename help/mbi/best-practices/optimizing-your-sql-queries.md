---
title: 優化SQL查詢
description: 了解如何優化SQL查詢。
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# 優化SQL查詢

SQLReport Builder允許您在任何給定時間查詢和迭代這些查詢。 如果您需要修改查詢，而不需要等待更新週期完成，才能實現您建立的欄或報表需要更新，這個功能就很實用。

執行查詢之前， [[!DNL MBI] 估計其成本](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html?lang=en). 成本會考慮執行查詢所需的時間長度和資源數。 如果該成本被認為過高，或返回行數超過MBI限制，則查詢將失敗。 對於查詢您的Data Warehouse（可確保您編寫盡可能簡化的查詢）,Adobe建議執行以下操作。

## 使用SELECT或選擇所有列

選擇所有列並不能使查詢及時、易於執行。 使用的查詢 `SELECT *` 可能需要相當長的時間才能執行，尤其是如果您的表格有許多欄時。

因此，Adobe建議您避免使用 `SELECT *` 盡可能，並僅包含您需要的欄：

| **而不是這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## 使用完全外連接

外連接選擇要連接的兩個表的整個，這會增加查詢的計算成本。 這表示您的查詢需要較長的時間才能執行，而且更可能會失敗，因為傳回結果所花的時間可能超過執行限制。

請考慮使用內連接或左連接，而不使用此類型的連接。 內部連接僅在表之間存在欄位匹配時返回結果(例如， `order_id` 都存在於 `customers` 和 `orders` 表格)。 左連接返回左表（第一表）中的所有結果以及右表（第二表）中的匹配結果。

查看如何重寫完整外連接查詢：

| **而不是這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

除了使用的JOIN類型之外，這些查詢在所有方面都相同。

## 使用多個聯接

雖然您可以在查詢中包含多個聯接，但請記住，這可能會增加查詢的成本。 為避免達到成本閾值，Adobe建議盡可能避免多個連接。

## 使用篩選

盡可能使用篩選。 `WHERE` 和 `HAVING` 子句會篩選結果，只提供您真正想要的資料。

## 在JOIN子句中使用篩選器

如果在執行聯接時使用過濾器，請確保將其應用於聯接中的兩個表。 即使是冗餘的，這也降低了查詢的計算成本並減少了執行時間。

| **而不是這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## 使用運算子

撰寫查詢時，請考慮使用「最不昂貴」運算子。 每個查詢都有計算成本，由構成查詢的函式、運算子和篩選器決定。 有些運算子需要的運算量較少，因此比其他運算子的成本較低。

比較運算子（>、&lt;、=等）最便宜，後面接著 [比如。 類似於和POSIX運算子](https://www.postgresql.org/docs/9.5/functions-matching.html) 最貴的運營商。

## 使用「存在」與「在」

使用 `EXISTS` vers `IN` 取決於您嘗試傳回的結果類型。 如果您只對單一值感興趣，請使用 `EXISTS` 子句，而不是 `IN`. `IN` 會與逗號分隔值清單搭配使用，而增加查詢的運算成本。

當 `IN` 查詢運行後，系統必須首先處理子查詢( `IN` 語句)，則根據 `IN` 語句。 `EXISTS` 效率會高得多，因為查詢不必執行多次 — 檢查查詢中指定的關係時會傳回true/false值。

簡單地說：使用 `EXISTS`.

| **而不是這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## 使用順序依據

`ORDER BY` 是SQL中一個昂貴的函式，可顯著提高查詢的成本。 如果您收到錯誤消息，說明查詢的EXPLAIN成本過高，請嘗試消除任何 `ORDER BY`除非必要，否則從查詢傳回。

這不是說 `ORDER BY` 無法使用，只是需要時才應使用。

## 使用分組依據和排序依據

在某些情況下，此方法可能不符合您嘗試執行的操作。 一般規則是，如果您使用 `GROUP BY` 和 `ORDER BY`，您應將這兩個子句中的欄按相同順序排列。 例如：

| **而不是這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## 包裝

學習編寫SQL（並且高效執行）的最佳方法是通過試驗和錯誤。 要查找最適合您的報表，請嘗試僅使用SQL編輯器重新建立一些報表。
