---
title: 預期Facebook廣告資料
description: 瞭解建議同步至Data Warehouse的表格概述
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA
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
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: c8d7097b4f841a4fe8c5777f207ea0ea53202a0f
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 0%

---

# 必須有[!DNL Facebook Ads]個資料

連線[您的 [!DNL Facebook Ads] 帳戶](../integrations/facebook-ads.md)後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關資料欄位以進行分析。

本主題為您提供Adobe建議您同步至Data Warehouse的表格之簡短概觀。 這只會反白顯示核心表格，因為有相當多的子表格。

## 核心廣告行銷活動表格

這些表格包含核心廣告行銷活動元件的相關資料。

### `facebook _campaigns_ (account-id)`

[`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

此表格是[!DNL Facebook Ads]帳戶中行銷活動的核心表格。 欄包括`campaign id`、`name`、`status (active/paused)`、`objective`。

### `facebook _adsets_ (account-id)`

[`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

此資料表記錄是[!DNL Facebook Ads]帳戶中[!DNL Facebook Ads]個集合的核心資料表。 欄包括廣告集所屬的廣告`Campaign id/name`、預算、競標型別、排程和對象目標定位資訊。

### `facebook _ads_ (account-id)`

[`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

此表格會記錄[!DNL Facebook Ads]帳戶中的所有廣告。 欄包括廣告資訊，包括其所屬的廣告集和廣告行銷活動、廣告競標、廣告目標定位，以及廣告使用的特定創意（影像/文字）參考。

### `facebook _adcreative_ (account-id)`

[`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

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
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
