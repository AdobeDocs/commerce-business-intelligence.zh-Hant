---
title: 導入其他廣告支出資料
description: 學習將離線或其他廣告支出資料導入 [!DNL Commerce Intelligence]。
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 導入其他廣告支出資料

上傳廣告支出資料使您能夠將廣告成本和 `customer lifetime value (CLV)` 從您的市場活動中獲得的用戶。

## 上傳廣告成本資料

分析廣告支出資料的第一步是獲取資料。 由於大多數廣告平台都允許您導出報告，Adobe建議您導出廣告平台中的原始資料，並將其直接上傳到 [!DNL Commerce Intelligence] 不受任何操縱。 您可以對Data Warehouse中的資料執行操作，因此無需加倍努力。

導出廣告支出資料後，使用 [`File Upload` 特徵](../connecting-data/using-file-uploader.md) 將資料帶入Data Warehouse。 可以將新資料上載到同一 [!DNL Commerce Intelligence] 時間表。

## 離線源

除了線上活動外，您還可能有離線廣告，例如在廣播或廣告牌上。 要處理這些案例，您可以手動將包含成本資料的電子錶格上載到 [!DNL Commerce Intelligence]。

在建立 `.csv` 檔案以記錄和花費資料。 此主題底部還附有一個模板檔案作為示例。 建議的列包括：

* `ID`  — 這是資料庫用作主鍵的每個資料行的唯一標識符。 每行必須不同。
* `Date`  — 這是市場活動運行的日期，格式為yyyy-mm-dd。
* `Amount`  — 這是您在市場活動上花費的金額。
* `campaign`  — 這是活動名稱。 如果您使用 [!DNL Google Analytics] 要跟蹤您的其他廣告支出資料，它應與utm\_campaign名稱匹配。
* `source`  — 這是源名稱。 如果您使用 [!DNL Google Analytics]，應匹配 `utm_source` 名稱。
* `other` （可選） — 您還可以合併其它列，以幫助您對市場活動和成本進行細分。 它還可以將幾種不同的UTM活動名稱總結為一個單一、連貫的活動，以便跟蹤。 與其手動設定，不如使用V-Lookup查找第二個工作表，將每個市場活動名稱與其他名稱匹配並在此處動態報告。

## 相關

* [連接 [!DNL AdWords] 資料](../integrations/google-adwords.md)
* [提高廣告活動的ROI](../../analysis/roi-ad-camp.md)
