---
title: 預期的Zendesk資料
description: 瞭解可以從Zendesk導入Commerce Intelligence的主要資料表，包括指向有關Zendesk資料的其他文檔的連結。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 預期 [!DNL Zendesk] 資料

之後 [您已連接 [!DNL Zendesk] 帳戶](../integrations/zendesk.md)，可以使用 [Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤相關資料欄位進行分析。

本主題探討可從中導入的主要資料表 [!DNL Zendesk] 入 [!DNL Adobe Commerce Intelligence]，包括其他文檔的連結關於 [!DNL Zendesk] 資料。

| 表名 | 說明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | 的 `Audits` 表記錄與票證關聯的活動，包括狀態更改以及客戶和座席響應。 此表包含一個票證ID，該票證ID可連結回 `Tickets` 表，用於分析每個票證的第一次響應時間和解決時間。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | 的 `audit_~\_events` 表是 `audits` 表和記錄票證事件的其他詳細資訊。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | 的 `Organizations` 表記錄有關最終用戶的公司資訊，如名稱、ID、關聯域名、標籤和任何自定義欄位。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | 的 `Tickets` 表記錄所有票證詳細資訊，包括 `created_at` 時間戳和 `requester\_id` 和 `assignee\_id`，允許您將票證連結到中的最終用戶和代理 `Users` 的下界。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | 的 `ticket fields` 表包含有關帳戶中基本文本欄位和自定義票證欄位的資訊。 此表的屬性包括欄位 `ID`。 `URL`。 `type`。 `title`。 `description`。 `position`。 `requirement setting`、代理和最終用戶特定資訊，以及建立和更新資訊。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | 的 `Users` 該表包含有關最終用戶和代理的所有詳細資訊，包括個人姓名和電子郵件。 這允許您分析最終用戶的參與和代理的效能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 組是Zendesk帳戶中座席的組織方式。 的 `Groups` 表記錄資訊，如 `group ID`。 `URL`。 `name`、建立和更新資訊。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 宏是您定義的修改票證欄位值的操作。 此表包含屬性，如宏的標題、ID、操作、限制以及建立和更新資訊。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | 的 `Tags` 表包含帳戶中所有標籤的清單。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表包含有關票證度量的資料。 欄位包括 `ticket ID`。 `URL`、以及組、受分配者、重新開啟、回復、回復時間（以分鐘為單位）、完全解決時間和上次更新（例如，狀態、受分配者或請求者）資訊的數量。 |

{style="table-layout:auto"}

## 相關

* [連接Zendesk](../integrations/zendesk.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
