---
title: 通過cPanel連接MySQL
description: 了解如何透過cPanel連接MySQL。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: e4ac176492913623ae461484c8ef2abe034e5f62
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# 通過cPanel連接MySQL

* [建立 [!DNL MBI] cPanel中的MySQL用戶](#cpanel)
* [在MBI中輸入連接和用戶資訊](#finish)

## 跳到

* [MySQL通過SSH隧道](../integrations/mysql-via-ssh-tunnel.md)
* [MySQL通過直接連接](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>Adobe建議您使用SSH或其他加密形式來保護資料！ 如果此選項不可用，您仍可以直接連接 [!DNL MBI] 使用本文中的說明，將資料庫重新命名。

本文將引導您將MySQL資料庫直接連接到 [!DNL MBI] 使用 `cPanel`. 此程式也可用來連線 [!DNL Adobe Commerce] 和任何其他基於MySQL的電子商務資料庫 [!DNL MBI].

1. 建立 [!DNL MBI] MySQL用戶 `cPanel`
1. 在 [!DNL MBI]

開始使用。

## 建立 [!DNL MBI] MySQL用戶 `cPanel` {#cpanel}

1. 登入 [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) 透過托管提供者。
1. 按一下 **[!UICONTROL MySQL Databases]**，位於 `Database` 區段。
1. 向下捲動至 `Add New User` 區段，並為 [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 按一下 **[!UICONTROL Create User]**.
1. 現在您已建立使用者，需要將其與資料庫建立關聯。 返回 `Add New User` 一節 — 請參閱 `Add User to Database?` 這就是你需要的。
1. 在 `User` 在此區段的下拉式清單中，選取您建立的使用者。
1. 在 `Database` 在此部分的下拉式清單中，選擇要連接的資料庫 [!DNL MBI].
1. 按一下 **[!UICONTROL Add]**.
1. 出現權限檢查清單時，請核取旁邊的方塊 `SELECT`  — 全部 [!DNL MBI] 需要連接到資料庫。

## 將連線和使用者資訊輸入 [!DNL MBI] {#finish}

總結一下，您需要將連線和使用者資訊輸入 [!DNL MBI]. 是否使MySQL憑據頁保持開啟？ 如果沒有，請前往 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，然後是MySQL表徵圖。

在此頁面的 `Database Connection` 小節：

* `Username`:的使用者名稱 [!DNL MBI] MySQL用戶
* `Password`:的密碼 [!DNL MBI] MySQL用戶
* `Port`:伺服器上的MySQL埠(`3306` 依預設)
* `Host`:公開地址 `MySQL` 伺服器 [!DNL MBI] 連線至。 這通常是您用來登入的URL `cPanel`.

如果您使用 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)，您必須輸入加密資訊。 設定 `Encrypted` 切換為 `Yes` 來顯示表單。

* `Connection Type`:將此設定為 `SSH Tunnel`
* `Remote Address`:伺服器的IP地址或主機名 [!DNL MBI] 將隧道
* `Username`:的使用者名稱 [!DNL MBI] `SSH (Linux)` 使用者，請參閱 [說明](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 如何執行此操作（如果尚未執行）
* `SSH Port`:伺服器上的SSH埠(`22` 依預設)

就這樣！ 完成後，按一下 **[!UICONTROL Save & Test]** 以完成設定。

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
