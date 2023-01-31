---
title: 了解資料庫和SQL編輯器之間的結果
description: 了解資料庫和SQL編輯器之間的結果。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 資料庫結果與 `SQL Editor` 結果

你也許很好奇 `Last successful update began` 欄位位於 `Integrations` 頁面：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 了解 `timestamp` 欄位

它顯示開始 `timestamp` （在帳戶上設定的時區） _上次成功更新週期_ 在你的賬戶上。

- 如果任何同步的表在上次更新週期期間發生問題，則此時間戳為 *未更新*.
- 因此，在某些情況下，報表可能已更新為最新資料，但 *上次成功更新開始* 仍然滯後。

## 識別「真實」的最後一個資料點

特定整合的最新資料點由 `Last Data Point Received` `timestamp` 位於每個整合的右側。 該時間戳記是指您的資料倉庫成功從該來源接收資料點的最後一個時間點，無論是資料庫、API或協力廠商整合。

檢查資料的新鮮度 *特定表*，建議您建立快速 [SQL報告](../../dev-reports/sql-rpt-bldr.md) 執行 `MAX(timestamp)` 在您帳戶中最重要的表格上。 將此時間戳記與 `Last Data Point` 會指出問題是否影響整個帳戶或表格的子集。 我們建議對三到四個常用的重要表執行此操作。

- 若 `MAX(timestamp)` 值最近於 `Last Data Point Received`，這表示表的子集受到影響，但整體帳戶的更新週期穩定。
- 若 `MAX(timestamp)` 值等於或之前 `Last Data Point Received`，表示帳戶的更新週期會受到影響。 在這種情況下， [提交支援票證](../../../guide-overview.md).
