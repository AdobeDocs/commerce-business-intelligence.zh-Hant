---
title: 開始使用Adobe Commerce Intelligence
description: 瞭解如何上線Adobe Commerce Intelligence。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 194
ht-degree: 0%

---

# 上線[!DNL Adobe Commerce Intelligence]

與`store`和`database`設定相關的上線問題可確保您正確設定您的報告。 有了這些答案，Adobe便可針對商店設定提供量身打造的報表。

## 商店設定

- *您的商店是否接受訪客結帳？* — 如果您允許客戶在您商店購買但不註冊帳戶，請選取&#x200B;**是**。

- `Timezone` — 選取您想要在其中檢視報告的`timezone`。

- `Currency` — 選取您的商店營運所在的`currency`。

- `Your week starts on...` — 在報表中選取您要作為一週開始的一週中的某天。

- *您使用哪個Commerce版本？* — 選取您的商店營運所在的`currency`。

- *您的商店是否位於歐盟？* — 如果您回答`Yes`此問題，Adobe會依照GDPR將您的Data Warehouse和所有資料託管於歐盟。

## 資料庫設定

- `Database name` - Commerce交易資料所在的&#x200B;*資料庫[!DNL MySQL]的*&#x200B;名稱為何？

- `Table prefix (optional)` — 您Commerce資料庫中包含的資料表是否前面有任何字元（例如`store_`）？ 情況通常並非如此，但這是可以進行的自訂。
