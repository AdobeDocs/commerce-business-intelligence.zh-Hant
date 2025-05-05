---
title: 預期的Facebook Ads資料
description: 瞭解建議同步至Data Warehouse的表格之簡短概觀
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 必須有[!DNL Facebook Ads]個資料

連線[您的 [!DNL Facebook Ads] 帳戶](../integrations/facebook-ads.md)後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關資料欄位以進行分析。

本主題提供表格Adobe的簡短概觀，建議您同步至您的Data Warehouse。 這只會反白顯示核心表格，因為有相當多的子表格。

## 核心廣告行銷活動表格

這些表格包含核心廣告行銷活動元件的相關資料。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

此表格是[!DNL Facebook Ads]帳戶中行銷活動的核心表格。 欄包括`campaign id`、`name`、`status (active/paused)`、`objective`。

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此資料表記錄是[!DNL Facebook Ads]帳戶中[!DNL Facebook Ads]個集合的核心資料表。 欄包括廣告集所屬的廣告`Campaign id/name`、預算、競標型別、排程和對象目標定位資訊。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

此表格會記錄[!DNL Facebook Ads]帳戶中的所有廣告。 欄包括廣告資訊，包括其所屬的廣告集和廣告行銷活動、廣告競標、廣告目標定位，以及廣告使用的特定創意（影像/文字）參考。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

此表格記錄在[!DNL Facebook Ads]中使用的創意。 創意內容包括創意名稱、說明，以及適用的相關影像URL。

## 區段行銷活動表格

下表包含每個每日行銷活動/集合/廣告組合的專案，並按維度（例如年齡、性別和國家/地區）分段。

### `facebook _ads insights_ (account-id)`

此表包括每天每個促銷活動/集合/廣告組合的專案，以及包括曝光數、點按數、成本、cpc、cpm、cpp、ctr、觸及率、社交觸及率和支出在內的統計資料。

### `facebook _ads insights_ (account-id)_~\_actions`

這是`facebook_ads_insights_{account_id}`資料表的子資料表。 其中包括根據不同行銷活動所發生動作的轉換資料。

### `facebook _ads insights country_ (account-id)`

此表格包含與`facebook_ads_insights_{account_id}`表格相同的資訊，並依國家加以區段。

### `facebook ads insights age and gender (account-id)`

此表格包含與`facebook_ads_insights_{account_id}`表格相同的資訊，並依年齡和性別進行分段。

## 相關

* [正在連線 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
