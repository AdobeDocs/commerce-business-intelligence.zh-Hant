---
title: '透過SSH通道連線 [!DNL MySQL] '
description: 瞭解如何透過SSH通道連線 [!DNL MySQL] 。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 透過[!DNL MySQL]連線[!DNL SSH Tunnel]

* [擷取 [!DNL Commerce Intelligence] 公開金鑰](#retrieve)
* [允許存取 [!DNL Commerce Intelligence] IP位址](#allowlist)
* [建立 [!DNL Commerce Intelligence]的Linux使用者](#linux)
* [為 [!DNL MySQL] 建立 [!DNL Commerce Intelligence]使用者](#mysql)
* [在 [!DNL Commerce Intelligence]中輸入連線和使用者資訊](#finish)

## 跳轉到

* [[!DNL MySQL]透過 ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL]透過 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

若要透過[!DNL MySQL]將您的[!DNL Commerce Intelligence]資料庫連線至`SSH tunnel`，您必須執行下列幾個動作：

1. 擷取[!DNL Commerce Intelligence] `public key`
1. 允許存取[!DNL Commerce Intelligence] `IP address`
1. 建立`Linux`的[!DNL Commerce Intelligence]使用者
1. 建立`MySQL`的[!DNL Commerce Intelligence]使用者
1. 在[!DNL Commerce Intelligence]中輸入連線和使用者資訊


## 正在擷取[!DNL Commerce Intelligence]公開金鑰 {#retrieve}

`public key`用於授權[!DNL Commerce Intelligence] `Linux`使用者。 在下一節中，您將建立使用者並匯入金鑰。

1. 移至&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;並按一下&#x200B;**[!UICONTROL Add New Data Source]**。
1. 按一下`MySQL`圖示。
1. 在`MySQL credentials`頁面開啟後，將`Encrypted`切換設定為`Yes`。 這會顯示SSH設定表單。
1. `public key`位於此表單下方。

在本教學課程中保持此頁面開啟 — 您需要在下一節及結尾使用它。

以下說明如何瀏覽[!DNL Commerce Intelligence]以擷取金鑰：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 允許存取[!DNL Commerce Intelligence] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 他們是`54.88.76.97`和`34.250.211.151`，但他們也在`MySQL credentials`頁面上。 請參閱上方GIF中的藍色方塊。

## 正在建立[!DNL Linux]的[!DNL Commerce Intelligence]使用者 {#linux}

只要包含即時（或經常更新）資料，這可以是生產或次要機器。 您可以用任何您喜歡的方式[限制此使用者](../../../administrator/account-management/restrict-db-access.md)，只要它保留連線至`MySQL`伺服器的權利。

1. 若要新增使用者，請以root身分在[!DNL Linux]伺服器上執行下列命令：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 還記得在第一節中擷取的`public key`嗎？ 若要確保使用者可以存取資料庫，您必須將金鑰匯入`authorized\_keys`。

   將整個金鑰複製到`authorized\_keys`檔案，如下所示：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 若要完成建立使用者，請變更`/home/rjmetric`目錄上的許可權，以允許透過`SSH`存取：

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>如果與伺服器相關聯的`sshd\_config`檔案未設定為預設選項，則只有特定使用者具有伺服器存取權 — 這會防止成功連線到[!DNL Commerce Intelligence]。 在這些情況下，必須執行`AllowUsers`之類的命令，才能允許`rjmetric`使用者存取伺服器。

## 正在建立[!DNL MySQL]的[!DNL Commerce Intelligence]使用者 {#mysql}

您的組織可能需要不同的程式，但建立此使用者最簡單的方法是在以有權授予許可權的使用者身分登入[!DNL MySQL]時執行以下查詢：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

以安全密碼取代`secure password here`，此密碼可能與`SSH`密碼不同。

若要限制此使用者存取特定資料庫、表格或欄中的資料，您可以改為執行GRANT查詢，僅允許存取您允許的資料。

## 正在將連線和使用者資訊輸入[!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須在[!DNL Commerce Intelligence]中輸入連線和使用者資訊。 您是否讓`MySQL credentials`頁面保持開啟狀態？ 如果沒有，請移至&#x200B;**[!UICONTROL Data** > **Connections]**&#x200B;並按一下&#x200B;**[!UICONTROL Add New Data Source]**，然後按一下[!DNL MySQL]圖示。 別忘了將`Encrypted`切換設為`Yes`。

在此頁面中輸入下列資訊，從`Database Connection`區段開始：

* `Username`： [!DNL Commerce Intelligence] [!DNL MySQL]使用者的使用者名稱
* `Password`： [!DNL Commerce Intelligence] [!DNL MySQL]使用者的密碼
* `Port`：伺服器上的[!DNL MySQL]連線埠（預設為3306）
* `Host`預設為localhost。 一般而言，這是[!DNL MySQL]伺服器的繫結位址值，預設值為`127.0.0.1 (localhost)`，但也可能為某些本機網路位址（例如`192.168.0.1`）或伺服器的公用IP位址。

  值可在您的`my.cnf`檔案（位於`/etc/my.cnf`）中讀取`\[mysqld\]`的行下找到。 若該檔案中的繫結位址列被註解，則您的伺服器將會受到外部連線嘗試的保護。

在`SSH Connection`區段中：

* `Remote Address`：伺服器[!DNL Commerce Intelligence]的IP位址或主機名稱將通道至
* `Username`： [!DNL Commerce Intelligence] SSH ([!DNL Linux])使用者的使用者名稱
* `SSH Port`：伺服器上的SSH連線埠（預設為22）

完成時，按一下&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成設定。

## 相關：

* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
