---
title: SQL與Data Warehouse管理員之間的差異
description: 瞭解SQL和Data Warehouse管理員之間的差異。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 兩者之間的差異 [!DNL SQL] 和 [!DNL Data Warehouse Manager]

在中建立的欄之間有兩個主要差異 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 以及使用 [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). 一個是與更新週期的相依性，另一個是欄如何儲存在您的帳戶中。

## 中的欄 [!DNL SQL Report Builder]

欄不依賴更新週期，因此您不必再等待一個欄完成即可對欄進行反複運算。 如果發生錯誤，只需要按幾下按鍵即可進行修正，不必再等待兩次更新完成後才能重新開始工作。

>[!IMPORTANT]
>
>您使用建立的欄 [!DNL SQL] 編輯器未儲存至您的Data Warehouse。 您一律可以存取包含欄的查詢，但如果您想要在多個報表中使用欄，則必須在每個報表的查詢中重新建立該欄。 這表示使用建立的欄 [!DNL SQL] 編輯器不能用在傳統中 [!DNL Report Builder].

## Data Warehouse管理員中的欄

欄取決於更新週期，因此必須先完成一個完整的週期，然後才能對其進行編輯。 這些欄會儲存至「Data Warehouse管理員」，並可在傳統檔案中使用 [!DNL Report Builder] 或 [!DNL SQL Report Builder].
