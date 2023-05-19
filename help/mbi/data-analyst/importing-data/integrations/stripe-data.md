---
title: 預期條帶資料
description: 瀏覽可從Stripe導入Commerce Intelligence的主資料表。
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 預期 [!DNL Stripe] 資料

之後 [您已連接 [!DNL Stripe] 帳戶](../integrations/stripe.md)，可以使用 [Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤相關資料欄位進行分析。

本主題探討可從中導入的主要資料表 [!DNL Stripe] 入 [!DNL Commerce Intelligence]。 安裝完成後，將在您的Data Warehouse中建立以下表。 按一下「表名」(Table Name)列中的連結，瞭解有關每個表中屬性的詳細資訊。

| **表名** | **說明** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 客戶對象允許您執行經常性費用並跟蹤與同一客戶關聯的多個費用。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | 此表包含有關信用卡和借記卡費用的資訊，包括金額、幣種、狀態、客戶ID等。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | 此表包含有關您可能要應用於客戶的百分比或金額折扣的資訊。 優惠券僅適用於發票；他們不適用一次性的指控。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | 此表包含有關發票的資訊，包括欠款額、訂閱、發票項、任何自動按比例分配調整等。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 此表包含站點上不同產品和功能級別的定價資訊。 例如，您可能有一個基本功能的10美元/月計畫和一個高級功能的20美元/月計畫。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | 此表包含客戶所屬的訂閱計畫的詳細資訊。 屬性包括客戶標識、狀態、日期取消/結束、稅百分比、試用資訊等。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | 事件讓您知道某個帳戶中發生的有趣事件。 [當發生有趣事件時](https://stripe.com/docs/api/events/types)，將建立新事件對象。 例如，當充電成功時 `charge.succeeded` 建立事件；或者，當發票無法 `invoice.payment\_failed` 建立事件。 |

{style="table-layout:auto"}

>[!NOTE]
>
>許多API請求可能導致建立多個事件。 例如，如果為客戶建立訂閱，則您將同時收到 `customer.subscription.created` 事件和  `charge.succeeded` 的子菜單。

## 相關：

* [連接 [!DNL Stripe]](../integrations/stripe.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
