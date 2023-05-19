---
title: 更改度量的操作表
description: 瞭解如何更改度量用於執行其操作的資料表。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 更改度量的操作表

在某些情況下，您可能決定更改度量用於執行其操作的資料表。 例如，如果您有新的用戶表，則要從  `Users\_Old` 表格 `Users\_New` 的雙曲餘切值。

1. 轉到 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. 按一下 **[!UICONTROL Edit]** 與要切換的度量旁邊 `operational` 的子菜單。
1. 在編輯器中，按一下 **[!UICONTROL Change]**。

   ![](../../assets/change-metrics-1.png)
1. 選擇要基於此度量的新表。
1. 將現有資料維與新表中的相應資料維匹配。 例如，如果您有一個 `User's registration date`，只需選擇新表中記錄相同日期資料的列。 （如果新表中沒有匹配的列，請參閱下一步）

   ![](../../assets/change-metrics-2.png)

1. 如果新表中沒有匹配列，則可以 **在資料表中建立** 或 [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 如果它是由 [!DNL Commerce Intelligence]。 您也可以 **從度量中刪除維**。 要刪除不再需要的維，只需返回到度量的編輯器並選擇要刪除的維 `Dimensions`。

   ![](../../assets/change-metrics-3.png)
