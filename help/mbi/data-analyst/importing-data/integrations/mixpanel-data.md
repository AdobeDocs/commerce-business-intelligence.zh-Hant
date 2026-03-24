---
title: 預期Mixpanel資料
description: 探索可從Mixpanel匯入至 [!DNL Commerce Intelligence] 帳戶的主要資料表。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
ht-degree: 0%

---

# 必須有[!DNL Mixpanel]個資料

在連線[您的 [!DNL Mixpanel] 帳戶](../integrations/mixpanel.md)後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。

本主題探索可從[!DNL Mixpanel]匯入至[!DNL Commerce Intelligence]帳戶的主要資料表。 在連線[!DNL Mixpanel]之後，將會在您的Data Warehouse中建立下列資料表。 若要檢視所有可用於追蹤的欄位，請按一下表格名稱欄中的連結。

>[!NOTE]
>
>由於[!DNL Mixpanel] API的限制，不會復寫歷史資料(從連線到[!DNL Commerce Intelligence]的日期起七(7)天以前的資料)。

| **資料表名稱** | **描述** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | 此表格包含原始事件資料，包括事件、事件日期和平台貯體。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | 此表格包含有關漏斗的資料，包括funnel ID、funnel長度（使用者必須完成funnel的天數），以及funnel的開始和結束日期。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | 這包含來自People Analytics的資料，包括工作階段ID、頁面和使用者資訊，以及上次檢視使用者的日期/時間。 |

{style="table-layout:auto"}

## 相關檔案

* [正在連線 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
