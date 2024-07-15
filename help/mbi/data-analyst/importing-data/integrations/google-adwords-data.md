---
title: 預期Google Adwords資料
description: 瞭解如何使用Data Warehouse管理員輕鬆追蹤相關資料欄位以進行分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# 必須有[!DNL Google Adwords]個資料

在連線[您的 [!DNL Google Adwords] 帳戶](../integrations/google-adwords.md)之後，您可以使用[Data Warehouse管理員](../../data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。

您在該處注意到有兩個表格可用於復寫至Data Warehouse：

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
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天行銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords]行銷活動識別碼 |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 行銷活動名稱（例如，[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 行銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天的曝光次數 |
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
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天行銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords]行銷活動識別碼 |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 行銷活動名稱（例如，[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 行銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天的曝光次數 |
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

如果您已同步上述欄位，[請連絡我們](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)以整合您的廣告支出。
