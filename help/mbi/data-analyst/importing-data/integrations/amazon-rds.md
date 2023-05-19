---
title: 連接AmazonRDS
description: 瞭解連接RDS實例的步驟。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# 連接 [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] 是在資料庫引擎上運行的托管資料庫服務，您可能已經熟悉它：

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

連接您的 [!DNL RDS] 實例會有所不同，具體取決於所使用的資料庫類型以及您是否使用加密連接(如 [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))，但這裡是基本的。

## 授權 [!DNL Commerce Intelligence] 訪問資料庫

在憑據頁(**[!UICONTROL Manage Data** > **Integrations]**)中，您會看到一個框，其中包含必須授權才能連接R的IP地址[!DNL RDS] 至 [!DNL Commerce Intelligence]: `54.88.76.97` 和 `34.250.211.151`。 這裡是 `MySQL credentials` 頁，其中您突出顯示了IP地址框：

![](../../../assets/RDS_IP.png)

對於 [!DNL Commerce Intelligence] 與 [!DNL RDS] 實例中，必須通過AWS管理控制台將這些IP地址添加到相應的資料庫安全組。 這些IP地址可以添加到現有組中，也可以建立一個IP地址 — 重要的是，組有權訪問要連接到的實例 [!DNL Commerce Intelligence]。

添加 [!DNL Commerce Intelligence] IP地址，確保添加 `/32` 到地址的末尾，以指示 [!DNL Amazon] 它是一個確切的IP地址。 別擔心；AWS介面明確表示這是必需的。

## 建立 `Linux` 用戶 [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>只有在使用加密連接時，才需要此步驟。 有關如何執行此操作的說明，請參閱所使用資料庫的設定主題(例如：MySQL)。 的 `Linux` 用戶允許我們建立 `SSH tunnel`這是最安全的通過網際網路發送資料的方法。

## 為建立資料庫用戶 [!DNL Commerce Intelligence]

這是流程中步驟不同的部分，具體取決於所使用的資料庫。 但是，這個想法是相同的，你為 [!DNL Commerce Intelligence] 用於訪問資料庫。 建立資料庫的說明 [!DNL Commerce Intelligence] 在所使用資料庫的設定主題中找到用戶。

## 在中輸入連接資訊 [!DNL Commerce Intelligence]

在你同意 [!DNL Commerce Intelligence] 訪問您的實例並為我們建立用戶，您最不需要做的就是輸入連接資訊 [!DNL Commerce Intelligence]。

的憑據頁 `MySQL`。 `Microsoft SQL`, `PostgreSQL` 通過 `Integrations` 頁(P)**[!UICONTROL Manage Data** > **Integrations]**) **[!UICONTROL Add Integration]**。 顯示整合清單時，按一下用於轉至「身份證明」頁的資料庫表徵圖。 如果您當前沒有訪問所需整合的權限，請與Adobe帳戶團隊聯繫。

要完成連接的建立，需要以下資訊：

* RDS實例的公用地址：可以在 [!DNL AWS] 管理控制台。
* 資料庫實例使用的埠：某些資料庫具有預設埠，該埠會自動填充 `Port` 的子菜單。 此資訊也可以在資料庫的安裝文檔中找到。
* 為建立的用戶的用戶名和密碼 [!DNL Commerce Intelligence]。

如果使用加密連接，請更改 `Encrypted` 在「資料庫憑據」頁上切換到 `Yes`。 這將顯示用於設定加密的額外表單：

![](../../../assets/sql-integration-encrypted-yes.png)


