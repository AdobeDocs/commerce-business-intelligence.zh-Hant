---
title: 限制量度存取
description: 了解如何使用量度存取和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 管理量度使用者

除了設定使用者權限層級外，您也可以依使用者限制對量度的存取。 例如，如果您希望您的會計部門能夠存取收入相關量度，但不能存取使用者贏取量度，則可以限制存取這些量度。

在這類情況下，Adobe建議將該使用者的帳戶設為 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 權限應授予不需要建立或變更量度、計算欄、整合或使用者，但他們需要存取Data Warehouse中的資料的使用者。 如果您想要完全限制對資料的存取，請使用 **[!UICONTROL Read Only]** 權限。

設定權限層級後，您可以選取 **[!UICONTROL Standard]** 使用者可透過下列方式來存取：

1. 前往 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 選取所需的使用者帳戶。
1. 此 **[!UICONTROL Metrics]** 索引標籤會顯示可用度量的清單。 檢查您希望使用者有權存取的量度；取消選取使用者不應具有存取權的項目。
1. [!DNL MBI] 自動保存更改。 如果變更成功， [!DNL MBI] 顯示 **[!UICONTROL Saved!]** 頁面頂端。

>[!NOTE]
>
>具有 **[!UICONTROL Standard]** 除了Data Warehouse中的所有量度外，權限還可透過「資料匯出」存取 [!DNL Google Analytics].

您也可以編輯量度並限制對量度的存取 **[!UICONTROL Standard]** 在 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 區段。

>[!NOTE]
>
>如果您複製量度， [!DNL MBI] 複製原始量度中設定的使用者權限。
