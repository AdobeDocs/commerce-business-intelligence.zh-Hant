---
title: 最佳化SQL查詢
description: 瞭解如何最佳化SQL查詢。
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# 最佳化SQL查詢

[!DNL SQL Report Builder]可讓您在任何指定時間查詢及反複處理這些查詢。 當您需要修改查詢而不必等待更新週期完成才能實現您建立的欄或報告需要更新時，這會很有用。

在執行查詢之前，[[!DNL Commerce Intelligence] 會估計其成本](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html?lang=zh-Hant)。 成本會考慮執行查詢所需的時間長度和資源數量。 如果該成本被認為太高，或者如果傳回的列數超過[!DNL Commerce Intelligence]限制，則查詢會失敗。 為了查詢您的[Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) （可確保您撰寫儘可能精簡的查詢），Adobe建議下列事項。

## 使用SELECT或選取所有欄

選取所有欄無法進行即時、輕鬆執行的查詢。 使用`SELECT *`的查詢可能需要相當長的時間才能執行，特別是如果您的表格有許多資料行。

因此，Adobe建議您儘可能避免使用`SELECT *`，而僅包含您需要的欄：

| **代替這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## 使用完整外部聯結

外部聯結會選取兩個要聯結之表格的整體，這會增加查詢的運算成本。 這表示您的查詢執行時間較長且很可能會失敗，因為傳回結果所花的時間可能會超過執行限制。

請考慮使用內部或左側聯結，而不使用這種型別的聯結。 只有當資料表之間有欄位相符時（例如，`order_id`同時存在於典型`customers`和`orders`資料表中），內聯結才會傳回結果。 左聯結會傳回左（第一個）表格中的所有結果，以及右（第二個）表格中的相符結果。

檢視如何重新寫入FULL OUTER JOIN查詢：

| **代替這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

除了它們使用的JOIN型別外，這些查詢在所有方面都是相同的。

## 使用多重聯結

雖然您可以在查詢中包含多個聯結，但請記住，這會增加查詢的成本。 為避免達到成本臨界值，Adobe建議儘可能避免多個聯結。

## 使用篩選器

儘可能使用篩選器。 `WHERE`和`HAVING`子句會篩選您的結果，並只提供您真正想要的資料。

## 在JOIN子句中使用篩選器

如果您在執行聯結時使用篩選器，請務必將其套用至聯結中的兩個表格。 即使它是多餘的，這也會減少查詢的運算成本並減少執行時間。

| **代替這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## 使用運運算元

在撰寫查詢時，請考慮儘可能使用「最便宜」的運運算元。 每個查詢都有計算成本，這是由組成查詢的函式、運運算元和篩選器所決定。 有些運運算元所需的運算量較少，因此較其他運運算元較便宜。

比較運運算元（>、&lt;、=等）是最便宜的，其次是[LIKE。 SIMILAR TO和POSIX運運算元](https://www.postgresql.org/docs/9.5/functions-matching.html)是最昂貴的運運算元。

## 使用EXISTS與IN

使用`EXISTS`與`IN`取決於您嘗試傳回的結果型別。 如果您只對單一值感興趣，請使用`EXISTS`子句而非`IN`。 `IN`與逗號分隔值清單一起使用，這會增加查詢的計算成本。

執行`IN`查詢時，系統必須先處理子查詢（`IN`陳述式），然後根據`IN`陳述式中指定的關聯性處理整個查詢。 `EXISTS`的效率更高，因為查詢不需要執行多次 — 檢查查詢中指定的關聯性時會傳回true/false值。

簡單地說：使用`EXISTS`時，系統不必處理這麼多。

| **代替這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## 使用ORDER BY

`ORDER BY`在SQL中是昂貴的函式，可能會大幅增加查詢的成本。 如果您收到錯誤訊息，指出查詢的EXPLAIN成本過高，請視需要嘗試從查詢中消除任何`ORDER BY`。

這並不是說`ORDER BY`不能使用 — 只是它應該只在必要時使用。

## 使用GROUP BY和ORDER BY

在少數情況下，此方法可能與您嘗試執行的操作不符。 一般規則是，如果您使用`GROUP BY`和`ORDER BY`，您應該將兩個子句中的資料行放在相同的順序。 例如：

| **代替這個……** | **試試這個！** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## 正在結束

學習撰寫SQL的最佳方法（並且效率很高）是透過反複試驗。 若要找出最適合您的報表，請嘗試僅使用SQL編輯器重新建立一些報表。
