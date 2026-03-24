---
title: 常見Commerce表格
description: 瞭解 [!DNL Commerce Intelligence] 客戶使用的一些較常見的表格。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/uYdgYNMbJGRz8kQ3mCF2McpZpflHSAa37Lk-CLaDlBw
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 461
ht-degree: 0%

---

# 常見Commerce表格

當您第一次將[!DNL Adobe Commerce]執行個體連線到[[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)時，[!DNL Commerce Intelligence]會自動複製您某些商務表格（通常是4-6個表格）中的資料，以設定儀表板和報表的初始集合。 雖然這是一個絕佳的起點，但大多數商店執行個體會產生數十個（如果不是數百個）額外的表格，這些表格可提供提升業務效能的關鍵insight。

以下是[!DNL Commerce Intelligence]客戶使用的一些較常用表格的清單。 在您[將您的Commerce執行個體連線至Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)後，您可以使用[Data Warehouse管理員](../../data-analyst/data-warehouse-mgr/tour-dwm.md)來追蹤相關的資料欄位。

| 表格名稱 | 說明 |
|---|---|
| `catalog_category_entity` | `catalog_category_entity`表格中的每一列都說明特定類別。 您可以使用相關聯的`catalog_category_entity_varchar`資料表和`catalog_category_product`對應資料表，取得每個產品的類別資訊。 |
| `catalog_category_product` | `catalog_category_product`表格中的每一列都列出產品與類別的組合。 因此，特定產品可以不同類別多次存在於此表上，並且特定類別可以多次存在於此表上與不同產品相關聯。 此資料表會索引`catalog_category_entity`資料表（包含類別層級詳細資訊）和`catalog_product_entity`資料表（包含產品層級詳細資訊）。 |
| `catalog_product_entity` | `catalog_product_entity`表格中的每一列代表特定產品。 包括在您的Commerce帳戶中建立該產品及其SKU的時間。 |
| `customer_entity` | [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md)表格中的每一列代表您網站上的註冊使用者。 基本的客戶層級詳細資料，例如其註冊日期和電子郵件地址已上線。 |
| `quote` | [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md)表格中的每一列代表結帳程式中建立的購物車，無論該購物車最終是否轉換為訂單。 由於此表格可能會有相當的大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。 |
| `quote_item` | [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md)表格中的每一列代表加入購物車的專案，無論購物車最終是否轉換為訂單。 由於此表格可能會有相當的大小，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。 |
| `sales_order` | [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md)表格中的每一列代表您網站上的訂單。 此表格包含訂單層次資訊，例如訂單日期、下訂單的客戶、訂單總計，以及折扣與優惠券代碼用途。 |
| `sales_order_address` | `sales_order_address`表格上的每一列都包含特定訂單的送貨與帳單資訊。 在`sales_order`表格上，指定訂單的`billing_address_id`與`shipping_address_id`參考`entity_id`表格上的特定列（由`sales_order_address`識別）。 |
| `sales_order_item` | [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md)表格中的每一列都會識別特定順序中的特定專案。 每一資料列都包含產品、採購數量及特定料號相關訂單等詳細資訊。 |

{style="table-layout:auto"}

## 相關檔案

[實體關係圖](../data-warehouse-mgr/entity-rel-diag.md)
