---
title: Zendesk的服務台報告
description: 瞭解您最重要的推薦渠道。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 幫助台報告 [!DNL Zendesk]

>[!NOTE]
>
>僅適用於 `Pro` 規劃和使用新的體系結構。 如果您擁有 `Data Warehouse Views` 選擇後 `Manage Data` 的上界。

整合您的 [!DNL Zendesk] 通過事務性資料庫獲取資料是更好地瞭解客戶如何與您的銷售團隊或客戶成功團隊互動的絕佳方法。 它還有助於您瞭解使用您的支援平台的客戶類型。 本主題演示了如何設定儀表板以獲取有關您的 [!DNL Zendesk] 效能和聯繫。

在開始之前，您要連接 [[!DNL Zendesk]](../integrations/zendesk.md)。 此分析包含 [高級計算列](../../data-warehouse-mgr/adv-calc-columns.md)。

<!-- Getting Started -->

## 入門

### 要跟蹤的列

* `audits` 表
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` 表
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` 表
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` 表
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 要建立的篩選器集

* `[!DNL Zendesk] Tickets` 表
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 計算列

### 要建立的列

* **`[!DNL Zendesk] user's`** 表
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `空` and `A!=`end-user` 然後 `Yes` 何時 `B` 不是 `null` 和 `B` 喜歡 `%@magento.com` 然後 `Yes` 其他 `No` 端

      * 替換 `@magento.com` 您的域

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** 表
   * 選擇定義： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] users`
   * 選擇 [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** 表
   * 選擇定義： `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 選擇定義： `Exists`
   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** 表
   * 選擇定義： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] users`
   * 選擇 [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 選擇定義： `Joined Column`
   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] users`
   * 選擇 [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 選擇定義： `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] audits`
   * 選擇 [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` 已更改 `solved = 1`

   * 選擇定義： `Min`
   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] audits`
   * 選擇 [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` 減 `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` 減 `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;相同表>計算&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype`  — 整數

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;相同表>計算&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` – `String`


* **`customer_entity`** 表
   * 選擇定義： `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 

      [!UICONTROL 1]: `customer_entity.email`

   * 選擇 [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;相同表>計算&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** 表
   * 選擇定義： `Joined Column`
   * 選擇 [!UICONTROL table]: `customer_entity`
   * 選擇 [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 度量

* **[!DNL Zendesk]新票證**
   * `Tickets we count`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此度量執行 **計數**
* 在 **`id`** 列
* 按 **`created_at`** 時間戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]已解決的票證**
   * `Tickets we count`
   * 狀態為 `closed, solved`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此度量執行 **計數**
* 在 **`id`** 列
* 按 **`created_at`** 時間戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]不同用戶歸檔票證**
   * `Tickets we count`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此度量執行 **非重複計數**
* 在 **`requester_id`** 列
* 按 **`created_at`** 時間戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]平均/中值票證解析時間**
   * `Tickets we count`
   * 狀態為 `closed, solved`

* 在 **`[!DNL Zendesk] tickets`** 表
* 此度量執行 **平均值（或中值）**
* 在 **`Seconds to resolution`** 列
* 按 **`created_at`** 時間戳
* [!UICONTROL Filter]:

* **[!DNL Zendesk]第一次響應的平均/中值時間**
   * 已計數的票證
   * 狀態IN已關閉，已解決

* 在 **`[!DNL Zendesk] tickets`** 表
* 此度量執行 **平均值（或中值）**
* 在 **`Seconds to first response`** 列
* 按 **`created_at`** 時間戳
* [!UICONTROL Filter]:

>[!NOTE]
>
>確保 [將所有新列作為維添加到度量](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新報告之前。

### 報告

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 狀態為 `new, open, pending`

* 度量 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 狀態為 `solved, closed`

* 度量 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 度量 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * 狀態為 `solved, closed`

* 度量 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* 度量 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* 度量 `A`: `New tickets`
* 度量 `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 度量 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * 狀態為 `solved, closed`

* 度量 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* 度量 `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* 度量 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* 度量 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 度量 `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 

      [!UICONTROL度量]: Users

* 度量 `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
