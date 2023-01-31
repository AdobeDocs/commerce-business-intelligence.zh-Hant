---
title: 預期的條帶資料
description: 探索可從條帶導入到的主資料表 [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 預期 [!DNL Stripe] 資料

之後 [您已將 [!DNL Stripe] 帳戶](../integrations/stripe.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤相關資料欄位以進行分析。

在本文中，我們將探索您可從匯入的主要資料表 [!DNL Stripe] into [!DNL MBI]. 完成設定後，會在您的資料倉庫中建立下清單格。 按一下「表名」列中的連結，以進一步了解每個表中的屬性。

| **表名** | **說明** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/api/curl#customer_object) | 客戶對象允許您執行經常性費用並跟蹤與同一客戶關聯的多個費用。 |
| [`Charges`](https://stripe.com/docs/api/curl#charge_object) | 此表包含有關信用卡和借記卡的費用的資訊，包括金額、幣種、狀態、客戶ID等。 |
| [`Coupons`](https://stripe.com/docs/api/curl#coupon_object) | 下表包含您可能想要套用至客戶的百分比或金額折扣的相關資訊。 請注意，抵用券僅適用於發票；它們不適用於一次性指控。 |
| [`Invoices`](https://stripe.com/docs/api/curl#invoice_object) | 此表包含有關發票的資訊，包括欠款額、訂閱、發票項、任何自動按比例分配調整等。 |
| [`Plans`](https://stripe.com/docs/api/curl#plan_object) | 下表包含您網站上不同產品和功能層級的定價資訊。 例如，基本功能的月計畫為$10，高級功能的月計畫為$20。 |
| [`Subscriptions`](https://stripe.com/docs/api/curl#subscription_object) | 此表包含客戶所屬訂閱計畫的詳細資訊。 屬性包括客戶ID、狀態、取消/結束日期、稅百分比、試用資訊等。 |
| [`Events`](https://stripe.com/docs/api/curl#event_object) | 事件可讓您了解剛在帳戶中發生的有趣事件。 [發生有趣的事件時](https://stripe.com/docs/api/curl#event_types)，則會建立新事件物件。 例如，電荷成功時 `charge.succeeded` 事件已建立；或者，當發票無法 `invoice.payment\_failed` 事件。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>許多API請求可能會建立多個事件。 例如，如果您為客戶建立新訂閱，您會收到 `customer.subscription.created` 事件與  `charge.succeeded` 事件。

## 相關：

* [連接 [!DNL Stripe]](../integrations/stripe.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151)
