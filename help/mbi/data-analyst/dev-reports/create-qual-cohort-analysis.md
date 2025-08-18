---
title: 建立質化同類群組分析
description: 瞭解什麼是質化同類群組、您為什麼可能有興趣建立此分析，以及如何在Commerce Intelligence中建立它。
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# 建立`Qualitative Cohort Analysis`

您知道與透過有機搜尋取得的客戶相比，您取得[!DNL Google Adwords]的客戶區段的LTV成長方式嗎？ 您是否曾考慮在相同報表中並排執行不同客戶區段的`cohort`分析？ 若是如此，`qualitative cohort analysis`可協助您回答這些問題。

此主題深入探討什麼是質化同類群組、您為何可能想要建立此分析，以及如何在[!DNL Commerce Intelligence]中建立此分析。

## 什麼是`qualitative cohorts`？ {#whatare}

一般來說，`Cohort`分析可廣義地定義為在其生命週期內具有類似特性的使用者群組的分析。 它可讓您識別不同使用者群組中的行為趨勢。

請參閱[同類群組分析](https://www.cohortanalysis.com/)。

大部分`cohort`會依共同日期將[!DNL Commerce Intelligence]個使用者分組分析（例如，指定月份中首次購買的所有客戶集）。 `qualitative cohort`有些不同：它是由非以時間為基準的特性所定義的使用者群組。 例如：

* 從廣告行銷活動取得的所有使用者集
* 首次購買包含優惠券（或未包含）的所有使用者集
* 屬於特定年齡段的所有使用者集

## 這跟一般的`cohort`產生器有何不同？ {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md)已針對使用以時間為基準的特性來分組同類群組而最佳化。 這非常適合用於針對特定使用者區段進行分析（例如，透過付費搜尋行銷活動取得的所有使用者）。 在`Cohort Analysis Builder`中，您可以(1)聚焦於該特定使用者群組，並(2)在日期（如其第一筆訂購日期）專注`cohort`。

不過，如果您想要分析相同同類群組報告中多個使用者區段的同類群組行為（`paid`搜尋與`organic`搜尋的比較或直接流量？），可在`Report Builder`中建構此更進階的分析。

## 我應該傳送哪些資訊給支援以設定我的分析？ {#support}

在`qualitative cohort`中建立`Report Builder`報告時，Adobe分析團隊會在必要的資料表上建立一些[進階計算資料行](../data-warehouse-mgr/creating-calculated-columns.md)。

若要建置這些專案，請提交[支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant) （並參考此文章！）。 以下是您需要瞭解的事項：

* 您要使用執行同類群組分析的`metric`及其使用的表格（範例： `Revenue`，建置在`orders`表格上）。

* 您要定義的`user segments`以及該資訊在資料庫中的存放位置（範例： `User's referral source`的不同值，原生於`users`資料表，並移至`orders`）。

* 您想要分析使用的`cohort date` （範例： `User's first order date`時間戳記）。 此範例可讓我們檢視每個區段並詢問`How does a user's revenue grow in the months following their first order date?`。

* 您想要檢視分析的`time interval` （範例： `weeks`、`months`或`quarters`之後的`User's first order date`）。

Adobe分析團隊回應上述要求後，您就會有一些新的進階計算欄來建置您的報表！ 然後，您可以按照以下說明執行此操作。

## 建立質化同類群組分析 {#create}

首先，您想要新增您想要加入同類群組的量度，針對您正在分析的每個`cohort`新增一次。 在此範例中，您想要檢視在客戶第一筆訂單後幾個月內完成的累積`Revenue` （以`User's referral source`分段）。 這表示您會為每個區段新增一個`Revenue`量度，並針對特定區段進行篩選：

![](../../assets/qualcohort1.gif)

第二，您應該對報表的時間選項進行兩項變更：

1. 將`time interval`設為`None`。 這是因為您最後會依時間間隔分組為維度，而不使用一般的時間選項。

1. 將`time range`設為報告涵蓋的時間範圍。

在此範例中，您檢視了`all time`的`Revenue`檢視。 接著，您應該會看到一連串的點：

![](../../assets/qualcohort2.gif)

第三，您調整以設定`cohorts`。 根據您指定給Adobe分析團隊的`cohort date`和`time interval`，您的帳戶中有一個維度可執行`cohort`約會。 在此範例中，該自訂維度稱為`Months between this order and customer's first order date`。 使用此維度，您應該：

* `Group by`具有`group by`選項的維度

* 選取您感興趣的`dimension`的所有值

* 使用`Show top/bottom option`，選取您感興趣的前X個月，並依`Months between this order and customer's first order date`維度排序

現在，您可以看到您指定的每個`cohort`有一行。 立即檢視範例 — 您會看到每個反向連結來源的使用者所貢獻的`Revenue`，`grouped by`其第一筆訂單與任何後續訂單之間的月數之差。 此範例也新增`Cumulative perspective`以檢視`cohorts'`彙總成長 — 檢視結果表格以取得更多詳細程度。

這告訴我們什麼？ 在此，特定轉介來源`Paid search`在客戶購買期限的第一個月很有價值，但無法透過重複收入保留其客戶基礎。 雖然`Direct Traffic`的開頭金額較低，但後續幾個月的收入實際會以類似的速度累積。

無論您如何決策，`cohort`分析都是分析工具箱中強大的工具。 此型別的分析可能會產生一些傳統`time-based cohorts`所無法提供的有關您企業的有趣見解，讓您能夠做出更好的資料導向式決策。
