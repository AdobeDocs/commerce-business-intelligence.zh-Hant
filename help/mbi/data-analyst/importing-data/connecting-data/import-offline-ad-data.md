---
title: 匯入其他廣告支出資料
description: 瞭解如何將離線或其他廣告支出資料匯入 [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 匯入其他廣告支出資料

上傳廣告支出資料可讓您將廣告成本與 `customer lifetime value (CLV)` 從您的行銷活動取得的使用者數量。

## 正在上傳廣告成本資料

分析廣告支出資料的第一步是取得資料。 由於大部分的廣告平台都可讓您匯出報表，因此Adobe建議您從廣告平台匯出原始資料，然後直接上傳至 [!DNL Commerce Intelligence] 而不進行任何操作。 您可以對Data Warehouse中的資料執行操作，因此無需加倍努力。

匯出廣告支出資料後，請使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 將資料帶入您的Data Warehouse。 您可以將新資料上傳至相同網站 [!DNL Commerce Intelligence] 表格在一段時間內的變化。

## 離線來源

除了您的線上行銷活動，您也可能有離線廣告，例如在廣播或廣告牌上。 若要解決這些情況，您可以手動上傳包含成本資料的試算表 [!DNL Commerce Intelligence].

建立時，建議使用下方探討的表格結構 `.csv` 用來記錄廣告支出資料的檔案。 範本檔案也會附加在本主題底部，以作為範例。 建議的欄包括：

* `ID`  — 這是資料庫用來作為主索引鍵的每個資料列的唯一識別碼。 每一列的名稱必須不同。
* `Date`  — 這是行銷活動執行的日期，格式為yyyy-mm-dd。
* `Amount`  — 這是您花在行銷活動上的金額。
* `campaign`  — 這是行銷活動名稱。 如果您使用 [!DNL Google Analytics] 若要追蹤您的其他廣告支出資料，該資料應符合utm\_campaign名稱。
* `source`  — 這是來源名稱。 如果您使用 [!DNL Google Analytics]，這應該符合 `utm_source` 名稱。
* `other` （選用） — 您也可以合併其他欄，協助您劃分促銷活動和成本。 它也可以將數個不同的UTM行銷活動名稱摘要為單一、一致的行銷活動，以用於追蹤目的。 建議您不要手動進行此設定，而應該使用V型查詢來比對第二個工作表，讓每個促銷活動名稱與其他名稱相符並在這裡動態回報。

## 相關

* [連線 [!DNL AdWords] 資料](../integrations/google-adwords.md)
* [提高廣告行銷活動的ROI](../../analysis/roi-ad-camp.md)
