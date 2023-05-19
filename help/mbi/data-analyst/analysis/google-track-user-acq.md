---
title: Google Analytics — 跟蹤用戶獲取源資料概覽
description: 瞭解如何按用戶獲取源分段資料。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: af1e3839839b4c419beabb0cc666c996ea2179d4
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# 按用戶獲取源分段

>[!NOTE]
>
>以下過程不支援 [!DNL Google Universal Analytics]。

能夠按用戶獲取來源對資料進行分段對於有效管理營銷計畫至關重要。 瞭解新用戶的購買來源可以顯示哪些渠道可以獲得最高的回報，並使您的團隊能夠放心地分配營銷資金。

如果您尚未跟蹤資料庫中的用戶獲取源， [!DNL Adobe Commerce Intelligence] 可以幫助您開始：

## 跟蹤用戶獲取源

[!DNL Adobe] 建議使用兩種方法根據設定跟蹤參考源資料：

### （選項1）通過以下方式跟蹤訂單推薦源資料： [!DNL Google Analytics E-Commerce] (包括 [!DNL Shopify] 商店)

如果您使用 [!DNL Google Analytics E-Commerce] 要跟蹤訂單和銷售資料，您可以 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 同步每個訂單的引用源資料。 這允許您按推薦來源劃分收入和訂單(例如， `utm_source` 或 `utm_medium`)。 您還可以通過以下方式瞭解客戶購買來源： [!DNL Commerce Intelligence] 自定義維，如 `User's first order source`。

>[!NOTE]
>
>**對於Shopify用戶**:開啟 [!DNL [Google Analytics E-Commerce] tracking in Shopify](https://help.shopify.com/en/manual/reports-and-analytics/google-analytics#ecommerce-tracking) 在連接 [!DNL Google Analytics E-Commerce] 帳戶 [!DNL Commerce Intelligence]。

### （選項2）保存 [!DNL Google Analytics]&#39;在資料庫中獲取源資料

本主題說明如何保存 [!DNL Google Analytics] 獲取渠道資訊到您自己的資料庫 — 即 `source`。 `medium`。 `term`。 `content`。 `campaign`, `gclid` 在用戶首次訪問您的網站時顯示的參數。 有關這些參數的說明，請 [!DNL [Google Analytics] documentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article)。 然後，您將探索一些功能強大的營銷分析，這些分析可以在 [!DNL Commerce Intelligence]。

#### 為什麼？

如果您只是查看預設 [!DNL Google Analytics] 轉換和獲取度量，你無法得到整幅圖。 雖然看到從有機搜索到付費搜索的轉換次數非常有趣，但您可以如何處理這些資訊？ 你應該花更多錢在付費搜索上嗎？ 這取決於來自該渠道的客戶的價值，而這不是Google Analytics提供的。

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 通過將事務資料儲存在 [!DNL Google Analytics]，但此解決方案不適用於非電子商務站點。 此外，某些工具，如隊列分析，在 [!DNL Google Analytics] 。

如果您要將後續交易通過電子郵件發送給從特定電子郵件活動中獲得的所有客戶，該怎麼辦？ 還是將採集資料與您的CRM系統整合？ 這在 [!DNL Google Analytics]  — 事實上，此舉違反 [!DNL Google Analytics] 儲存標識個人的任何資料。 但是，你可以自己儲存這些資料。

#### 方法

[!DNL Google Analytics] 將訪問者推薦資訊儲存在名為 `__utmz`。 設定此cookie後(由 [!DNL Google Analytics] 跟蹤代碼)，其內容將隨後從該用戶向您的域發送每個請求。 例如，在PHP中，您可以檢查 `$_COOKIE['__utmz']` 你會看到一個類似的字串：

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

顯然有一些採集源資料被編碼到字串中。 測試此資訊以確認這是訪問者的最新獲取來源和相關市場活動資料。 現在你需要知道如何提取資料。

此代碼已轉換為 [在github上承載的PHP庫](https://github.com/RJMetrics/referral-grabber-php)。 要使用庫， `include` 引用 `ReferralGrabber.php` 然後打

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返回 `$data` 陣列是鍵的映射 `source`。 `medium`。 `term`。 `content`。 `campaign`。 `gclid`，以及它們各自的值。

[!DNL Adobe] 建議將表添加到資料庫，例如， `user_referral`，其中列如下： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`。 每當用戶註冊時，請獲取推薦資訊並將其儲存到此表中。

#### 如何使用此資料

現在您正在保存用戶獲取源，如何使用它？

假設您使用SQL資料庫，並且 `users` 具有以下結構的表：

| ID | 電子郵件 | 聯接日期 | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | 谷歌 | 有機 |
| 2 | jim@abc.com | 2012-01-24 | 谷歌 | 黨 |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 推薦 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有機 |
| ... | ... | ... | ... | ... |

首先，您可以對資料庫運行以下查詢來計算每個推薦渠道的用戶數：

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果大致如下：

| ACQ_SOURCE | 用戶計數 |
|--- |--- |
| 谷歌 | 294 |
| 直接 | 156 |
| 推薦 | 55 |
| 其他 | 16 |

這很有趣，但用途有限。 你最想知道的是：

* 這些數字隨時間推移的增長率
* 各收購來源產生的收入金額
* a [隊列分析](https://en.wikipedia.org/wiki/Cohort_analysis) 來自每個源的用戶
* 其中一個渠道的用戶將來作為客戶返回的可能性。

執行這些分析所需的查詢很複雜。 利用這些資訊，您可以確定最有利可圖的收購渠道，並相應地集中營銷時間和資金。

### 相關

* **[發現您最有價值的收購來源和渠道](../analysis/most-value-source-channel.md)**
* **[連接 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)**
* **[提高廣告活動的ROI](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM歸因工作？](../analysis/utm-attributes.md)**
