---
title: Google Analytics和UTM歸因
description: 瞭解Google Analytics來源歸因程式。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Google Analytics]和UTM歸因

[追蹤使用者贏取來源](../../data-analyst/analysis/google-track-user-acq.md)至[識別表現最佳的廣告行銷活動](../../data-analyst/analysis/most-value-source-channel.md)至關重要。 本主題探索[!DNL Google Analytics]來源歸因程式。 換句話說，會在何時記錄哪一則資訊。

## 什麼是歸因？

`Attribution`是關於指定特定活動的轉介來源。 這些活動通常是巨集轉換或微集轉換，巨集是&#x200B;**購買**&#x200B;之類的專案，微集是&#x200B;**註冊、電子郵件註冊、部落格評論、**&#x200B;等專案。

理想情況下，每次發生轉換事件時，都會記錄轉介來源。 但來源是如何決定的？

事實上，使用者在點選/認可微或巨集轉換之前，通常來自許多來源。 例如，他們可能透過有機方式造訪網站，然後離開，接著透過付費搜尋造訪，然後離開，接著直接造訪網站本身。 這些來源追蹤資訊通常透過UTM引數提供給網站，但也有更複雜的系統。 基於您的目的，請專注於[UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998)。

## [!DNL Google Analytics]如何透過UTM引數來認定反向連結來源？

在URL上指定UTM引數時，這些引數會被剖析並放入[!DNL Google Analytics] [Cookie](https://en.wikipedia.org/wiki/HTTP_cookie)。 如果網站沒有[!DNL Google Analytics]，則沒有UTM就沒有意義。 [!DNL Google Analytics]對於如何處理在其存留期內使用UTM點選多個URL的使用者有規則（稍後將詳加說明）。 假設網站已設定為將UTM引數擷取到外部資料庫，當發生微處理或巨集轉換時，轉換時[!DNL Google Analytics] Cookie中的任何內容都會複製到資料庫。

## 首次點按與上次點按

### 最終點按歸因

最後點按歸因是[!DNL Google Analytics]最常用的歸因模型。 在此案例中，[!DNL Google Analytics] Cookie代表轉換事件前最新來源的UTM引數，而這是記錄在資料庫](../../data-analyst/analysis/google-track-user-acq.md)中的[。 如果使用者點按包含新UTM引數集的新URL，[!DNL Google Analytics] Cookie只會覆寫先前的UTM引數。

例如，假設某個使用者先透過[!DNL Google Analytics] *付費搜尋*&#x200B;造訪網站，然後透過&#x200B;*有機搜尋*&#x200B;傳回，最後在轉換事件之前直接或透過&#x200B;*電子郵件連結* **（不含UTM引數**）返回&#x200B;*網站*。 在此範例中，[!DNL Google Analytics] Cookie指出使用者的來源是有機的，因為這是轉換前的最後一個來源。 已忽略最終轉換事件之前使用者的&#x200B;*路徑*。 如果使用者改為透過包含UTM的電子郵件連結造訪網站，則[!DNL Google Analytics] Cookie會指出來源為「電子郵件」。 因此，如果Cookie中存在UTM引數，且使用者透過直接進入，則[!DNL Google Analytics] Cookie會顯示UTM引數而非「直接」。

>[!NOTE]
>
>當Cookie [過期](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)或使用者在瀏覽器中清除其Cookie時，特定使用者的[!DNL Google Analytics] Cookie引數會被清除。*

### 首次點按歸因

有些付費歸因工具可讓您擷取使用者路徑中的來源「蛋糕棧疊」。 在這種情況下，在上述範例中，首次點按歸因將告知我們付費搜尋。 或者，有些網站會實作自己的Cookie，擷取煎餅棧疊，並將第一個來源儲存到資料庫中。

## 如何分析歸因？

[!DNL Google Analytics]的網頁介面有一些強大的功能，可讓您執行四種不同的歸因模型：

1. 按一下
1. 最後點按
1. 線性（將收入平均分配到路徑中的所有來源）
1. 加權（自訂歸因）

現在您已經瞭解每個微觀或巨集轉換的歸因模型是什麼，問題就變成了「您如何處理使用者的轉換總數？」  例如，檢視根據GA最後點按邏輯記錄的UTM：

* 使用者在有機底下註冊
* 使用者在付費搜尋下的首次購買$5.00
* 使用者在電子郵件底下的第二次購買$50.00
* 使用者第三次購買有機費$10.00

您會在這裡問：「我從付費搜尋得到了多少收入？ 來自電子郵件？  有機食品？」 您可以說答案是5、50和10 （無論最後一個來源為何），或者您也可以說您將所有收入歸因於第一個來源（所有65個都歸因於有機來源）。 您也可以套用某些加權分析或線性模型（大約每個22個）。

## 相關檔案

* [透過 [!DNL Google Analytics] E-Commerce追蹤訂單轉介來源](../importing-data/integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../analysis/google-track-user-acq.md)
* [追蹤資料庫中的使用者裝置、瀏覽器和作業系統資料](../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告行銷活動的ROI](../analysis/roi-ad-camp.md)
* [在 [!DNL Google Analytics]中進行UTM標籤的五個最佳實務](../../best-practices/utm-tagging-google.md)
