---
title: 去除您的 [!DNL Commerce Intelligence] 帳戶
description: 瞭解如何清理您的 [!DNL Commerce Intelligence] 帳戶。
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 清理您的 [!DNL Adobe Commerce Intelligence] 帳戶

無論您是否曾與 [!DNL Commerce Intelligence] 在六個月或六年的時間裡，保持合理的帳戶對於貴組織充分運用平台至關重要。 長期下來，通常會有一些使用者、控制面板、報表、量度和欄不再需要這些專案。 您可能建立了報表以供一次性使用，但已忘記該報表，或離開貴公司的使用者從未停用帳戶。

替換為 [標準化、清除所有元素的命名](../best-practices/naming-elements.md)的) [!DNL Commerce Intelligence] 帳戶，以下帳戶稽核步驟可協助您減少使用者的雜亂和不必要的分析。 一個額外的權益包括 [更新週期可能更快](../best-practices/reduce-update-cycle-time.md).

## 步驟1：識別非作用中的使用者

清理帳戶的第一步是停用非作用中使用者的帳戶，例如已離開公司或不再使用的使用者 [!DNL Commerce Intelligence] 他們目前的角色。

若要這麼做，請按一下右上角導覽列中的公司名稱，然後選取 **[!UICONTROL Manage Users]**. 接著，選取您要停用的使用者，然後按一下 **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>您需要 [管理員許可權](../administrator/user-management/user-management.md) 以執行此操作。

>[!WARNING]
>
>停用使用者會移除該使用者建立的圖表、儀表板和其他資產。 如果您想要保留這些資產，請聯絡 [!DNL Commerce Intelligence] [支援](../guide-overview.md#Submitting-a-Support-Ticket) 團隊。 支援可協助您將這些資產轉移給其他使用者。

### 重新啟用使用者

若要重新啟用使用者，請使用已停用的相同電子郵件地址重新建立其帳戶，以重新邀請使用者，並在登入時還原其存取權和擁有的資料。

## 步驟2：刪除未使用的儀表板和報表

稽核帳戶的下一個步驟是刪除任何未使用的儀表板和報表。

>[!NOTE]
>
>您需要 `Admin` 或 `Standard` [使用者許可權](../administrator/user-management/user-management.md) 以執行此操作。

每位使用者具有 `Admin` 或 `Standard` 存取可建立報告和儀表板。 因此，擁有這些許可權的所有人都必須遵循下列步驟，以識別並移除未使用的報表。

### 檢閱您的儀表板和報表

在刪除任何專案之前，您應該檢閱報告和儀表板，以評估正在使用的專案。 雖然您可以使用 **[!UICONTROL find unused reports]** 這項功能如下所述，任何初步審查都會讓您的清理工作更有效率。

### 刪除控制面板和報表

存取控制面板和報表後，您就可以開始清理帳戶。

**從控制面板移除報表**

1. 在控制面板上找出您要移除的報告。
1. 選取 **[!UICONTROL Options]** 報表的右上角。
1. 按一下 **[!UICONTROL Remove From Dashboard]**.

**刪除整個儀表板**

1. 選取 **[!UICONTROL Manage Data]**，然後**[!UICONTROL Dashboards**].
1. 按一下您要刪除的控制面板。
1. 按一下 **[!UICONTROL Delete Dashboard]**.

您也可以選取 **[!UICONTROL Dashboard Options]**，然後 **[!UICONTROL Delete]** 從儀表板本身。

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>刪除儀表板不會刪除其中的報告，因此您必須再執行一個步驟來刪除報告。

**若要刪除未使用的報表**

1. 選取 **[!UICONTROL Manage Data]**，然後 **[!UICONTROL Reports]**.
1. 檢查 **僅顯示未使用的報告** 方塊。 這會建立一份報告清單，列出未在控制面板或電子郵件摘要中使用的報告。
1. 選取您要刪除的報告。 您可以按一下報表清單上方的核取方塊來選取全部。
1. 按一下 **[!UICONTROL Delete Selected]**.

以下是未使用報表刪除程式的概覽：

![](../../mbi/assets/unused_reports.png)

## 步驟3：刪除未使用的量度

清除使用者清單、控制面板和報表後，您就可以開始稽核量度清單。 這可協助您識別任何可能已過期或未使用的專案，例如，已使用不同定義建立的新量度。

1. 若要產生量度的相依報表清單，請前往 **[!DNL Manage Data]**，然後選取按一下 **[!UICONTROL Metrics]**.
1. 按一下 **[!UICONTROL Edit]** 量度旁。
1. 在頁面底部，您會看到名為的區段 **[!UICONTROL Dependent Charts]**. 按一下連結，即可產生此量度的相依報表清單。
1. 系統完成檢查後， [!DNL Commerce Intelligence] 顯示使用此量度的控制面板、報表和使用者清單。

![](../../mbi/assets/report_dependecies.png)

如果您決定不再需要該量度，請導覽回 **[!UICONTROL Metrics]** 按一下以建立頁面 **[!UICONTROL Back to Metric List]** 以尋找您要刪除的量度。 按一下 **[!UICONTROL Delete]**.

## 步驟4：評估您的同步欄

最後一個步驟是評估Data Warehouse中目前同步的欄。 取消同步資料行不僅會減少帳戶的負擔，還有可能縮短更新時間。

如果您想要達成此目的，請聯絡 [!DNL Commerce Intelligence] [支援](../guide-overview.md#Submitting-a-Support-Ticket). 支援團隊可建立一份報表，其中包含所有未在任何使用者的控制面板中使用，以及未用於電子郵件摘要的所有欄，但不包括SQL報表。 然後，您可以使用此報表作為透過「Data Warehouse管理員」選取要取消同步之欄的指南。

>[!NOTE]
>
>您日後一律可以再次開始同步這些欄。 取消同步欄會從Data Warehouse中移除任何資料；這僅表示在更新週期期間不會檢查此欄是否有新值或更新值。

**取消同步欄（或欄）**

1. 前往 **[!DNL Manage Data]**，然後 **[!UICONTROL Data Warehouse]**.
1. 在 **[!UICONTROL Synced Tables]** 清單，導覽至包含欄的表格。
1. 勾選一或多個要取消同步之欄旁的一或多個方塊。
   >[!NOTE]
   >
   >您不刪除整個資料表就無法取消同步處理主索引鍵資料行。

1. 按一下 **[!UICONTROL Remove]** 以取消同步一或多個欄。

以下是整個程式的概況：

![](../../mbi/assets/drop_column.png)

## 正在結束

您的 [!DNL Commerce Intelligence] 您和您的團隊現在應該可以更整潔、更輕鬆地導覽帳戶。
