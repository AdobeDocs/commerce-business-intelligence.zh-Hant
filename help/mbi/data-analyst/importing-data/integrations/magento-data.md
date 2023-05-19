---
title: 預期商業資料
description: 瀏覽Commerce用戶導入Commerce Intelligence的主資料表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 預期 [!DNL Adobe Commerce] 資料

等你 [已連接 [!DNL Adobe Commerce] 商店](../../../data-analyst/importing-data/integrations/magento.md)，您可以使用Data Warehouse管理器輕鬆跟蹤Commerce資料庫中的相關資料欄位以進行分析。

本主題探討Commerce用戶導入的主要資料表 [!DNL Commerce Intelligence]。

| **表名** | **說明** |
|-----|-----|
| `Customers` | 的 `customer\_entity` 和相關表描述了與每個 *註冊客戶* 就像他們的電子郵件地址和註冊日期。 利用此資訊，您可以開始按客戶級屬性和組進行分段。 |
| `Orders` | 的 `sales\_flat\_order` 表記錄所有訂單，包括 `created\_at` 下單的時間戳和 `base\_grand\_total` 用來計算收入的欄位。 這些欄位是訂單級度量的基礎。 如果訂單是由 *註冊客戶*，也請參見Wiki頁。 `customer\_id` 返回到  `customer\_entity` 表，以便分析客戶購買行為。 |
| `Order items` | 的 `sales\_flat\_order\_item` 表記錄屬於訂單的每個項目。 這包括 `price` 和 `qty\_ordered` 的 `order\_id` 與 `sales\_flat\_order` 的子菜單。 此表是度量的基礎，例如 `Item sold`，並允許您按 `product` 和 `product type`。 |
| `Products` | 的 `catalog\_product\_entity` 表儲存有關產品級屬性的資訊，如類別、大小和顏色。 |
| `Categories` | 您的產品屬於一個或多個不同 `product categories`，具體取決於您的Commerce生成的設定方式。 的 `catalog\_category\_entity` 表儲存這些類別的層次結構（例如，服裝>上衣> T-Stors）, `catalog\_category\_product` 表記錄您的產品與這些類別之間的連接。 |

{style="table-layout:auto"}

## 相關

* [連接 [!DNL Adobe Commerce]](../integrations/magento.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
