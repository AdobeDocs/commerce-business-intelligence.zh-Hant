---
title: 限制度量訪問
description: 瞭解如何使用度量訪問和限制。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 管理度量用戶

除了設定用戶權限級別外，您還可以按用戶限制對度量的訪問。 例如，如果您希望您的會計部門有權訪問與收入相關的指標，但不能訪問用戶獲取指標，則可以限制訪問這些指標。

在此類情況下，Adobe建議將用戶帳戶設定為 **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**。 **[!UICONTROL Standard]** 應向不需要建立或更改度量、計算列、整合或用戶的用戶授予權限，但他們確實需要訪問Data Warehouse中的資料。 如果要完全限制對資料的訪問，請使用 **[!UICONTROL Read Only]** 權限。

在設定權限級別後，您可以選擇 **[!UICONTROL Standard]** 用戶可通過執行以下操作來訪問：

1. 轉到 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**。
1. 選擇所需的用戶帳戶。
1. 的 **[!UICONTROL Metrics]** 頁籤顯示可用度量的清單。 檢查希望用戶有權訪問的度量，並取消選擇用戶無權訪問的度量。
1. [!DNL Adobe Commerce Intelligence] 自動保存更改。 如果更改成功， [!DNL Commerce Intelligence] 顯示 **[!UICONTROL Saved!]** 頁面頂部。

>[!NOTE]
>
>所有用戶 **[!UICONTROL Standard]** 權限可以通過「資料導出」以及Data Warehouse中的所有度量訪問所有資料 [!DNL Google Analytics]。

也可以通過編輯度量和 **[!UICONTROL Standard]** 在 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 的子菜單。

>[!NOTE]
>
>如果複製度量， [!DNL Commerce Intelligence] 複製原始度量中設定的用戶權限。
