---
title: 修改資料庫以支援增量複製
description: 瞭解如何修改您的資料庫以支援增量複製。
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# 支援增量複製

如果您的表格目前不允許增量複製，請參閱下列建議以取得可能的解決方案。

## 修改時間

此 `Modified At` 方法是最理想的複製方法，它會使用 `datetime` 欄，以偵測新的和/或更新後的資料。 請記住 `datetime` 使用此方法的資料表中的資料行必須編制索引，而且任何時候都不能包含null值。

如果您的表格沒有 `datetime` 欄，您可以新增索引 `modified at` 欄。 Null值不允許在 `modified at` 欄。 檢查欄是否填入每一列。

若要確保 `Modified At` 方法如預期運作，您無法從表格中刪除列。 反之，您應新增「 」，將此列標籤為無效 `deleted` 資料行至資料表。 此欄傳回 `1` 如果資料列無效且 `0` 否則。 然後，當您建置量度和報表時，可以使用此欄來篩選掉無效的列。

## 單一自動增加主索引鍵的修改

如果 `Modified At` 無法啟用方法，則「單一自動增加主索引鍵」為下一個最佳選項。 透過搜尋大於Data Warehouse中目前最高值的主鍵值，使用此方法在表格中探索新資料。

請記住，使用此方法的表格是單一欄，具有整數自動增加主索引鍵。 若要在資料庫中使用此方法，請進行下列修改：

* 如果主鍵是複合鍵或非整數，請將主鍵變更為自動遞增整數
* 如果主索引鍵是單一整數欄，但索引鍵是以非循序方式指派，請將主索引鍵變更為自動遞增

## 正在結束

只要對表格進行微幅修改，您就可以使用更快、更有效的增量複製方法。 不過，如果無法執行此操作，您仍可採取其他步驟 [縮短更新時間](../best-practices/reduce-update-cycle-time.md) 和 [最佳化您的資料庫](../best-practices/opt-db-analysis.md).
