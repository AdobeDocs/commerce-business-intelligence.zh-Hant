---
title: 預期的Stripe資料
description: 探索可從Stripe匯入Commerce Intelligence的主要資料表。
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 必須有[!DNL Stripe]個資料

在連線[您的 [!DNL Stripe] 帳戶](../integrations/stripe.md)之後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。

本主題探索可從[!DNL Stripe]匯入至[!DNL Commerce Intelligence]的主要資料表。 安裝完成後，會在您的Data Warehouse中建立下清單格。 按一下「表格名稱」資料欄中的連結，以進一步瞭解每個表格中的屬性。

| **資料表名稱** | **描述** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 客戶物件可讓您執行重複產生費用，並追蹤與同一客戶相關的多項費用。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | 此表格包含信用卡與借記卡費用的相關資訊，包括金額、幣別、狀態、客戶ID等。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | 此表格包含您可能想要套用至客戶的折扣百分比或折扣金額的相關資訊。 優惠券只適用於發票，不適用於一次性費用。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | 此表格包含有關商業發票的資訊，包括缺款金額、訂閱、商業發票專案、任何自動攤派調整等等。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 此表格包含您網站上不同產品和功能層級的定價資訊。 例如，您可能對基本功能有$10美元/月的計畫，而高級功能有$20美元/月的計畫。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | 此表格包含您客戶所屬訂閱計畫的詳細資料。 屬性包括客戶ID、狀態、已取消/結束日期、稅捐百分比、試用資訊等。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | 事件可讓您瞭解帳戶中發生的有趣事件。 [發生有趣的事件時](https://stripe.com/docs/api/events/types)，會建立新的事件物件。 例如，當費用成功`charge.succeeded`時，已建立事件；或者，當無法支付商業發票時，已建立`invoice.payment\_failed`事件。 |

{style="table-layout:auto"}

>[!NOTE]
>
>許多API請求都可能導致建立多個事件。 例如，如果您為客戶建立訂閱，您會同時收到`customer.subscription.created`事件和`charge.succeeded`事件。

## 相關：

* [正在連線 [!DNL Stripe]](../integrations/stripe.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
