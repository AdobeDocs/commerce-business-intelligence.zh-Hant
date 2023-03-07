---
title: Google Analytics — 追蹤使用者贏取來源資料概觀
description: 了解如何依使用者贏取來源劃分資料。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: ad95a03193853eebf2b695cd6f5c3cb5a9837f93
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# 依使用者贏取來源劃分

>[!NOTE]
>
>以下流程不支援 [!DNL GoogleUniversal Analytics].

依使用者贏取來源劃分資料的能力，對於有效管理行銷計畫至關重要。 了解新使用者的贏取來源，可顯示哪些管道可產生最高的回報，並讓您的團隊有信心分配行銷資金。

如果您尚未在資料庫中追蹤使用者贏取來源， [!DNL MBI] 可協助您開始使用：

## 追蹤使用者贏取來源

Adobe建議您根據您的設定，使用兩種方法來追蹤反向連結來源資料：

### （選項1）透過 [!DNL Google Analytics E-Commerce] (包括 [!DNL Shopify] 商店)

如果您使用 [!DNL Google Analytics E-Commerce] 若要追蹤訂單和銷售資料，您可以使用 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 同步每個訂單的轉介來源資料。 這可讓您依反向連結來源(例如 `utm_source` 或 `utm_medium`)。 您也可以透過 [!DNL MBI] 自訂維度，例如 `User's first order source`.

>[!NOTE]
>
>Shopify用戶**:開啟 [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) 在連接 [!DNL Google Analytics E-Commerce] 帳戶 [!DNL MBI].

### （選項2）保存 [!DNL Google Analytics]&#39;資料庫中的贏取源資料

本文說明如何儲存 [!DNL Google Analytics] 贏取管道資訊放入您自己的資料庫 — 即 `source`, `medium`, `term`, `content`, `campaign`，和 `gclid` 使用者首次造訪您的網站時所呈現的參數。 如需這些參數的說明，請查看 [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 接著，您可以探索一些功能強大的行銷分析，這些分析可以在 [!DNL MBI].

#### 為什麼？

如果您只是查看預設值 [!DNL Google Analytics] 轉換和贏取量度，則無法獲得完整圖景。 雖然自然搜尋與付費搜尋的轉換次數相當有趣，但您可以利用這些資訊做什麼？ 你應該花更多錢搜索付費嗎？ 這取決於來自該管道的客戶價值，而這不是Google Analytics提供的。

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 通過將事務資料儲存在 [!DNL Google Analytics]，但此解決方案不適用於非電子商務網站。 此外，同類群組分析等特定工具在 [!DNL Google Analytics] 介面。

如果您想要將後續交易電子郵件傳送給從特定電子郵件行銷活動取得的所有客戶，該怎麼辦？ 還是將贏取資料與您的CRM系統整合？ 在 [!DNL Google Analytics]  — 事實上，這違反服務條款 [!DNL Google Analytics] 儲存可識別個人的任何資料。 但是，你可以自己儲存這些資料。

#### 方法

[!DNL Google Analytics] 將訪客反向連結資訊儲存在名為的Cookie中 `__utmz`. 設定此Cookie後(由 [!DNL Google Analytics] 追蹤程式碼)，其內容將會與該使用者向您的網域提出的每個後續請求一併傳送。 例如，在PHP中，您可以檢查 `$_COOKIE['__utmz']` 你會看到一串類似這樣的字串：

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

顯然有些擷取來源資料已編碼為字串。 這會進行測試，以確認這是訪客的最新贏取來源和相關的促銷活動資料。 現在您需要了解如何擷取資料。 幸運的是，Justin Cutroni先前已說明此編碼的運作方式，並共用一些JavaScript程式碼來擷取資訊的關鍵位元。

此程式碼已轉譯為 [托管於github的PHP程式庫](https://github.com/RJMetrics/referral-grabber-php). 若要使用程式庫， `include` 參考 `ReferralGrabber.php` 然後呼叫

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

傳回 `$data` 陣列是索引鍵的地圖 `source`, `medium`, `term`, `content`, `campaign`, `gclid`，及其各自的值。

Adobe建議將表添加到資料庫，例如， `user_referral`，包含下列欄： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 每當使用者登入時，請抓取反向連結資訊並儲存至此表格。

#### 如何使用此資料

現在您正在儲存使用者贏取來源，如何使用？

假設您使用SQL資料庫，且 `users` 表格，其結構如下：

| ID | 電子郵件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有機 |
| 2 | jim@abc.com | 2012-01-24 | google | cp |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 轉介 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有機 |
| ... | ... | ... | ... | ... |

首先，您可以對資料庫執行下列查詢，以計算來自每個反向連結管道的使用者人數：

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果看起來像這樣：

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 轉介 | 55 |
| 其他 | 16 |

這很有趣，但用途有限。 您真正想知道的是：

* 這些數字隨時間的增長率
* 各收購來源產生的收入金額
* a [同類群組分析](https://en.wikipedia.org/wiki/Cohort_analysis) 來自每個來源的使用者
* 其中一個管道的使用者日後回訪客戶的可能性。

執行這些分析所需的查詢很複雜。 利用這些資訊，您可以確定最有利可圖的收購渠道，並據此將行銷時間和資金集中在一起。

### 相關

* **[探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)**
* **[連接您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)**
* **[提高廣告宣傳的投資報酬率](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM歸因功能是否正常？](../analysis/utm-attributes.md)**
