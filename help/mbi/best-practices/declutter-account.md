---
title: 脫脂 [!DNL Commerce Intelligence] 帳戶
description: 瞭解如何清除 [!DNL Commerce Intelligence] 帳戶。
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 清理 [!DNL Adobe Commerce Intelligence] 帳戶

無論你和 [!DNL Commerce Intelligence] 在6個月或6年的時間裡，保持一個整潔的帳戶對您的組織來說至關重要，因為它能夠最大限度地利用平台。 隨著時間的推移，用戶、儀表板、報告、度量和列不再需要，這是很自然的。 也許您建立了一次性使用的報告，但忘記了報告，或者離開您公司的用戶從未停用其帳戶。

與 [標準化，清晰命名所有元素](../best-practices/naming-elements.md)) [!DNL Commerce Intelligence] 帳戶，下面的帳戶審核步驟可幫助您減少用戶的雜亂和不必要的分析。 另外一項好處包括 [可能更快的更新週期](../best-practices/reduce-update-cycle-time.md)。

## 步驟1:確定非活動用戶

清理帳戶的第一步是停用非活動用戶的帳戶，例如已離開公司或不再使用的用戶 [!DNL Commerce Intelligence] 在他們當前的角色中。

為此，請按一下右上導航欄中的公司名稱，然後選擇 **[!UICONTROL Manage Users]**。 接下來，選擇要停用的用戶，然後按一下 **[!UICONTROL Deactivate User]**。

>[!NOTE]
>
>你需要 [管理權限](../administrator/user-management/user-management.md) 做這個。

>[!WARNING]
>
>停用用戶將刪除該用戶建立的圖表、儀表板和其他資產。 如果要保留這些資產，請與 [!DNL Commerce Intelligence] [支援](../guide-overview.md#Submitting-a-Support-Ticket) 在停用用戶之前，先進行小組。 支援可幫助您將這些資產轉移給其他用戶。

### 重新激活用戶

要重新激活用戶，請通過使用已停用的相同電子郵件地址重新建立其帳戶來重新邀請用戶，並在登錄時恢復其訪問權限和擁有的資料。

## 步驟2:刪除未使用的儀表板和報表

審核帳戶的下一步是刪除任何未使用的儀表板和報告。

>[!NOTE]
>
>你需要 `Admin` 或 `Standard` [用戶權限](../administrator/user-management/user-management.md) 做這個。

每個用戶 `Admin` 或 `Standard` 訪問可以建立報表和儀表板。 因此，具有這些權限的所有人都必須遵循以下步驟來標識和刪除未使用的報告。

### 查看儀表板和報告

在刪除任何內容之前，您應查看報告和儀表板以評估正在使用的內容。 當您使用 **[!UICONTROL find unused reports]** 如下所述，任何初始審閱都會使您的清理工作效率更高。

### 刪除儀表板和報表

訪問儀表板和報表後，您可以開始清理帳戶。

**從儀表板中刪除報表**

1. 在儀表板上找到要刪除的報告。
1. 選擇 **[!UICONTROL Options]** 在報告右上角。
1. 按一下 **[!UICONTROL Remove From Dashboard]**。

**刪除整個儀表板**

1. 選擇 **[!UICONTROL Manage Data]**，然後是**[!UICONTROL Dashboards**]。
1. 按一下要刪除的儀表板。
1. 按一下 **[!UICONTROL Delete Dashboard]**。

也可以選擇 **[!UICONTROL Dashboard Options]**，則 **[!UICONTROL Delete]** 從儀表板本身。

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>刪除儀表板不會刪除其中的報表，因此您必須再執行一步來刪除報表。

**刪除未使用的報告**

1. 選擇 **[!UICONTROL Manage Data]**，則 **[!UICONTROL Reports]**。
1. 檢查 **僅顯示未使用的報告** 清單中的所有條目。 這將建立儀表板或電子郵件摘要中未使用的報告清單。
1. 選擇要刪除的報表。 可通過按一下報告清單上方的複選框來選擇全部。
1. 按一下 **[!UICONTROL Delete Selected]**。

下面是未使用的報告刪除過程：

![](../../mbi/assets/unused_reports.png)

## 第3步：刪除未使用的度量

清理了用戶清單、儀表板和報告後，您可以轉到審核度量清單。 這有助於您識別任何可能已過時的指標（例如，使用不同定義建立了新指標），或者沒有使用。

1. 要生成度量的從屬報告清單，請轉到 **[!DNL Manage Data]**，然後選擇按一下 **[!UICONTROL Metrics]**。
1. 按一下 **[!UICONTROL Edit]** 指標旁邊。
1. 在頁面底部，您看到一個名為 **[!UICONTROL Dependent Charts]**。 按一下連結可生成此度量的從屬報告清單。
1. 系統完成檢查後， [!DNL Commerce Intelligence] 顯示使用此度量的儀表板、報告和用戶的清單。

![](../../mbi/assets/report_dependecies.png)

如果確定不再需要度量，請導航回 **[!UICONTROL Metrics]** 按一下 **[!UICONTROL Back to Metric List]** 查找要刪除的度量。 按一下 **[!UICONTROL Delete]**。

## 第4步：評估同步列

最後一步是評估當前在Data Warehouse中同步的列。 不僅取消同步列會降低帳戶的安全性，還可能減少更新時間。

如果你想追查，請聯繫 [!DNL Commerce Intelligence] [支援](../guide-overview.md#Submitting-a-Support-Ticket)。 支援團隊可以建立一個報告，該報告包括所有未在任何儀表板中用於任何用戶的列，以及未在電子郵件摘要（不包括SQL報告）中使用的列。 然後，您可以使用此報告作為指南，選擇要通過Data Warehouse管理器取消同步的列。

>[!NOTE]
>
>您以後始終可以重新開始同步這些列。 取消同步列會從您的Data Warehouse中刪除任何資料；它只表示在更新週期中不檢查此列是否有新值或更新值。

**取消同步列（或列）**

1. 轉到 **[!DNL Manage Data]**，則 **[!UICONTROL Data Warehouse]**。
1. 在 **[!UICONTROL Synced Tables]** 清單，導航到包含該列的表。
1. 選中要取消同步的一個或多個列旁邊的一個或多個框。
   >[!NOTE]
   >
   >如果不刪除整個表，則無法取消同步主鍵列。

1. 按一下 **[!UICONTROL Remove]** 取消同步一個或多個列。

下面是整個過程：

![](../../mbi/assets/drop_column.png)

## 收尾

您 [!DNL Commerce Intelligence] 現在，客戶應該更輕鬆，更便於您和您的團隊瀏覽。
