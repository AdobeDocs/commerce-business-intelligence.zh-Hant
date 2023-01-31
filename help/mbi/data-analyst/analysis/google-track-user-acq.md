---
title: Google Analytics — 追蹤使用者贏取來源資料概觀
description: 了解如何依使用者贏取來源劃分資料。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# 依使用者贏取來源劃分

>[!NOTE]
>
>以下流程不支援 [!DNL GoogleUniversal Analytics].

依使用者贏取來源劃分資料的能力，對於有效管理行銷計畫至關重要。 了解新使用者的贏取來源，可顯示哪些管道可產生最高的回報，並讓您的團隊有信心分配行銷資金。

如果您尚未在資料庫中追蹤使用者贏取來源， [!DNL MBI] 可協助您開始使用：

## 追蹤使用者贏取來源

建議您根據您的設定，使用兩種方法來追蹤反向連結來源資料：

### （選項1）透過 [!DNL Google Analytics E-Commerce] (包括 [!DNL Shopify] 商店)

如果您利用 [!DNL Google Analytics E-Commerce] 要跟蹤訂單和銷售資料，您可以利用 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 同步每個訂單的轉介來源資料。 這可讓您依反向連結來源(例如 `utm_source` 或 `utm_medium`)，並透過 [!DNL MBI] 自訂維度，例如 `User's first order source`.

>[!NOTE]
>
>Shopify用戶**:開啟 [!DNL [Google Analytics E-Commerce] tracking in Shopify](http://docs.shopify.com/manual/settings/general/google-analytics#ecommerce-tracking) 在連接 [!DNL Google Analytics E-Commerce] 帳戶 [!DNL MBI].

### （選項2）保存 [!DNL Google Analytics]&#39;資料庫中的贏取源資料

在本文中，我們將說明如何儲存 [!DNL Google Analytics] 贏取管道資訊放入您自己的資料庫 — 即 `source`, `medium`, `term`, `content`, `campaign`，和 `gclid` 使用者首次造訪您的網站時所呈現的參數。 如需這些參數的說明，請查看 [!DNL [Google Analytics] documentation](http://support.google.com/analytics/bin/answer.py?hl=en&amp;answer=1191184). 接著，我們將探索一些功能強大的行銷分析，這些分析可透過 [!DNL MBI].

#### 為什麼？

如果您只是查看預設值 [!DNL Google Analytics] 轉換和贏取量度，則無法獲得完整圖景。 雖然自然搜尋與付費搜尋的轉換次數相當有趣，但您可以利用這些資訊做什麼？ 你應該花更多錢搜索付費嗎？ 這取決於來自該管道的客戶價值，而這不是Google Analytics提供的。

>[!NOTE]
>
>[!DNL [Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) 將交易資料儲存在 [!DNL Google Analytics]，但此解決方案不適用於非電子商務網站，且某些工具（例如同類群組分析）在 [!DNL Google Analytics] 介面。

如果您想要將後續交易電子郵件傳送給從特定電子郵件行銷活動取得的所有客戶，該怎麼辦？ 還是將贏取資料與您的CRM系統整合？ 在 [!DNL Google Analytics]  — 事實上，這違反服務條款 [!DNL Google Analytics] 儲存可識別個人的任何資料。  但這並不意味著你不能自己儲存這些資料。

#### 方法

[!DNL Google Analytics] 將訪客反向連結資訊儲存在名為的Cookie中 `__utmz`. 設定此Cookie後(由 [!DNL Google Analytics] 追蹤程式碼)，其內容將會與該使用者向您的網域提出的每個後續請求一併傳送。 例如，在PHP中，您可以檢查 `$_COOKIE['__utmz']` 你會看到一串類似這樣的字串：

> `100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

顯然有些贏取來源資料已編碼至字串，我們經過測試以確認這是訪客的最新贏取來源和相關促銷活動資料。 現在我們只需要知道如何提取資料。 幸運的是，Justin Cutroni先前已描述此編碼的運作方式，並共用了一些javascript代碼來擷取關鍵資訊的比特。

我們把代碼翻譯成 [托管於github的PHP程式庫](https://github.com/RJMetrics/referral-grabber-php).   若要使用程式庫， `include` 參考 `ReferralGrabber.php` 然後呼叫

> `$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

傳回 `$data` 陣列是鍵的映射 `source`, `medium`, `term`, `content`, `campaign`, `gclid` 和各自的值。

建議將新表格新增至您的資料庫，例如 `user_referral`，包含下列欄： `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. 每當使用者登入時，請抓取反向連結資訊並儲存至此表格。

#### 如何使用此資料

現在我們正在儲存使用者贏取來源，該如何使用？

假設我們使用SQL資料庫，且 `users` 表格，其結構如下：

| ID | 電子郵件 | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有機 |
| 2 | jim@abc.com | 2012-01-24 | google | cp |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | 轉介 | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | 其他 | 有機 |
| ... | ... | ... | ... | ... |

首先，我們可以對您的資料庫執行下列查詢，以計算來自每個反向連結管道的使用者人數：

> `SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果會如下所示：

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| 轉介 | 55 |
| 其他 | 16 |

這很有趣，但用途有限。 我們真正想知道的是這些數字隨著時間的增長，每個收購來源產生的收入， [同類群組分析](http://cohortanalysis.com/) 來自每個來源的使用者數，以及其中一個管道的使用者日後以客戶身分回訪的可能性。 執行這些分析所需的查詢是複雜的，這是我們建立 [!DNL MBI]. 有了這些資訊，我們可以確定最有利可圖的收購渠道，並相應地集中我們的營銷時間和資金。

### 相關

* **[在資料庫中追蹤使用者裝置、瀏覽器和作業系統資料](https://support.magento.com/hc/en-us/articles/360016732911)**
* **[探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)**
* **[連接您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)**
* **[提高廣告宣傳的投資報酬率](../analysis/roi-ad-camp.md)**
* **[如何 [!DNL Google Analytics] UTM歸因功能是否正常？](../analysis/utm-attributes.md)**
