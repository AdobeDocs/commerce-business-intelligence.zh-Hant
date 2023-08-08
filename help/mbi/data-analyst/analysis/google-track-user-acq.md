---
title: Google Analytics — 追蹤使用者贏取來源資料概述
description: 瞭解如何依使用者贏取來源劃分資料。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# 依使用者贏取來源細分

>[!NOTE]
>
>以下程式不支援 [!DNL Google Universal Analytics].

依使用者贏取來源劃分資料區段的功能，是有效管理行銷計畫的關鍵。 瞭解新使用者的贏取來源，可顯示哪些管道產生最高回報，並讓您的團隊充滿信心地配置行銷資金。

如果您尚未在資料庫中追蹤使用者贏取來源， [!DNL Adobe Commerce Intelligence] 可以協助您開始使用：

## 追蹤使用者贏取來源

[!DNL Adobe] 建議根據您的設定，使用兩種方法來追蹤反向連結來源資料：

### （選項1）透過追蹤訂單轉介來源資料 [!DNL Google Analytics E-Commerce]

如果您使用 [!DNL Google Analytics E-Commerce] 若要追蹤您的訂單與銷售資料，您可以使用 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 以同步每個訂單的轉介來源資料。 這可讓您依反向連結來源來劃分收入與訂單(例如， `utm_source` 或 `utm_medium`)。 您也可以透過以下方式瞭解客戶贏取來源 [!DNL Commerce Intelligence] 自訂維度，例如 `User's first order source`.

### （選項2）儲存 [!DNL Google Analytics]&#39;資料庫中的贏取來源資料

本主題說明如何儲存 [!DNL Google Analytics] 贏取管道資訊放入您自己的資料庫，即 `source`， `medium`， `term`， `content`， `campaign`、和 `gclid` 使用者首次造訪您的網站時出現的引數。 如需這些引數的說明，請參閱 [[!DNL Google Analytics] 檔案](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 然後，您會探索可以使用此資訊在中執行的一些強大行銷分析 [!DNL Commerce Intelligence].

#### 為什麼？

如果您只檢視預設值 [!DNL Google Analytics] 轉換和贏取量度，你就無法全面掌握。 雖然檢視有機搜尋與付費搜尋的轉換次數很有趣，您可以如何處理這些資訊？ 您應該在付費搜尋上花更多錢嗎？ 這取決於來自該管道的客戶的價值，而非Google Analytics提供的東西。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 透過將交易資料儲存在中來緩解此問題 [!DNL Google Analytics]，但此解決方案不適用於非電子商務網站。 此外，同類群組分析等特定工具在中也不容易 [!DNL Google Analytics] 介面。

如果您想要透過電子郵件向所有從特定電子郵件促銷活動取得的客戶傳送後續交易，該怎麼做？ 或是將贏取資料與CRM系統整合？ 這是不可能的 [!DNL Google Analytics]  — 事實上，這違反了 [!DNL Google Analytics] 儲存可識別個人的任何資料。 不過，您可以自行儲存這些資料。

#### 方法

[!DNL Google Analytics] 會將訪客反向連結資訊儲存在名為的Cookie中 `__utmz`. 在此Cookie設定後(由 [!DNL Google Analytics] 追蹤程式碼)，則其內容會隨著該使用者的每次後續請求而傳送至您的網域。 例如，在PHP中，您可以將 `$_COOKIE['__utmz']` 您會看到類似以下的字串：

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

很明顯有些贏取來源資料會編碼為字串。 測試以確認這是訪客的最新贏取來源和相關聯的行銷活動資料。 現在您需要瞭解如何擷取資料。

此程式碼已轉譯為 [在github上託管的PHP程式庫](https://github.com/RJMetrics/referral-grabber-php). 若要使用程式庫， `include` 參考 `ReferralGrabber.php` 然後呼叫

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

傳回的 `$data` 陣列是索引鍵的對應 `source`， `medium`， `term`， `content`， `campaign`， `gclid`，以及其各自的值。

Adobe建議將表格新增至您的資料庫，例如 `user_referral`，具有以下欄： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 每當使用者註冊時，請擷取轉介資訊並將其儲存至此表格。

#### 如何使用此資料

現在您正在儲存使用者贏取來源，該如何使用？

假設您正在使用SQL資料庫，並且具有 `users` 具有下列結構的表格：

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
* A [同類群組分析](https://en.wikipedia.org/wiki/Cohort_analysis) 來自每個來源的使用者數量
* 這些管道之一的使用者未來會傳回為客戶的機率

進行這些分析所需的查詢很複雜。 有了這些資訊，您就可以決定最有利可圖的贏取管道，並相應地集中行銷時間和金錢。

### 相關

* **[探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)**
* **[連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)**
* **[提高廣告行銷活動的ROI](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM歸因工作？](../analysis/utm-attributes.md)**
