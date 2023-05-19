---
title: UTM跟蹤Google Analytics
description: 瞭解Google Analytics中UTM跟蹤（標籤）的最佳做法。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM跟蹤

`UTM` 跟蹤是URL的標籤約定，使您能夠分析用戶來自何處。 如果查看從大多數營銷電子郵件或橫幅廣告中按一下的URL，則會看到UTM標籤。 是那些長的聯繫，以這樣的東西結束 `utm\_source` 和 `utm\_medium`。

[!DNL Google Analytics] 使用 `UTM` 標籤以瞭解您的流量來自何處。 其中一些資訊來自 [HTTP引用者](https://en.wikipedia.org/wiki/HTTP_referer) 但其餘的你必須給自己 `UTM` 參數。 當你看到 `google adwords` 或 `email marketing`是指 `UTM` 從原始連結中記錄的參數按一下，然後儲存在用戶的cookie中。 從那裡， [!DNL Google Analytics] 使用資料 [屬性有趣行為](../data-analyst/analysis/google-track-user-acq.md) 在你的網站上。 瞭解這些參數的用途有助於您瞭解如何最好地設定和使用UTM標籤。

## UTM標籤的最佳做法

下面列出了在設定URL時要記住的五項最重要的內容 `UTM` 標籤。

### 1。目標是標籤每個您可以控制的URL，以訪問您的站點

每次您要求人員按一下連結時，應設定 `UTM` 標籤。 這包括您的所有電子郵件連結（您的電子郵件服務提供商可能有一種方法自動為URL添加標籤）、廣告連結、新聞文章、部落格帖子。

### 2.使用工具建立URL

`UTM`-tagged URL可能很麻煩。 不要嘗試長時間鍵入它們，請使用工具 [像](https://support.google.com/analytics/answer/1033867?hl=en) 來幫你。 這可確保您考慮將所有合理參數添加到URL，並從中獲得要複製貼上的URL。 要管理社交連結，工具如 [!DNL Hootsuite] 包括將自定義URL參數添加到所有連結的選項。

### 3.確保參數值區分大小寫

記住標籤很重要 `utm\_source=adwords` 與 `utm\_source=Adwords`。 考慮把所有事情都變小。

### 4.將UTM參數值儲存在資料庫中

每次發生交易或事件時，您都要評估市場營銷活動的績效。 通過從 [[!DNL Google Analytics] 將Cookie儲存到資料庫](../data-analyst/analysis/google-track-user-acq.md)。

### 5.想想你如何命名市場活動

為了跟蹤營銷工作如何隨著時間推移而改善，您需要對命名慣例保持謹慎。 保持簡單，盡可能小。 複雜的命名系統更難維護。

一旦您在資料庫中捕獲此資料，您就可以通過更複雜的分析來評估您的營銷和廣告的效能，包括 [客戶生存期價值](../data-analyst/analysis/ess-expected-ltv.md)。 [重複採購費率](../data-analyst/analysis/repurchase-behavior.md), [平均訂單值](../data-analyst/analysis/basic-analytics.md)。
