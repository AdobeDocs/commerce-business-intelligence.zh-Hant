---
title: 預期Zendesk資料
description: 瞭解可從Zendesk匯入Commerce Intelligence的主要資料表，包括有關Zendesk資料的其他檔案的連結。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 必須有[!DNL Zendesk]個資料

在連線[您的 [!DNL Zendesk] 帳戶](../integrations/zendesk.md)之後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。

本主題探索您可以從[!DNL Zendesk]匯入至[!DNL Adobe Commerce Intelligence]的主要資料表，包括有關[!DNL Zendesk]資料的其他檔案的連結。

| 表格名稱 | 說明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | `Audits`表格會記錄與票證相關的活動，包括狀態變更以及客戶與代理程式回應。 此表格包含連結回`Tickets`表格的票證識別碼，可讓您分析每個票證的首次回應時間和解析時間。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | `audit_~\_events`資料表是`audits`資料表的子系，並記錄票證事件的其他詳細資料。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | `Organizations`表格會記錄您一般使用者的公司資訊，例如名稱、ID、關聯的網域名稱、標籤及任何自訂欄位。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | `Tickets`表格會記錄所有票證詳細資料，包括`created_at`時間戳記以及`requester\_id`和`assignee\_id`，可讓您將票證分別連結至`Users`表格中的一般使用者和代理程式。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | `ticket fields`表格包含有關您帳戶中的基本文字欄位和自訂票證欄位的資訊。 此資料表的屬性包含欄位`ID`、`URL`、`type`、`title`、`description`、`position`、`requirement setting`、代理程式和一般使用者特定資訊，以及建立和更新資訊。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | `Users`表格包含一般使用者和代理程式的所有詳細資料，包括個人姓名和電子郵件。 這可讓您分析使用者的參與度和代理程式的效能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 群組是代理程式在您的Zendesk帳戶中的組織方式。 `Groups`資料表會記錄`group ID`、`URL`、`name`等資訊，以及建立和更新資訊。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 巨集是您定義的動作，可修改票證欄位的值。 此表格包含巨集的標題、ID、動作、限制，以及建立和更新資訊等屬性。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | `Tags`表格包含您帳戶中所有標籤的清單。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表格包含票證量度的相關資料。 欄位包含`ticket ID`、`URL`，以及群組、受指派人、重新開啟、回覆、回覆時間（以分鐘為單位）、完整解決時間和上次更新（例如狀態、受指派人或請求者）等資訊。 |

{style="table-layout:auto"}

## 相關

* [正在連線Zendesk](../integrations/zendesk.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
