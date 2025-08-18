---
title: Pro的預期期限值(LTV)分析
description: 瞭解如何設定儀表板，協助您瞭解客戶期限值成長情況及客戶的預期期限值。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 預期期限值分析

本主題說明如何設定儀表板，協助您瞭解客戶期限值成長與客戶的預期期限值。

![](../../assets/exp-lifetim-value-anyalysis.png)

此分析僅供使用新架構的Pro客戶使用。 如果您的帳戶可以存取`Persistent Views`側邊列下的`Manage Data`功能，則表示您使用新的架構，並可依照此處列出的指示，自行建立此分析。

開始使用前，請先熟悉[同類群組Report Builder。](../dev-reports/cohort-rpt-bldr.md)

## 計算欄

使用&#x200B;**30天月**&#x200B;時，要在&#x200B;**訂單**&#x200B;資料表上建立的資料行：

* [!UICONTROL Column name]： `Months between first order and this order`
* [!UICONTROL Column type]： `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `Seconds between customer's first order date and this order`
* 
  [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]： `Months since order`
* [!UICONTROL Column type]： `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `created_at`
* 
  [!UICONTROL Datatype]: `Integer`
* 定義： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

使用&#x200B;**`orders`**&#x200B;行事曆&#x200B;**個月時，要在**&#x200B;資料表上建立的資料行：

* [!UICONTROL Column name]： `Calendar months between first order and this order`
* [!UICONTROL Column type]： `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]：
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
  [!UICONTROL Datatype]: `Integer`
* 定義： `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]： `Calendar months since order`
* [!UICONTROL Column type]： `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： `A` = `created_at`
* 
  [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]： `Is in current month? (Yes/No)`
* [!UICONTROL Column type]： `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `created_at`
* 
  [!UICONTROL Datatype]: `String`
* 定義： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 量度

### 量度指示

要建立的量度

* 依第一筆訂單日期&#x200B;**不同的客戶**
   * 如果您啟用來賓訂單，請使用`customer_email`

* 在&#x200B;**`orders`**&#x200B;資料表中
* 此量度執行&#x200B;**計算不同的值**
* 在&#x200B;**`customer_id`**&#x200B;欄上
* 依&#x200B;**`Customer's first order date`**&#x200B;時間戳記排序

>[!NOTE]
>
>在建立新報表之前，請務必[將所有新欄新增為量度](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。

## 報表

### 報表指示

**每個客戶的預期月收入**

* 量度`A`： `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （請為X挑選一些合理的數字，例如24個月）
   * `Is in current month?` = `No`

* 
  [！UICONTROL公制]: `Revenue`
* [!UICONTROL Filter]：

* 量度`B`： `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]： `New customers by first order date`
* [!UICONTROL Filter]：

* 量度`C`： `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]： `New customers by first order date`
* [!UICONTROL Filter]：

* [!UICONTROL Formula]： `Expected revenue`
* [!UICONTROL Formula]： `A / (B - C)`
* 
  [!UICONTROL Format]: `Currency`

其他圖表詳細資料

* [!UICONTROL Time period]： `All time`
* 時間間隔： `None`
* [!UICONTROL Group by]： `Calendar months between first order and this order` — 全部顯示
* 使用`group by`旁的鉛筆圖示，將`All time customers`量度的`group by`變更為「獨立」
* 編輯`Show top/bottom`欄位，如下所示：
   * [!UICONTROL Revenue]： `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]： `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]： `Top 24 sorted by All time customers by month since first order`

**同類群組每月平均收入**

* 量度`A`： `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]： `Customer's first order date`
* [!UICONTROL Perspective]： `Average value per cohort member`

**依同類群組的每月累計平均收入**

* 量度`A`： `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]： `Customer's first order date`
* [!UICONTROL Perspective]： `Cumulative average value per cohort member`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像頁面頂端的影像。

如果您在建立此分析時遇到任何問題，或只是想與專業服務團隊互動，請[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
