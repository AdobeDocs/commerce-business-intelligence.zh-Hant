---
title: 通過cPanel連接MySQL
description: 瞭解如何通過cPanel連接MySQL。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 連接 [!DNL MySQL] 通過 [!DNL cPanel]

* [建立 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶 [!DNL cPanel]](#cpanel)
* [在中輸入連接和用戶資訊 [!DNL Commerce Intelligence]](#finish)

## 跳到

* [[!DNL MySQL] 通過SSH隧道](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 通過直接連接](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] 建議您使用SSH或某種其他形式的加密來保護資料！ 如果不能選擇，您仍然可以直接連接 [!DNL Commerce Intelligence] 使用本主題中的說明將其發送到資料庫。

本主題引導您直接連接 [!DNL MySQL] 資料庫 [!DNL Commerce Intelligence] 使用 [!DNL cPanel]。 此過程也可用於連接 [!DNL Adobe Commerce] 和其他基於MySQL的電子商務資料庫 [!DNL Commerce Intelligence]。

1. 建立 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶 [!DNL cPanel]
1. 在中輸入連接和用戶資訊 [!DNL Commerce Intelligence]

開始。

## 建立 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶 [!DNL cPanel] {#cpanel}

1. 登錄到 [!DNL cPanel] 通過托管提供商。
1. 按一下 **[!UICONTROL [!DNL MySQL] Databases]**&#x200B;的 `Database` 的子菜單。
1. 向下滾動到 `Add New User` 和為 [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 按一下 **[!UICONTROL Create User]**。
1. 現在您已建立用戶，您需要將其與資料庫關聯。 返回 `Add New User` 部分 — 請參閱 `Add User to Database?` 這才是你需要的。
1. 在 `User` 從此節的下拉清單中，選擇您建立的用戶。
1. 在 `Database` 從此部分的下拉清單中，選擇要連接到的資料庫 [!DNL Commerce Intelligence]。
1. 按一下 **[!UICONTROL Add]**。
1. 當出現權限核對表時，選中旁邊的框 `SELECT`  — 全部 [!DNL Commerce Intelligence] 需要連接到資料庫。

## 將連接和用戶資訊輸入 [!DNL Commerce Intelligence] {#finish}

要總結內容，您需要將連接和用戶資訊輸入 [!DNL Commerce Intelligence]。 你是不是離開了 [!DNL MySQL] 「憑據」頁面開啟？ 否則，請轉到 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，則 [!DNL MySQL] 表徵圖

在 `Database Connection` 部分：

* `Username`:用戶名 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶
* `Password`:的密碼 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶
* `Port`:伺服器上的MySQL埠(`3306` 預設)
* `Host`:公共地址 `MySQL` 伺服器 [!DNL Commerce Intelligence] 連接到。 這通常是用於登錄的URL `[!DNL cPanel]`。

如果使用 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)，必須輸入加密資訊。 設定 `Encrypted` 切換至 `Yes` 的子菜單。

* `Connection Type`:將此設定為 `SSH Tunnel`
* `Remote Address`:伺服器的IP地址或主機名 [!DNL Commerce Intelligence] 會穿過隧道
* `Username`:用戶名 [!DNL Commerce Intelligence] `SSH (Linux)` 用戶，請參閱 [說明](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) 如果尚未執行，則說明如何執行此操作)
* `SSH Port`:伺服器上的SSH埠(`22` 預設)

完成後，按一下 **[!UICONTROL Save & Test]** 完成設定。

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
