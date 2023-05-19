---
title: 預期Spree資料
description: 瀏覽可從Spree導入到的主資料表 [!DNL Commerce Intelligence] 帳戶。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 預期 [!DNL Spree] 資料

等你 [已連接 [!DNL Spree] 商店](../../../data-analyst/importing-data/integrations/spree.md)，可以使用 [Data Warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤 [!DNL Spree] 分析平台。

本主題探討可從中導入的主要資料表 [!DNL Spree] 你 [!DNL Commerce Intelligence] 帳戶，包括指向 [附加文檔](https://guides.spreecommerce.org/developer/addresses.html#address) 關於 [!DNL Spree] 資料。

| **表名** | **說明** |
|-----|-----|
| `Users` | 的 `users` 表包括已註冊客戶的帳戶詳細資訊，包括個人的電子郵件、姓名和註冊日期。 這允許您分析不同的客戶細分市場及其購買行為。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 的 `orders` 表是所有訂單級度量的基礎。 此處記錄了您的所有購買訂單詳細資訊 [!DNL Spree] 商店，包括 `completed\_at` （順序的時間戳）, `user\_id` （下訂單的註冊用戶的id）。 如果訂單由註冊用戶進行， `user\_id` 連結返回 `users` 表以允許分析用戶購買行為。 |
| `Line items` | 的 `line\_items` 表是任意一個 `orders` 表格 `subscriptions`。 它記錄訂單或訂閱的行項目詳細資訊。 對於具有多個產品的訂單，每個產品在此表中都有其自己的資料行，包括 `product\_id` 讓你把它綁在 `Products` 的子菜單。 |
| `Products` | 的 `products` 表記錄Spree目錄中可銷售項目的所有產品詳細資訊。 這允許您按產品屬性對行項目層度量進行分段。 |
| `Subscriptions` | 如果你有 [!DNL Spree] 訂閱擴展， `subscriptions` 表包含每個訂閱的資訊，包括 `created\_at` （開始日期）, `cancelled\_at` （取消訂閱的日期）, `interval` 的下界。 |

{style="table-layout:auto"}

## 相關：

* [連接 [!DNL Spree]](../integrations/spree.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
