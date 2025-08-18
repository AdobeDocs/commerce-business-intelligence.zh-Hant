---
title: 透過cPanel連線MySQL
description: 瞭解如何透過cPanel連線MySQL。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 透過[!DNL MySQL]連線[!DNL cPanel]

* [在 [!DNL Commerce Intelligence] [!DNL MySQL]中建立 [!DNL cPanel]使用者](#cpanel)
* [在 [!DNL Commerce Intelligence]中輸入連線和使用者資訊](#finish)

## 跳轉到

* [透過SSH通道的[!DNL MySQL]](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL]透過直接連線](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe]建議您使用SSH或其他加密形式來保護您的資料！ 如果這不是選項，您仍然可以使用本主題中的指示直接將[!DNL Commerce Intelligence]連線到您的資料庫。

此主題將引導您使用[!DNL MySQL]直接將您的[!DNL Commerce Intelligence]資料庫連線到[!DNL cPanel]。 此處理程式也可用來將[!DNL Adobe Commerce]和任何其他以MySQL為基礎的電子商務資料庫連線到[!DNL Commerce Intelligence]。

1. 在[!DNL Commerce Intelligence]中建立[!DNL MySQL] [!DNL cPanel]使用者
1. 在[!DNL Commerce Intelligence]中輸入連線和使用者資訊

開始使用。

## 在[!DNL Commerce Intelligence]中建立[!DNL MySQL] [!DNL cPanel]使用者 {#cpanel}

1. 透過您的託管提供者登入[!DNL cPanel]。
1. 按一下位於&#x200B;**[!UICONTROL [!DNL MySQL] Databases]**&#x200B;區段中的`Database`。
1. 向下捲動至`Add New User`區段並建立[!DNL Commerce Intelligence]的使用者：

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 按一下&#x200B;**[!UICONTROL Create User]**。
1. 現在您已建立使用者，您需要將其與資料庫建立關聯。 返回`Add New User`區段 — 檢視您所需的`Add User to Database?`設定。
1. 在此區段的`User`下拉式清單中，選取您建立的使用者。
1. 在此區段的`Database`下拉式清單中，選取您要連線至[!DNL Commerce Intelligence]的資料庫。
1. 按一下&#x200B;**[!UICONTROL Add]**。
1. 當許可權檢查清單出現時，請勾選`SELECT`旁的方塊 — 這是[!DNL Commerce Intelligence]連線到資料庫所需的全部。

## 正在將連線和使用者資訊輸入[!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須在[!DNL Commerce Intelligence]中輸入連線和使用者資訊。 您是否讓[!DNL MySQL]認證頁面保持開啟狀態？ 如果沒有，請移至&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;並按一下&#x200B;**[!UICONTROL Add New Data Source]**，然後按一下[!DNL MySQL]圖示。

在此頁面的`Database Connection`區段中輸入下列資訊：

* `Username`： [!DNL Commerce Intelligence] [!DNL MySQL]使用者的使用者名稱
* `Password`： [!DNL Commerce Intelligence] [!DNL MySQL]使用者的密碼
* `Port`：伺服器上的MySQL連線埠（預設為`3306`）
* `Host`： `MySQL`伺服器[!DNL Commerce Intelligence]所連線的公用位址。 這通常是您用來登入`[!DNL cPanel]`的URL。

如果您使用[`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)，則必須輸入加密資訊。 將`Encrypted`切換設定為`Yes`以顯示表單。

* `Connection Type`：將此專案設為`SSH Tunnel`
* `Remote Address`：伺服器[!DNL Commerce Intelligence]的IP位址或主機名稱將通道至
* `Username`： [!DNL Commerce Intelligence] `SSH (Linux)`使用者的使用者名稱，請參閱[指示](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md)如何執行此動作（如果尚未完成）
* `SSH Port`：伺服器上的SSH連線埠（預設為`22`）

完成時，按一下&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成設定。

## 相關：

* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
