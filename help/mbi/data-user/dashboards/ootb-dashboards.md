---
title: 包含的儀表板
description: 瞭解如何檢查基本量度的健康情況，例如使用者期限收入、重複購買次數等，從而為未來的探索奠定堅實的基礎。
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 包含的儀表板

[!DNL Adobe] 優惠方案 `eCommerce` 和 `SaaS` 入門套件。 這些由Adobe分析師建立的套件包含資料集的自訂控制面板和報表集。 這些套件中包含的分析可讓您檢查基本量度的健康情況，例如使用者期限收入、重複購買次數等，從而為未來的探索奠定堅實的基礎。

>[!NOTE]
>
>部分儀表板的可用性取決於您的資料集。

如果您有疑問或有興趣將套件新增至您的帳戶，請提交 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 以取得協助。

## 執行概覽

此 `executive overview` 儀表板是從其他儀表板上的圖表建置的。 此儀表板是資料的高層級概觀，包含每天都會檢閱的圖表，而其他儀表板則包含更詳細的資訊。 最初，它被設定為每個帳戶中的預設儀表板。

其中有一組圖表可供您使用。 Adobe建議您新增您最常使用的其他圖表，根據自己的需求量身打造此儀表板。

## 同類群組分析

此 `cohort analysis` 儀表板包含一組圖表，顯示依註冊同類群組分組的平均使用者期限收入增長和遞增收入增長。 這會顯示客戶期限值(LTV)、客戶對企業的價值是否隨時間增加，也會識別LTV成長趨勢。 根據預設， *所有註冊的使用者（購買者和非購買者）皆已入帳* 在平均LTV計算中 — 請參閱 [同類群組分析主題](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

此儀表板也可能包含同類群組圖表，以分析來自特定贏取來源、管道或人口統計學（例如，紐約或加州）的使用者期限收入。 這是為了示範如何分析使用者群特定區段的LTV，以及瞭解某個群組是否會隨著時間產生較高的LTV。

如需同類群組的詳細資訊，請參閱 [執行同類群組分析](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

如果您目前未追蹤使用者贏取來源，請參閱 [追蹤使用者贏取來源資料概述](../../data-analyst/analysis/google-track-user-acq.md).

## 電子郵件摘要

此 `Email Summary` 儀表板包括可用於自動化每日電子郵件摘要的一組圖表範例。 請參閱 [建立自動化電子郵件摘要](../../data-user/export-data/email-summaries.md) 以取得關於設定電子郵件摘要的詳細資訊。  

## 保留健康狀態

此 `Retention health` 儀表板會顯示您的使用者群重複購買的行為。

此 `Time between orders` 圖表顯示使用者第一至第二順序、第二至第三順序等之間的平均和/或中位數經過時間。 您可以 [請考慮使用此資料來設定您的電子郵件行銷活動](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

此 `Users by lifetime number of orders` 圖表會列出每個存留期訂單的使用者總數，以提供重複購買行為的一般概覽。  

此 `Repeat order probability` 圖表會顯示特定訂單編號的使用者重複購買的可能性。 若要檢視客戶進行變更的可能性 `x` 要完成的訂單 `(x+1)` 訂購，只要將至少完成訂購的人數除以 `(x+1)` 依至少完成購買的人數進行購買 `x` 購買。

### 範例

一生中購買一次的客戶數： `90`

終身購買兩次的客戶人數： `30`

一生中購買過三次的客戶數： `10`

在此範例中，在其有生之年購買過一次以進行第二次購買的客戶的重複訂購機率是： `(30 + 10) / (30+10+90) = 30.77%`.

## 客戶LTV成長

此 `Customer LTV growth` 控制面板包含一組圖表，可找出每位使用者的平均收入。 圖表是根據註冊後前30、60、90或365天內產生的平均收入分段。  

圖表底列會顯示這些依贏取來源或人口統計區段的平均值，以顯示哪些使用者群組隨著時間產生最多收入。

## 產品績效

此 `Product Performance` 儀表板包含可顯示銷售專案數和依專案收入以及識別績效最好的產品來顯示一般產品績效的圖表。

## 最近活動

此 `Recent Activity` 儀表板會顯示過去30天的效能資料。

## 異動健康狀態

此 `Transaction Health` 儀表板包含收入、訂單和平均訂單值的概觀圖表。 這些圖表可依行銷管道、人口統計或特殊優惠券代碼分段。

## 要鎖定的使用者

此 `Users to target` 控制面板包含表格樣式圖表，列出具有特定常見購買行為的使用者。 範例包括：

* 購買過的一次性購買者清單 `X` 幾個月前（您想要重新啟動的對象）

* 頂級消費者清單（您可能希望讓哪些人滿意）

* 過去主要使用者的清單 `X` 天數（您可能會想要獎勵的對象）

使用您的資料匯出工具，可輕鬆進行 [針對target行銷建立具有類似購買行為之使用者的電子郵件清單](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## 使用者活動

此 `User activity` 儀表板包括依各種資料（包括贏取來源、人口統計資料和平均首次訂購）劃分使用者的圖表。 其中也包含使用者同類群組分析，包括依使用者註冊月份區分的整體平均期限收入。

此 `% of cohort members who have purchased` 圖表很有價值，因為它會根據使用者註冊的時間來顯示使用者的轉換率（從0到1） （每行代表一組使用者）。 此外，也會顯示首次購買的時間（例如，註冊後第1、2、3個月……）。 您可能會發現10%的使用者是在第1個月啟動，而此數目是在第2、3、4個月增長……並在稍後穩定增長。

通常，一段時間後，此圖表中的線條會變成水平線。 這表示在此時間點之後，只有少數其他同類群組成員會進行有機轉換 — 大部分要購買的使用者都已完成轉換。 此時，這些成員極不可能在不進行干預的情況下轉換為購買者。 [透過自訂促銷活動或目標電子郵件聯絡他們，是快速開始此族群轉換的低風險方式。](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
