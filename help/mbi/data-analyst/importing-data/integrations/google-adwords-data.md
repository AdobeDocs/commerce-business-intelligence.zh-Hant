---
title: 預期的Google Adwords資料
description: 了解如何使用「Data Warehouse管理員」輕鬆追蹤相關資料欄位以進行分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 預期的Google Adwords資料

之後 [您已將 [!DNL Google Adwords] 帳戶](../integrations/google-adwords.md)，您可以使用 [Data Warehouse管理員](../../data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤相關資料欄位以進行分析。

在那裡，您會發現兩個表格可供複製至您的Data Warehouse: `campaigns[account-id]` 和 `adwords[account-id]`.

此 `campaigns` 表格 *預設會使用*，因此您可以開始同步該表格中的所有相關欄位。

此 `adwords` 表格包含四欄，而這些欄不在 `campaigns` 表格：

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

每當您想要執行考量這些屬性的分析時，必須使用 `adwords` 表格。

>[!IMPORTANT]
>
>此表格會排除這四列皆為 `null`.

以下是兩個表的預期架構：

## `Campaigns` 表格

此 `campaigns` 表格包含下列各欄：

| **欄** | **說明** |
|-----|-----|
| `\_id` | 表的主鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天促銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 促銷活動ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促銷活動名稱(例如 [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 促銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天曝光次數 |
| `profileId` | 設定檔ID |
| `profileName` | 設定檔名稱 |
| `\_updated\_at` | 此行上次更新的日期和時間 |

{style="table-layout:auto"}

## AdWords表格

此 `adwords` 表格包含下列各欄：

| **欄** | **說明** |
|-----|-----|
| `\_id` | 表的主鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天促銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 促銷活動ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促銷活動名稱(例如 [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 促銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天曝光次數 |
| `profileId` | 設定檔ID |
| `profileName` | 設定檔名稱 |
| `\_updated\_at` | 此行上次更新的日期和時間 |
| `keyword` | 促銷活動的關鍵字 |
| `adContent` | 線上促銷活動的文字第一行 |
| `adDestinationUrl` | URL [!DNL Adwords] 廣告參考流量 |
| `adGroup` | 的名稱 [!DNL Adwords] 廣告群組 |

{style="table-layout:auto"}

使用此資料，您可以開始建立 [量度 ](../../../data-user/reports/ess-manage-data-metrics.md) 和 [報告](../../../tutorials/using-visual-report-builder.md) 根據支出資料和 [將它與您的終身收入結合，以計算ROI](../../analysis/roi-ad-camp.md).

## 統一表

Adobe建議建立 `consolidated ad spend` 表格，將來自所有多個廣告來源的資料合併成單一表格。 這可讓您使用單一量度集進行廣告分析。

若沒有統一表格，如果您在 `adwords` 表格，您需要複製報表或建立重複量度，以便將該資料與您的 [!DNL Facebook Ads] 資料。 使用統一表可以無縫整合 [!DNL Facebook Ads] 資料 [!DNL Adwords] 報表。 您也可以依廣告平台來區隔。

如果您已同步上述欄位，請聯絡我們以合併您的廣告支出。
