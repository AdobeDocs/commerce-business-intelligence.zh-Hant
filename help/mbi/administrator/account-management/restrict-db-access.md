---
title: 限制對資料庫的存取
description: 瞭解如何限制存取，限制對存放您資料庫的伺服器的存取。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 限制存取

當您建立與伺服器的SSH通道時，[!DNL Adobe Commerce Intelligence]不需要存取資料庫以外的任何專案。 如果您不希望[!DNL Commerce Intelligence]擁有存放您資料庫的伺服器的完整存取權，您可以強制將[!DNL Commerce Intelligence Linux]使用者置於[受限的bash shell](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html)中，以限制存取權。

您可能從名稱猜到了，但使用受限的bash shell來設定比標準shell更受控制的環境。 這類殼層的重要一點在於，受限殼層使用者無法存取系統功能或進行任何修改。

若要限制[!DNL Commerce Intelligence Linux]使用者，您必須執行下列兩個動作：

1. 將PATH環境變數變更為空字串。 這表示使用者無法存取系統可執行檔。

1. 確定執行的殼層是`bash -r`

這兩項作業都可在使用者本位`dir/.ssh`目錄的`authorized_keys`檔案中完成，做為使用者登入時執行命令的一部分。 看起來像這樣：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成時，您為[!DNL Commerce Intelligence]建立的使用者無法變更您的系統。
