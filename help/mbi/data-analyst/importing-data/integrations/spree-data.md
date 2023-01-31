---
title: 預期的Spree資料
description: 探索可從Spree匯入至您 [!DNL MBI] 帳戶。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 預期 [!DNL Spree] 資料

在您 [已連接 [!DNL Spree] 商店](../../../data-analyst/importing-data/integrations/spree.md)，您可以使用 [Data Warehouse管理員](../../data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤 [!DNL Spree] 分析平台。

在本文中，我們將探索您可從匯入的主要資料表 [!DNL Spree] 進入 [!DNL MBI] 帳戶，包括連結 [其他檔案](https://guides.spreecommerce.org/developer/addresses.html#address) 關於 [!DNL Spree] 資料。

| **表名** | **說明** |
|-----|-----|
| `Users` | 此 `users` 表格包含註冊客戶的帳戶詳細資訊，包括個人的電子郵件、姓名和註冊日期。 這可讓您分析不同的客戶區段及其購買行為。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 此 `orders` 表格是所有訂單層級量度的基礎。 此處記錄的是您 [!DNL Spree] 商店，包括 `completed\_at` （訂單的時間戳記）, `user\_id` （下訂單的註冊用戶id）。 若訂單是由註冊使用者所訂購，則 `user\_id` 會連結回 `users` 表格，以便分析使用者購買行為。 |
| `Line items` | 此 `line\_items` 表是其中一個的子項 `orders` 表格或 `subscriptions`. 它會記錄訂單或訂閱的行項目詳細資訊。 若訂購多項產品，每個產品在此表格中會有各自的資料列，包括 `product\_id` 讓你將它與 `Products` 表格。 |
| [`Products`](https://guides.spreecommerce.com/developer/products.html#overview) | 此 `products` 表記錄Spree目錄中可銷售項目的所有產品詳細資訊。 這可讓您依產品屬性劃分行項目層級量度。 |
| `Subscriptions` | 如果您有 [!DNL Spree] 訂閱擴充功能， `subscriptions` 表格包含每個個別訂閱的資訊，包括 `created\_at` （開始日期）, `cancelled\_at` （取消訂閱的日期），而 `interval` 訂閱。 |

{style=&quot;table-layout:auto&quot;}

## 相關：

* [連接 [!DNL Spree]](../integrations/spree.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
