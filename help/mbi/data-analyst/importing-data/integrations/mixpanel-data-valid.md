---
title: Mixpanel中的資料驗證
description: 瞭解如何確認您已同步可直接在Mixpanel中使用的所有相同資料。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!DNL Mixpanel]中的資料驗證

當[!DNL Adobe Commerce Intelligence]首次連線到您的[!DNL Mixpanel]資料時，您的帳戶管理員或分析人員可能會要求您從[!DNL Mixpanel]提供資料匯出以進行驗證。 這可讓您確認您已同步所有可在[!DNL Mixpanel]中直接供您使用的相同資料。

## 資料匯出程式： `Events`

1. 造訪您的`Segmentation`區段並檢視`Your Top Events`。

   ![](../../../assets/your-top-events.png)

1. 為時間範圍選取`Past 96 Hours`

   ![](../../../assets/past-96-hours.png)

1. 捲動至報告的右下方，並匯出`.csv`檔案：

   ![](../../../assets/export-csv-mixpanel.png)

1. 將`.csv`檔案傳送給您正在處理此驗證程式的客戶經理或分析人員。
