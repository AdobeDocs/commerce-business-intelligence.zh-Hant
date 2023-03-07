---
title: 通過SSH通道連接PostgreSQL
description: 了解如何將PostgreSQL資料庫連接到 [!DNL MBI] 透過SSH通道。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Connect `PostgreSQL` via `SSH` 隧道

連接 `PostgreSQL` 資料庫 [!DNL MBI] 透過 `SSH tunnel`，您（或您的團隊，如果您不是技術人員）必須執行下列操作：

1. [擷取 [!DNL MBI] 公開金鑰](#retrieve)
1. [允許存取 [!DNL MBI] IP位址](#allowlist)
1. [建立Linux](#linux)
1. [為建立Postgres使用者 [!DNL MBI] ](#postgres)
1. [在MBI中輸入連接和用戶資訊](#finish)

它聽起來並不那麼複雜。 開始使用。

## 擷取 [!DNL MBI] `public key` {#retrieve}

此 `public key` 用於授權 [!DNL MBI] Linux®用戶。 在下一節中，您將建立使用者並匯入金鑰。

1. 前往 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add a Data Source]**.
1. 按一下 `PostgreSQL` 表徵圖。
1. 在 `PostgreSQL credentials` 頁面開啟，設定 `Encrypted` 切換為 `Yes`. 這會顯示 `SSH` 設定表單。
1. 此 `public key` 位於此表單下。

在整個教學課程中，請保持此頁面開啟，您需要在下一節和結尾處開啟。

如果你迷路了，這就是如何瀏覽 [!DNL MBI] 要檢索密鑰，請執行以下操作：

![擷取RJMetrics公開金鑰](../../../assets/get-mbi-public-key.gif)

## 允許存取 [!DNL MBI] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 是 `54.88.76.97/32`，但也在 `PostgreSQL` 憑據頁。 看見上面GIF的藍色方塊了？ 就這樣！

## 建立 `Linux` 用戶 [!DNL MBI] {#linux}

只要包含即時（或經常更新）資料，就可以是生產或次要電腦。 您可以 [限制此用戶](../../../administrator/account-management/restrict-db-access.md) 只要保留連接到PostgreSQL伺服器的權利，您可以選擇任何方式。

1. 若要新增新使用者，請在 `Linux` 伺服器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 記住 `public key` 你在第一節中檢索到的？ 若要確保使用者擁有資料庫的存取權，您需要將金鑰匯入 `authorized\_keys`.

   將整個金鑰複製到 `authorized\_keys` 檔案如下：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 若要完成建立使用者，請變更 `/home/rjmetric` 允許訪問的目錄 `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>若 `sshd\_config` 與伺服器關聯的檔案未設定為預設選項，只有某些用戶具有伺服器訪問權 — 這會阻止成功連接到 [!DNL MBI]. 在這些情況下，必須執行類似 `AllowUsers` 允許rjmetric使用者存取伺服器。

## 建立 [!DNL MBI] Postgres使用者 {#postgres}

您的組織可能需要不同的程式，但建立此使用者最簡單的方式，是當您以具有授予權限權限的使用者身分登入Postgres時，執行下列查詢。 使用者也應擁有 [!DNL MBI] 正在被授予存取權。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

取代 `secure password` 使用您自己的安全密碼，該密碼可能與SSH密碼不同。 此外，請務必取代 `database name` 和 `schema name` 資料庫中的適當名稱。

如果要連接多個資料庫或架構，請視需要重複此過程。

## 將連線和使用者資訊輸入 [!DNL MBI] {#finish}

總結一下，您需要將連線和使用者資訊輸入 [!DNL MBI]. 是否使PostgreSQL憑據頁保持開啟？ 如果沒有，請前往 **[!UICONTROL Manage Data > Connections]** 按一下 **[!UICONTROL Add a Data Source]**，然後顯示PostgreSQL表徵圖。 別忘了設定 `Encrypted` 切換為 `Yes`.

從「資料庫連接」部分開始，在此頁中輸入以下資訊：

* `Username`:RJMetrics Postgres使用者名稱（應為rjmetric）
* `Password`:RJMetrics Postgres密碼
* `Port`:伺服器上的PostgreSQL埠（預設為5432）
* `Host`: 127.0.0.1

在 `SSH Connection`:

* `Remote Address`:要SSH到的伺服器的IP地址或主機名
* `Username`:您的SSH登入名稱（應為rjmetric）
* `SSH Port`:伺服器上的SSH埠（預設為22個）

就這樣！ 完成後，按一下 **儲存並測試** 以完成設定。

### 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
