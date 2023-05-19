---
title: 連接 [!DNL MySQL] 通過SSH隧道
description: 瞭解如何連接 [!DNL MySQL] 通過SSH隧道。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 連接 [!DNL MySQL] 通過 [!DNL SSH Tunnel]

* [檢索 [!DNL Commerce Intelligence] 公鑰](#retrieve)
* [允許訪問 [!DNL Commerce Intelligence] IP地址](#allowlist)
* [建立Linux用戶 [!DNL Commerce Intelligence]](#linux)
* [建立 [!DNL MySQL] 用戶 [!DNL Commerce Intelligence]](#mysql)
* [在中輸入連接和用戶資訊 [!DNL Commerce Intelligence]](#finish)

## 跳至

* [[!DNL MySQL] 通過 ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] 通過 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

連接 [!DNL MySQL] 資料庫 [!DNL Commerce Intelligence] 通過 `SSH tunnel`，您必須做幾件事：

1. 檢索 [!DNL Commerce Intelligence] `public key`
1. 允許訪問 [!DNL Commerce Intelligence] `IP address`
1. 建立 `Linux` 用戶 [!DNL Commerce Intelligence]
1. 建立 `MySQL` 用戶 [!DNL Commerce Intelligence]
1. 在中輸入連接和用戶資訊 [!DNL Commerce Intelligence]


## 檢索 [!DNL Commerce Intelligence] 公鑰 {#retrieve}

的 `public key` 用於授權 [!DNL Commerce Intelligence] `Linux` 。 在下一節中，將建立用戶並導入密鑰。

1. 轉到 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**。
1. 按一下 `MySQL` 表徵圖
1. 在 `MySQL credentials` 開啟，設定 `Encrypted` 切換至 `Yes`。 這將顯示SSH設定表單。
1. 的 `public key` 位於此窗體下。

在本教程的整個過程中，保持本頁開啟 — 您需要在下一節和結尾處開啟本頁。

下面是如何瀏覽 [!DNL Commerce Intelligence] 要檢索密鑰：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 允許訪問 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使連接成功，必須配置防火牆以允許從IP地址訪問。 他們 `54.88.76.97` 和 `34.250.211.151` 但它們也在 `MySQL credentials` 的子菜單。 請參閱上面的GIF中的藍色框。

## 建立 [!DNL Linux] 用戶 [!DNL Commerce Intelligence] {#linux}

這可以是生產機或輔助機，只要它包含即時（或頻繁更新）資料。 你可以 [限制此用戶](../../../administrator/account-management/restrict-db-access.md) 只要它保留連接到 `MySQL` 伺服器。

1. 要添加新用戶，請以root身份在您的 [!DNL Linux] 伺服器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 記住 `public key` 在第一節里找到的？ 要確保用戶有權訪問資料庫，您需要將密鑰導入 `authorized\_keys`。

   將整個密鑰複製到 `authorized\_keys` 檔案，如下所示：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 要完成用戶建立，請更改 `/home/rjmetric` 允許訪問的目錄 `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 與伺服器關聯的檔案未設定為預設選項，只有某些用戶具有伺服器訪問權限 — 這會阻止成功連接到 [!DNL Commerce Intelligence]。 在這些情況下，需要運行類似 `AllowUsers` 允許 `rjmetric` 用戶訪問伺服器。

## 建立 [!DNL MySQL] 用戶 [!DNL Commerce Intelligence] {#mysql}

您的組織可能需要不同的進程，但建立此用戶的最簡單方法是登錄時執行以下查詢 [!DNL MySQL] 作為有權授予權限的用戶：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

替換 `secure password here` 密碼安全，與 `SSH` 密碼。

要限制此用戶訪問特定資料庫、表或列中的資料，可以改為運行僅允許訪問您允許的資料的GRANT查詢。

## 將連接和用戶資訊輸入 [!DNL Commerce Intelligence] {#finish}

要總結內容，您需要將連接和用戶資訊輸入 [!DNL Commerce Intelligence]。 你是不是離開了 `MySQL credentials` 開啟？ 否則，請轉到 **[!UICONTROL Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，則 [!DNL MySQL] 表徵圖 不要忘記設定 `Encrypted` 切換至 `Yes`。

在此頁中輸入以下資訊，從 `Database Connection` 部分：

* `Username`:用戶名 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶
* `Password`:的密碼 [!DNL Commerce Intelligence] [!DNL MySQL] 用戶
* `Port`: [!DNL MySQL] 伺服器上的埠（預設為3306）
* `Host` 預設情況下，這是localhost。 通常，它是您的 [!DNL MySQL] 伺服器，預設情況下 `127.0.0.1 (localhost)`，但也可能是某個本地網路地址(例如， `192.168.0.1`)或伺服器的公共IP地址。

   可以在 `my.cnf` 檔案(位於 `/etc/my.cnf`)下面的 `\[mysqld\]`。 如果在該檔案中注釋掉綁定地址行，則伺服器將受到外部連接嘗試的保護。

在 `SSH Connection` 部分：

* `Remote Address`:伺服器的IP地址或主機名 [!DNL Commerce Intelligence] 會穿過隧道
* `Username`:用戶名 [!DNL Commerce Intelligence] SSH([!DNL Linux])用戶
* `SSH Port`:伺服器上的SSH埠（預設為22）

完成後，按一下 **[!UICONTROL Save & Test]** 完成設定。

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
