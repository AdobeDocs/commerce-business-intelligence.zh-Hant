---
title: Mixpanel中的資料驗證
description: 瞭解如何確認您已同步可直接在Mixpanel中使用的所有相同資料。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D6qvHVgPX0WEbKZSYel4siWMLTu9BloFBQMTxXxnbY0
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
source-wordcount: 134
ht-degree: 0%

---

# [!DNL Mixpanel]中的資料驗證

當[!DNL Adobe Commerce Intelligence]首次連線到您的[!DNL Mixpanel]資料時，您的帳戶管理員或分析人員可能會要求您從[!DNL Mixpanel]提供資料匯出以進行驗證。 這可讓您確認您已同步所有可在[!DNL Mixpanel]中直接供您使用的相同資料。

## 資料匯出程式： `Events`

1. 造訪您的`Segmentation`區段並檢視`Your Top Events`。

   ![顯示您熱門事件的Mixpanel儀表板](../../../assets/your-top-events.png)

1. 為時間範圍選取`Past 96 Hours`

   ![Mixpanel時間範圍選擇器顯示過去96小時的選項](../../../assets/past-96-hours.png)

1. 捲動至報告的右下方，並匯出`.csv`檔案：

   ![功能表中的Mixpanel匯出至CSV選項](../../../assets/export-csv-mixpanel.png)

1. 將`.csv`檔案傳送給您正在處理此驗證程式的客戶經理或分析人員。

