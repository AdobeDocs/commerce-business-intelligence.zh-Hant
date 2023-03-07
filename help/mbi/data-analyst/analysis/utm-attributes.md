---
title: Google Analytics和UTM歸因
description: 了解Google Analytics來源歸因程式。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Google Analytics和UTM歸因

這對 [追蹤使用者贏取來源](../../data-analyst/analysis/google-track-user-acq.md) to [識別成效最佳的廣告行銷活動](../../data-analyst/analysis/most-value-source-channel.md). 本文探討Google Analytics來源歸因程式。 換句話說，當記錄什麼資訊時。

## 歸因是什麼？

`Attribution` 是指定特定活動的反向連結來源。 這些活動通常是巨集轉換或微觀轉換，巨集就像 **購買**&#x200B;微觀 **註冊，電子郵件註冊，部落格評論，** 等等。

理想情況下，每次發生轉換事件時，都會記錄轉介來源。 但來源又如何確定？

事實上，使用者在點擊/提交微觀或巨集轉換前，通常會先從許多來源取得。 例如，他們可能透過自然方式來到網站，然後離開，然後透過付費搜尋來，然後離開，然後直接來到網站本身。 此源跟蹤資訊通常通過UTM參數提供給站點，但是也有更複雜的系統。 為您的目的，請著重於 [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 如何 [!DNL Google Analytics] 是否透過UTM參數提供屬性轉介來源？

在URL上指定UTM參數時，系統會剖析這些參數並放入 [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). 如果網站沒有 [!DNL Google Analytics]，則擁有UTM沒有意義。 [!DNL Google Analytics] 有規則來處理在期限內使用UTM點擊多個URL的使用者（稍後會詳加說明）。 假設網站設定為將UTM參數擷取到外部資料庫，則發生微或巨集轉換時， [!DNL Google Analytics] 轉換時的cookie會複製到資料庫。

## 首次點按與上次點按

### 上次點按歸因

最後點按歸因是 [!DNL Google Analytics]. 在此情況下， [!DNL Google Analytics] cookie代表轉換事件前最新來源的UTM參數，這是 [記錄在資料庫中](../../data-analyst/analysis/google-track-user-acq.md). 此 [!DNL Google Analytics] 只有當使用者點按包含一組新UTM參數的新URL時，cookie才會覆寫先前的UTM參數。

例如，假設使用者先透過 [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *付費搜尋*，然後傳回 *有機搜尋*，最後返回 *直接* 或透過 *電子郵件連結* **不含UTM參數** 在轉換事件之前。 在此範例中， [!DNL Google Analytics] cookie會指出使用者的來源是自然的，因為這代表轉換前的最後一個來源。 此 *路徑* ，而系統才會忽略最終轉換事件。 若使用者改為透過UTM的電子郵件連結造訪網站，則 [!DNL Google Analytics] cookie會說來源是「電子郵件」。 因此，如果Cookie中有現有UTM參數，且使用者透過直接傳入，則 [!DNL Google Analytics] cookie會顯示UTM參數，而非「直接」。

>[!NOTE]
>
>特定使用者的 [!DNL Google Analytics] cookie參數會在Cookie [過期](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)，或使用者在瀏覽器中清除其cookie時覆寫分類。*)

### 首次點按歸因

有些付費歸因工具可讓您擷取使用者路徑中來源的「煎餅堆疊」。 在這種情況下，在上述範例中，按一下「歸因」後即會得知付費搜尋。 或者，有些網站會實作自己的Cookie來擷取煎餅堆疊，並將第一個來源儲存至其資料庫。

## 如何分析歸因？

[!DNL Google Analytics] 其網頁介面具備一些強大功能，可讓您執行四種不同的歸因模型：

* 首次點按
* 上次點按
* 線性（將收入平均分配給路徑中的所有來源）
* 加權（自訂歸因）

現在您了解每個微觀或巨集轉換的歸因模型為何了，問題就變成「您該如何處理使用者轉換總數？」。  例如，查看根據GA上次點按邏輯記錄的UTM:

* 用戶註冊在自然狀態下
* 使用者首次付費搜尋購買$5.00
* 使用者在電子郵件下購買的第二次$50.00
* 使用者以自然方式購買的第三筆費用$10.00

這裡是你問的「我從付費搜索中獲得了多少收入？ 從電子郵件？  從有機的？」 您可以說答案是5、50和10（無論最後一個來源是什麼），或者您也可以說將所有收入歸因於第一個來源（65個全部歸於有機來源）。 您也可以套用一些加權分析，或套用線性模型（亦即每個約22個）。

## 相關檔案

* [透過追蹤訂單轉介來源 [!DNL Google Analytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [在您的資料庫中追蹤使用者反向連結來源](../analysis/google-track-user-acq.md)
* [在資料庫中追蹤使用者裝置、瀏覽器和作業系統資料](../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連接您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告宣傳的投資報酬率](../analysis/roi-ad-camp.md)
* [中UTM標籤的五個最佳作法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
