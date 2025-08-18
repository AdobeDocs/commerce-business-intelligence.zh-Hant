---
title: Google Analytics — 追蹤使用者贏取Source資料概述
description: 瞭解如何依使用者贏取來源劃分資料。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# 依使用者贏取來源細分

>[!NOTE]
>
>下列程式不支援[!DNL Google Universal Analytics]。

依使用者贏取來源劃分資料區段的功能，是有效管理行銷計畫的關鍵。 瞭解新使用者的贏取來源，可顯示哪些管道產生最高回報，並讓您的團隊充滿信心地配置行銷資金。

如果您尚未追蹤資料庫中的使用者贏取來源，[!DNL Adobe Commerce Intelligence]可以協助您開始使用：

## 追蹤使用者贏取來源

[!DNL Adobe]建議根據您的設定，使用兩種方法來追蹤轉介來源資料：

### （選項1）透過[!DNL Google Analytics E-Commerce]追蹤訂單轉介來源資料

如果您使用[!DNL Google Analytics E-Commerce]追蹤您的訂單與銷售資料，則可以使用[[!DNL [Google Analytics E-Commerce Connector]]](../importing-data/integrations/google-ecommerce.md)同步每個訂單的轉介來源資料。 這可讓您依反向連結來源（例如，`utm_source`或`utm_medium`）來劃分收入與訂單。 您也可透過[!DNL Commerce Intelligence]自訂維度（例如`User's first order source`）瞭解客戶贏取來源。

### （選項2）將[!DNL Google Analytics]的贏取來源資料儲存在資料庫中

此主題說明如何將[!DNL Google Analytics]贏取管道資訊儲存到您自己的資料庫中，也就是使用者第一次造訪您的網站時所顯示的`source`、`medium`、`term`、`content`、`campaign`和`gclid`引數。 如需這些引數的說明，請參閱[[!DNL Google Analytics] 檔案](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article)。 然後，您探索可在[!DNL Commerce Intelligence]中使用此資訊執行的一些強大行銷分析。

#### 為什麼？

如果您只是檢視預設的[!DNL Google Analytics]轉換和贏取量度，就代表您並未掌握全貌。 雖然檢視有機搜尋與付費搜尋的轉換次數很有趣，您可以如何處理這些資訊？ 您應該在付費搜尋上花更多錢嗎？ 這取決於來自該管道的客戶的價值，而非Google Analytics所提供的功能。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce)透過將交易資料儲存在[!DNL Google Analytics]來緩解此問題，但此解決方案不適用於非電子商務網站。 此外，[!DNL Google Analytics]介面中也不容易執行同類群組分析等特定工具。

如果您想要透過電子郵件向所有從特定電子郵件促銷活動取得的客戶傳送後續交易，該怎麼做？ 或是將贏取資料與CRM系統整合？ [!DNL Google Analytics]中不可能有此功能 — 事實上，它違反[!DNL Google Analytics]的服務條款，以儲存任何可識別個人的資料。 不過，您可以自行儲存這些資料。

#### 方法

[!DNL Google Analytics]會將訪客轉介資訊儲存在名為`__utmz`的Cookie中。 在此Cookie設定後（由[!DNL Google Analytics]追蹤程式碼設定），其內容將隨該使用者的每個後續要求傳送至您的網域。 因此，在PHP中，您可以簽出`$_COOKIE['__utmz']`的內容，您會看到類似以下的字串：

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

很明顯有些贏取來源資料會編碼為字串。 測試以確認這是訪客的最新贏取來源和相關聯的行銷活動資料。 現在您需要瞭解如何擷取資料。

此程式碼已轉譯為github[上託管的](https://github.com/RJMetrics/referral-grabber-php)PHP程式庫。 若要使用程式庫，`include`對`ReferralGrabber.php`的參照，然後呼叫

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

傳回的`$data`陣列是索引鍵`source`、`medium`、`term`、`content`、`campaign`、`gclid`及其各自值的對應。

Adobe建議將名為`user_referral`的資料表新增至您的資料庫，其資料行如下： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`。 每當使用者註冊時，請擷取轉介資訊並將其儲存至此表格。

#### 如何使用此資料

現在您正在儲存使用者贏取來源，該如何使用？

假設您正在使用SQL資料庫，且有具有以下結構的`users`表格：

| ID | 電子郵件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有機 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 轉介 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有機 |
| ... | ... | ... | ... | ... |

首先，您可以對資料庫執行下列查詢，以計算來自每個轉介管道的使用者數量：

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果看起來像這樣：

| ACQ_SOURCE | 使用者計數 |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 轉介 | 55 |
| 其他 | 16 |

這很有趣，但用途有限。 您真正想知道的是：

* 這些數字在一段時間內的成長率
* 每個贏取來源產生的收入金額
* 來自每個來源的使用者的[同類群組分析](https://en.wikipedia.org/wiki/Cohort_analysis)
* 這些管道之一的使用者未來會傳回為客戶的機率

進行這些分析所需的查詢很複雜。 有了這些資訊，您就可以決定最有利可圖的贏取管道，並相應地集中行銷時間和金錢。

### 相關

* **[探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)**
* **[連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)**
* **[提高廣告行銷活動的ROI](../analysis/roi-ad-camp.md)**
* **[ [!DNL Google Analytics] UTM歸因如何運作？](../analysis/utm-attributes.md)**
