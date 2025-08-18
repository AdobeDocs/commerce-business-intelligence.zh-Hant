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

`Modified At`方法是最理想的復寫方法，它使用`datetime`資料行偵測新的和/或更新資料。 請記住，使用此方法的資料表中的`datetime`資料行必須編制索引，而且任何時候都不能包含null值。

如果您的資料表沒有`datetime`資料行，您可以新增索引`modified at`資料行。 `modified at`欄中不允許空值。 檢查欄是否填入每一列。

為確保`Modified At`方法如預期運作，您無法從資料表中刪除資料列。 您應該將`deleted`欄新增至資料表，將資料列標示為無效。 如果資料列無效，此資料行傳回`1`，否則傳回`0`。 然後，當您建置量度和報表時，可以使用此欄來篩選掉無效的列。

## 單一自動增加主索引鍵的修改

如果無法啟用`Modified At`方法，則「單一自動增加主索引鍵」是下一個最佳選項。 透過搜尋高於Data Warehouse中目前最高值的主鍵值，使用此方法在表格中發現新資料。

請記住，使用此方法的表格是單一欄，具有整數自動增加主索引鍵。 若要在資料庫中使用此方法，請進行下列修改：

* 如果主鍵是複合鍵或非整數，請將主鍵變更為自動遞增整數
* 如果主索引鍵是單一整數欄，但索引鍵是以非循序方式指派，請將主索引鍵變更為自動遞增

## 正在結束

只要對表格進行微幅修改，您就可以使用更快、更有效的增量複製方法。 不過，如果無法這麼做，您仍可採取其他步驟[縮短更新時間](../best-practices/reduce-update-cycle-time.md)和[最佳化您的資料庫](../best-practices/opt-db-analysis.md)。
