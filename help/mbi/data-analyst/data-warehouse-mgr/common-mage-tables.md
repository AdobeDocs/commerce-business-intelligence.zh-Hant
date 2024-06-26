---
title: 常見Commerce表格
description: 瞭解以下一些較常見的表格 [!DNL Commerce Intelligence] 客戶使用。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 常見Commerce表格

當您第一次連線 [!DNL Adobe Commerce] 執行個體至 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)， [!DNL Commerce Intelligence] 自動複製部分commerce表格（通常是4-6個表格）中的資料，以設定儀表板和報表的初始集合。 雖然這是一個絕佳的起點，但大多數商店執行個體會產生數十個甚至數百個額外的表格，以提供對業務效能的重要深入分析。

以下是一些較常見的表格清單，其中 [!DNL Commerce Intelligence] 客戶使用。 在您之後 [將您的Commerce執行個體連線到Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)，您可以使用 [Data Warehouse管理員](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以追蹤相關資料欄位。

| 表格名稱 | 說明 |
|---|---|
| `catalog_category_entity` | 中的每一列 `catalog_category_entity` 此表格說明特定類別。 與相關聯的 `catalog_category_entity_varchar` 表格和 `catalog_category_product` 對應表格中，您可以取得每個產品的類別資訊。 |
| `catalog_category_product` | 中的每一列 `catalog_category_product` 此表格會列出產品與類別的組合。 因此，特定產品可以不同類別多次存在於此表上，並且特定類別可以多次存在於此表上與不同產品相關聯。 此表格會編制以下專案的索引： `catalog_category_entity` 表格（包含類別層次明細）與 `catalog_product_entity` 表格（包含產品層級詳細資訊）。 |
| `catalog_product_entity` | 中的每一列 `catalog_product_entity` 表格代表特定產品。 包括在您的Commerce帳戶及其SKU中建立產品的時間。 |
| `customer_entity` | 中的每一列 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表格代表您網站上的註冊使用者。 基本的客戶層級詳細資料，例如其註冊日期和電子郵件地址已上線。 |
| `quote` | 中的每一列 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 表格代表結帳程式中建立的購物車，無論該購物車最終是否轉換為訂單。 由於此表格可能會有大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。 |
| `quote_item` | 中的每一列 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表格代表新增至購物車的專案，無論購物車最終是否轉換為訂單。 由於此表格可能會有大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。 |
| `sales_order` | 中的每一列 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 表格代表您網站上的訂單。 此表格包含訂單層次資訊，例如訂單日期、下訂單的客戶、訂單總計，以及折扣與優惠券代碼用途。 |
| `sales_order_address` | 上的每一列 `sales_order_address` 表格包含特定訂單的送貨與帳單資訊。 在 `sales_order` 表格， `billing_address_id` 和 `shipping_address_id` 若為特定順序，請參閱特定列(識別為 `entity_id`)在 `sales_order_address` 表格。 |
| `sales_order_item` | 中的每一列 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表格會識別特定訂單中的特定專案。 每一資料列都包含產品、採購數量及特定料號相關訂單等詳細資訊。 |

{style="table-layout:auto"}

## 相關檔案

[實體關係圖](../data-warehouse-mgr/entity-rel-diag.md)
