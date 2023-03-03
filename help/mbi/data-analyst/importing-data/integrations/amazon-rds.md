---
title: 連接Amazon RDS
description: 了解連接RDS實例的步驟。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 連接Amazon RDS

Amazon關係資料庫服務(RDS)是一種托管資料庫服務，在您可能已經熟悉的資料庫引擎上運行。 [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)，和 [[!DNL PostgreSQ]](../integrations/postgresql.md).

連接RDS實例的步驟會根據您使用的資料庫類型（使用上面的連結獲取每個資料庫的詳細說明）以及您是否使用加密連接(如 [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))，但基本功能如下：

## 授權 [!DNL MBI] 訪問資料庫

在憑證頁面(**[!UICONTROL Manage Data** > **Integrations]**)，您將看到一個框，其中包含您需要授權才能將RDS連接到MBI的IP地址： `54.88.76.97` 和 `34.250.211.151`. 以下是 `MySQL credentials` 頁面中，我們突出顯示了IP地址框：

![](../../../assets/RDS_IP.png)

針對 [!DNL MBI] 要成功與您的RDS實例連接，您需要通過AWS管理控制台將這些IP地址添加到相應的資料庫安全組。 這些IP位址可以新增至現有群組，或者您可以建立新的群組 — 重要的是，群組已獲授權可存取您要連線的執行個體 [!DNL MBI].

新增 [!DNL MBI] IP位址，請務必新增 `/32` 到位址的結尾，以向Amazon指出這是確切的IP位址。 別擔心；AWS介面會明確指出這是必要項目。

## 建立 `Linux` 用戶 [!DNL MBI] {#linux}

>[!NOTE]
>
>只有在您使用加密的連線時，才需要執行此步驟。 有關如何執行此操作的說明，請參閱使用之資料庫的設定文章(例如：MySQL)。 此 `Linux` 使用者可讓我們建立 `SSH tunnel`，這是最安全的透過網際網路傳送資料的方法。

## 為MBI建立資料庫用戶

這是程式的一部分，其中的步驟會因您使用的資料庫而異。 不過，其想法是相同的：您將為 [!DNL MBI] 用於訪問資料庫。 建立資料庫的說明 [!DNL MBI] 您可以在您使用之資料庫的設定文章中找到使用者。

## 在MBI中輸入連接資訊

在你同意 [!DNL MBI] 存取您的執行個體並為我們建立使用者，您最不需要做的就是在中輸入連線資訊 [!DNL MBI].

的憑據頁 `MySQL`, `Microsoft SQL`，和 `PostgreSQL` 可透過 `Integrations` 頁面(**[!UICONTROL Manage Data** > **Integrations]**) **[!UICONTROL Add Integration]**. 顯示整合清單時，按一下您用來前往認證頁面之資料庫的圖示。 如果您目前沒有存取所需整合的權限，請連絡您的Adobe帳戶團隊。

要完成連接的建立，我們需要以下資訊：

* RDS實例的公用地址：您可在AWS管理主控台中找到。
* 資料庫實例使用的埠：有些資料庫有預設埠，會自動填入 `Port` 欄位。 此資訊也可在資料庫的設定檔案中找到。
* 您為建立的用戶的用戶名和密碼 [!DNL MBI].

如果您使用加密的連線，請變更 `Encrypted` 開啟「資料庫憑據」頁以 `Yes`. 這將顯示用於設定加密的附加表單：

![](../../../assets/sql-integration-encrypted-yes.png)

這就是一切！ 連接RDS實例已完成。
