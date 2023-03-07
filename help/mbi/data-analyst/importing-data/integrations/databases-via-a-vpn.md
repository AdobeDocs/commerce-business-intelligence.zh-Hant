---
title: 通過VPN連接資料庫
description: 了解如何透過VPN（而非SSH通道）連線資料庫。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 通過VPN連接資料庫

雖然Adobe建議您使用SSH通道連接資料庫，但您也可以使用加密的VPN連接來保證資料安全。 A `VPN` 可用於任何資料庫整合，而且為了簡單起見，程式與設定 `SSH tunnel`:

1. [建立 [!DNL MBI] 資料庫用戶](#database)
1. [建立 [!DNL MBI] VPN用戶](#vpn)
1. [允許存取 [!DNL MBI] IP位址](#allowlist)
1. [將連接和VPN用戶資訊輸入MBI](#finish)

除了資料庫憑據外，您還必須輸入VPN用戶的憑據以總結情況。 任何VPN用戶都能工作，但Adobe建議您建立 [!DNL MBI] 使用者 — 讓您更輕鬆追蹤帳戶上的使用者。

## 為 [!DNL MBI] {#database}

建立資料庫用戶的過程因您所連接的資料庫類型而異。 要查看每種資料庫類型的說明，請按一下下面的連結。

* [Microsoft](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## 建立 `VPN` 用戶 [!DNL MBI] {#vpn}

如前所述，任何有效 `VPN` 使用者有效 — 但Adobe建議您僅為 [!DNL MBI] 使用。

## 允許存取 [!DNL MBI] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 是 `54.88.76.97` 和 `34.250.211.151`，但也在 `credentials` 頁，用於任何資料庫整合：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 進入連線並 `VPN` 使用者資訊 [!DNL MBI] {#finish}

總結一下，您需要將連線和使用者資訊輸入 [!DNL MBI]. 你離開了資料庫 `credentials` 頁面開啟？ 如果沒有，請前往 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，然後是您連接的資料庫的表徵圖。 別忘了變更 `Encrypted` 切換為 `Yes`.

在此頁面中輸入以下資訊，從 `Database Connection` 小節：

* `Username`:的使用者名稱 [!DNL MBI] 資料庫用戶
* `Password`:的密碼 [!DNL MBI] 資料庫用戶
* `Port`:伺服器上資料庫的埠。 預設值為：
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`:預設情況下，此為localhost `127.0.0.1`，但也可能是您伺服器的公用IP位址或區域網路位址。
* `Database Name (optional)`:如果僅允許訪問一個資料庫（這在資料庫用戶建立步驟中指定），請在此處輸入該資料庫的名稱。

在 `Encryption Connection` 小節：

* `Encryption Type`:將此設定為 `Cisco IPsec VPN`
* `Gateway Address`:VPN伺服器的IP地址
* `Group Name`:用於組身份驗證的組的名稱
* `Group Secret`:與組對應的密碼。
* `Username`:此 [!DNL MBI] `VPN` 用戶名
* `Password`:此 [!DNL MBI] `VPN` 使用者密碼

就這樣！ 完成後，按一下 **[!UICONTROL Save & Test]** 以完成設定。
