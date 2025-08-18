---
title: 預期的Spree資料
description: 探索您可以從Spree匯入 [!DNL Commerce Intelligence] 帳戶的主要資料表。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 必須有[!DNL Spree]個資料

連線[您的 [!DNL Spree] 存放區](../../../data-analyst/importing-data/integrations/spree.md)後，您可以使用[Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md)輕鬆追蹤您[!DNL Spree]平台中的相關資料欄位以進行分析。

本主題探索您可以從[!DNL Spree]匯入至[!DNL Commerce Intelligence]帳戶的主要資料表，包括[其他檔案](https://guides.spreecommerce.org/developer/addresses.html#address)有關[!DNL Spree]資料的連結。

| **資料表名稱** | **描述** |
|-----|-----|
| `Users` | `users`表格包含註冊客戶的帳戶詳細資料，包括個人的電子郵件、名稱和註冊日期。 這可讓您分析不同的客戶區段及其購買行為。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | `orders`表格可作為您所有訂單層級量度的基礎。 這裡記錄的是從您的[!DNL Spree]商店購買的所有訂單詳細資料，包括`completed\_at` （訂單的時間戳記）、`user\_id` （下訂單的註冊使用者識別碼）。 如果訂單是由註冊的使用者所訂，則`user\_id`會連結回`users`表格，以分析使用者的購買行為。 |
| `Line items` | `line\_items`資料表是`orders`資料表或`subscriptions`的子系。 它會記錄訂單或訂閱的行專案詳細資料。 針對具有多個產品的訂單，此表格中每個產品都有自己的資料列，包括可讓您將其連結至`product\_id`表格的`Products`。 |
| `Products` | `products`表格會記錄Spree目錄中可銷售專案的所有產品詳細資料。 這可讓您依產品屬性來劃分條列專案層級量度。 |
| `Subscriptions` | 如果您有[!DNL Spree]訂閱延伸，`subscriptions`表格會保留每個個別訂閱的資訊，包括`created\_at` （開始日期）、`cancelled\_at` （取消訂閱的日期）以及訂閱的`interval`。 |

{style="table-layout:auto"}

## 相關：

* [正在連線 [!DNL Spree]](../integrations/spree.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
