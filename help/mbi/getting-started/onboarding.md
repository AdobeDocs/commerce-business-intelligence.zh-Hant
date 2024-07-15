---
title: 開始使用Adobe Commerce Intelligence
description: 瞭解如何上線Adobe Commerce Intelligence。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 上線[!DNL Adobe Commerce Intelligence]

與`store`和`database`設定相關的上線問題可確保您正確設定您的報告。 有了這些答案，Adobe就能提供您專為商店設定量身打造的報表。

## 商店設定

- *您的商店是否接受訪客結帳？* — 如果您允許客戶在您商店購買但不註冊帳戶，請選取&#x200B;**是**。

- `Timezone` — 選取您想要在其中檢視報告的`timezone`。

- `Currency` — 選取您的商店營運所在的`currency`。

- `Your week starts on...` — 在報表中選取您要作為一週開始的一週中的某天。

- *您使用哪個Commerce版本？* — 選取您的商店營運所在的`currency`。

- *您的商店是否位於歐盟？* — 如果您回答`Yes`此問題，Adobe會根據GDPR將您的Data Warehouse和所有資料託管於歐盟。

## 資料庫設定

- `Database name` - Commerce交易資料所在的[!DNL MySQL]資料庫&#x200B;*的*&#x200B;名稱為何？

- `Table prefix (optional)` — 您Commerce資料庫中包含的資料表是否前面有任何字元（例如`store_`）？ 情況通常並非如此，但這是可以進行的自訂。
