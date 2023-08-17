---
title: 正在連線 [!DNL MySQL] 透過SSH通道
description: 瞭解如何連結 [!DNL MySQL] 透過SSH通道。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 連線 [!DNL MySQL] via [!DNL SSH Tunnel]

* [擷取 [!DNL Commerce Intelligence] 公開金鑰](#retrieve)
* [允許存取 [!DNL Commerce Intelligence] IP位址](#allowlist)
* [建立Linux使用者 [!DNL Commerce Intelligence]](#linux)
* [建立 [!DNL MySQL] 使用者 [!DNL Commerce Intelligence]](#mysql)
* [在中輸入連線和使用者資訊 [!DNL Commerce Intelligence]](#finish)

## 跳轉到

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

連線您的 [!DNL MySQL] 資料庫至 [!DNL Commerce Intelligence] 透過 `SSH tunnel`，您必須執行下列動作：

1. 擷取 [!DNL Commerce Intelligence] `public key`
1. 允許存取 [!DNL Commerce Intelligence] `IP address`
1. 建立 `Linux` 使用者 [!DNL Commerce Intelligence]
1. 建立 `MySQL` 使用者 [!DNL Commerce Intelligence]
1. 在中輸入連線和使用者資訊 [!DNL Commerce Intelligence]


## 正在擷取 [!DNL Commerce Intelligence] 公開金鑰 {#retrieve}

此 `public key` 用於授權 [!DNL Commerce Intelligence] `Linux` 使用者。 在下一節中，您將建立使用者並匯入金鑰。

1. 前往 **[!UICONTROL Manage Data** > **Connections]** 並按一下 **[!UICONTROL Add New Data Source]**.
1. 按一下 `MySQL` 圖示。
1. 在 `MySQL credentials` 頁面開啟，設定 `Encrypted` 切換至 `Yes`. 這會顯示SSH設定表單。
1. 此 `public key` 位在此表單下方。

在本教學課程中保持此頁面開啟 — 您需要在下一節及結尾使用它。

以下說明瀏覽步驟 [!DNL Commerce Intelligence] 擷取金鑰：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 允許存取 [!DNL Commerce Intelligence] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 它們是 `54.88.76.97` 和 `34.250.211.151` 但它們也在 `MySQL credentials` 頁面。 請參閱上方GIF中的藍色方塊。

## 建立 [!DNL Linux] 使用者 [!DNL Commerce Intelligence] {#linux}

只要包含即時（或經常更新）資料，這可以是生產或次要機器。 您可以 [限制此使用者](../../../administrator/account-management/restrict-db-access.md) 任何您喜歡的方式，只要它保留連線至 `MySQL` 伺服器。

1. 若要新增使用者，請以root身分在 [!DNL Linux] 伺服器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 記住 `public key` 您在第一節中擷取了嗎？ 為確保使用者有權存取資料庫，您需要將金鑰匯入 `authorized\_keys`.

   將整個金鑰複製到 `authorized\_keys` 檔案如下所示：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 若要完成建立使用者，請變更以下專案的許可權： `/home/rjmetric` 允許透過存取的目錄 `SSH`：

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 與伺服器關聯的檔案未設定為預設選項，只有特定使用者擁有伺服器存取權 — 這會防止成功連線至 [!DNL Commerce Intelligence]. 在這些情況下，必須執行類似以下的命令 `AllowUsers` 以允許 `rjmetric` 使用者對伺服器的存取權。

## 建立 [!DNL MySQL] 使用者 [!DNL Commerce Intelligence] {#mysql}

您的組織可能需要不同的流程，但建立此使用者最簡單的方法是在登入時執行以下查詢 [!DNL MySQL] 以有權授予許可權的使用者身分：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

取代 `secure password here` 安全密碼，此密碼可能與 `SSH` 密碼。

若要限制此使用者存取特定資料庫、表格或欄中的資料，您可以改為執行GRANT查詢，僅允許存取您允許的資料。

## 將連線和使用者資訊輸入到 [!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須在中輸入連線和使用者資訊 [!DNL Commerce Intelligence]. 您是否離開 `MySQL credentials` 頁面是否開啟？ 如果沒有，請前往 **[!UICONTROL Data** > **Connections]** 並按一下 **[!UICONTROL Add New Data Source]**，然後 [!DNL MySQL] 圖示。 別忘了設定 `Encrypted` 切換至 `Yes`.

在此頁面中輸入以下資訊，從 `Database Connection` 區段：

* `Username`：的使用者名稱 [!DNL Commerce Intelligence] [!DNL MySQL] 使用者
* `Password`：的密碼 [!DNL Commerce Intelligence] [!DNL MySQL] 使用者
* `Port`： [!DNL MySQL] 伺服器上的連線埠（預設為3306）
* `Host` 依預設，這是localhost。 一般而言，它是的繫結位址值 [!DNL MySQL] 伺服器，預設為 `127.0.0.1 (localhost)`，但也可能是某個本機網路位址(例如 `192.168.0.1`)或伺服器的公用IP位址。

  值可在以下連結中找到： `my.cnf` 檔案(位於 `/etc/my.cnf`)的行下方 `\[mysqld\]`. 若該檔案中的繫結位址列被註解，則您的伺服器將會受到外部連線嘗試的保護。

在 `SSH Connection` 區段：

* `Remote Address`：伺服器的IP位址或主機名稱 [!DNL Commerce Intelligence] 將通道至
* `Username`：的使用者名稱 [!DNL Commerce Intelligence] SSH ([!DNL Linux])使用者
* `SSH Port`：伺服器上的SSH連線埠（預設為22）

完成後，按一下 **[!UICONTROL Save & Test]** 以完成設定。

## 相關：

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
