---
title: Zendesk的服務台報告
description: 了解您最重要的轉介管道。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 服務台報告 [!DNL Zendesk]

>[!NOTE]
>
>這僅適用於位於 `Pro` 規劃並使用新架構。 您在 [新架構](https://support.magento.com/hc/en-us/articles/360016503052-New-Architecture-FAQ) 如果你有 `Data Warehouse Views` 選取後可用的區段 `Manage Data` 中。

整合您的 [!DNL Zendesk] 使用交易資料庫的資料是更好地了解客戶與銷售或客戶成功團隊互動情況，以及使用您的支援平台的客戶類型的絕佳方式。 在本文中，我們示範如何設定控制面板，以取得關於您的 [!DNL Zendesk] 效能和關聯。

開始之前，您需要連接 [[!DNL Zendesk]](../integrations/zendesk.md). 此分析包含 [進階計算欄](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## 快速入門

### 要追蹤的欄

* `audits` 表格
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` 表格
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` 表格
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` 表格
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 要建立的篩選集

* `[!DNL Zendesk] Tickets` 表格
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 計算欄

### 要建立的列

* **`[!DNL Zendesk] user's`** 表格
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` then `Yes` when `B` 不是 `null` 和 `B` like `%@magento.com` then `Yes` else `No` 結束

      * 取代 `@magento.com` 與您的網域

      * `Datatype` - `String`

* **`[Zendesk] audits_~_events`** 表格
   * 選取定義： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * 選取 [!UICONTROL table]: `[Zendesk] users`
   * 選取 [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[Zendesk] audits`** 表格
   * 選取定義： `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[Zendesk] audits._id`

   * 選取 [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 選取定義： `Exists`
   * 選取 [!UICONTROL table]: `[Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[Zendesk] audits_~_events._id_of_parent = [Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[Zendesk] Tickets`** 表格
   * 選取定義： `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[Zendesk] users.id`

   * 選取 [!UICONTROL table]: `[Zendesk] users`
   * 選取 [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * 選取定義： `Joined Column`
   * 選取 [!UICONTROL table]: `[Zendesk] users`
   * 選取 [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[Zendesk] tickets.requester_id = [Zendesk] users.id`

   * 選取定義： `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[Zendesk] tickets.id`

   * 選取 [!UICONTROL table]: `[Zendesk] audits`
   * 選取 [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` 變更為 `solved = 1`

   * 選取定義： `Min`
   * 選取 [!UICONTROL table]: `[Zendesk] audits`
   * 選取 [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[Zendesk] audits.ticket_id = [Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` 減號 `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` 減號 `created_at`

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

      *`Datatype` - `String`


* **`customer_entity`** 表格
   * 選取定義： `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[Zendesk] tickets.email`
   * 

      [!UICONTROL One]: `customer_entity.email`

   * 選取 [!UICONTROL table]: `[Zendesk] tickets`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;相同表>計算&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[Zendesk] Tickets`** 表格
   * 選取定義： `Joined Column`
   * 選取 [!UICONTROL table]: `customer_entity`
   * 選取 [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 量度

* **[!DNL Zendesk]新票證**
   * `Tickets we count`

* 在 **`[Zendesk] tickets`** 表格
* 此量度會執行 **計數**
* 在 **`id`** 欄
* 由 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]已解決的票證**
   * `Tickets we count`
   * 狀態IN `closed, solved`

* 在 **`[Zendesk] tickets`** 表格
* 此量度會執行 **計數**
* 在 **`id`** 欄
* 由 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]不同用戶歸檔票證**
   * `Tickets we count`

* 在 **`[Zendesk] tickets`** 表格
* 此量度會執行 **相異計數**
* 在 **`requester_id`** 欄
* 由 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]平均/中位票證解析時間**
   * `Tickets we count`
   * 狀態IN `closed, solved`

* 在 **`[Zendesk] tickets`** 表格
* 此量度會執行 **平均值（或中位數）**
* 在 **`Seconds to resolution`** 欄
* 由 **`created_at`** timestamp
* [!UICONTROL Filter]:

* **[!DNL Zendesk]首次回應的平均/中位數時間**
   * 我們數的票
   * 狀態已關閉，已解決

* 在 **`[Zendesk] tickets`** 表格
* 此量度會執行 **平均值（或中位數）**
* 在 **`Seconds to first response`** 欄
* 由 **`created_at`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>一定要 [將所有新欄新增為量度](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

### 報表

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 狀態IN `new, open, pending`

* 量度 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * 狀態IN `solved, closed`

* 量度 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 量度 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * 狀態IN `solved, closed`

* 量度 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* 量度 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* 量度 `A`: `New tickets`
* 量度 `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 量度 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * 狀態IN `solved, closed`

* 量度 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* 量度 `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* 量度 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* 量度 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 量度 `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 

      [!UICONTROL量度]: Users

* 量度 `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
