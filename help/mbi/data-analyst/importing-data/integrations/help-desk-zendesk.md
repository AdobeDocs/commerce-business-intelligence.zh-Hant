---
title: Zendesk服務檯報告
description: 瞭解您最有價值的轉介管道。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# [!DNL Zendesk]的服務檯報告

>[!NOTE]
>
>這僅適用於處於`Pro`計畫且使用新架構的使用者端。 如果您在選取主工具列中的`Data Warehouse Views`後有`Manage Data`區段可用，則表示您使用新架構。

將您的[!DNL Zendesk]資料與交易式資料庫合併，是瞭解客戶如何與您的銷售或客戶成功團隊互動的絕佳方式。 它還有助於您瞭解哪些型別的客戶正在使用您的支援平台。 此主題示範如何設定儀表板，以取得有關您[!DNL Zendesk]效能和關聯交易式客戶的精細報告。

開始之前，您想要連線您的[[!DNL Zendesk]](../integrations/zendesk.md)。 此分析包含[進階計算資料行](../../data-warehouse-mgr/adv-calc-columns.md)。

<!-- Getting Started -->

## 快速入門

### 要追蹤的欄

* `audits`資料表
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events`資料表
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets`資料表
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users`資料表
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 要建立的篩選器集

* `[!DNL Zendesk] Tickets`資料表
   * `status != deleted`

* `Filter set name`： `Tickets we count`
* `Filter set logic`：

## 計算欄

### 要建立的欄

* **`[!DNL Zendesk] user's`**&#x200B;資料表
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`，`email`

      * `SQL Calculation` `- case when `A` is not `null` and `A！=`end-user`然後`Yes`，當`B`不是`null`且`B`類似`%@magento.com`然後`Yes`否則`No`結束

      * 以您的網域取代`@magento.com`

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`**&#x200B;資料表
   * 選取定義： `Joined Column`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]： `[!DNL Zendesk] users.id`

   * 選取[!UICONTROL table]： `[!DNL Zendesk] users`
   * 選取[!UICONTROL column]： `User is agent? (Yes/No)`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`**&#x200B;資料表
   * 選取定義： `Exists`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]： `[!DNL Zendesk] audits._id`

   * 選取[!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]：
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 選取定義： `Exists`
   * 選取[!UICONTROL table]： `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]： `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`**&#x200B;資料表
   * 選取定義： `Joined Column`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]： `[!DNL Zendesk] users.id`

   * 選取[!UICONTROL table]： `[!DNL Zendesk] users`
   * 選取[!UICONTROL column]： `email`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 選取定義： `Joined Column`
   * 選取[!UICONTROL table]： `[!DNL Zendesk] users`
   * 選取[!UICONTROL column]： `role`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 選取定義： `Max`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]： `[!DNL Zendesk] tickets.id`

   * 選取[!UICONTROL table]： `[!DNL Zendesk] audits`
   * 選取[!UICONTROL column]： `created_at`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]：
   * `status`已變更為`solved = 1`

   * 選取定義： `Min`
   * 選取[!UICONTROL table]： `[!DNL Zendesk] audits`
   * 選取[!UICONTROL column]： `created_at`
   * [!UICONTROL Path]： `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]：
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date`減去`created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date`減去`created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - 「相同表格>計算」

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` — 整數

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - 「相同表格>計算」

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`**&#x200B;資料表
   * 選取定義： `Count`
   * [!UICONTROL Create Path]：
   * [!UICONTROL Many]： `[!DNL Zendesk] tickets.email`
   * 
     [！UICONTROL One]: `customer_entity.email`

   * 選取[!UICONTROL table]： `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]：
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - 「相同表格>計算」

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`**&#x200B;資料表
   * 選取定義： `Joined Column`
   * 選取[!UICONTROL table]： `customer_entity`
   * 選取[!UICONTROL column]： `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]： `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 量度

* **[!DNL Zendesk]張新票證**
   * `Tickets we count`

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;資料表中
* 此量度執行&#x200B;**計數**
* 在&#x200B;**`id`**&#x200B;欄上
* 依&#x200B;**`created_at`**&#x200B;時間戳記排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]個已解決的票證**
   * `Tickets we count`
   * `closed, solved`中的狀態

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;資料表中
* 此量度執行&#x200B;**計數**
* 在&#x200B;**`id`**&#x200B;欄上
* 依&#x200B;**`created_at`**&#x200B;時間戳記排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]個不同的使用者提交票證**
   * `Tickets we count`

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;資料表中
* 此量度執行&#x200B;**相異計數**
* 在&#x200B;**`requester_id`**&#x200B;欄上
* 依&#x200B;**`created_at`**&#x200B;時間戳記排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]平均/中值票證解析時間**
   * `Tickets we count`
   * `closed, solved`中的狀態

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;資料表中
* 此量度執行&#x200B;**平均值（或中位數）**
* 在&#x200B;**`Seconds to resolution`**&#x200B;欄上
* 依&#x200B;**`created_at`**&#x200B;時間戳記排序
* [!UICONTROL Filter]：

* **[!DNL Zendesk]第一次回應的平均/中間時間**
   * 已計票的票證
   * 狀態為關閉，已解決

* 在&#x200B;**`[!DNL Zendesk] tickets`**&#x200B;資料表中
* 此量度執行&#x200B;**平均值（或中位數）**
* 在&#x200B;**`Seconds to first response`**&#x200B;欄上
* 依&#x200B;**`created_at`**&#x200B;時間戳記排序
* [!UICONTROL Filter]：

>[!NOTE]
>
>在建立新報表之前，請務必[將所有新欄新增為量度](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)的維度。

### 報表

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]： `New Tickets`
   * [!UICONTROL Filter]：
   * `new, open, pending`中的狀態

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]： `New Tickets`
   * [!UICONTROL Filter]：
   * `solved, closed`中的狀態

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]： `Average time to first response`

* 量度`A`： `Average time to first response`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]： `Average time to resolution`
   * [!UICONTROL Filter]：
   * `solved, closed`中的狀態

* 量度`A`： `Average time to resolution`
* `Time period`： `All time`
* `Interval`： `None`
* `Chart Type`： `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]： `New Tickets`

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Group by`： `status`
* `Chart Type`： `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]： `New Tickets`

   * [!UICONTROL Metric]： `New Tickets`

* 量度`A`： `New tickets`
* 量度`B`： `Solved tickets`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]： `Average time to first response`

* 量度`A`： `Average time to first response`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]： `Average time to resolution`
   * [!UICONTROL Filter]：
   * `solved, closed`中的狀態

* 量度`A`： `Average time to resolution`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]： `Distinct users filing tickets`

* 量度`A`： `Distinct users filing tickets`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Chart Type`： `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]： `New Tickets`

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Group by`： `Ticket created_at (day of week)`
* `Chart Type`： `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]：`New Tickets`

   * `Show top/bottom`： `Top 100% sorted by created_at (hour of the day)`

* 量度`A`： `New tickets`
* `Time period`： `All time`
* `Interval`： `None`
* `Group by`： `Ticket created_at (hour of the day)`
* `Chart Type`： `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]： `Average lifetime revenue`

* 量度`A`： `Average lifetime revenue`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Group by`： `User has filed a support ticket?`
* `Chart Type`： `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 
     [！UICONTROL公制]: Users

* 量度`A`： `New users`
* `Time period`： `All time`
* `Interval`： `Monthly`
* `Group by`： `User has filed a support ticket?`
* `Chart Type`： `Column`
