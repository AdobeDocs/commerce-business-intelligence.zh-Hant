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

# 中的資料驗證 [!DNL Mixpanel]

時間 [!DNL Adobe Commerce Intelligence] 首先連線至您的 [!DNL Mixpanel] 資料，您的客戶經理或分析師可能會要求您提供資料匯出來源 [!DNL Mixpanel] 以進行驗證。 這可讓您確認您已同步可直接在中取得的所有相同資料 [!DNL Mixpanel].

## 資料匯出程式： `Events`

1. 造訪您的 `Segmentation` 截面和檢視 `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. 選取 `Past 96 Hours` 針對時間範圍

   ![](../../../assets/past-96-hours.png)

1. 捲動至報表的右下方，然後匯出 `.csv` 檔案：

   ![](../../../assets/export-csv-mixpanel.png)

1. 傳送 `.csv` 將檔案傳送給您正在處理此驗證程式的客戶經理或分析師。
