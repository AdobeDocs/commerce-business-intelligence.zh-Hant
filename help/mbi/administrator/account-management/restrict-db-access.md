---
title: 限制對資料庫的訪問
description: 瞭解如何限制訪問，限制對儲存資料庫的伺服器的訪問。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 限制訪問

建立到伺服器的SSH隧道時，無需 [!DNL Adobe Commerce Intelligence] 除了資料庫之外的一切。 如果你不想 [!DNL Commerce Intelligence] 要完全訪問儲存資料庫的伺服器，可以通過強制 [!DNL Commerce Intelligence Linux] 用戶 [受限空殼](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html)。

您可能已經從名稱中猜到了，但是使用受限的bash shell來設定比標準shell更受控制的環境。 此類shell的重要之處在於受限的shell用戶不能訪問系統功能或進行任何修改。

要限制 [!DNL Commerce Intelligence Linux] 用戶：您必須執行兩個操作：

1. 將PATH環境變數更改為空字串。 這意味著用戶無法訪問系統執行檔。

1. 確保執行的shell `bash -r`

這兩個都可以在 `authorized_keys` 用戶首頁中的檔案 `dir/.ssh` 目錄，作為用戶登錄時執行的命令的一部分。 它看起來是這樣的：

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

完成後，為建立的用戶 [!DNL Commerce Intelligence] 無法對系統進行更改。
