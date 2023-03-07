---
title: 常見商務表
description: 了解一些較常見的表格， [!DNL MBI] 客戶使用。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 常見商務表

將Commerce執行個體首次連結至 [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] 會自動複製某些商務表格（通常為4到6個表格）中的資料，以設定控制面板和報表的初始集合。 雖然這提供了絕佳的起點，但大多數儲存實例都會生成數十個（甚至數百個）的附加表，這些表可提供對您業務效能的關鍵分析。

以下是一些較常見表格的清單， [!DNL MBI] 客戶使用。 在 [將您的Commerce實例連接到MBI](../../data-analyst/importing-data/integrations/magento.md)，您可以使用 [Data Warehouse管理員](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 來追蹤相關資料欄位。

| 表名 | 說明 |
|---|---|
| `catalog_category_entity` | 中的每一列 `catalog_category_entity` 表格說明特定類別。 與 `catalog_category_entity_varchar` 表格和 `catalog_category_product` 映射表，可獲取每個產品的類別資訊。 |
| `catalog_category_product` | 中的每一列 `catalog_category_product` 表格列出產品和類別的組合。 因此，給定產品可以在此表上多次存在，且不同類別不同，並且給定類別可以在此表上存在多次，與不同產品相關聯。 此表索引 `catalog_category_entity` 表（包含類別層詳細資訊）和 `catalog_product_entity` 表格（包含產品層級詳細資料）。 |
| `catalog_product_entity` | 中的每一列 `catalog_product_entity` 表格代表特定產品。 這包括在您的商務帳戶及其SKU中建立該產品時。 |
| `customer_entity` | 中的每一列 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表格代表您網站上的註冊使用者。 此表格上會顯示基本客戶層級詳細資訊，例如其註冊日期和電子郵件地址。 |
| `quote` | 中的每一列 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 表格代表在結帳過程中建立的購物車，無論該購物車最終是否轉換為訂單。 由於此表的潛在大小，Adobe建議您在符合某些標準時（例如，如果有任何未轉換的購物車超過60天）定期刪除記錄。 |
| `quote_item` | 中的每一列 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表格代表新增至購物車的項目，無論該購物車最終是否轉換為訂單。 由於此表的潛在大小，Adobe建議您在符合某些標準時（例如，如果有任何未轉換的購物車超過60天）定期刪除記錄。 |
| `sales_order` | 中的每一列 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 表格代表您網站上的訂單。 此表包含訂單層級的資訊，如訂單日期、下單的客戶、訂單總計，以及折扣和抵用券代碼使用情況。 |
| `sales_order_address` | 上的每一列 `sales_order_address` 表包含特定訂單的發運和開單資訊。 在 `sales_order` 表格、 `billing_address_id` 和 `shipping_address_id` 對於指定訂單，請參閱特定列(識別者： `entity_id`) `sales_order_address` 表格。 |
| `sales_order_item` | 中的每一列 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表從特定訂單中標識特定項。 每一列都包含詳細資訊，例如產品、購買數量以及與指定項目關聯的訂單。 |

{style="table-layout:auto"}

## 相關檔案

[實體關係圖](../data-warehouse-mgr/entity-rel-diag.md)
