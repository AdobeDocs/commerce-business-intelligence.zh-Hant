---
title: 管理儀表板
description: 瞭解如何管理您擁有的儀表板的使用者許可權、刪除您不再需要的儀表板，以及設定預設儀表板。
exl-id: 32c21093-2a7d-4d8e-afc0-19bd702f9b36
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 管理儀表板

>[!NOTE]
>
>需要 [管理員許可權](../../administrator/user-management/user-management.md).

在 **[!DNL Manage Data** > **Dashboards]**，您可以管理自己所擁有控制面板的使用者許可權、刪除不再需要的控制面板，以及設定預設控制面板。 本主題涵蓋：

1. [重新命名儀表板](#rename)

1. [管理儀表板許可權](#userperm)

1. [變更預設儀表板](#default)

1. [刪除儀表板](#delete)

## 重新命名控制面板 {#rename}

若要重新命名儀表板：

1. 按一下您要變更的控制面板名稱。

2. 輸入新名稱，在 `Dashboard Name` 欄位。

## 管理使用者許可權 {#userperm}

中存在三個存取層級 [!DNL Commerce Intelligence] 針對儀表板 —  `View`， `Edit`、和 `None`.

* `View` 可讓選取的使用者檢視控制面板，但無法加以編輯。 使用者也可調整圖表大小、匯出資料，以及使用「另存新檔」功能將圖表複製到自己的控制面板上（如果使用者擁有標準或管理員許可權）。

* `Edit` 如果選取的使用者擁有標準或管理員許可權，則可編輯圖表並儲存至此儀表板。 此外，擁有編輯許可權的使用者也可以與其他使用者共用控制面板。

* `None` 這表示選取的使用者無法檢視或編輯此控制面板。

變更使用者許可權有兩種方式：針對所有使用者或個別使用者。

1. *若要變更所有使用者的許可權，* 使用「 」旁的下拉式選單 `Set all users' permissions to…` 標籤。

1. *若要變更個別使用者的許可權，* 使用使用者名稱旁邊的下拉式選單來設定所需的存取層級。

## 變更預設儀表板 {#default}

若要變更帳戶的預設儀表板：

1. 按一下您要做為預設的儀表板名稱。

1. 按一下 **[!UICONTROL Make Default]**.

## 刪除儀表板 {#delete}

若要刪除控制面板：

1. 按一下要刪除的控制面板名稱。

1. 按一下 **[!UICONTROL Delete Dashboard]**.
