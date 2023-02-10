---
title: Connect [!DNL MongoDB] 透過SSH通道
description: 了解如何連線 [!DNL MongoDB] 通過SSH通道。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Connect [!DNL MongoDB] 透過SSH通道


連接 [!DNL MongoDB] 資料庫 [!DNL MBI] 透過SSH通道，您（或您的團隊，如果您不是技術人員）需要執行下列操作：

1. [擷取 [!DNL MBI] 公開金鑰](#retrieve)
1. [允許存取 [!DNL MBI] IP位址](#allowlist)
1. [為MBI建立Linux用戶](#linux)
1. [建立 [!DNL MongoDB] MBI用戶](#mongodb)
1. [在 [!DNL MBI]](#finish)

>[!NOTE]
>
>由於此設定的技術性質，建議您循環使用開發人員，以說明您之前是否未執行此作業。

## 擷取 [!DNL MBI] 公開金鑰 {#retrieve}

此 `public key` 用於授權 [!DNL MBI] `Linux` 使用者。 在下一節中，我們會建立使用者並匯入金鑰。

1. 前往 **[!UICONTROL Data** > **Connections]** 按一下 **[!UICONTROL Add New Data Source]**.
1. 按一下 [!DNL MONGODB] 表徵圖。
1. 在 [!DNL MongoDB] 「憑據」頁開啟，更改 `Encrypted` 切換為 `Yes`. 這會顯示SSH設定表單。
1. 此 `public key` 位於此表單下。

在整個教學課程中，請保持此頁面開啟，您需要在下一節和結尾處開啟。

如果您有點迷路，以下是如何導覽 [!DNL MBI] 要檢索密鑰，請執行以下操作：

![擷取RJMetrics公開金鑰](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 允許存取 [!DNL MBI] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從我們的IP位址存取。 是 `54.88.76.97` 和 `34.250.211.151`，但也在 [!DNL MongoDB] 憑據頁：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 建立 `Linux` 用戶 [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>若 `sshd_config` 與伺服器相關聯的檔案未設定為預設選項，只有某些使用者能存取伺服器 — 這會防止成功連線至 [!DNL MBI]. 在這些情況下，必須執行類似 `AllowUsers` 允許 `rjmetric` 對伺服器的用戶訪問。

只要包含即時（或經常更新）資料，就可以是生產或次要電腦。 只要此用戶保留連接到的權限，您可以按任何需要的方式限制該用戶 [!DNL MongoDB] 伺服器。

若要新增新使用者，請在 `Linux` 伺服器：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

記住 `public key` 我們在第一節中擷取的？ 為確保用戶能夠訪問資料庫，我們需要將密鑰導入 `authorized_keys`. 將整個金鑰複製到 `authorized_keys` 檔案如下：

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

要完成建立用戶，請更改/home/rjmetric目錄的權限以允許通過SSH訪問：

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## 建立 [!DNL MBI] [!DNL MongoDB] 使用者 {#mongodb}

[!DNL MongoDB] 伺服器有兩種執行模式 —  [一個具有「auth」選項](#auth) `(mongod -- auth)` 一個沒有， [為預設值](#default). 建立 [!DNL MongoDB] 根據您的伺服器使用的模式，使用者會有所不同，因此請務必驗證模式，再繼續。

### 若您的伺服器使用 `Auth` 選項： {#auth}

連接到多個資料庫時，可以通過登錄來添加用戶 [!DNL MongoDB] 以管理員使用者身分執行下列命令。

>[!NOTE]
>
>要查看所有可用的資料庫， [!DNL MBI] 使用者需要執行權限 `listDatabases.`

此命令將授予 [!DNL MBI] 使用者存取權 `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

使用此命令可授予 [!DNL MBI] 使用者存取權 `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

這會列印如下的回應：

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### 如果您的伺服器使用預設選項 {#default}

如果您的伺服器未使用 `auth` 模式，您的 [!DNL MongoDB] 即使沒有用戶名和密碼，伺服器仍可訪問。 不過，您應確保 `mongodb.conf` 檔案 `(/etc/mongodb.conf)` 有以下幾行 — 如果沒有，請在添加這些行後重新啟動伺服器。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

系結 [!DNL MongoDB] 伺服器到不同的地址，在下一步中相應地調整資料庫主機名。

## 將連線和使用者資訊輸入 [!DNL MBI] {#finish}

總結一下，我們需要將連線和使用者資訊輸入 [!DNL MBI]. 你離開 [!DNL MongoDB] 憑據頁開啟？ 如果沒有，請前往 **[!UICONTROL Data > Connections]** 按一下 **[!UICONTROL Add New Data Source]**，則 [!DNL MongoDB] 表徵圖。 別忘了改變 `Encrypted` 切換為 `Yes`.

在此頁面中輸入以下資訊，從 `Database Connection` 小節：

* `Host`: `127.0.0.1`
* `Username`:此 [!DNL MBI] [!DNL MongoDB] 用戶名( `rjmetric`)
* `Password`:此 [!DNL MBI] [!DNL MongoDB] 密碼
* `Port`:伺服器上的MongoDB埠(`27017` 依預設)
* `Database Name` （可選）:如果只允許訪問一個資料庫，請在此處指定該資料庫的名稱。

在 `SSH Connection` 小節：

* `Remote Address`:我們要SSH到的伺服器的IP地址或主機名
* `Username`:此 [!DNL MBI] Linux(SSH)使用者名稱（應為量度）
* `SSH Port`:伺服器上的SSH埠（預設為22個）

就這樣！ 完成後，按一下 **[!UICONTROL Save Test]** 以完成設定。

### 相關

* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
