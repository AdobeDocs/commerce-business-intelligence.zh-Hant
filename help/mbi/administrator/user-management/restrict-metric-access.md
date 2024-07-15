---
title: 限制量度存取
description: 瞭解如何使用量度存取和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 管理量度使用者

除了設定使用者許可權層級外，您也可以根據個別使用者來限制量度的存取權。 例如，如果您希望會計部門可以存取收入相關度量，但不能存取使用者贏取度量，則可以限制這些度量的存取權。

在這樣的情況下，Adobe建議將該使用者的帳戶設定為&#x200B;**[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**。 應該向不需要建立或變更量度、計算欄、整合或使用者的使用者授予&#x200B;**[!UICONTROL Standard]**&#x200B;許可權，但他們確實需要存取Data Warehouse中的資料。 如果您想要完全限制資料的存取，請改用&#x200B;**[!UICONTROL Read Only]**&#x200B;許可權。

設定許可權層級後，您可以執行下列動作，選取&#x200B;**[!UICONTROL Standard]**&#x200B;使用者可以存取的量度：

1. 前往&#x200B;**[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**。
1. 選取所需的使用者帳戶。
1. **[!UICONTROL Metrics]**&#x200B;索引標籤會顯示可用量度的清單。 勾選您要讓使用者存取的量度，並取消選取使用者不應該存取的量度。
1. [!DNL Adobe Commerce Intelligence]會自動儲存變更。 如果變更成功，[!DNL Commerce Intelligence]會在頁面頂端顯示&#x200B;**[!UICONTROL Saved!]**。

>[!NOTE]
>
>除了來自[!DNL Google Analytics]的所有量度之外，所有具有&#x200B;**[!UICONTROL Standard]**&#x200B;許可權的使用者都可以透過「資料匯出」存取Data Warehouse中的所有資料。

您也可以編輯量度，並在&#x200B;**[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**&#x200B;區段中選取&#x200B;**[!UICONTROL Standard]**&#x200B;位使用者，以限制量度的存取權。

>[!NOTE]
>
>如果您複製量度，[!DNL Commerce Intelligence]會複製在原始量度中設定的使用者許可權。
