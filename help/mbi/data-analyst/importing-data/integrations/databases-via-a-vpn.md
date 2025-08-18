---
title: 透過VPN連線資料庫
description: 瞭解如何透過VPN而非SSH通道連線資料庫。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 透過VPN連線資料庫

雖然Adobe建議您使用`SSH tunnel`連線資料庫，但您也可以使用加密的`VPN`連線來確保安全。 `VPN`可用於任何資料庫整合，而且為了保持簡單，程式與設定`SSH tunnel`幾乎相同：

1. [建立 [!DNL Commerce Intelligence] 資料庫使用者](#database)
1. [建立 [!DNL Commerce Intelligence] VPN使用者](#vpn)
1. [允許存取 [!DNL Commerce Intelligence] IP位址](#allowlist)
1. [在Commerce Intelligence中輸入連線和VPN使用者資訊](#finish)

除了資料庫證明資料之外，您還必須輸入VPN使用者的證明資料，才能完成。 任何VPN使用者都可以運作，但Adobe建議您建立[!DNL Commerce Intelligence]使用者，因為這樣可讓您更輕鬆地追蹤您帳戶上的使用者。

## 正在建立[!DNL Commerce Intelligence]的資料庫使用者 {#database}

建立資料庫使用者的程式因您連線的資料庫型別而異。 若要檢視每種資料庫型別的指示，請按一下下列連結。

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## 正在建立`VPN`的[!DNL Commerce Intelligence]使用者 {#vpn}

如前所述，任何有效的`VPN`使用者都可以運作，但Adobe建議您建立使用者僅供[!DNL Commerce Intelligence]使用。

## 允許存取[!DNL Commerce Intelligence] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 它們是`54.88.76.97`和`34.250.211.151`，但它也位於任何資料庫整合的`credentials`頁面上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 正在將連線和`VPN`使用者資訊輸入至[!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須在[!DNL Commerce Intelligence]中輸入連線和使用者資訊。 您是否讓資料庫`credentials`頁面保持開啟狀態？ 如果沒有，請移至&#x200B;**[!UICONTROL Manage Data** > **Connections]**。 按一下&#x200B;**[!UICONTROL Add New Data Source]**，然後按一下您連線之資料庫的圖示。 別忘了將`Encrypted`切換變更為`Yes`。

在此頁面中輸入下列資訊，從`Database Connection`區段開始：

* `Username`： [!DNL Commerce Intelligence]資料庫使用者的使用者名稱
* `Password`： [!DNL Commerce Intelligence]資料庫使用者的密碼
* `Port`：您伺服器上的資料庫連線埠。 預設值為：
   * `MicrosoftSQL`： `1433`
   * `MongoDB`： `27017`
   * `MySQL`： `3306`
   * `PostgreSQL`： `5432`
* `Host`：預設為localhost `127.0.0.1`，但也可以是伺服器的公用IP位址或區域網路位址。
* `Database Name (optional)`：如果您只允許存取一個資料庫（這是在資料庫使用者建立步驟中指定的），請在這裡輸入該資料庫的名稱。

在`Encryption Connection`區段下：

* `Encryption Type`：將此專案設為`Cisco IPsec VPN`
* `Gateway Address`： VPN伺服器的IP位址
* `Group Name`：用於群組驗證的群組名稱
* `Group Secret`：與群組對應的密碼。
* `Username`： [!DNL Commerce Intelligence] `VPN`使用者名稱
* `Password`： [!DNL Commerce Intelligence] `VPN`使用者密碼

完成時，按一下&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成設定。
