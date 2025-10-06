---
title: Mixpanel中的資料驗證
description: 瞭解如何確認您已同步可直接在Mixpanel中使用的所有相同資料。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '134'
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
