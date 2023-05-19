---
title: SQL與Data Warehouse管理器的差異
description: 瞭解SQL和Data Warehouse管理器之間的區別。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 差異 [!DNL SQL] 和 [!DNL Data Warehouse Manager]

在 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 和那些用 [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md)。 一個是對更新週期的依賴，另一個是列如何保存在帳戶中。

## 中的列 [!DNL SQL Report Builder]

列不依賴於更新週期，因此您不必再等待一個更新週期完成，然後才能迭代列。 如果你犯了錯誤，只需按幾下鍵就可以糾正它 — 不再等待兩個更新完成，然後才能恢復工作。

>[!IMPORTANT]
>
>使用建立的列 [!DNL SQL] 編輯器未保存到您的Data Warehouse。 您始終有權訪問包含該列的查詢，但如果要在多個報表中使用該列，則必須在每個報表的查詢中重新建立該列。 這意味著使用 [!DNL SQL] 不能在傳統 [!DNL Report Builder]。

## Data Warehouse管理器中的列

列取決於更新週期，因此必須先完成完整週期，然後才能編輯它們。 這些列將保存到「Data Warehouse管理器」中，並可用於傳統 [!DNL Report Builder] 或 [!DNL SQL Report Builder]。
