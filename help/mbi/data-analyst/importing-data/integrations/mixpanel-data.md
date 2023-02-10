---
title: 預期的Mixpanel資料
description: 探索可從Mixpanel匯入至您 [!DNL MBI] 帳戶。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 預期 [!DNL Mixpanel] 資料

之後 [您已將 [!DNL Mixpanel] 帳戶](../integrations/mixpanel.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤相關資料欄位以進行分析。

在本文中，我們將探索您可從匯入的主要資料表 [!DNL Mixpanel] 進入 [!DNL MBI] 帳戶。 連接Mixpanel後，會在您的資料倉庫中建立下表。 若要檢視所有可用於追蹤的欄位，請按一下表格名稱欄中的連結。

>[!NOTE]
>
>由於 [!DNL Mixpanel] API，歷史資料 — 從連線至之日起七(7)天以前的資料 [!DNL MBI]  — 不會複製。

| **表名** | **說明** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | 此表格包含原始事件資料，包括事件、事件日期和平台貯體。 |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | 此表格包含漏斗的相關資料，包括漏斗ID、漏斗長度（使用者必須完成漏斗的天數），以及漏斗的開始和結束日期。 |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | 這包含People Analytics的資料，包括工作階段ID、頁面和使用者資訊，以及上次看到使用者的日期/時間。 |

{style=&quot;table-layout:auto&quot;}

## 相關檔案

* [連接 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
