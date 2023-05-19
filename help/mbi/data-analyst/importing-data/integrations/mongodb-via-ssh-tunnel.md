---
title: 連接 [!DNL MongoDB] 通過SSH隧道
description: 瞭解如何連接 [!DNL MongoDB] 通過SSH隧道。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 連接 [!DNL MongoDB] 通過SSH隧道

連接 [!DNL MongoDB] 資料庫 [!DNL Commerce Intelligence] 通過SSH隧道，您必須執行以下幾項操作：

1. [檢索 [!DNL Commerce Intelligence] 公鑰](#retrieve)
1. [允許訪問 [!DNL Commerce Intelligence] IP地址](#allowlist)
1. [為Commerce Intelligence建立Linux用戶](#linux)
1. [建立 [!DNL MongoDB] Commerce Intelligence用戶](#mongodb)
1. [在中輸入連接和用戶資訊 [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>由於此設定的技術性質，Adobe建議您在開發人員中循環以幫助您（如果您以前沒有這樣做）。

## 檢索 [!DNL Commerce Intelligence] 公鑰 {#retrieve}

的 `public key` 用於授權 [!DNL Commerce Intelligence] `Linux` 。 下一節將指導您建立用戶並導入密鑰。

1. 轉到 **[!UICONTROL Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**。
1. 按一下 [!DNL MONGODB] 表徵圖
1. 在 [!DNL MongoDB] 「憑據」頁面，更改 `Encrypted` 切換至 `Yes`。 這將顯示SSH設定表單。
1. 的 `public key` 位於此窗體下。

在本教程的整個過程中，保持本頁開啟 — 您需要在下一節和結尾處開啟本頁。

如果你迷路了，下面是如何在 [!DNL Commerce Intelligence] 要檢索密鑰：

![檢索RJMetrics公鑰](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 允許訪問 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使連接成功，必須配置防火牆以允許從IP地址訪問。 他們 `54.88.76.97` 和 `34.250.211.151`，但也在 [!DNL MongoDB] 「憑據」頁：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 建立 `Linux` 用戶 [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>如果 `sshd_config` 與伺服器關聯的檔案未設定為預設選項，只有某些用戶具有伺服器訪問權限 — 這會阻止成功連接到 [!DNL Commerce Intelligence]。 在這些情況下，需要運行類似 `AllowUsers` 允許 `rjmetric` 用戶訪問伺服器。

這可以是生產機或輔助機，只要它包含即時（或頻繁更新）資料。 只要用戶保留連接至 [!DNL MongoDB] 伺服器。

要添加新用戶，請以root身份在您的 `Linux` 伺服器：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

記住 `public key` 在第一節里找到的？ 要確保用戶有權訪問資料庫，您需要將密鑰導入 `authorized_keys`。 將整個密鑰複製到 `authorized_keys` 檔案，如下所示：

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

要完成用戶的建立，請更改/home/rjmetric目錄上的權限，以允許通過SSH訪問：

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## 建立 [!DNL Commerce Intelligence] [!DNL MongoDB] 用戶 {#mongodb}

[!DNL MongoDB] 伺服器有兩種運行模式 —  [帶有「auth」選項的](#auth) `(mongod -- auth)` 一個沒有， [預設](#default)。 建立 [!DNL MongoDB] 用戶因伺服器使用的模式而異。 請確保在繼續之前驗證模式。

### 如果伺服器使用 `Auth` 選項： {#auth}

連接到多個資料庫時，可以通過登錄到 [!DNL MongoDB] 作為管理員用戶並運行以下命令。

>[!NOTE]
>
>要查看所有可用資料庫， [!DNL Commerce Intelligence] 用戶需要運行權限 `listDatabases.`

此命令授予 [!DNL Commerce Intelligence] 用戶訪問 `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

使用此命令授予 [!DNL Commerce Intelligence] 用戶訪問 `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

此處顯示如下響應：

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### 如果伺服器使用預設選項 {#default}

如果伺服器不使用 `auth` 模式 [!DNL MongoDB] 即使沒有用戶名和密碼，也可以訪問伺服器。 但是，您應確保 `mongodb.conf` 檔案 `(/etc/mongodb.conf)` 具有以下行 — 如果沒有，請在添加伺服器後重新啟動伺服器。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

綁定 [!DNL MongoDB] 伺服器到其他地址，在下一步中相應調整資料庫主機名。

## 將連接和用戶資訊輸入 [!DNL Commerce Intelligence] {#finish}

要總結內容，您需要將連接和用戶資訊輸入 [!DNL Commerce Intelligence]。 你是不是離開了 [!DNL MongoDB] 「憑據」頁面開啟？ 否則，請轉到 **[!UICONTROL Data > Connections]** 按一下 **[!UICONTROL Add New Data Source]**，則 [!DNL MongoDB] 表徵圖 不要忘記更改 `Encrypted` 切換至 `Yes`。

在此頁中輸入以下資訊，從 `Database Connection` 部分：

* `Host`: `127.0.0.1`
* `Username`:的 [!DNL Commerce Intelligence] [!DNL MongoDB] 用戶名(應 `rjmetric`)
* `Password`:的 [!DNL Commerce Intelligence] [!DNL MongoDB] 密碼
* `Port`:伺服器上的MongoDB埠(`27017` 預設)
* `Database Name` （可選）:如果只允許訪問一個資料庫，請在此處指定該資料庫的名稱。

在 `SSH Connection` 部分：

* `Remote Address`:要SSH到的伺服器的IP地址或主機名
* `Username`:的 [!DNL Commerce Intelligence] Linux(SSH)用戶名（應為rjmetric）
* `SSH Port`:伺服器上的SSH埠（預設為22）

完成後，按一下 **[!UICONTROL Save Test]** 完成設定。

### 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
