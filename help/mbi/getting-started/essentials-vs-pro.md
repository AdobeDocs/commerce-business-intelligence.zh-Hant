---
title: MBI Essentials與Pro
description: 了解MBI Essentials與MBI Pro有何不同。
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
source-git-commit: 1703e469e245629797bbe08d691d7f8e816a4019
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# [!DNL MBI Essentials] vs [!DNL MBI Pro]

>[!NOTE]
>
>這是 [!DNL MBI].

下表介紹了Essentials和Pro中包含的內容。

|  | **`MBI Essentials`** | **`MBI Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | 最多100 | 自訂 |
| `Pre-Defined Dashboards` | 5-6 | 自訂 |
| `New Custom Report Creation` | 是 | 是 |
| `Magento Commerce Tables` | 4-6 | 無限制 |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | 是 | 是 |
| `Data Warehouse Manager` | 不可用 | 可用 |
| `Email Reports` | 是 | 是 |
| `Cohort Report Builder` | 是 | 是 |
| `Google Analytics Live Integration` | 是 | 無限制 |
| `3rd Party Integrations` | 不可用 | 可用 |
| `Full API Access` | 否 | 是 |
| `Access to CS, AM, or Analysts` | 否 | 是 |
| `Professional Services` | 可用 | 可用 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>表數取決於來賓簽出。

**包含的表**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## Essentials中包含的列

中的項目 _斜體_ 為計算欄位。

* `sales_order` 表格
   * `entity_id`
   * `base_grand_total`
   * `customer_id`
   * `status`
   * `customer_email`
   * `store_id`
   * `base_currency_code`
   * `billing_address_id`
   * `shipping_address_id`
   * `base_shipping_amount`
   * `base_tax_amount`
   * `coupon_code`
   * `created_at`
   * `updated_at`
   * `base_subtotal`
   * `customer_group_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `increment_id`
   * `Customer's order number`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Is customer's last order?`
   * `Billing address region`
   * `Shipping address country`
   * `Customer's lifetime revenue`
   * `Seconds between customer's first order date and this order`
   * `Seconds since previous order`
   * `Store name`
   * `Customer's lifetime number of coupons`
   * `Customer's order number (previous-current)`
   * `Shipping address region`
   * `Number of items in order`
   * `Billing address city`
   * `Shipping address city`
   * `Customer's group code`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's creation date`
   * `Billing address country`

* `sales_order_item` 表格
   * `item_id`
   * `qty_ordered`
   * `base_price`
   * `name`
   * `order_id`
   * `sku`
   * `product_type`
   * `product_id`
   * `created_at`
   * `updated_at`
   * `parent_item_id`
   * `store_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `Order's coupon_code`
   * `Order item total value (quantity * price)`
   * `Order's increment_id`
   * `Customer's email`
   * `Customer's lifetime number of orders`
   * `Store name`
   * `Customer's order number`
   * `Order's status`
   * `Customer's lifetime revenue`

* `sales_order_address` 表格
   * `entity_id`
   * `city`
   * `region`
   * `country_id`

* `customer_entity` 表格
   * `entity_id`
   * `email`
   * `group_id`
   * `created_at`
   * `updated_at`
   * `store_id`
   * `Customer's lifetime revenue`
   * `Customer's lifetime number of coupons`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Seconds since customer's first order date`
   * `Customer's first 30 day revenue`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's group code`
   * `Store name`

* `customer_group` 表格
   * `customer_group_id`
   * `customer_group_code`

* `store` 表格
   * `store_id`
   * `name`

請參考下列影片系列，進一步了解 [!DNL MBI Essentials] 和 [!DNL MBI Pro].

* [`Essentials`](https://support.magento.com/hc/en-us/articles/360005305614)
* [`Pro`](https://support.magento.com/hc/en-us/articles/360005373453)
