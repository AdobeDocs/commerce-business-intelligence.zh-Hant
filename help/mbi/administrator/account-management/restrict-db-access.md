---
title: 限制對資料庫的存取
description: 瞭解如何限制存取，限制對存放您資料庫的伺服器的存取。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 限制存取

當您建立與伺服器的SSH通道時，不需要 [!DNL Adobe Commerce Intelligence] 以存取資料庫以外的任何專案。 如果您不想 [!DNL Commerce Intelligence] 若要對存放您資料庫的伺服器擁有完整存取權，您可以透過強制 [!DNL Commerce Intelligence Linux] 將使用者移入 [受限制的bash shell](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

您可能從名稱猜到了，但使用受限的bash shell來設定比標準shell更受控制的環境。 這類殼層的重要一點在於，受限殼層使用者無法存取系統功能或進行任何修改。

若要限制 [!DNL Commerce Intelligence Linux] 使用者，您必須執行下列兩件事：

1. 將PATH環境變數變更為空字串。 這表示使用者無法存取系統可執行檔。

1. 確定執行的Shell為 `bash -r`

這兩項作業都可以在內完成 `authorized_keys` 位於使用者首頁的檔案 `dir/.ssh` 目錄，當使用者登入時執行命令的一部分。 看起來像這樣：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成時，您為建立的使用者 [!DNL Commerce Intelligence] 無法變更您的系統。
