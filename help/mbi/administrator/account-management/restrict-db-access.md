---
title: 限制對資料庫的訪問
description: 了解如何限制訪問，限制對儲存資料庫的伺服器的訪問。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# 限制存取

當我們建立到您伺服器的SSH通道時，不需要 [!DNL MBI] 只能存取資料庫。 如果您不想 [!DNL MBI] 要完全訪問儲存資料庫的伺服器，可以通過強制 [!DNL MBI Linux] 使用者 [受限bash殼](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

您可能已從名稱中猜到，但受限bash shell用於設定比標準shell更受控制的環境。 這種shell的重要之處是，受限制的shell用戶不能訪問系統函式或進行任何修改。

若要限制 [!DNL MBI Linux] 使用者，您必須執行兩項作業：

1. 將PATH環境變數變數變更為空字串。 這表示用戶將無法訪問系統執行檔。

1. 請確定執行的殼層為 `bash -r`

這兩項皆可在 `authorized_keys` 檔案 `dir/.ssh` 目錄，作為用戶登錄時執行的命令的一部分。 看起來會像這樣：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成後，您為建立的使用者 [!DNL MBI] 將無法對您的系統進行任何變更。
