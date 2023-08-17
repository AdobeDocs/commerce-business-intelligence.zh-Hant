---
title: 連線 [!DNL MongoDB] 透過SSH通道
description: 瞭解如何連結 [!DNL MongoDB] 透過SSH通道。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 連線 [!DNL MongoDB] 透過SSH通道

連線您的 [!DNL MongoDB] 資料庫至 [!DNL Commerce Intelligence] 透過SSH通道，您必須進行一些工作：

1. [擷取 [!DNL Commerce Intelligence] 公開金鑰](#retrieve)
1. [允許存取 [!DNL Commerce Intelligence] IP位址](#allowlist)
1. [建立Commerce Intelligence的Linux使用者](#linux)
1. [建立 [!DNL MongoDB] Commerce Intelligence使用者](#mongodb)
1. [在中輸入連線和使用者資訊 [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>由於此設定的技術性質，Adobe建議您找開發人員使用回圈，協助解決您以前未執行此設定的問題。

## 正在擷取 [!DNL Commerce Intelligence] 公開金鑰 {#retrieve}

此 `public key` 用於授權 [!DNL Commerce Intelligence] `Linux` 使用者。 下一節將引導您建立使用者和匯入金鑰。

1. 前往 **[!UICONTROL Data** > **Connections]** 並按一下 **[!UICONTROL Add New Data Source]**.
1. 按一下 [!DNL MONGODB] 圖示。
1. 在 [!DNL MongoDB] 認證頁面開啟，變更 `Encrypted` 切換至 `Yes`. 這會顯示SSH設定表單。
1. 此 `public key` 位在此表單下方。

在本教學課程中保持此頁面開啟 — 您需要在下一節及結尾使用它。

如果您有點不知所措，以下說明如何瀏覽 [!DNL Commerce Intelligence] 擷取金鑰：

![正在擷取RJMetrics公開金鑰](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 允許存取 [!DNL Commerce Intelligence] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 它們是 `54.88.76.97` 和 `34.250.211.151`，但也在 [!DNL MongoDB] 證明資料頁面：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 建立 `Linux` 使用者 [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>如果 `sshd_config` 與伺服器關聯的檔案未設定為預設選項，只有特定使用者擁有伺服器存取權 — 這會防止成功連線至 [!DNL Commerce Intelligence]. 在這些情況下，必須執行類似以下的命令 `AllowUsers` 以允許 `rjmetric` 使用者對伺服器的存取權。

只要包含即時（或經常更新）資料，這可以是生產或次要機器。 只要該使用者保留連線至的權利，您就可以透過您喜歡的方式限制該使用者 [!DNL MongoDB] 伺服器。

若要新增使用者，請以root身分在 `Linux` 伺服器：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

記住 `public key` 您在第一節中擷取了嗎？ 為確保使用者有權存取資料庫，您需要將金鑰匯入 `authorized_keys`. 將整個金鑰複製到 `authorized_keys` 檔案如下所示：

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

若要完成建立使用者，請變更/home/rjmetric目錄的許可權，以允許透過SSH存取：

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## 建立 [!DNL Commerce Intelligence] [!DNL MongoDB] 使用者 {#mongodb}

[!DNL MongoDB] 伺服器有兩種執行模式 —  [一個具有「驗證」選項](#auth) `(mongod -- auth)` 一個沒有， [這是預設值](#default). 建立「 」的步驟 [!DNL MongoDB] 使用者依伺服器使用的模式而異。 繼續之前，請務必驗證模式。

### 如果您的伺服器使用 `Auth` 選項： {#auth}

連線到多個資料庫時，您可以登入來新增使用者 [!DNL MongoDB] 以管理員使用者身分執行以下命令。

>[!NOTE]
>
>若要檢視所有可用的資料庫， [!DNL Commerce Intelligence] 使用者需要許可權才能執行 `listDatabases.`

這個指令會授予 [!DNL Commerce Intelligence] 使用者存取 `to all databases`：

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

使用此命令授予 [!DNL Commerce Intelligence] 使用者存取 `to a single database`：

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

這會列印如下所示的回應：

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### 如果您的伺服器使用預設選項 {#default}

如果您的伺服器未使用 `auth` 模式，您的 [!DNL MongoDB] 即使沒有使用者名稱和密碼，伺服器也可以存取。 不過，您應確保 `mongodb.conf` 檔案 `(/etc/mongodb.conf)` 有以下各行 — 如果沒有，請在新增後重新啟動伺服器。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

若要繫結您的 [!DNL MongoDB] 伺服器至不同的位址，請在下一個步驟中相應地調整資料庫主機名稱。

## 將連線和使用者資訊輸入到 [!DNL Commerce Intelligence] {#finish}

若要完成工作，您必須在中輸入連線和使用者資訊 [!DNL Commerce Intelligence]. 您是否離開 [!DNL MongoDB] 憑證頁面是否開啟？ 如果沒有，請前往 **[!UICONTROL Data > Connections]** 並按一下 **[!UICONTROL Add New Data Source]**，然後 [!DNL MongoDB] 圖示。 別忘了變更 `Encrypted` 切換至 `Yes`.

在此頁面中輸入以下資訊，從 `Database Connection` 區段：

* `Host`: `127.0.0.1`
* `Username`：此 [!DNL Commerce Intelligence] [!DNL MongoDB] 使用者名稱(應為 `rjmetric`)
* `Password`：此 [!DNL Commerce Intelligence] [!DNL MongoDB] 密碼
* `Port`：伺服器上的MongoDB連線埠(`27017` 預設值)
* `Database Name` （選擇性）：如果您只允許存取一個資料庫，請在此處指定該資料庫的名稱。

在 `SSH Connection` 區段：

* `Remote Address`：您要透過SSH連線的伺服器IP位址或主機名稱
* `Username`：此 [!DNL Commerce Intelligence] Linux (SSH)使用者名稱（應為rjmetric）
* `SSH Port`：伺服器上的SSH連線埠（預設為22）

完成後，按一下 **[!UICONTROL Save Test]** 以完成設定。

### 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
