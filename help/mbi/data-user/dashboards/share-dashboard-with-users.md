---
title: 與其他使用者共用儀表板
description: 瞭解如何與其他使用者共用控制面板。
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 與其他使用者共用儀表板

共用儀表板是讓您的團隊處於循環中並鼓勵合作討論的絕佳方法。 透過建立和共用中央儀表板，您可以在維持控制權的同時，為團隊提供所需的資訊。 [[!DNL Adobe] 建議](../../best-practices/share-dashboard-best-practice.md){： target=&quot;_blank&quot;}您授予的 `Edit` 少數幾個的許可權，可將意外的變更降至最低。

>[!NOTE]
>
>如果您共用的控制面板包含以特定使用者無權存取的量度建立的報告，則報告會顯示 `Error Loading Data` 訊息。 如果您希望資料顯示給特定使用者，請 [管理員使用者](../../administrator/user-management/user-management.md) 必須授與存取權給這些報表中使用的所有量度。

## 共用儀表板

1. 按一下 **[!UICONTROL Share Dashboard]** ，位於畫面頂端。

   您的所有使用者清單 [!DNL Commerce Intelligence] 帳戶將會顯示。

1. 若要選取要與其共用控制面板的使用者，請核取其名稱左側的方塊。

   若要選取/取消選取所有使用者，請按一下 **[!UICONTROL Select]** 並選取 `Everyone` 或 `None`，依序輸入。

1. 許可權可依個別使用者或整體設定。

   *若要設定個別許可權*，按一下 **[!UICONTROL None]** 位於使用者名稱右側。 從此下拉式清單中，選取使用者應具有的許可權型別。

   *若要大量設定許可權*，按一下 **[!UICONTROL Set Permissions]**. 從此下拉式清單中，選取所選使用者應具有的許可權型別。

   >[!NOTE]
   >
   >您也可以使用此功能來更新先前設定的許可權。 例如，如果您要停止與某人共用控制面板，請將其許可權設為 `None`.

1. 若要共用控制面板，請按一下 **[!UICONTROL Save Changes]**. 選取的使用者會收到電子郵件邀請他們檢視控制面板。

範例：

![共用儀表板](../../assets/Share_Dashboards.gif)
