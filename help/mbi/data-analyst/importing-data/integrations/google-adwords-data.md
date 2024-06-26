---
title: 預期Google Adwords資料
description: 瞭解如何使用Data Warehouse管理員輕鬆追蹤相關資料欄位以進行分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# 預期 [!DNL Google Adwords] 資料

晚於 [您已連線 [!DNL Google Adwords] 帳戶](../integrations/google-adwords.md)，您可以使用 [Data Warehouse管理員](../../data-warehouse-mgr/tour-dwm.md) 以輕鬆追蹤相關資料欄位以供分析。

您在該處注意到有兩個表格可用於復寫至Data Warehouse：

* `campaigns[account-id]`
* `adwords[account-id]`

此 `campaigns` 表格 *預設應該使用*，以便您能從該表格的所有相關欄位開始同步。

此 `adwords` 表格中有四欄不在 `campaigns` 表格：

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

當您想要執行考慮這些屬性的分析時，必須使用 `adwords` 表格。

>[!IMPORTANT]
>
>此表格會排除所有這四欄的資料列 `null`.

以下是兩個表格的預期結構描述。

## [!DNL Campaigns] 表格

此 `campaigns` 表格包含下列資料欄：

| **欄** | **說明** |
|-----|-----|
| `\_id` | 表格的主索引鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天行銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 行銷活動ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促銷活動名稱(例如 [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 行銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天的曝光次數 |
| `profileId` | 設定檔ID |
| `profileName` | 設定檔名稱 |
| `\_updated\_at` | 此列最後一次更新的日期和時間 |

{style="table-layout:auto"}

## [!DNL AdWords] 表格

此 `adwords` 表格包含下列資料欄：

| **欄** | **說明** |
|-----|-----|
| `\_id` | 表格的主索引鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 當天的點按總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天行銷活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 行銷活動ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 促銷活動名稱(例如 [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 行銷活動執行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天的曝光次數 |
| `profileId` | 設定檔ID |
| `profileName` | 設定檔名稱 |
| `\_updated\_at` | 此列最後一次更新的日期和時間 |
| `keyword` | 行銷活動的關鍵字 |
| `adContent` | 線上行銷活動文字的第一行 |
| `adDestinationUrl` | URL的 [!DNL Adwords] 廣告引用的流量 |
| `adGroup` | 的名稱 [!DNL Adwords] 廣告群組 |

{style="table-layout:auto"}

使用此資料，您可以開始建立 [量度](../../../data-user/reports/ess-manage-data-metrics.md) 和 [報表](../../../tutorials/using-visual-report-builder.md) 根據支出資料和 [將其與您的終身收入結合以計算ROI](../../analysis/roi-ad-camp.md).

## 整合的表格

[!DNL Adobe] 建議建立 `consolidated ad spend` 表格，用於將來自您所有多個廣告來源的資料合併到單一表格中。 這可讓您使用一組單一量度進行廣告分析。

如果您沒有統一表格，而您在上建置美麗儀表板 `adwords` 表格，您需要複製報告或建立重複的量度，將該資料與您的比較 [!DNL Facebook Ads] 資料。 使用整合表格可讓您順暢地整合 [!DNL Facebook Ads] 使用您現有的資料 [!DNL Adwords] 報表。 您也可以依廣告平台分段。

如果您已同步上述欄位， [聯絡我們](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 以整合您的廣告支出。
