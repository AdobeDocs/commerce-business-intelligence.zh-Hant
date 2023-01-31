---
title: 預期的Zendesk資料
description: 了解可從Zendesk導入MBI的主要資料表，包括有關Zendesk資料的其他文檔的連結。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# 預期的Zendesk資料

之後 [您已將 [!DNL Zendesk] 帳戶](../integrations/zendesk.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤相關資料欄位以進行分析。

在本文中，我們將探索您可從匯入的主要資料表 [!DNL Zendesk] into [!DNL MBI]，包括其他檔案的相關連結 [!DNL Zendesk] 資料。

| 表名 | 說明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | 此 `Audits` 表記錄與票證關聯的活動，包括狀態更改以及客戶和代理響應。 此表包含票證ID，可連結回 `Tickets` 表格，可讓您分析每個票證的首次回應時間和解析時間。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | 此 `audit_~\_events` 表是的子項 `audits` 表格並記錄票證事件的其他詳細資訊。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | 此 `Organizations` 表格會記錄與您的一般使用者相關的公司資訊，例如名稱、ID、相關網域名稱、標籤和任何自訂欄位。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | 此 `Tickets` 表記錄所有票證詳細資訊，包括 `created_at` 時間戳記以及 `requester\_id` 和 `assignee\_id`，這可讓您將票證連結至 `Users` 表格。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | 此 `ticket fields` 表包含有關帳戶中基本文本欄位和自定義票證欄位的資訊。 此表的屬性包括欄位 `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`、代理和最終用戶特定資訊，以及建立和更新資訊。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | 此 `Users` 表格包括有關最終用戶和代理的所有詳細資訊，包括個人姓名和電子郵件。 這可讓您分析使用者的參與程度以及代理的效能。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | 組是在您的Zendesk帳戶中組織座席的方式。 此 `Groups` 表格記錄資訊，例如 `group ID`, `URL`, `name`，以及建立和更新資訊。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | 宏是由您定義的操作，用於修改票證欄位的值。 此表包含諸如宏的標題、ID、操作、限制以及建立和更新資訊等屬性。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | 此 `Tags` 表格包含帳戶中所有標籤的清單。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | 此表包含有關票證度量的資料。 欄位包括 `ticket ID`, `URL`，以及群組、受分配者、重新開啟、回覆、回覆時間（以分鐘為單位）、完全解析時間和上次更新（例如狀態、受託人或請求者）資訊的數量。 |

{style=&quot;table-layout:auto&quot;}

## 相關

* [連接Zendesk](../integrations/zendesk.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
