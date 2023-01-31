---
title: 匯入其他廣告支出資料
description: 了解如何將離線或其他廣告支出資料匯入 [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 匯入其他廣告支出資料

上傳廣告支出資料可讓您結合廣告成本和客戶，借此衡量行銷活動的ROI `lifetime value (CLV)` 從您的行銷活動獲得的使用者。

## 上傳廣告成本資料

分析廣告支出資料的第一步是取得資料。 由於大部分的廣告平台都允許您匯出報表，因此建議您從廣告平台匯出原始資料，並直接將其上傳至 [!DNL MBI] 不用任何操縱。 您可以對資料倉庫中的資料執行操作，因此無需加倍努力。

匯出廣告支出資料後，請使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 將資料匯入您的資料倉庫。 您可以將新資料上傳至相同 [!DNL MBI] 表格。

## 離線來源

除了您的線上行銷活動，您也可能有離線廣告，例如收音機或廣告牌上的廣告。 若要解決這些情況，您可以手動上傳含成本資料的試算表至 [!DNL MBI].

建立 `.csv` 檔案來記錄廣告支出資料。 本文底部也會附加範本檔案以作為範例。 建議的欄包括：

* `ID`  — 這是資料庫用作主鍵的每個資料行的唯一標識符。 每一列的這個值都必須不同。
* `Date`  — 這是促銷活動執行的日期，格式為yyyy-mm-dd。
* `Amount`  — 這是您在促銷活動上花費的金額。
* `campaign`  — 這是促銷活動名稱。 如果您使用 [!DNL Google Analytics] 若要追蹤您的其他廣告支出資料，它應符合utm\_campaign名稱。
* `source`  — 這是源名稱。 如果您使用 [!DNL Google Analytics]，這應符合 `utm_source` 名稱。
* `other` （選用） — 您也可以合併其他欄，協助您劃分促銷活動和成本。 這也可以是將數個不同的UTM促銷活動名稱匯總為單一、一致的促銷活動，以便追蹤。 與其手動設定，最好使用V查詢功能來比對每個促銷活動名稱與其他名稱，並在此動態報告。

## 相關

* [Connect [!DNL AdWords] 資料](../integrations/google-adwords.md)
* [提高廣告宣傳的投資報酬率](../../analysis/roi-ad-camp.md)
