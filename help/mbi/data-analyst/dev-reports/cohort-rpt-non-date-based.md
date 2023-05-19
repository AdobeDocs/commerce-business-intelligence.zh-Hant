---
title: 基於非日期的群體Report Builder
description: 學習按類似活動或屬性對用戶進行分組。
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] 用於非基於日期的組

的 [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) 幫助商家研究不同用戶群隨時間的流逝行為。 過去， `Cohort Report Builder` 已針對按公用分組用戶進行了優化 `cohort date` （例如，在給定月份首次購買的所有客戶的集）。 的 `Non-Date Based Cohort` 功能現在允許您通過類似的活動或屬性對用戶進行分組。 查看此功能的幾個使用案例。

## 使用案例

這不是一個全面的清單，但下面是一些可使用此功能完成的潛在分析。

* 檢查從C.M.C.M.C.M.A. [!DNL Google] 與 [!DNL Facebook]
* 分析第一次購買是在美國與加拿大的客戶
* 從各種廣告活動中獲得客戶的行為

## 如何建立分析

1. 按一下 **[!UICONTROL Report Builder]** 的 **[!UICONTROL Add Report** > **Create Report]** 在任何儀表板中。

1. 在 `Report Builder Selection` 螢幕，按一下 **[!UICONTROL Create Report]** 的 `Visual Report Builder` 的雙曲餘切值。

### 添加度量

既然你在 `Report Builder`，添加要對其執行分析的度量(例如： `Revenue` 或 `Orders`)。

>[!NOTE]
>
>本機 [!DNL Google Analytics] 度量與 `Cohort Report Builder`。 本示例的目標是查看通過不同方式收購的第一訂單客戶的隨時間變化的收入 [!DNL Google Analytics] 源。

### 切換 `Metric View` 至 `Cohort`

![1-toggle度量視圖到隊列](../../assets/1-toggle-metric-view-to-cohort.png)

這將開啟一個新窗口，您可以在其中配置隊列報告的詳細資訊。

編製隊列報告需要五個規格：

1. 如何對小組進行分組
1. 選擇群
1. 操作時間戳
1. 隊列首次動作時間範圍
1. 隊列發生後的時間範圍

![群體](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->

!![cohort-first-action-time-range]<!--(../../assets/3-cohort-first-action-time-range.png){: width="400" height="554"}-->

#### 1。分組 `cohorts`

`Cohorts` 按行為特徵分組，在本例中 `Customer's first order GA source`。 此處提供的選項是已指定為 `groupable` 的下界。

#### 2.選擇群

可顯示給定特徵的所有結果。 因為這可能導致 `cohorts`，可以選擇 `cohorts` (與可用於 `Customer's first order GA source`)。

![群體](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

這允許您選擇基於日期的列，而不是建立度量的列。 在下面，您將查看選擇適用於給定時間範圍 `action timestamp`。

#### 4. `Cohort first action time range`

此處是您選擇包含 `cohorts action timestamp` （因此，自2017年11月至2018年10月首次訂購的客戶）。 這可以是移動日期範圍或固定日期範圍。

#### 5. `Time range after cohort occurrence`

你想看 `cohorts` 按月、按周或按年逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個逐個地逐個逐個逐個逐個逐個逐個逐個地逐個逐個逐個地逐個逐個逐個地逐個逐個逐個地逐個逐個逐個地逐個地逐個地逐個逐個逐個地逐個逐個地逐個地逐個地逐個地逐個地逐個地逐個逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個地逐個 這是你做這些選擇的地方。 在該部分下，您將選擇 `time range` 在 `cohort action timestamp` 已發生。 例如，這顯示在活動時間範圍內下單的客戶12個月的資料。

![隊列 — 第一行動 — 時間範圍](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] 當您在以下狀態之間切換時，應用的度量仍保持不變 `Standard` 和 `Cohort` 的子菜單。

### 相關

請參閱 [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md)。
