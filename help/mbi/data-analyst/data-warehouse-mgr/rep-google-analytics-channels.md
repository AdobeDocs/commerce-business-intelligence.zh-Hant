---
title: 使用獲取源複製Google Analytics通道
description: 瞭解如何使用獲取源複製Google Analytics渠道。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] 使用獲取源

## 什麼是頻道？ {#channels}

建立自定義段以查看不同流量的運行情況並觀察趨勢是最強大的用途之一 [!DNL Google Analytics]。 預設存在於 [!DNL Google Analytics] 是 `Channels`。 渠道是人們訪問您站點的常用方式的分組。  [!DNL Google Analytics] 自動對您獲取用戶的多種方式進行排序 — 無論是社交媒體、按按一下付費、電子郵件還是推薦連結 — 並將它們捆綁到儲存桶或渠道中。

## 為什麼我不看到 `channels` 商業情報？ {#nochannels}

`Channels` 是簡單的資料集合桶。 要將您的收購分類到Channel儲存桶中， [!DNL Google] 使用特定參數設定不同的規則和定義：收購組合 [源](https://support.google.com/analytics/answer/1033173?hl=en) （您的流量來源）和獲取 [中](https://support.google.com/analytics/answer/6099206?hl=en) （來源的一般類別）。

雖然擁有這些儲存段可以幫助您瞭解流量的來源，但此資料不是按通道標籤的，而是按源和媒體的組合標籤的。 因為 [!DNL Google] 將通道資訊作為兩個獨立的資料點發送，通道分組不會自動顯示在 [!DNL Commerce Intelligence]。

## 預設頻道分組是什麼？ 它們是如何建立的？

預設情況下， [!DNL Google] 設定八個不同的頻道。 確定如何建立通道的規則如下。

| **頻道** | **怎麼了？** | **它是如何建立的？** |
|---|---|---|
| 直接 | 任何直接進入您網站的人。 | 源= `Direct`<br>和中= `(not set); OR Medium = (none)` |
| 有機搜索 | 在無報酬搜索引擎中有機排序的流量。 | 中= `organic` |
| 推薦 | 來自非Organic Search的外部連結或來自非社交網路的網站的通信。 | 中= `referral` |
| 付費搜索 | 具有UTM跟蹤代碼的通信，其中介質為「cpc」、「ppc」或「paidsearch」，並且是與「內容」不匹配的廣告分發網路。 | 中= `^(cpc|ppc|paidsearch)$`<br>AND廣告分發網≠ `Content` |
| 社會 | 來自以下任何一項的推薦流量 [400個社交網路](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) 沒有標籤為廣告。 | 社交來源推薦= `Yes`<br>或中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 電子郵件 | 標籤有「電子郵件」介質的會話的通信。 | UTM中的跟蹤代碼= `email` |
| 顯示 | 具有UTM跟蹤代碼的通信，其中介質為顯示或cpm。 還包括廣告分發網路與「內容」匹配的AdWords交互 | 中= `^(display|cpm|banner)$`<br>OR廣告分發網路= `Content`<br>AND廣告格≠ `Text` |
| 其他 | 其他廣告渠道（不包括付費搜索）的會話，這些廣告渠道以&quot;cpc&quot;、&quot;ppc&quot;、&quot;cpm&quot;、&quot;cpv&quot;、&quot;cpa&quot;、&quot;cpp&quot;、&quot;關聯&quot;等媒介標籤。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## 如何在我的Data Warehouse中重新建立這些渠道分組？ {#recreate}

既然您知道渠道只是源和媒介的組合，在您的Data Warehouse中重新建立這些分組將是一個簡單的三步過程。

1. **啟用[!DNL Google ECommerce]整合**

   [啟用時](../importing-data/integrations/google-ecommerce.md)，確保 [同步](./){{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **介質** 和 **源** 的子菜單。 完成此操作後，中和源採集資料將帶入您的Data Warehouse。

1. **上載Google頻道分組的映射**

   Adobe Commerce建立一個表，其預設分組映射為一個檔案 [下載](../../assets/ga-channel-mapping.csv)。

   如果你是 [!DNL Google Analytics] pro並建立了您自己的通道，您希望在將檔案上載到映射表中之前將特定規則添加到映射表中 [!DNL Commerce Intelligence]。

   把它帶進你的Data Warehouse [檔案上載](../importing-data/connecting-data/using-file-uploader.md)。

   ![](../../assets/Setting_Primary_Keys.png)

1. **在[!DNL Google ECommerce]和映射檔案上載**

   在[!DNL Google ECommerce] 和映射表， [提交支援請求](../../guide-overview.md#Submitting-a-Support-Ticket) 您的資料分析團隊並參考此主題。 分析員將建立一個名為 **頻道** 的子菜單。 **在完整更新週期後**，此列將可以在 `Filter` 或 `Group by`。

你現在 [!DNL Google Analytics Channel] Data Warehouse中的分組，這意味著您可以從新的角度分析資料：

![按通道分段階數度量](../../assets/GA_Channel_Gif.gif)

在此示例中，您開始使用分段 **訂單數** 度量 **頻道**。 Test新列，查看您可以在中確定的趨勢 [!DNL Google Analytics Channel] 資料！

## 相關文檔

* [使用Report Builder](../../tutorials/using-visual-report-builder.md)
* [預期[!DNL Google ECommerce]資料](../importing-data/integrations/google-ecommerce-data.md)
* [大樓[!DNL Google ECommerce]包含訂單和客戶資料的維](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [您最有價值的收購來源和渠道是什麼？](../analysis/most-value-source-channel.md)
