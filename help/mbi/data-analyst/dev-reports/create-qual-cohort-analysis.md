---
title: 建立定性隊列分析
description: 瞭解一個定性群體是什麼，你為什麼可能對構建這種分析感興趣，以及如何在Commerce Intelligence中建立它。
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 建立 `Qualitative Cohort Analysis`

你知道 [!DNL Google Adwords] — 購買的客戶群與從有機搜索中購買的客戶相比，增加了他們的LTV? 你有沒有想過 `cohort` 是否在同一報告中並排分析不同客戶細分市場？ 如果是，a `qualitative cohort analysis` 幫助你回答這些問題。

這個主題深入闡述了質的群體是什麼，你為什麼可能對構建這個分析感興趣，以及你如何在 [!DNL Commerce Intelligence]。

## 什麼是 `qualitative cohorts`不管怎樣？ {#whatare}

`Cohort` 分析一般可以廣義地定義為對在其生命週期中具有相似特徵的用戶組的分析。 它允許您識別不同用戶組的行為趨勢。

請參閱 [隊列分析](https://www.cohortanalysis.com/)。

最多 `cohort` 分析 [!DNL Commerce Intelligence] 按公用日期將用戶分組在一起（例如，在給定月份首次購買的所有客戶集）。 A `qualitative cohort` 有點不同：它是由不基於時間的特徵定義的用戶組。 示例包括：

* 從廣告活動獲取的所有用戶集
* 第一次購買時包括優惠券（或沒有）的所有用戶集
* 特定年齡的所有用戶集

## 這和正常情況有什麼不同 `cohort` 建築師？ {#different}

的 [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) 使用基於時間的特徵對分組組合進行優化。 這非常適用於針對特定用戶段（例如，通過付費搜索市場活動獲得的所有用戶）的分析。 在 `Cohort Analysis Builder`，可以(1)關注該特定用戶組，和(2) `cohort` 日期（如他們的首次訂單日期）。

但是，如果要分析同一隊列報告中多個用戶段的隊列行為(`paid` 搜索 `organic` 搜索與直接通信，可能？)，可以在 `Report Builder`。

## 我應發送哪些資訊以支援設定分析？ {#support}

建立 `qualitative cohort` 報告 `Report Builder` 涉及Adobe分析團隊建立 [高級計算列](../data-warehouse-mgr/creating-calculated-columns.md) 在必要的桌子上。

要構建這些，請提交 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （並參考本文！） 以下是您需要瞭解的：

* 的 `metric` 您想使用及使用什麼表來執行隊列分析(例如： `Revenue`，在 `orders` )的正平方根。

* 的 `user segments` 您希望定義該資訊並將其放在資料庫中的位置(例如：不同值 `User's referral source`，本機 `users` 然後重新定位到 `orders`)。

* 的 `cohort date` 要使用分析(例如：這樣 `User's first order date` 時間戳)。 此示例允許我們查看每個段並詢問 `How does a user's revenue grow in the months following their first order date?`。

* 的 `time interval` 要查看的分析(例如： `weeks`。 `months`或 `quarters` 在 `User's first order date`)。

一旦Adobe分析團隊響應了上述問題，您就有幾個新的高級計算列來構建報告！ 然後，您可以按照以下指示執行此操作。

## 建立定性隊列分析 {#create}

首先，您希望添加您感興趣的度量，每個 `cohort` 你在分析。 在此示例中，您要查看累積 `Revenue` 在客戶第一次訂單後的幾個月內完成， `User's referral source`。 這意味著，對於每個段，您都添加一個 `Revenue` 特定段的度量和篩選：

![](../../assets/qualcohort1.gif)

其次，應對報告的時間選項進行兩項更改：

1. 設定 `time interval` 至 `None`。 這是因為您最終將時間間隔分組為維，而不是使用通常的時間選項。

1. 設定 `time range` 到您希望報告覆蓋的時間窗口。

在本例中，您看到 `all time` 視圖 `Revenue`。 在此之後，你最後應該看到一串點：

![](../../assets/qualcohort2.gif)

第三，調整以設定 `cohorts`。 基於 `cohort date` 和 `time interval` 您指定給Adobe分析師團隊的維，您的帳戶中有一個維 `cohort` 約會。 在本示例中，該自定義維稱為 `Months between this order and customer's first order date`。 使用此維時，應：

* `Group by` 具有 `group by` 選項

* 選擇 `dimension` 你感興趣的

* 使用 `Show top/bottom option`，選擇您感興趣的前X個月，並按 `Months between this order and customer's first order date` 尺寸

現在，你可以看到每條線 `cohort` 你指定的。 現在查看示例 — 您看到 `Revenue` 由每個推薦來源的用戶提供， `grouped by` 第一個訂單和任何後續訂單之間的月數。 該示例還添加了 `Cumulative perspective` 查看 `cohorts'` 聚合增長 — 查看結果表以瞭解更細的粒度。

這告訴我們什麼？ 這裡，具體的推薦來源 `Paid search` 在客戶購買生命週期的第一個月中很有價值，但無法以重複的收入保留其客戶群。 同時 `Direct Traffic` 從較低金額開始，隨後幾個月的收入實際上以類似的速度累積。

不管你怎麼切， `cohort` 分析是分析工具箱中的強大工具。 此類分析可為您的業務提供一些有趣的見解，傳統 `time-based cohorts` 可能不會，使您能夠做出更好的資料驅動決策。
