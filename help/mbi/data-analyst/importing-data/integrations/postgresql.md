---
title: 通過SSH隧道連接PostgreSQL
description: 瞭解如何通過SSH隧道將PostgreSQL資料庫連接到Commerce Intelligence。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 連接 [!DNL PostgreSQL] 通過 [!DNL SSH Tunnel]

連接 [!DNL PostgreSQL] 資料庫 [!DNL Commerce Intelligence] 通過 `SSH tunnel`，您必須做幾件事：

1. [檢索 [!DNL Commerce Intelligence] 公鑰](#retrieve)
1. [允許訪問 [!DNL Commerce Intelligence] IP地址](#allowlist)
1. [建立 [!DNL Linux] 用戶 [!DNL Commerce Intelligence] ](#linux)
1. [建立 [!DNL PostgreSQL] 用戶 [!DNL Commerce Intelligence] ](#postgres)
1. [在中輸入連接和用戶資訊 [!DNL Commerce Intelligence]](#finish)

## 檢索 [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

的 `public key` 用於授權 [!DNL Commerce Intelligence] [!DNL Linux] 。 現在，您將建立用戶並導入密鑰。

1. 轉到 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add a Data Source]**。
1. 按一下 [!DNL PostgreSQL] 表徵圖
1. 在 `PostgreSQL credentials` 開啟，設定 `Encrypted` 切換至 `Yes`。 這將顯示 `SSH` 的下界。
1. 的 `public key` 位於此窗體下。

在本教程的整個過程中，保持本頁開啟 — 您需要在下一節和結尾處開啟本頁。

下面演示如何導航 [!DNL Commerce Intelligence] 要檢索密鑰：

![檢索RJMetrics公鑰](../../../assets/get-mbi-public-key.gif)

## 允許訪問 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使連接成功，必須將防火牆配置為允許從IP地址訪問。 是 `54.88.76.97/32`，但也在 `PostgreSQL` 「憑據」頁。 請參閱上面的GIF中的藍色框。

## 建立 [!DNL Linux] 用戶 [!DNL Commerce Intelligence] {#linux}

這可以是生產機或輔助機，只要它包含即時（或頻繁更新）資料。 你可以 [限制此用戶](../../../administrator/account-management/restrict-db-access.md) 只要它保留連接到 [!DNL PostgreSQL] 伺服器。

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
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 與伺服器關聯的檔案未設定為預設選項，只有某些用戶具有伺服器訪問權限 — 這會阻止成功連接到 [!DNL Commerce Intelligence]。 在這些情況下，需要運行類似 `AllowUsers` 允許rjmetric用戶訪問伺服器。

## 建立 [!DNL Commerce Intelligence] [!DNL Postgres] 用戶 {#postgres}

您的組織可能需要不同的進程，但建立此用戶的最簡單的方法是以具有授予權限權限權限的用戶身份登錄Postgres時執行以下查詢。 用戶還應擁有 [!DNL Commerce Intelligence] 正被授予訪問權限。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

替換 `secure password` 與SSH密碼不同的安全密碼。 另外，確保 `database name` 和 `schema name` 資料庫中相應的名稱。

如果要連接多個資料庫或架構，請根據需要重複此過程。

## 將連接和用戶資訊輸入 [!DNL Commerce Intelligence] {#finish}

要總結內容，您需要將連接和用戶資訊輸入 [!DNL Commerce Intelligence]。 你是不是離開了 [!DNL PostgreSQL] 「憑據」頁面開啟？ 否則，請轉到 **[!UICONTROL Manage Data > Connections]** 按一下 **[!UICONTROL Add a Data Source]**，則 [!DNL PostgreSQL] 表徵圖 不要忘記設定 `Encrypted` 切換至 `Yes`。

在此頁中輸入以下資訊，從 `Database Connection` 部分：

* `Username`:RJMetrics Postgres用戶名（應為rjmetric）
* `Password`:RJMetrics Postgres密碼
* `Port`:伺服器上的PostgreSQL埠（預設為5432）
* `Host`: 127.0.0.1

下 `SSH Connection`:

* `Remote Address`:要SSH到的伺服器的IP地址或主機名
* `Username`:您的SSH登錄名（應為rjmetric）
* `SSH Port`:伺服器上的SSH埠（預設為22）

完成後，按一下 **保存和Test** 完成設定。

### 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
