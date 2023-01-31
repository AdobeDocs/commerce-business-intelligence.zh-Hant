---
title: 通過直接連接連接MySQL
description: 了解如何連線 [!DNL MongoDB] 直接連線。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Connect [!DNL MongoDB] 透過直接連線

## 本文

* [允許存取 [!DNL MBI] IP位址](#allowlist)
* [建立 ](#steptwo)
* [在 [!DNL MBI]](#stepthree)

## 跳到

* [&#39;通過SSH隧道的MySQL&#39;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&#39;MySQL（通過cPanel）&#39;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>強烈建議您使用 [SSH](../integrations/mysql-via-ssh-tunnel.md) 或其他加密方式，以保護您的資料！ 如果此選項不可用，您仍可以直接連接 [!DNL MBI] 使用本文中的說明，將資料庫重新命名。

在本文中，我們將引導您直接將MySQL資料庫連接到 [!DNL MBI]. 這些設定也可與Commerce或使用MySQL的任何其他電子商務資料庫一起使用。

## 允許存取 [!DNL MBI] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從我們的IP位址存取。 是 `54.88.76.97` 和 `34.250.211.151`，但也位於MySQL憑據頁上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 為 [!DNL MBI]

建立 `MySQL` 用戶 [!DNL MBI] 是在登入時執行下列查詢 `MySQL` with `GRANT` 權限。 取代 `MBI IP Address` 和 [!DNL MBI] IP位址和更換 `secure password` 使用您所選擇的安全密碼：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

要限制此用戶訪問特定資料庫、表或列中的資料，可以改為運行 `GRANT` 僅允許訪問您允許的資料的查詢。

**使用相同的用戶和密碼為所有必需IP重新運行GRANT查詢。**

## 在MBI中輸入連接資訊

總結一下，我們需要將連線和使用者資訊輸入 [!DNL MBI]. 是否使MySQL憑據頁保持開啟？ 如果沒有，請前往 **[!UICONTROL Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，然後是MySQL表徵圖。 別忘了變更 `Encrypted` 切換為 `Yes`.

在此頁面中輸入以下資訊，從 `Database Connection` 小節：

* `Connection Nickname`:輸入整合的名稱（例如Ecommerce Store）
* `Username`:的使用者名稱 [!DNL MBI] MySQL用戶
* `Password`:的密碼 [!DNL MBI] MySQL用戶
* `Port`:伺服器上的MySQL埠(`3306` 依預設)
* `Host`:預設情況下，此為localhost。 一般來說，它將是MySQL伺服器的綁定地址值，預設為 `127.0.0.1 (localhost)`，但也可能是某些本機網路位址(例如， `192.168.0.1`)或伺服器的公用IP位址。

   可在 `my.cnf` 檔案(通常位於 `/etc/my.cnf`)，這行會讀 `\[mysqld\]`. 如果在該檔案中注釋了bind-address行，則伺服器將從外部連接嘗試中獲得安全。

就這樣！ 完成後，按一下 **[!UICONTROL Save & Test]** 以完成設定。

## 相關檔案

* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
