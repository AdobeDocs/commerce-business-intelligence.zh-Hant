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

# 入門 [!DNL Adobe Commerce Intelligence]

與相關的入門問題 `store` 和 `database` 設定可確保您正確設定報表。 有了這些答案，Adobe就能提供您專為商店設定量身打造的報表。

## 商店設定

- *您的商店是否接受訪客結帳？*  — 選取 **是** 如果您允許客戶在商店購買商品，而不需註冊帳戶。

- `Timezone`  — 選取 `timezone` 您希望在中檢視報告的內容。

- `Currency`  — 選取 `currency` 您的商店營運所在的地區。

- `Your week starts on...`  — 在報表中選取您要作為一週開始的一週中的某天。

- *您使用哪個版本的Commerce？*  — 選取 `currency` 您的商店營運所在的地區。

- *您的商店位於歐盟嗎？*  — 如果您回答 `Yes` 針對此問題，Adobe會遵循GDPR規定，將您的Data Warehouse和所有資料託管於歐盟。

## 資料庫設定

- `Database name`  — 什麼是 *的名稱 [!DNL MySQL] 資料庫* 您的Commerce交易資料位於何處？

- `Table prefix (optional)`  — 您的Commerce資料庫中包含的表格是否會在前面加上任何內容(例如 `store_`)？ 情況通常並非如此，但這是可以進行的自訂。
