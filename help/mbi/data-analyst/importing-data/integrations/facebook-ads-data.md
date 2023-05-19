---
title: 預期Facebook廣告資料
description: 瞭解建議您同步到Data Warehouse的表的簡要概述
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 預期 [!DNL Facebook Ads] 資料

等你 [已連接 [!DNL Facebook Ads] 帳戶](../integrations/facebook-ads.md)，可以使用 [Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤相關資料欄位進行分析。

本主題將簡要概述表Adobe建議您同步到Data Warehouse。 這僅突出了核心表，因為有許多子表。

## 核心廣告活動表

這些表包含有關核心廣告活動元件的資料。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

此表是 [!DNL Facebook Ads] 帳戶。 列包括 `campaign id`。 `name`。 `status (active/paused)`。 `objective`。

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此表記錄是 [!DNL Facebook Ads] 在 [!DNL Facebook Ads] 帳戶。 列包括廣告 `Campaign id/name` 廣告集屬於的、預算、投標類型、計畫和受眾目標資訊。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

此表記錄了 [!DNL Facebook Ads] 帳戶。 欄包括廣告資訊，包括廣告集和廣告活動所屬的廣告、廣告投標、廣告目標，以及對廣告使用的特定創意（影像/文本）的引用。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

此表記錄了在 [!DNL Facebook Ads]。 創意包括創意名稱、描述和相關影像url（如適用）。

## 分段的市場活動表

下表包含每天的每個市場活動/集/廣告組合的條目，按年齡、性別和國家/地區等維度分段。

### `facebook _ads insights_ (account-id)`

此表包括每天每個活動/集/廣告組合的條目，以及包括印象、點擊量、成本、cpc、cpm、cpp、ctr、reach、社交聯繫和支出在內的統計資訊。

### `facebook _ads insights_ (account-id)_~\_actions`

這是 `facebook_ads_insights_{account_id}` 的子菜單。 它包括根據不同市場活動發生的活動的轉換資料。

### `facebook _ads insights country_ (account-id)`

此表包含與 `facebook_ads_insights_{account_id}` 按國家/地區分類。

### `facebook ads insights age and gender (account-id)`

此表包含與 `facebook_ads_insights_{account_id}` 按年齡和性別分類。

## 相關

* [連接 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
