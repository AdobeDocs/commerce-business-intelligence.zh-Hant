---
title: 預期的Facebook Ads資料
description: 了解建議您同步至Data Warehouse的表格概觀
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 預期 [!DNL Facebook Ads] 資料

![](../../../assets/Facebook_Logo.png)

在您 [已連接 [!DNL Facebook Ads] 帳戶](../integrations/facebook-ads.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤相關資料欄位以進行分析。

本文提供表格Adobe的簡要概述，建議您同步至Data Warehouse。 這不是完整清單，因為有很多子表。 它只會反白標示核心表格。

## 核心廣告行銷活動表格

這些表格包含核心廣告促銷活動元件的相關資料。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

此表格是 [!DNL Facebook Ads] 帳戶。 欄包括 `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此表記錄是 [!DNL Facebook Ads] 在 [!DNL Facebook Ads] 帳戶。 欄包含廣告 `Campaign id/name` 廣告集屬於、預算、競標類型、排程和對象鎖定目標資訊。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

此表記錄 [!DNL Facebook Ads] 帳戶。 欄包含廣告資訊，包括其所屬的廣告集和廣告促銷活動、廣告競標、廣告鎖定目標，以及廣告使用的特定創作（影像/文字）參考。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

此表記錄了 [!DNL Facebook Ads]. 創意內容包括創意名稱、說明和相關影像URL（如適用）。

## 分段的促銷活動表格

下表包含每日每個促銷活動/集/廣告組合的項目，並依年齡、性別和國家等維度分段。

### `facebook _ads insights_ (account-id)`

此表格包含每日每個促銷活動/集/廣告組合的項目，以及統計資料，包括曝光數、點按、成本、cpc、cpp、ctr、觸及、社交觸及和支出。

### `facebook _ads insights_ (account-id)_~\_actions`

這是 `facebook_ads_insights_{account_id}` 表格。 其中包含根據不同促銷活動而發生之動作的轉換資料。

### `facebook _ads insights country_ (account-id)`

此表包含與 `facebook_ads_insights_{account_id}` 表格並依國家/地區分段。

### `facebook ads insights age and gender (account-id)`

此表包含與 `facebook_ads_insights_{account_id}` 表格並依年齡和性別加以區分。

## 相關

* [連接 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
