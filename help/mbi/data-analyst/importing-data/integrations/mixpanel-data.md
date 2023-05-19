---
title: 預期的Mixpanel資料
description: 瀏覽可從Mixpanel導入到的主資料表 [!DNL Commerce Intelligence] 帳戶。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 預期 [!DNL Mixpanel] 資料

之後 [您已連接 [!DNL Mixpanel] 帳戶](../integrations/mixpanel.md)，可以使用 [Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤相關資料欄位進行分析。

本主題探討可從中導入的主要資料表 [!DNL Mixpanel] 你 [!DNL Commerce Intelligence] 帳戶。 連接後將在Data Warehouse中建立以下表 [!DNL Mixpanel]。 要查看所有可用於跟蹤的欄位，請按一下表名列中的連結。

>[!NOTE]
>
>由於 [!DNL Mixpanel] API，歷史資料 — 自連接日期起七(7)天以前的資料 [!DNL Commerce Intelligence]  — 未複製。

| **表名** | **說明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 此表包含原始事件資料，包括事件、事件日期和平台儲存桶。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 此表包含有關漏斗的資料，包括漏斗ID、漏斗長度（用戶必須完成漏斗的天數#）以及漏斗的開始和結束日期。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 這包含來自People Analytics的資料，包括會話ID、頁面和用戶資訊，以及上次查看用戶的日期/時間。 |

{style="table-layout:auto"}

## 相關文檔

* [連接 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
