---
title: Google Analytics中的UTM追蹤
description: 瞭解Google Analytics中UTM追蹤（標籤）的最佳實務。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# UTM追蹤

`UTM`追蹤是URL的標籤慣例，可讓您分析使用者的來源。 如果您檢視您從大多數行銷電子郵件或橫幅廣告點按的URL，您會看到UTM標籤。 是那些以`utm\_source`和`utm\_medium`之類的結尾的長連結。

[!DNL Google Analytics]使用`UTM`標籤來知道您的流量來自何處。 部分資訊來自[HTTP反向連結](https://en.wikipedia.org/wiki/HTTP_referer)，但其餘的資訊必須提供`UTM`引數給您自己。 當您看到`google adwords`或`email marketing`時，這表示這些`UTM`引數是從原始連結點選記錄下來，然後儲存在使用者的Cookie中。 從那裡，[!DNL Google Analytics]會使用該資料來[將您網站上的有趣行為](../data-analyst/analysis/google-track-user-acq.md)歸因。 瞭解這些引數的用途可協助您瞭解如何以最佳方式設定及使用UTM標籤。

## UTM標籤的最佳作法

以下列出使用`UTM`標籤設定您的URL時應記住的五個最重要事項。

### 1.請務必標籤您可以控制的所有網站URL

每次要求人員按一下連結時，您都應該設定`UTM`標籤。 這包括您的所有電子郵件連結（您的電子郵件服務供應商可能會自動標籤您的URL）、廣告連結、新聞文章、部落格。

### 2.使用工具建立URL

`UTM`標籤的URL可能很麻煩。 不要嘗試輸入長整數，請使用類似此[&#128279;](https://support.google.com/analytics/answer/1033867?hl=en)的工具來協助您。 這可確保您考慮將所有合理的引數新增到URL中，並且讓URL直接從其中複製貼上。 若要管理社交連結，[!DNL Hootsuite]等工具包含將自訂URL引數新增至所有連結的選項。

### 3.請確定引數值區分大小寫

請務必記住，標籤`utm\_source=adwords`與`utm\_source=Adwords`是不同的標籤。 考慮將所有內容變為小寫。

### 4.將UTM引數值儲存在資料庫中

每次發生交易或事件時，您都要評估行銷活動的效能。 您可以從[[!DNL Google Analytics] Cookie將UTM引數值的值讀入資料庫](../data-analyst/analysis/google-track-user-acq.md)來執行此操作。

### 5.思考如何為行銷活動命名

若要追蹤您的行銷活動如何隨著時間改善，您需要對命名慣例保持聰明。 保持簡單，並儘可能最小化。 複雜的命名系統較難維護。

在資料庫中擷取此資料後，您可以透過更複雜的分析來評估行銷和廣告的效能，包括[客戶期限值](../data-analyst/analysis/ess-expected-ltv.md)、[重複購買率](../data-analyst/analysis/repurchase-behavior.md)和[平均訂單值](../data-analyst/analysis/basic-analytics.md)。
