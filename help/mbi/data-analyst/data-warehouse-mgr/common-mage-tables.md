---
title: 常用商業表
description: 瞭解一些更常見的表 [!DNL Commerce Intelligence] 客戶使用。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 常用商業表

首次連接時 [!DNL Adobe Commerce] 實例 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)。 [!DNL Commerce Intelligence] 自動從某些商業表（通常為4-6個表）中複製資料，以配置初始儀表板和報表集。 儘管這提供了一個極好的起點，但大多數儲存實例都會生成幾十個甚至幾百個附加表，這些表能夠提供對您業務效能的關鍵見解。

下面是一些比較常見的表的清單 [!DNL Commerce Intelligence] 客戶使用。 在你之後 [將您的Commerce實例連接到Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)，可以使用 [Data Warehouse管理器](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 跟蹤相關資料欄位。

| 表名 | 說明 |
|---|---|
| `catalog_category_entity` | 中的每一行 `catalog_category_entity` 表描述了特定類別。 與關聯 `catalog_category_entity_varchar` 和 `catalog_category_product` 映射表，可獲取每個產品的類別資訊。 |
| `catalog_category_product` | 中的每一行 `catalog_category_product` 表列出了產品和類別的組合。 因此，給定產品可以多次存在於此表中，並且具有不同的類別，並且給定類別可以多次存在於此表中與不同產品相關聯。 此表索引 `catalog_category_entity` 表（包含類別級詳細資訊）和 `catalog_product_entity` 表（包含產品級詳細資訊）。 |
| `catalog_product_entity` | 中的每一行 `catalog_product_entity` 表表示特定產品。 這包括在您的Commerce帳戶及其SKU中建立該產品的時間。 |
| `customer_entity` | 中的每一行 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表表示您網站上的註冊用戶。 此表中包含基本的客戶級詳細資訊，如其註冊日期和電子郵件地址。 |
| `quote` | 中的每一行 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 表表示在簽出過程中建立的購物車，無論該購物車最終是否轉換為訂單。 由於此表的潛在大小，Adobe建議您在滿足某些條件時定期刪除記錄，例如，如果有任何未轉換的購物車超過60天。 |
| `quote_item` | 中的每一行 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表表示添加到購物車的物料，即購物車是否最終轉換為訂單。 由於此表的潛在大小，Adobe建議您在滿足某些條件時定期刪除記錄，例如，如果有任何未轉換的購物車超過60天。 |
| `sales_order` | 中的每一行 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 表表示在您的站點上下達的訂單。 此表包含訂單層資訊，如訂單日期、下訂單的客戶、訂單合計以及折扣和優惠券代碼使用情況。 |
| `sales_order_address` | 上的每一行 `sales_order_address` 表包含特定訂單的發運和開單資訊。 在 `sales_order` 的 `billing_address_id` 和 `shipping_address_id` 對於給定訂單，請參閱特定行(由 `entity_id`) `sales_order_address` 的子菜單。 |
| `sales_order_item` | 中的每一行 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表從特定訂單中標識特定項。 每行都包含詳細資訊，如產品、已採購數量以及與給定物料關聯的訂單。 |

{style="table-layout:auto"}

## 相關文檔

[實體關係圖](../data-warehouse-mgr/entity-rel-diag.md)
