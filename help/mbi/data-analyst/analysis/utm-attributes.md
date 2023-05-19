---
title: Google Analytics與UTM屬性
description: 瞭解Google Analytics源屬性流程。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] 和UTM屬性

對於 [跟蹤用戶獲取源](../../data-analyst/analysis/google-track-user-acq.md) 至 [確定表現最佳的廣告活動](../../data-analyst/analysis/most-value-source-channel.md)。 本主題探討 [!DNL Google Analytics] 源屬性過程。 換句話說，記錄哪條資訊的時間。

## 歸因是什麼？

`Attribution` 是指定特定活動的引用源。 這些活動通常是宏轉換或微轉換，宏是類似 **購買**&#x200B;微生物 **註冊，電子郵件註冊，部落格評論，** 等等。

理想地，每次發生轉換事件時，都記錄引用源。 但消息來源如何確定？

現實情況是，用戶在點擊/提交微或宏轉換之前，往往來自許多來源。 比如，他們可以通過有機方式來到網站，然後離開，然後通過付費搜索，然後離開，然後直接來到網站本身。 此源跟蹤資訊通常通過UTM參數提供給站點，但也有更複雜的系統。 為您的目的，請集中注意 [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998)。

## 如何 [!DNL Google Analytics] 是否通過UTM參數提供屬性引用源？

在URL上指定UTM參數時，這些參數會被解析出並放入 [!DNL Google Analytics] [餅](https://en.wikipedia.org/wiki/HTTP_cookie)。 如果網站沒有 [!DNL Google Analytics]，擁有UTM沒有意義。 [!DNL Google Analytics] 有規則，說明在UTM的有生之年（以後更多），它如何處理與多個URL相連的用戶。 假設網站配置為將UTM參數捕獲到外部資料庫，則當發生微或宏轉換時， [!DNL Google Analytics] 轉換時的cookie將被複製到資料庫。

## 首次按一下與上次按一下

### 上次按一下屬性

最後一次點擊屬性是最常用的屬性模型 [!DNL Google Analytics]。 在這個例子中， [!DNL Google Analytics] cookie表示轉換事件之前最新源的UTM參數，這是 [記錄在資料庫中](../../data-analyst/analysis/google-track-user-acq.md)。 的 [!DNL Google Analytics] 僅當用戶按一下包含一組新UTM參數的新URL時，cookie才會覆蓋以前的UTM參數。

例如，假設用戶首次通過 [!DNL Google Analytics] *付費搜索*，然後返回 *有機搜索*，最後回到 *網站* 或通過 *電子郵件連結* **沒有UTM參數** 的子菜單。 在此示例中， [!DNL Google Analytics] cookie表示用戶的源是有機的，因為這表示轉換前的最後一個源。 的 *路徑* 將忽略該最終轉換事件之前的用戶。 如果用戶通過帶有UTM的電子郵件連結訪問網站，則 [!DNL Google Analytics] cookie會說來源是「電子郵件」。 因此，如果cookie中存在現有UTM參數，並且用戶通過direct進入，則 [!DNL Google Analytics] cookie顯示的是UTM參數，而不是「direct」。

>[!NOTE]
>
>特定用戶的 [!DNL Google Analytics] 當cookie時，cookie參數將被擦除 [過期](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)，或當用戶在瀏覽器中清除其cookie時。*

### 首次按一下屬性

一些付費歸屬工具允許您捕獲用戶路徑中的「煎餅堆」源。 在這種情況下，在上例中，首先按一下屬性將告訴我們付費搜索。 或者，一些網站會實現自己的cookie，以捕獲煎餅堆並將第一個源儲存到其資料庫中。

## 如何分析歸因？

[!DNL Google Analytics] 在其web介面中具有一些強大的功能，允許您執行四種不同的屬性模型：

1. 首次按一下
1. 最後按一下
1. 線性（在路徑中所有來源之間平均分配收入）
1. 加權（自定義屬性）

既然您瞭解了每個微或宏轉換的屬性模型是什麼，問題就變成了「您如何處理用戶轉換的全部內容？」。  例如，查看根據GA上次按一下邏輯記錄的UTM:

* 有機用戶註冊
* 付費搜索下用戶的首次購買$5.00
* 用戶在電子郵件下的第二次購買$50.00
* 用戶第三次有機購買10.00美元

你問：&quot;我從付費搜索中獲得了多少收入？ 電子郵件？  來自有機？」 你可以說答案是5 、 50和10（不管最後一個來源是什麼），或者你也可以說將所有收入都歸於第一個來源（所有65都歸有機來源）。 也可以應用一些加權分析或應用線性模型（即每個約22個）。

## 相關文檔

* [跟蹤訂單推薦來源 [!DNL Google Analytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [跟蹤資料庫中的用戶推薦源](../analysis/google-track-user-acq.md)
* [跟蹤資料庫中的用戶設備、瀏覽器和OS資料](../analysis/google-track-user-acq.md)
* [發現您最有價值的收購來源和渠道](../analysis/most-value-source-channel.md)
* [連接 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告活動的ROI](../analysis/roi-ad-camp.md)
* [UTM標籤的五個最佳做法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
