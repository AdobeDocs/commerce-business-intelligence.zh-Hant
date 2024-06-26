---
title: 透過直接連線連線MySQL
description: 瞭解如何連結 [!DNL MongoDB] 透過直接連線。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 連線 [!DNL MySQL] 透過直接連線

## 在此主題中

* [允許存取 [!DNL Commerce Intelligence] IP位址](#allowlist)
* [建立 [!DNL MySQL] 使用者 [!DNL Commerce Intelligence]](#steptwo)
* [將連線資訊輸入到 [!DNL Commerce Intelligence]](#stepthree)

## 跳轉到

* [[!DNL MySQL] via ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] 建議您使用 [SSH](../integrations/mysql-via-ssh-tunnel.md) 或是其他加密方式，保護您的資料！ 如果這不是選項，您仍然可以直接連線 [!DNL Commerce Intelligence] 使用本主題中的指示至您的資料庫。

本主題將引導您瞭解如何直接連線 [!DNL MySQL] 資料庫至 [!DNL Commerce Intelligence]. 這些設定也可搭配 [!DNL Adobe Commerce] 或其他任何使用MySQL的電子商務資料庫。

## 允許存取 [!DNL Commerce Intelligence] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 它們是 `54.88.76.97` 和 `34.250.211.151`，但也在 [!DNL MySQL] 證明資料頁面：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 建立 [!DNL MySQL] 使用者 [!DNL Commerce Intelligence]

最簡單的建立方式 `MySQL` 使用者 [!DNL Commerce Intelligence] 是在登入時執行以下查詢 `MySQL` 替換為 `GRANT` 許可權。 取代 `Commerce Intelligence IP Address` 使用 [!DNL Commerce Intelligence] IP位址和取代 `secure password` 選擇安全的密碼：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

若要限制此使用者存取特定資料庫、表格或欄中的資料，您可以改為執行 `GRANT` 僅允許存取您允許之資料的查詢。

**使用相同的使用者和密碼，為所有必要的IP重新執行GRANT查詢。**

## 在Commerce Intelligence中輸入連線資訊

若要完成工作，您必須在中輸入連線和使用者資訊 [!DNL Commerce Intelligence]. 您是否離開 [!DNL MySQL] 憑證頁面是否開啟？ 如果沒有，請前往 **[!UICONTROL Data** > **Connections]** 並按一下 **[!UICONTROL Add New Data Source]**，然後按一下 [!DNL MySQL] 圖示。 別忘了變更 `Encrypted` 切換至 `Yes`.

在此頁面中輸入以下資訊，從 `Database Connection` 區段：

* `Connection Nickname`：輸入整合的名稱（例如電子商務商店）
* `Username`：的使用者名稱 [!DNL Commerce Intelligence] [!DNL MySQL] 使用者
* `Password`：的密碼 [!DNL Commerce Intelligence] [!DNL MySQL] 使用者
* `Port`：伺服器上的MySQL連線埠(`3306` 預設值)
* `Host`：預設為localhost。 一般而言，它是的繫結位址值 [!DNL MySQL] 伺服器，預設為 `127.0.0.1 (localhost)`，但也可能是某個本機網路位址(例如 `192.168.0.1`)或伺服器的公用IP位址。

  值可在以下連結中找到： `my.cnf` 檔案(位於 `/etc/my.cnf`)的行下方 `\[mysqld\]`. 若該檔案中的繫結位址列被註解，則您的伺服器將會受到外部連線嘗試的保護。

完成後，按一下 **[!UICONTROL Save & Test]** 以完成設定。

## 相關檔案

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
