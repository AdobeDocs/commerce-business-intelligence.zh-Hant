---
title: 通過SSH隧道連接MySQL
description: 了解如何透過SSH通道連接MySQL。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Connect `MySQL` via `SSH Tunnel`

* [擷取 [!DNL MBI] 公開金鑰](#retrieve)
* [允許存取 [!DNL MBI] IP位址](#allowlist)
* [為建立Linux用戶 [!DNL MBI]](#linux)
* [為 [!DNL MBI]](#mysql)
* [在 [!DNL MBI]](#finish)

## 跳到

* `MySQL via SSH tunnel`
* [&#39;MySQL&#39;](../integrations/mysql-via-a-direct-connection.md)
* [&#39;MySQL&#39;](../integrations/mysql-via-cpanel.md)

連接 `MySQL` 資料庫 [!DNL MBI] 透過 `SSH tunnel`，您（或您的團隊，如果您不是技術人員）需要執行下列操作：

1. 擷取 [!DNL MBI] `public key`
1. 允許存取 [!DNL MBI] `IP address`
1. 建立 `Linux` 用戶 [!DNL MBI]
1. 建立 `MySQL` 用戶 [!DNL MBI]
1. 在 [!DNL MBI]

它聽起來並不那麼複雜。 讓我們開始吧。

## 擷取 [!DNL MBI] 公開金鑰 {#retrieve}

此 `public key` 用於授權 [!DNL MBI] `Linux` 使用者。 在下一節中，我們將建立使用者並匯入金鑰。

1. 前往 **[!UICONTROL Manage Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**.
1. 按一下 `MySQL` 表徵圖。
1. 在 `MySQL credentials` 頁面開啟，設定 `Encrypted` 切換為 `Yes`. 這會顯示SSH設定表單。
1. 此 `public key` 位於此表單下。

在整個教學課程中，請保持此頁面開啟，您需要在下一節和結尾處開啟。

如果你迷路了，這裡是如何導航 [!DNL MBI] 要檢索密鑰，請執行以下操作：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 允許存取 [!DNL MBI] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從我們的IP位址存取。 是 `54.88.76.97` 和 `34.250.211.151` 但也在 `MySQL credentials` 頁面。 看見上面GIF的藍色方塊了？ 就這樣！

## 建立 `Linux` 用戶 [!DNL MBI] {#linux}

只要包含即時（或經常更新）資料，就可以是生產或次要電腦。 您可以 [限制此用戶](../../../administrator/account-management/restrict-db-access.md) 只要保留連接至 `MySQL` 伺服器。

1. 若要新增新使用者，請在 `Linux` 伺服器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 記住 `public key` 我們在第一節中擷取的？ 為確保用戶能夠訪問資料庫，我們需要將密鑰導入 `authorized\_keys`.

   將整個金鑰複製到 `authorized\_keys` 檔案如下：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 若要完成建立使用者，請變更 `/home/rjmetric` 允許訪問的目錄 `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>若 `sshd\_config` 與伺服器相關聯的檔案未設定為預設選項，只有某些使用者能存取伺服器 — 這會防止成功連線至 [!DNL MBI]. 在這些情況下，必須執行類似 `AllowUsers` 允許 `rjmetric` 對伺服器的用戶訪問。

## 建立 `MySQL` 用戶 [!DNL MBI] {#mysql}

您的組織可能需要不同的程式，但建立此使用者最簡單的方式是在登入時執行下列查詢 `MySQL` 以具有授予權限權限的使用者身分：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

取代 `secure password here` 使用安全密碼，該密碼可以與 `SSH` 密碼。

要限制此用戶訪問特定資料庫、表或列中的資料，可以改為運行僅允許訪問您允許的資料的GRANT查詢。

## 將連線和使用者資訊輸入 [!DNL MBI] {#finish}

總結一下，我們需要將連線和使用者資訊輸入 [!DNL MBI]. 你離開 `MySQL credentials` 頁面開啟？ 如果沒有，請前往 **[!UICONTROL Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**，然後是MySQL表徵圖。 別忘了設定 `Encrypted` 切換為 `Yes`.

從「資料庫連接」部分開始，在此頁中輸入以下資訊：

* `Username`:的使用者名稱 [!DNL MBI] MySQL用戶
* `Password`:的密碼 [!DNL MBI] MySQL用戶
* `Port`:伺服器上的MySQL埠（預設為3306）
* `Host` 預設情況下，此為localhost。 一般來說，它將是MySQL伺服器的綁定地址值，預設為 `127.0.0.1 (localhost)`，但也可能是某些本機網路位址(例如， `192.168.0.1`)或伺服器的公用IP位址。

   可在 `my.cnf` 檔案(通常位於 `/etc/my.cnf`)，這行會讀 `\[mysqld\]`. 如果在該檔案中注釋了bind-address行，則伺服器將從外部連接嘗試中獲得安全。

在 `SSH Connection` 小節：

* `Remote Address`:伺服器的IP地址或主機名 [!DNL MBI] 將隧道
* `Username`:的使用者名稱 [!DNL MBI] SSH(Linux)用戶
* `SSH Port`:伺服器上的SSH埠（預設為22個）

就這樣！ 完成後，按一下 **[!UICONTROL Save & Test]** 以完成設定。

## 相關：

* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
