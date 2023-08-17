---
title: 變更量度的作業表格
description: 瞭解如何變更量度用來執行其操作的資料表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 變更量度的作業表格

在某些情況下，您可以決定變更量度用來執行操作的資料表格。 例如，如果您有新的使用者表格，您想要將使用者相關量度從  `Users\_Old` 表格以使用 `Users\_New` 表格。

1. 前往 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 按一下 **[!UICONTROL Edit]** 位於您要切換的量度旁 `operational` 表格。
1. 在編輯器中，按一下 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. 選取您要以此量度為基礎的新表格。
1. 比對現有資料維度與新表格中對應的資料維度。 例如，如果您有一個名為 `User's registration date`，只要選取新表格中哪一欄記錄相同的日期資料即可。 （如果新表格中沒有相符的欄，請參閱下一步）

   ![](../../assets/change-metrics-2.png)

1. 如果新表格中沒有相符的欄，您可以 **在您的資料表中建立它** 或 [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果是由建立的計算欄或維度 [!DNL Commerce Intelligence]. 您也可以 **從量度中刪除維度**. 若要刪除您不再需要的維度，只需返回量度的編輯器，並選取要刪除的維度 `Dimensions`.

   ![](../../assets/change-metrics-3.png)
