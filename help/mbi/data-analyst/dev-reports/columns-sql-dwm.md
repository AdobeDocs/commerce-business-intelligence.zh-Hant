---
title: SQL與Data Warehouse管理器之間的差異
description: 了解SQL與Data Warehouse管理器之間的差異。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# SQL與Data Warehouse管理器之間的差異

在 [SQLReport Builder](../dev-reports/sql-rpt-bldr.md) 和使用 [Data Warehouse管理員](../data-warehouse-mgr/creating-calculated-columns.md):一個是對更新週期的依賴，另一個是欄在帳戶中的儲存方式。

## 中的欄 `SQL Report Builder`

欄與更新週期無關，因此您不必再等待一個完成，便可反覆計算欄。 如果你犯了錯誤，只需按幾下鍵來糾正它 — 就不必再等待兩個更新完成，然後才能恢復工作。

>[!IMPORTANT]
>
>使用SQL編輯器建立的列不會保存到Data Warehouse。 您始終可以訪問包含該列的查詢，但如果要在多個報表中使用該列，則必須在每個報表的查詢中重新建立該列。 這表示使用SQL編輯器建立的列不能用於傳統 `Report Builder`.

## Data Warehouse管理器中的欄

欄取決於更新週期，因此必須先完成完整週期，才能進行編輯。 這些欄會儲存至「Data Warehouse管理員」，並可用於傳統 `Report Builder` 或 `SQL Report Builder`.
