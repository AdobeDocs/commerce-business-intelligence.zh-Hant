---
title: 連接Microsoft&reg;&reg;SQL Server
description: 了解如何連接您的Microsoft&reg;SQL資料庫要 [!DNL MBI] 四步進程。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 連接Microsoft® SQL Server

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

本文說明如何連接您的 `Microsoft SQL` 資料庫 [!DNL MBI] 四步進程。 此過程需要一些與伺服器連接和SQL相關的技術專業知識，並且可能需要您團隊的開發人員的支援。

MBI支援 [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft®; SQL Azure]，以及大部分其他雲端伺服器提供者。 如果你對你的主人有疑問， [提交支援票證](../../../guide-overview.md) 要求我們提供這些資訊。

您的系統需要對資料庫運行SELECT查詢。 這最初是為了獲取資料庫結構的快照，然後定期加班以保持資料最新。 您的更新是增量的，Adobe會限制更新的頻率和時間，以防止伺服器上出現任何不想要的載入。

最好的方法是通過TCP/IP連接到資料庫伺服器。 為我們建立只能運行SELECT查詢的用戶（可選，只能從您指定的表中選擇資料）。 您必須針對您所連線的每個伺服器執行此操作 [!DNL MBI].

## 連接 `Microsoft SQL` to [!DNL MBI]:

1. 確保伺服器允許通過TCP/IP和混合模式身份驗證進行連接。

1. 確保防火牆允許您伺服器的專用IP連接。

   您可以在的 `Settings` 頁面。

1. 建立用於登錄到資料庫伺服器的用戶。 你有兩個選擇；透過 `UI` 或透過 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （第二個範例）

1. 在中輸入伺服器IP位址、使用者名稱和密碼 [!DNL MBI] 在 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. 按一下 **[!UICONTROL Add a Data Source]**.

1. 選擇以連接 `Microsoft SQL` 資料庫，並在新 `Connections` 頁面。

   如果您使用 `Windows Azure`，您也必須指定資料庫名稱。
