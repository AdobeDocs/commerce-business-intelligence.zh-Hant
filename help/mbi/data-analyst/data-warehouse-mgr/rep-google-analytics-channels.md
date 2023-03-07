---
title: 使用贏取來源複製Google Analytics通道
description: 了解如何使用贏取來源復寫Google Analytics管道。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Google Analytics使用贏取來源

## 什麼是管道？ {#channels}

建立自訂區段，以查看不同流量的表現和觀察趨勢，是  [!DNL Google Analytics ]. 預設存在於 [!DNL Google Analytics ] 為 `Channels`. 管道是訪客造訪您網站的常用方式分組。  [!DNL Google Analytics ] 自動排序您取得使用者的許多方式（無論是社交媒體、每次點按付費、電子郵件或轉介連結），並將它們整合至貯體或管道。

## 為什麼我看不到我的 `channels` 在MBI? {#nochannels}

`Channels` 是簡單的資料集。 若要將贏取排序至管道貯體，Google會使用特定參數來設定不同的規則和定義：收購組合 [來源](https://support.google.com/analytics/answer/1033173?hl=en) （流量來源）和贏取 [中](https://support.google.com/analytics/answer/6099206?hl=en) （源的一般類別）。

雖然擁有這些貯體可協助您了解流量來自何處，但此資料並非以管道標籤，而是以來源和媒體的組合標籤。 由於Google會以兩個不同的資料點傳送管道資訊，因此管道群組不會自動顯示於 [!DNL MBI].

## 預設管道群組為何？ 如何建立？

依預設，Google會設定您8個不同的管道。 查看決定建立規則的規則：

| 管道 | 是什麼？ | 如何建立？ |
|---|---|---|
| 直接 | 直接進入您網站的任何人。 | 來源= `Direct`<br>和中= `(not set); OR Medium = (none)` |
| 自然搜尋 | 已在無報酬搜尋引擎中有機排名的流量。 | 中= `organic` |
| 轉介 | 來自非有機搜尋的外部連結或來自非社交網路的網站的流量。 | 中= `referral` |
| 付費搜尋 | 具有UTM追蹤程式碼的流量，其中媒體為「cpc」、「ppc」或「paidsearch」，且是不符合「內容」的廣告分送網路。 | 中= `^(cpc|ppc|paidsearch)$`<br>和廣告分送網路≠ `Content` |
| 社交 | 來自任何約 [400個社交網路](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) 和未標籤為廣告。 | 社交來源反向連結= `Yes`<br>或中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 電子郵件 | 來自以「電子郵件」為媒體標籤之工作階段的流量。 | 中的UTM追蹤代碼= `email` |
| 顯示 | 具有UTM追蹤代碼的流量，其中媒體為顯示或cpm。 也包含廣告發佈網路與「內容」相符的AdWords互動 | 中= `^(display|cpm|banner)$`<br>OR廣告分送網路= `Content`<br>和廣告格式≠ `Text` |
| 其他 | 以「cpc」、「ppc」、「cpm」、「cpv」、「cpa」、「cpp」、「cpp」、「cpp」、「cpp」、「cpp」、「cpp」、「附屬單位」為標籤的其他廣告管道（不包括付費搜尋）的工作階段。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## 如何在我的Data Warehouse中重新建立這些管道群組？ {#recreate}

既然您知道管道只是來源和媒體的組合，在您的Data Warehouse中重新建立這些群組是一個簡單的三步驟程式。

1. **啟用[!DNL Google ECommerce]整合**

   [啟用後](../importing-data/integrations/google-ecommerce.md)，請確定 [同步](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **媒體** 和 **來源** 欄位。 完成後，中型和來源贏取資料會匯入您的Data Warehouse。

1. **上傳Google管道群組的對應**

   為節省時間，商務已建立一個表格，其預設分組映射為可供您 [下載](../../assets/ga-channel-mapping.csv).

   如果您是Google Analytics專業人員並建立了自己的管道，請先將特定規則新增至對應表格，再將檔案上傳至 [!DNL MBI].

   將其帶入您的Data Warehouse，作為 [檔案上傳](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **建立[!DNL Google ECommerce]和映射檔案上載**

   建立[!DNL Google ECommerce]和映射表， [提交支援請求](../../guide-overview.md) 敬請您的資料分析人員團隊，並參考本文。 分析師會建立新的計算欄，稱為 **管道** （在電子商務表中）。 **完整更新週期後**，此欄即可用於篩選或群組依據。

恭喜！ 現在您的Data Warehouse中已有Google Analytics管道群組，這表示您可以從新的角度分析資料：

![依管道劃分訂購量度](../../assets/GA_Channel_Gif.gif)

在此範例中，您開始使用簡單 — 將 **訂購數** 量度依據 **管道**. 現在輪到您了 — 請測試您的新欄，並查看您可在Google Analytics管道資料中識別哪些趨勢！

## 相關檔案

* [使用Report Builder](../../tutorials/using-visual-report-builder.md)
* [預期[!DNL Google ECommerce]資料](../importing-data/integrations/google-ecommerce-data.md)
* [建置[!DNL Google ECommerce]包含訂單和客戶資料的維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [您最有價值的贏取來源和管道為何？](../analysis/most-value-source-channel.md)
