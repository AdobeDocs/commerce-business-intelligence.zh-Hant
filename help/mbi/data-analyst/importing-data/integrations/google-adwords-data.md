---
title: 預期的GoogleAdwords資料
description: 瞭解如何使用Data Warehouse管理器輕鬆跟蹤相關資料欄位以進行分析。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# 預期 [!DNL Google Adwords] 資料

之後 [您已連接 [!DNL Google Adwords] 帳戶](../integrations/google-adwords.md)，可以使用 [Data Warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤相關資料欄位進行分析。

在這裡，您會注意到兩個表可用於複製到您的Data Warehouse中：

* `campaigns[account-id]`
* `adwords[account-id]`

的 `campaigns` 表 *應預設使用*，因此您可以首先同步該表中的所有相關欄位。

的 `adwords` 表包含四列，這些列不在 `campaigns` 表：

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

每當您想要執行考慮這些屬性的分析時，必須使用 `adwords` 的子菜單。

>[!IMPORTANT]
>
>此表不包括所有四列都位於 `null`。

下面是兩個表的預期架構。

## [!DNL Campaigns] 表

的 `campaigns` 表包含以下列：

| **列** | **說明** |
|-----|-----|
| `\_id` | 表的主鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 一天的點擊總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天市場活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 市場活動ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 市場活動名稱(例如， [utm\_市場活動](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 市場活動運行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天印數 |
| `profileId` | 配置檔案ID |
| `profileName` | 配置檔案名稱 |
| `\_updated\_at` | 此行上次更新的日期和時間 |

{style="table-layout:auto"}

## [!DNL AdWords] 表

的 `adwords` 表包含以下列：

| **列** | **說明** |
|-----|-----|
| `\_id` | 表的主鍵 |
| `accountId` | 帳戶ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | 一天的點擊總數 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | 當天市場活動的總成本 |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] 市場活動ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | 市場活動名稱(例如， [utm\_市場活動](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | 市場活動運行的日期 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | 當天印數 |
| `profileId` | 配置檔案ID |
| `profileName` | 配置檔案名稱 |
| `\_updated\_at` | 此行上次更新的日期和時間 |
| `keyword` | 市場活動的關鍵字 |
| `adContent` | 聯機市場活動的文本第一行 |
| `adDestinationUrl` | 指向的URL [!DNL Adwords] 廣告引用的流量 |
| `adGroup` | 名稱 [!DNL Adwords] ad group（廣告組） |

{style="table-layout:auto"}

使用此資料，可以開始建立 [度量](../../../data-user/reports/ess-manage-data-metrics.md) 和 [報告](../../../tutorials/using-visual-report-builder.md) 基於支出資料和 [將它與您的終生收入掛鈎，以計算ROI](../../analysis/roi-ad-camp.md)。

## 統一表

[!DNL Adobe] 建議建立 `consolidated ad spend` 表，將來自所有多個廣告源的資料合併到單個表中。 這使您能夠使用一組度量來進行廣告分析。

如果沒有統一表，並且在 `adwords` 表中，您需要複製報告或建立重複的度量以將資料與 [!DNL Facebook Ads] 資料。 使用統一表可無縫合併 [!DNL Facebook Ads] 資料 [!DNL Adwords] 報告。 您也可以按廣告平台分段。

如果您已同步上述欄位， [聯繫我們](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 整合廣告支出。
