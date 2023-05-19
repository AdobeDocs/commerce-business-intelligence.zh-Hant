---
title: 通過直接連接連接MySQL
description: 瞭解如何連接 [!DNL MongoDB] 直接連接。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 連接 [!DNL MySQL] 通過直接連接

## 在此主題中

* [允許訪問 [!DNL Commerce Intelligence] IP地址](#allowlist)
* [建立 [!DNL MySQL] 用戶 [!DNL Commerce Intelligence]](#steptwo)
* [在中輸入連接資訊 [!DNL Commerce Intelligence]](#stepthree)

## 跳到

* [[!DNL MySQL] 通過 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 通過 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] 建議您使用 [SSH](../integrations/mysql-via-ssh-tunnel.md) 或其他加密形式來保護您的資料！ 如果不能選擇，您仍然可以直接連接 [!DNL Commerce Intelligence] 使用本主題中的說明將其發送到資料庫。

本主題引導您直接連接 [!DNL MySQL] 資料庫 [!DNL Commerce Intelligence]。 這些設定也可與 [!DNL Adobe Commerce] 或使用MySQL的其他電子商務資料庫。

## 允許訪問 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使連接成功，必須配置防火牆以允許從IP地址訪問。 他們 `54.88.76.97` 和 `34.250.211.151`，但也在 [!DNL MySQL] 「憑據」頁：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 建立 [!DNL MySQL] 用戶 [!DNL Commerce Intelligence]

建立 `MySQL` 用戶 [!DNL Commerce Intelligence] 是登錄時執行以下查詢 `MySQL` 與 `GRANT` 權限。 替換 `Commerce Intelligence IP Address` 和 [!DNL Commerce Intelligence] IP地址和替換 `secure password` 使用您選擇的安全密碼：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

要限制此用戶訪問特定資料庫、表或列中的資料，可以改為運行 `GRANT` 僅允許訪問您允許的資料的查詢。

**使用相同的用戶和密碼為所有必需IP重新運行GRANT查詢。**

## 在Commerce Intelligence中輸入連接資訊

要總結內容，您需要將連接和用戶資訊輸入 [!DNL Commerce Intelligence]。 你是不是離開了 [!DNL MySQL] 「憑據」頁面開啟？ 否則，請轉到 **[!UICONTROL Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，然後按一下 [!DNL MySQL] 表徵圖 不要忘記更改 `Encrypted` 切換至 `Yes`。

在此頁中輸入以下資訊，從 `Database Connection` 部分：

* `Connection Nickname`:輸入整合的名稱（例如，E-commerce Store）
* `Username`:用戶名 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶
* `Password`:的密碼 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶
* `Port`:伺服器上的MySQL埠(`3306` 預設)
* `Host`:預設情況下，這是localhost。 通常，它是您的 [!DNL MySQL] 伺服器，預設情況下 `127.0.0.1 (localhost)`，但也可能是某個本地網路地址(例如， `192.168.0.1`)或伺服器的公共IP地址。

   可以在 `my.cnf` 檔案(位於 `/etc/my.cnf`)下面的 `\[mysqld\]`。 如果在該檔案中注釋掉綁定地址行，則伺服器將受到外部連接嘗試的保護。

完成後，按一下 **[!UICONTROL Save & Test]** 完成設定。

## 相關文檔

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
