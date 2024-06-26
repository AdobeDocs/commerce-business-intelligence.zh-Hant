---
title: 預期的Facebook Ads資料
description: 瞭解建議同步至Data Warehouse的表格之簡短概觀
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 預期 [!DNL Facebook Ads] 資料

在您擁有 [已連線您的 [!DNL Facebook Ads] 帳戶](../integrations/facebook-ads.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以輕鬆追蹤相關資料欄位以供分析。

本主題提供表格Adobe的簡短概觀，建議您同步至您的Data Warehouse。 這只會反白顯示核心表格，因為有相當多的子表格。

## 核心廣告行銷活動表格

這些表格包含核心廣告行銷活動元件的相關資料。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

此表格為中行銷活動的核心表格 [!DNL Facebook Ads] 帳戶。 欄包括 `campaign id`， `name`， `status (active/paused)`， `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此表格記錄為下列專案的核心表格： [!DNL Facebook Ads] 在中設定 [!DNL Facebook Ads] 帳戶。 欄包括廣告 `Campaign id/name` 「廣告集」屬於、預算、競標型別、排程和對象鎖定目標資訊。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

此表格會將所有廣告記錄在 [!DNL Facebook Ads] 帳戶。 欄包括廣告資訊，包括其所屬的廣告集和廣告行銷活動、廣告競標、廣告目標定位，以及廣告使用的特定創意（影像/文字）參考。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

此表格記錄以下專案所使用的創意： [!DNL Facebook Ads]. 創意內容包括創意名稱、說明，以及適用的相關影像URL。

## 區段行銷活動表格

下表包含每個每日行銷活動/集合/廣告組合的專案，並按維度（例如年齡、性別和國家/地區）分段。

### `facebook _ads insights_ (account-id)`

此表包括每天每個促銷活動/集合/廣告組合的專案，以及包括曝光數、點按數、成本、cpc、cpm、cpp、ctr、觸及率、社交觸及率和支出在內的統計資料。

### `facebook _ads insights_ (account-id)_~\_actions`

這是 `facebook_ads_insights_{account_id}` 表格。 其中包括根據不同行銷活動所發生動作的轉換資料。

### `facebook _ads insights country_ (account-id)`

此表格包含與下列專案相同的資訊： `facebook_ads_insights_{account_id}` 表格並按國家/地區細分。

### `facebook ads insights age and gender (account-id)`

此表格包含與下列專案相同的資訊： `facebook_ads_insights_{account_id}` 表格並按年齡和性別細分。

## 相關

* [正在連線 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
