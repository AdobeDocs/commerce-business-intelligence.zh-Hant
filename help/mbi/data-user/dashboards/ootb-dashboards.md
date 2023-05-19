---
title: 包含的儀表板
description: 瞭解如何檢查基本指標的運行狀況，如用戶壽命收入、重複購買次數等，從而為將來的探索奠定堅實的基礎。
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 包含的儀表板

[!DNL Adobe] 提供 `eCommerce` 和 `SaaS` 簡易包。 這些包由Adobe分析員建立，包含資料集的自定義儀表板和報告集。 這些軟體包中包含的分析使您能夠檢查基本指標的運行狀況，從而為將來的探索奠定堅實的基礎。

>[!NOTE]
>
>某些儀表板的可用性取決於您的資料集。

如果您有疑問或希望將包添加到帳戶，請提交 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 的雙曲餘切值。

## 執行概述

的 `executive overview` 儀表板是根據其他儀表板上存在的圖表構建的。 此儀表板是您資料的高級概述，包含每天都要檢查的圖表，而其他儀表板則包含更詳細的資訊。 最初，它被設定為每個帳戶中的預設儀表板。

此時將為您提供一組常規圖表。 Adobe建議您通過添加您最經常使用的其他圖表來定制此儀表板。

## 隊列分析

的 `cohort analysis` 儀表板包括一組圖表，這些圖表顯示按註冊組分組的平均用戶生存期收入增長和增量收入增長。 這揭示了客戶生命週期價值(LTV)、客戶對企業的價值是否隨著時間而增加，以及LTV增長的趨勢。 預設情況下， *所有註冊用戶（買方和非買方）均* 在平均LTV計算中 — 請參閱 [隊列分析主題](../../data-analyst/dev-reports/cohort-rpt-bldr.md)。

此儀表板還可能包括隊列圖表，這些隊列圖表分析特定獲取來源、渠道或人口結構（例如，紐約或加利福尼亞）用戶的終身收入。 這將演示如何分析用戶群中特定段的LTV，並查看一個組或另一個組是否會隨著時間推移產生更高的LTV。

有關群的詳細資訊，請參見 [執行隊列分析](../../data-analyst/dev-reports/cohort-rpt-bldr.md)。

如果您當前未跟蹤用戶獲取源，請參閱 [跟蹤用戶獲取源資料概覽](../../data-analyst/analysis/google-track-user-acq.md)。

## 電子郵件摘要

的 `Email Summary` 儀表板包括一組圖表示例，這些圖表可用於自動化的每日電子郵件摘要。 請參閱 [建立自動電子郵件摘要](../../data-user/export-data/email-summaries.md) 有關配置電子郵件摘要的詳細資訊。  

## 保留狀況

的 `Retention health` 儀表板顯示用戶群的重複購買行為。

的 `Time between orders` 圖表顯示用戶的第一和第二階、第二和第三階之間的平均和/或中值已用時間，依此類推。 你可以 [考慮使用此資料來配置您的電子郵件營銷活動](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)。

的 `Users by lifetime number of orders` 圖表列出了每個生命週期訂單數的用戶總數，以提供重複採購行為的一般概覽。  

的 `Repeat order probability` 圖表顯示具有特定訂單號的用戶重複購買的可能性。 查看客戶完成 `x` 訂單 `(x+1)` 命令，只是把至少 `(x+1)` 按至少賺過錢的人數 `x` 購買。

### 示例

在有生之年購買一次產品的客戶數： `90`

在有生之年進行兩次採購的客戶數： `30`

一生中進行三次購買的客戶數量： `10`

在本例中，在有生之年已進行一次採購以進行第二次採購的客戶的重複訂單概率為： `(30 + 10) / (30+10+90) = 30.77%`。

## 客戶LTV增長

的 `Customer LTV growth` 儀表板包括一組查找每個用戶平均收入的圖表。 根據在登記後的前30天、60天、90天或365天內產生的平均收入，對圖表進行分段。  

圖表的底行顯示，這些平均值按購置來源或人口統計資料分段，以揭示一段時間內哪些用戶組產生的收入最多。

## 產品效能

的 `Product Performance` 控制面板包括圖表，這些圖表通過按項目顯示銷售的項目數和收入來顯示一般產品效能，並標識效能最好的產品。

## 最近的活動

的 `Recent Activity` 儀表板顯示過去30天的效能資料。

## 事務性運行狀況

的 `Transaction Health` 控制面板包括收入、訂單和平均訂單值的概覽圖表。 這些圖表可以按營銷渠道、人口統計或特殊優惠券代碼分段。

## 目標用戶

的 `Users to target` 儀表板包括表格樣式圖表，列出具有特定採購行為的用戶。 幾個示例包括：

* 一次性購買者清單 `X` 月前（您可能希望重新激活的人）

* 支出最高者清單（您可能希望保持滿意）

* 過去活動的支出最多者清單 `X` 天（您可能想獎勵誰）

使用資料導出工具， [為目標市場營銷建立具有相似採購行為的用戶電子郵件清單](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/)。

## 用戶活動

的 `User activity` 儀表板包括按各種資料（包括採購來源、人口統計和平均首次訂購時間）劃分用戶的圖表。 它還包括用戶群體分析，包括按用戶註冊月計算的總體平均壽命收入。

的 `% of cohort members who have purchased` 圖表很有價值，因為它根據用戶註冊時間（每行代表一組用戶）來顯示用戶的轉換率（從0到1）。 它還顯示了他們首次購買的時間(例如，在第1、2、3月……註冊後)。 這可能會顯示10%的用戶在第1月激活，而此數字在第2、3、4月增加……可能會稍後平緩。

通常，此圖表中的線條在一段時間後變為水準。 這表明，在此之後，幾乎沒有其他群體成員進行有機轉化 — 大多數打算購買的用戶已經這樣做了。 目前，這些成員極不可能在沒有干預的情況下轉變為買家。 [通過定制促銷或有針對性的電子郵件與他們接觸是一種低風險的方式，可以迅速改變這一人群。](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
