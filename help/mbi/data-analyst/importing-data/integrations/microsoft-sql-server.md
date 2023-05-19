---
title: 連接MicrosoftSQL Server
description: 瞭解如何將您的MicrosoftSQL資料庫連接到 [!DNL Commerce Intelligence] 四步法。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 連接 [!DNL Microsoft SQL] 伺服器

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

![](../../../assets/MicrosoftSQLServer-logo.png)

本主題說明如何連接 [!DNL Microsoft SQL] 資料庫 [!DNL Commerce Intelligence] 四步法。 此過程需要一些與伺服器連接和SQL相關的技術專業知識，並且可能需要您團隊中的開發人員的支援。

[!DNL Commerce Intelligence] 支援 [!DNL Amazon RDS]。 [!DNL EC2]。 [!DNL Microsoft SQL Azure]，以及大多數其他雲伺服器提供商。 如果你對你的主人有疑問， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 要求我們提供這些資訊。

您的系統需要對資料庫運行SELECT查詢。 這首先是為了獲取資料庫結構的快照，然後定期加班以保持資料最新。 您的更新是增量的，Adobe會限制更新頻率和時間，以防止伺服器上的任何不需要的載入。

最好的方法是通過TCP/IP連接到資料庫伺服器。 為我們建立只能運行SELECT查詢的用戶（可選地，只能從您指定的表中選擇資料）。 必須針對您要連接到的每台伺服器執行此操作 [!DNL Commerce Intelligence]。

## 連接 `Microsoft SQL` 至 [!DNL Commerce Intelligence]:

1. 確保伺服器允許通過TCP/IP和混合模式身份驗證進行連接。

1. 確保防火牆允許您伺服器的專用IP連接。

   您可以在連接部分中找到用於連接到伺服器的IP地址 `Settings` 的子菜單。

1. 建立用於登錄到資料庫伺服器的用戶。 你有兩個選擇。通過 `UI` 或通過 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （第二個示例）

1. 在中輸入伺服器IP地址、用戶名和密碼 [!DNL Commerce Intelligence] 在 **[!UICONTROL Manage Data** > **Connections]**。

   ![](../../../assets/manage-data-connections.png)

1. 按一下 **[!UICONTROL Add a Data Source]**。

1. 選擇以連接 `Microsoft SQL` 並在新的 `Connections` 的子菜單。

   如果您使用 `Windows Azure`，您還必須指定資料庫名稱。
