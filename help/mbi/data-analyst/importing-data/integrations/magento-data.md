---
title: 預期的商務資料
description: 探索商務用戶導入到MBI的主要資料表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 預期的商務資料

在您 [已連接您的商務商店](../../../data-analyst/importing-data/integrations/magento.md)，您可以使用「Data Warehouse管理員」，輕鬆追蹤您商務資料庫中的相關資料欄位，以進行分析。

本文探討了商務使用者匯入的主要資料表 [!DNL MBI].

| **表名** | **說明** |
|-----|-----|
| `Customers` | 此 `customer\_entity` 和相關表描述與每個 *註冊客戶* 在資料庫中，例如其電子郵件地址和註冊日期。 透過此資訊，您可以依客戶層級屬性和同類群組開始分段。 |
| `Orders` | 此 `sales\_flat\_order` 表記錄所有訂單，包括 `created\_at` 下單的時間戳記和 `base\_grand\_total` 匯總收入的欄位。 這些欄位將是訂單層級量度的基礎。 如果訂單是由 *註冊客戶*, `customer\_id` 欄位將連結回  `customer\_entity` 表格，以便分析客戶購買行為。 |
| `Order items` | 此 `sales\_flat\_order\_item` 表記錄屬於訂單的每個項目。 這包括 `price` 和 `qty\_ordered` 欄位，以及 `order\_id` 欄位 `sales\_flat\_order` 表格。 此表格是 `Item sold`，並可讓您依 `product` 和 `product type`. |
| `Products` | 此 `catalog\_product\_entity` 表格會儲存產品層級屬性的相關資訊，例如類別、大小和顏色。 |
| `Categories` | 您的產品將屬於一或多個不同 `product categories`，具體取決於您的商務組建設定方式。 此 `catalog\_category\_entity` 表格會儲存這些類別的階層（例如Apprarel > Tops > T-Thirts），以及 `catalog\_category\_product` 表格會記錄您的產品與這些類別之間的連線。 |

{style=&quot;table-layout:auto&quot;}

## 相關

* [連接 [!DNL Magento]](../integrations/magento.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
