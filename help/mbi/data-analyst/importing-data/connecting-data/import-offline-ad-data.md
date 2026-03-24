---
title: 匯入其他廣告支出資料
description: 瞭解如何將離線或其他廣告支出資料匯入 [!DNL Commerce Intelligence]。
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/jx-MMry1-XGeM4htPkH6GC1Et5nYjyD7aWn3p-nmcC8
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 0%

---

# 匯入其他廣告支出資料

Uploading your advertising spend data allows you to measure campaign ROI by marrying your advertising cost and the `customer lifetime value (CLV)` of users acquired from your campaigns.

## Uploading advertising cost data

分析廣告支出資料的第一步是取得資料。 由於大部分的廣告平台都可讓您匯出報表，因此Adobe建議您從廣告平台匯出原始資料，並直接上傳至[!DNL Commerce Intelligence]，而不需進行任何操作。 您可以對Data Warehouse中的資料執行操作，因此不需要加倍努力。

匯出廣告支出資料後，請使用[`File Upload`功能](../connecting-data/using-file-uploader.md)將資料匯入Data Warehouse。 您可以隨時間將新資料上傳到相同的[!DNL Commerce Intelligence]資料表。

## 離線來源

除了您的線上行銷活動，您也可能有離線廣告，例如在廣播或廣告牌上。 若要說明這些情況，您可以手動將包含成本資料的試算表上傳至[!DNL Commerce Intelligence]。

建立`.csv`檔案以記錄廣告支出資料時，建議使用下面探索的表格結構。 範本檔案也會附加在本主題底部，以作為範例。 建議的欄包括：

* `ID` - This is a unique identifier for each data row which is used by the database as primary key. 每一列的名稱必須不同。
* `Date` - This is the date that the campaign ran, in yyyy-mm-dd format.
* `Amount` — 這是您花在行銷活動上的金額。
* `campaign` — 這是行銷活動名稱。 如果您使用[!DNL Google Analytics]追蹤您的其他廣告支出資料，它應該符合utm\_campaign名稱。
* `source` — 這是來源名稱。 如果您使用[!DNL Google Analytics]，這應該符合`utm_source`名稱。
* `other` （選用） — 您也可以合併其他欄，協助您劃分行銷活動和成本。 它也可以將數個不同的UTM行銷活動名稱摘要為單一、一致的行銷活動，以用於追蹤目的。 建議您不要手動進行此設定，而應該使用V型查詢來比對第二個工作表，讓每個促銷活動名稱與其他名稱相符並在這裡動態回報。

## 相關

* [連線 [!DNL AdWords] 資料](../integrations/google-adwords.md)
* [提高廣告行銷活動的ROI](../../analysis/roi-ad-camp.md)
