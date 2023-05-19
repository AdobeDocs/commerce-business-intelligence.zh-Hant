---
title: 通過VPN連接資料庫
description: 瞭解如何通過VPN而不是SSH通道連接資料庫。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# 通過VPN連接資料庫

而Adobe建議您使用 `SSH tunnel`，您還可以使用加密 `VPN` 保證安全。 A `VPN` 可用於任何資料庫整合，並且為了保持簡單，該過程與設定 `SSH tunnel`:

1. [建立 [!DNL Commerce Intelligence] 資料庫用戶](#database)
1. [建立 [!DNL Commerce Intelligence] VPN用戶](#vpn)
1. [允許訪問 [!DNL Commerce Intelligence] IP地址](#allowlist)
1. [將連接和VPN用戶資訊輸入Commerce Intelligence](#finish)

除了資料庫憑據外，您還必須輸入VPN用戶的憑據來總結。 任何VPN用戶都能工作，但Adobe建議您建立 [!DNL Commerce Intelligence] 用戶，因為它使您更容易跟蹤帳戶上的用戶。

## 為建立資料庫用戶 [!DNL Commerce Intelligence] {#database}

建立資料庫用戶的過程因您所連接的資料庫類型而異。 要查看每種資料庫類型的說明，請按一下下面的連結。

* [MicrosoftSQL](../integrations/microsoft-sql-server.md)
* [蒙戈DB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## 建立 `VPN` 用戶 [!DNL Commerce Intelligence] {#vpn}

如前所述，任何 `VPN` 用戶工作 — 但Adobe建議您僅為 [!DNL Commerce Intelligence] 。

## 允許訪問 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使連接成功，必須配置防火牆以允許從IP地址訪問。 他們 `54.88.76.97` 和 `34.250.211.151`，但也在 `credentials` 頁，用於任何資料庫整合：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 進入連接並 `VPN` 用戶資訊 [!DNL Commerce Intelligence] {#finish}

要總結內容，您需要將連接和用戶資訊輸入 [!DNL Commerce Intelligence]。 你離開了資料庫 `credentials` 開啟？ 否則，請轉到 **[!UICONTROL Manage Data** > **Connections]**。 按一下 **[!UICONTROL Add New Data Source]**，然後按一下所連接資料庫的表徵圖。 不要忘記更改 `Encrypted` 切換至 `Yes`。

在此頁中輸入以下資訊，從 `Database Connection` 部分：

* `Username`:用戶名 [!DNL Commerce Intelligence] 資料庫用戶
* `Password`:的密碼 [!DNL Commerce Intelligence] 資料庫用戶
* `Port`:伺服器上的資料庫埠。 預設值為：
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`:預設情況下，這是localhost `127.0.0.1`，但也可能是伺服器的公共IP地址或區域網路地址。
* `Database Name (optional)`:如果您只允許訪問一個資料庫（這是在資料庫用戶建立步驟中指定的），請在此處輸入該資料庫的名稱。

在 `Encryption Connection` 部分：

* `Encryption Type`:將此設定為 `Cisco IPsec VPN`
* `Gateway Address`:VPN伺服器的IP地址
* `Group Name`:用於組身份驗證的組的名稱
* `Group Secret`:與組對應的密碼。
* `Username`:的 [!DNL Commerce Intelligence] `VPN` 用戶名
* `Password`:的 [!DNL Commerce Intelligence] `VPN` 用戶密碼

完成後，按一下 **[!UICONTROL Save & Test]** 完成設定。
