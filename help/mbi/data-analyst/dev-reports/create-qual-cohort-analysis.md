---
title: 建立質化同類群組分析
description: 瞭解什麼是質化同類群組、您為什麼可能有興趣建立此分析，以及如何在Commerce Intelligence中建立它。
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 建立 `Qualitative Cohort Analysis`

您知道您如何 [!DNL Google Adwords] — 相較於從有機搜尋取得的客戶，收購的客戶區段的LTV是否有所增加？ 您是否曾考慮過執行 `cohort` 在相同報表中以並排方式分析不同客戶區段？ 若是如此，則 `qualitative cohort analysis` 可協助您回答這些問題。

本主題將深入探討什麼是質化同類群組，您為何對建立此分析感興趣，以及如何在中建立它 [!DNL Commerce Intelligence].

## 什麼是 `qualitative cohorts`，仍然？ {#whatare}

`Cohort` 一般而言，分析可廣義地定義為分析在其生命週期內具有類似特性的使用者群組。 它可讓您識別不同使用者群組中的行為趨勢。

另請參閱 [同類群組分析](https://www.cohortanalysis.com/).

最多 `cohort` 分析 [!DNL Commerce Intelligence] 依共同日期將使用者分組（例如，指定月份中首次購買的所有客戶集）。 A `qualitative cohort` 有點不同：這是由非時間型特性所定義的使用者群組。 例如：

* 從廣告行銷活動取得的所有使用者集
* 首次購買包含優惠券（或未包含）的所有使用者集
* 屬於特定年齡段的所有使用者集

## 這跟正常有什麼不同 `cohort` 產生器？ {#different}

此 [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) 已使用時間型特性對同類群組進行最佳化。 這非常適合用於針對特定使用者區段進行分析（例如，透過付費搜尋行銷活動取得的所有使用者）。 在 `Cohort Analysis Builder`，您可以(1)聚焦於該特定使用者群組，以及(2) `cohort` 日期（如其第一個訂購日期）。

不過，如果您想要分析相同同類群組報表中多個使用者區段的同類群組行為(`paid` 搜尋與 `organic` 搜尋與直接流量比較)，以下專案可建構此更進階的分析： `Report Builder`.

## 我應該傳送哪些資訊給支援以設定我的分析？ {#support}

建立 `qualitative cohort` 中的報告 `Report Builder` 涉及Adobe分析團隊建立一些 [進階計算欄](../data-warehouse-mgr/creating-calculated-columns.md) 在必要的表格上。

若要建置這些專案，請提交 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （請參考本文章！）。 以下是您需要瞭解的事項：

* 此 `metric` 您要使用及其使用的表格執行同類群組分析(例如： `Revenue`，建立在 `orders` 表格)。

* 此 `user segments` 您想要定義該資訊在資料庫中的存留位置(範例：不同的值 `User's referral source`，原生 `users` 資料表，並已重新定位至 `orders`)。

* 此 `cohort date` 您希望您的分析使用(例如： `User's first order date` timestamp)。 此範例可讓我們檢視每個區段並詢問 `How does a user's revenue grow in the months following their first order date?`.

* 此 `time interval` 您希望透過它檢視分析(例如： `weeks`， `months`，或 `quarters` 在 `User's first order date`)。

Adobe分析團隊對上述內容做出回應後，您就會有一些新的進階計算欄來建置您的報表！ 然後，您可以按照以下說明執行此操作。

## 建立質化同類群組分析 {#create}

首先，您想要新增您感興趣的量度同類群組，針對每個同類群組新增一次 `cohort` 您正在分析。 在此範例中，您想要檢視累積 `Revenue` 在客戶首次訂購後的幾個月內完成，並以 `User's referral source`. 這表示您要為每個區段新增一個 `Revenue` 特定區段的量度和篩選器：

![](../../assets/qualcohort1.gif)

第二，您應該對報表的時間選項進行兩項變更：

1. 設定 `time interval` 至 `None`. 這是因為您最後會依時間間隔分組為維度，而不使用一般的時間選項。

1. 設定 `time range` 至您要報告涵蓋的時間範圍。

在此範例中，您會檢視 `all time` 檢視 `Revenue`. 接著，您應該會看到一連串的點：

![](../../assets/qualcohort2.gif)

第三，您可以調整以設定 `cohorts`. 根據 `cohort date` 和 `time interval` 您指定給Adobe分析人員團隊，您的帳戶中有一個維度可執行 `cohort` 約會。 在此範例中，該自訂維度稱為 `Months between this order and customer's first order date`. 使用此維度，您應該：

* `Group by` 具有的維度 `group by` 選項

* 選取所有值 `dimension` 您感興趣的

* 使用 `Show top/bottom option`，選取您感興趣的前X個月，並依 `Months between this order and customer's first order date` 維度

現在，您可以為每個欄位顯示一行 `cohort` 您所指定的。 立即檢視範例 — 您會看到 `Revenue` 由每個反向連結來源的使用者所貢獻， `grouped by` 第一筆訂單與任何後續訂單之間的月數。 此範例也新增了 `Cumulative perspective` 以檢視 `cohorts'` 彙總成長 — 檢視結果表格以取得詳細程度。

這告訴我們什麼？ 在此，特定的反向連結來源 `Paid search` 在客戶購買期限的第一個月很有價值，但無法透過重複收入保留其客戶群。 當 `Direct Traffic` 開始時數額較低，實際上隨後幾個月的收入會以類似的速度累積。

無論您如何選擇， `cohort` analysis是分析工具箱中的強大工具。 此類分析可產生一些關於您企業的有趣見解，這些見解 `time-based cohorts` 但也可能不會，讓您能夠做出更好的資料導向式決策。
