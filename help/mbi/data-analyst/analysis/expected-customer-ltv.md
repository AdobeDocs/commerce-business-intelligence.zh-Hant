---
title: Pro的預期生存期值(LTV)分析
description: 瞭解如何設定儀表板，幫助您瞭解客戶的生命週期價值增長和預期客戶的生命週期價值。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 預期壽命值分析

本主題演示了如何設定儀表板，幫助您瞭解客戶的生命週期價值增長和客戶的預期生命週期價值。

![](../../assets/exp-lifetim-value-anyalysis.png)

此分析僅適用於專業客戶對新體系結構的分析。 如果您的帳戶有權訪問 `Persistent Views` 特徵 `Manage Data` 側欄，您位於新體系結構中，可以按照此處列出的說明自行構建此分析。

在開始之前，您需要熟悉 [組報告生成器。](../dev-reports/cohort-rpt-bldr.md)

## 計算列

要在 **訂單** 表 **30天月**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* 定義： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

要在 **`orders`** 表 **日曆** 月：

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* 定義： `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* 定義： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 度量

### 度量指令

要建立的度量

* **按第一訂單日期劃分的不同客戶**
   * 如果啟用來賓訂單，請使用 `customer_email`

* 在 **`orders`** 表
* 此度量執行 **計數不同值**
* 在 **`customer_id`** 列
* 按 **`Customer's first order date`** 時間戳

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

## 報告

### 報告說明

**每個客戶按月的預期收入**

* 度量 `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （為X選取一些合理的數字，例如24個月）
   * `Is in current month?` = `No`

* 
   [!UICONTROL度量]: `Revenue`
* [!UICONTROL Filter]:

* 度量 `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 度量 `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

其他圖表詳細資訊

* [!UICONTROL Time period]: `All time`
* 時間間隔： `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order`  — 顯示全部
* 更改 `group by` 為 `All time customers` 使用旁邊的鉛筆表徵圖獨立 `group by`
* 編輯 `Show top/bottom` 欄位：
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**按組群列出的每月平均收入**

* 度量 `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**按組群列出的每月累計平均收入**

* 度量 `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與頁面頂部的影像相似。

如果您在構建此分析時遇到任何問題，或者只想與專業服務團隊接洽， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
