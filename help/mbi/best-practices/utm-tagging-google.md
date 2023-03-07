---
title: UTM追蹤Google Analytics
description: 了解Google Analytics中UTM追蹤（標籤）的最佳作法。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# UTM追蹤

`UTM` 追蹤是URL的標籤慣例，可讓您分析使用者來自何處。 如果您查看大部分行銷電子郵件或橫幅廣告中所點按的URL，則會看到UTM標籤。 就是那些長的連結，結尾是 `utm\_source` 和 `utm\_medium`.

[!DNL Google Analytics] uses `UTM` 標籤以知道流量來自何處。 部分資訊來自 [HTTP反向連結](https://en.wikipedia.org/wiki/HTTP_referer) 但其餘的你必須給自己 `UTM` 參數。 當您看到 `google adwords` 或 `email marketing`，這表示 `UTM` 從原始連結點按記錄的參數，然後儲存在使用者的cookie中。 從那裡， [!DNL Google Analytics] 使用資料 [屬性感興趣的行為](../data-analyst/analysis/google-track-user-acq.md) 在您的網站上。 了解這些參數的用途有助於您了解如何最有效地設定和使用UTM標籤。

## UTM標籤最佳作法

下列列出在設定URL時應記住的5項最重要事項 `UTM` 標籤。

### 1.目標是標籤每個可控制來到您網站的URL

每次您要求使用者點按連結時，應先設定 `UTM` 標籤。 這包括您的所有電子郵件連結（您的電子郵件服務提供者可能有自動標籤URL的方式）、廣告連結、新聞文章、部落格文章。

### 2.使用工具建立URL

`UTM` — 標籤的URL可能很麻煩。 請使用工具，而不要長時間輸入 [如此](https://support.google.com/analytics/answer/1033867?hl=en) 來幫你。 這可確保您考慮將所有合理參數新增至URL，並立即取得要複製貼上的URL。 若要管理社交連結，工具如 [!DNL Hootsuite] 納入將自訂URL參數新增至所有連結的選項。

### 3.請務必在參數值中區分大小寫

請務必記住標籤 `utm\_source=adwords` 是與 `utm\_source=Adwords`. 請考慮讓一切都變小寫。

### 4.將UTM參數值儲存在資料庫中

每次發生交易或事件時，您都要評估行銷活動的績效。 您可以從 [[!DNL Google Analytics] cookie到資料庫](../data-analyst/analysis/google-track-user-acq.md).

### 5.思考如何為行銷活動命名

為了追蹤您的行銷工作隨著時間而改善的情形，您必須謹慎處理您的命名慣例。 保持簡單，盡可能減少。 複雜的命名系統更難維護。

一旦您在資料庫中擷取此資料，您就可以透過更複雜的分析來評估行銷和廣告的效能，包括 [客戶期限值](../data-analyst/analysis/ess-expected-ltv.md), [重複購買率](../data-analyst/analysis/repurchase-behavior.md)，和 [平均訂購值](../data-analyst/analysis/basic-analytics.md).
