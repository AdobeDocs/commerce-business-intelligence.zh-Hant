---
title: 瞭解資料庫和SQL編輯器之間的結果
description: 瞭解資料庫和SQL編輯器之間的結果。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 資料庫結果與 [!DNL SQL Editor] 結果

你可能好奇 `Last successful update began` 欄位位於 `Integrations` 頁：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## 瞭解 `timestamp` 場

它顯示了 `timestamp` （在帳戶上設定的時區） _上次成功更新週期_ 你的賬戶。

- 如果任何同步表在上次更新週期中遇到問題，則此時間戳為 *未更新*。
- 因此，可能有報告已用新資料更新，但 *上次成功更新開始* 還在落後。

## 確定「真實」的最後一個資料點

特定整合的最新資料點由 `Last Data Point Received` 位於每個整合右側的時間戳。 該時間戳是指Data Warehouse成功從該源接收資料點（無論是資料庫、 API還是第三方整合）的最後一個點。

檢查資料的新鮮度 *特定表*,Adobe建議建立快速 [[!DNL SQL] 報告](../../dev-reports/sql-rpt-bldr.md) 執行 `MAX(timestamp)` 你帳戶上最重要的表格。 將此時間戳與 `Last Data Point` 指示問題是否影響整個帳戶或表的子集。 Adobe建議對三到四個常用的重要表執行此操作。

- 如果 `MAX(timestamp)` 值比 `Last Data Point Received`，表示表的子集受到了影響，但總帳戶的更新週期穩定。
- 如果 `MAX(timestamp)` 值等於或早於 `Last Data Point Received`，表示帳戶的更新週期受到影響。 在這種情況下， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
