---
title: 優化資料庫以進行分析
description: 了解如何最佳化資料庫以進行分析。
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# 優化資料庫

將操作資料庫用於業務智慧的主要好處是，不需要建立或修改任何內容來收集資料。 寶貴的資訊已經存在；你只需解鎖它。

本主題包含一些建議，可協助您最佳化資料庫以進行分析，並從原始資料中取得可操作的深入分析。

## 請勿刪除資料

>[!TIP]
>
>影響您的業務（以及您自己的服務條款）的當地和國際法律可能會影響您可以保留的資料類型，以及您可以保留資料的時間。 您應優先遵守這些法律。

取消訂單、使用者停用其帳戶或產品停產時，很容易刪除資料庫中的相關資訊。 桌子越來越多，消除凌亂似乎是一個謹慎的想法。 但是，刪除行意味著此資訊將永遠丟失，或者您需要挖掘舊備份才能找到它。

反之，您可以將狀態欄新增至表格，指出該列何時不再使用或不再相關。 也建議您新增欄來儲存進行變更的日期，或建立歷史變更的記錄。 如果表的規模已經足夠大，效能開始下降，請考慮將舊資料歸檔到用於分析的表中。

## 很少覆寫資料

覆寫資料時應謹慎謹慎。

以登入日期為例，許多公司會儲存上次登入日期，而非歷史登入表格。 雖然您可能只需要上次登入日期才能正常運作，但從分析角度來看，覆寫資料會造成重大損失。 若不保留這些動作的完整記錄，便無法查看有多少使用者長時間離開並重新啟動。 這也使得您無法根據登入建立使用者參與同類群組分析等項目。

通常，如果您因某種用戶操作而更新記錄，請勿覆蓋先前或單獨用戶操作的相關資訊。

## 包括 `Updated_at` 隨時間更新的資料欄

如果表格的列會隨著時間而改變值，例如 **order\_status** 變更`processing` to `complete`，納入 **已更新\_at** 欄以記錄最新變更的發生時間。 確保 **已更新\_at** 值會在首次插入新資料列時(當 **已更新\_at** 日期對應至 **已建立\_at** 日期。

除了優化分析外， **已更新\_at** 欄也可讓您使用 [增量複製方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)，有助於縮短更新週期。

## 儲存用戶贏取源

最常見的錯誤之一是 [使用者贏取來源](../data-analyst/analysis/google-track-user-acq.md) (UAS)未儲存在操作資料庫中。 在多數情況下，如果發生問題，系統只會透過 [!DNL Google Analytics] 或其他網頁分析工具。 雖然這些工具可能很有價值，但將UAS專門儲存在它們中也有一些缺點；例如，您無法從這些工具中擷取使用者層級資料。 如果有可能，通常是一個困難的過程。 您應該可以輕鬆取得這些資訊，並將其與其他來源的資料（例如也儲存在資料庫中的行為和交易資訊）結合。

將UAS儲存在您自己的資料庫中通常是線上業務對其分析能力所能帶來的最大改進。 這可讓您依UAS分析銷售、使用者參與、回報期、客戶期限值、流失率和其他關鍵量度。 [在決定要將行銷資源投資於何處時，此資料至關重要](../data-analyst/analysis/most-value-source-channel.md).

太多公司只專注於尋找以最低成本提供新使用者的管道。 如果您沒有追蹤從每個管道取得的使用者品質，便有可能吸引未產生商業價值的使用者。

## 資料表設定

### 設定主鍵

A [主鍵](https://en.wikipedia.org/wiki/Unique_key) 是不會改變的列（或一組列），在表內生成唯一值。 主鍵非常重要，因為它們確保在 [!DNL MBI].

建立主索引鍵時，對自動增加的欄使用整數資料類型。 Adobe建議您盡可能避免使用多列主鍵。

如果表是SQL視圖，請添加可作為主鍵的列。 [!DNL MBI] 會自動將此欄識別為主索引鍵。

### 將資料類型指派給資料欄

如果資料欄未指派 [資料類型](https://en.wikipedia.org/wiki/Data_type), [!DNL MBI] 猜測要使用的資料類型。 如果系統猜錯了，則在Adobe支援團隊將列調整為適當的資料類型之前，您可能無法執行相關分析。 例如，如果日期欄被猜為數值資料類型，您可以使用該日期維度來分析一段時間的趨勢。

### 如果您有多個資料庫，請將前置詞添加到資料表中

如果連接了多個資料庫 [!DNL MBI],Adobe建議您將前置詞新增至表格，以避免混淆。 前置詞可協助您記住量度或資料維度的來源位置。
