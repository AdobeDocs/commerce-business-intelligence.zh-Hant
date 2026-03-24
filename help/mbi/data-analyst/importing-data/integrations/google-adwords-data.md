---
title: 預期Google Adwords資料
description: 瞭解如何使用Data Warehouse Manager輕鬆追蹤相關資料欄位以進行分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iCKOCRAELybmKfHS8F7XaKpEx9blpkRK0i0e-eEYJgU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# 必須有[!DNL Google Adwords]個資料

在連線[您的 [!DNL Google Adwords] 帳戶](../integrations/google-adwords.md)後，您可以使用[Data Warehouse管理員](../../data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。

您在該處注意到兩個可用於復寫至Data Warehouse的表格：

* `campaigns[account-id]`
* `adwords[account-id]`

`campaigns`資料表&#x200B;*預設應該使用*，所以您可以先同步該資料表的所有相關欄位。

`adwords`資料表包含四個不在`campaigns`資料表中的資料行：

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

每當您想要執行考量這些屬性的分析時，都必須使用`adwords`表格。

>[!IMPORTANT]
>
>此表格不包括全部四欄為`null`的資料列。

以下是兩個表格的預期結構描述。

## [!DNL Campaigns]資料表

`campaigns`資料表包含下列資料行：

| **資料行** | **描述** |
|-----|-----|
| `\_id` | 表格的主索引鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | 當天行銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords]行銷活動識別碼 |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | 行銷活動名稱（例如，[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | 行銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | 當天的曝光次數 |
| `profileId` | 設定檔ID |
| `profileName` | 設定檔名稱 |
| `\_updated\_at` | 此列最後一次更新的日期和時間 |

{style="table-layout:auto"}

## [!DNL AdWords]資料表

`adwords`資料表包含下列資料行：

| **資料行** | **描述** |
|-----|-----|
| `\_id` | 表格的主索引鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | 當天行銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords]行銷活動識別碼 |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | 行銷活動名稱（例如，[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | 行銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | 當天的曝光次數 |
| `profileId` | 設定檔ID |
| `profileName` | 設定檔名稱 |
| `\_updated\_at` | 此列最後一次更新的日期和時間 |
| `keyword` | 行銷活動的關鍵字 |
| `adContent` | 線上行銷活動文字的第一行 |
| `adDestinationUrl` | [!DNL Adwords]廣告參考流量的URL |
| `adGroup` | [!DNL Adwords]廣告群組的名稱 |

{style="table-layout:auto"}

您可以使用此資料，根據花費資料開始建立[量度](../../../data-user/reports/ess-manage-data-metrics.md)和[報告](../../../tutorials/using-visual-report-builder.md)，並[將其與您的終身收入結合，以計算ROI](../../analysis/roi-ad-camp.md)。

## 整合的表格

[!DNL Adobe]建議建立`consolidated ad spend`資料表，將所有來自您多個廣告來源的資料合併到單一資料表中。 這可讓您使用一組單一量度進行廣告分析。

如果您沒有整合表格，但您在`adwords`表格上建置了精美的儀表板，則需要復寫報告或建立重複的量度，以便將該資料與您的[!DNL Facebook Ads]資料進行比較。 使用合併表格可讓您順暢地將[!DNL Facebook Ads]資料與現有的[!DNL Adwords]報告合併。 您也可以依廣告平台分段。

如果您已同步上述欄位，[請連絡我們](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)以整合您的廣告支出。
