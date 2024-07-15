---
title: 預期Mixpanel資料
description: 探索可從Mixpanel匯入至 [!DNL Commerce Intelligence] 帳戶的主要資料表。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 必須有[!DNL Mixpanel]個資料

在連線[您的 [!DNL Mixpanel] 帳戶](../integrations/mixpanel.md)之後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。

本主題探索可從[!DNL Mixpanel]匯入至[!DNL Commerce Intelligence]帳戶的主要資料表。 連線[!DNL Mixpanel]後，將在您的Data Warehouse中建立下列資料表。 若要檢視所有可用於追蹤的欄位，請按一下表格名稱欄中的連結。

>[!NOTE]
>
>由於[!DNL Mixpanel] API的限制，不會復寫歷史資料(從連線到[!DNL Commerce Intelligence]的日期起七(7)天以前的資料)。

| **資料表名稱** | **描述** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 此表格包含原始事件資料，包括事件、事件日期和平台貯體。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 此表格包含有關漏斗的資料，包括漏斗ID、漏斗長度（使用者必須完成漏斗的天數）以及漏斗的開始和結束日期。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 這包含來自People Analytics的資料，包括工作階段ID、頁面和使用者資訊，以及上次檢視使用者的日期/時間。 |

{style="table-layout:auto"}

## 相關檔案

* [正在連線 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
