---
title: 連線Microsoft SQL Server
description: 瞭解如何將Microsoft SQL資料庫連結至 [!DNL Commerce Intelligence] 四個步驟的流程。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 連線 [!DNL Microsoft SQL] 伺服器

>[!NOTE]
>
>需要 [管理員許可權](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

本主題說明如何連結 [!DNL Microsoft SQL] 資料庫至 [!DNL Commerce Intelligence] 四個步驟的流程。 此程式需要伺服器連線和SQL的相關技術專業知識，並且可能需要團隊開發人員的支援。

[!DNL Commerce Intelligence] 支援 [!DNL Amazon RDS]， [!DNL EC2]， [!DNL Microsoft SQL Azure]和大部分其他雲端伺服器提供者。 如果您對特定主機有疑問， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 要求我們提供此資訊。

您的系統需要對資料庫執行SELECT查詢。 這項作業最初是為了取得資料庫結構的快照，然後定期超時以保持資料最新。 您的更新是漸進式的，而Adobe會限制更新頻率和時間，以防止伺服器上出現任何不想要的負載。

最佳方法是透過TCP/IP連線到您的資料庫伺服器。 建立僅能執行SELECT查詢的使用者（以及選擇性地僅能選取您指定之資料表中的資料）。 您必須針對要連線的每個伺服器執行此作業 [!DNL Commerce Intelligence].

## 正在連線 `Microsoft SQL` 至 [!DNL Commerce Intelligence]：

1. 請確定您的伺服器允許透過TCP/IP和混合模式驗證進行連線。

1. 請確定您的防火牆允許伺服器的專用IP連線。

   您可以在的連線區段中找到用來連線至伺服器的IP位址 `Settings` 頁面。

1. 建立用來登入資料庫伺服器的使用者。 您有兩個選項；可以透過 `UI` 或透過 `query`：
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （第二個範例）

1. 在中輸入伺服器IP位址、使用者名稱和密碼 [!DNL Commerce Intelligence] 在 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. 按一下 **[!UICONTROL Add a Data Source]**.

1. 選取以連線 `Microsoft SQL` 資料庫並在新資料庫上的欄位中輸入您的認證 `Connections` 頁面。

   如果您使用 `Windows Azure`，您也必須指定資料庫名稱。
