---
title: 隊列Report Builder
description: 瞭解在其生命週期中具有相似特徵的用戶組的分析。
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# 隊列Report Builder

您是否曾希望研究用戶的不同子集隨時間的變化情況？ 例如，有沒有想過，在促銷期間註冊的用戶是否擁有比沒有註冊的用戶更高的平均終身收入？ 如果答案是 `Yes`，則 `Cohort Report Builder` 是你的完美工具。 [!DNL Adobe Commerce Intelligence] 已優化以執行此分析並使其與您的業務相關。

## 隊列分析是什麼？ {#what}

`Cohort` 分析可以被廣泛定義為對在其生命週期中具有相似特徵的用戶組的分析。 它允許您識別不同用戶組的行為趨勢。

深入的底漆 `cohort` 分析、審閱 [此頁](https://www.cohortanalysis.com/)。

在 [!DNL Commerce Intelligence] 儀表板，可輕鬆建立用戶 `cohorts` 基於 `cohort` 日期和您帳戶中的度量。

## 為什麼隊列分析很重要？ {#important}

如上所述， `cohort` 分析允許您識別不同用戶組之間的行為趨勢。 通過對某些組的行為有深入的瞭解，您可以定制決策和支出以最大限度地提高銷售。 例如，以一生的收入為例 `cohort` 分析 — 雖然這種分析出於許多原因是有益的，但當務之急是做出更好的客戶收購決策。

## 如何建立自己的 `cohort` 分析？

### 新體系結構

這些是使用 `Cohort Report Builder` 的 [新體系結構](../../administrator/account-management/new-architecture.md)。

1. 按一下 **[!UICONTROL Report Builder]** 的 **[!UICONTROL Add Report** > **Create Report]** 在任何儀表板中。

1. 在 `Report Builder` 選擇螢幕，按一下 **[!UICONTROL Create Report]** 的 `Visual Report Builder` 的雙曲餘切值。

**添加度量**

既然你在 `Report Builder`，添加要對其執行分析的度量(例如： `Revenue` 或 `Orders`)。

>[!NOTE]
>
>本機 [!DNL Google Analytics] 度量與 `Cohort Report Builder`。

**將度量視圖切換為`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

這將開啟一個新窗口以配置 `Cohort` 報告。

### 需要五個規格來構建 `Cohort` 報告：

1. 如何對 `cohorts`
1. 的 `cohort` 時段
1. 數 `cohorts` 查看
1. 每個資料的最小數量 `cohort` 必須包含
1. 時間範圍 `cohort` 發生

#### 1。分組 `cohorts`

`Cohorts` 按時間戳分組，如 **註冊日期** 或 **第一訂單日期**。

>[!NOTE]
>
>不能使用與為 `cohort` 日期。 對於需要此項的分析，可以使用 `Standard report builder` 的雙曲餘切值。

#### 2. `Cohort` 時段

選擇要分組的時間期 `cohorts` 。 換句話說，您在上面選擇的時間戳中哪一部分最重要；這樣 `week`。 `month`。 `quarter`或 `year`? 您的報告以您在此處選擇的任何間隔顯示資料

#### 3.和4。 設定 `cohorts` 查看和查看每個 `cohort` 必須

這些參數只幫助您查看 `cohorts` 你最感興趣的，而且 `Preview` 框中顯示了報告中顯示的代碼。

預設情況下，當前 `cohort` 除非您更改了每個應用程式所需的最小資料量 `cohort` 至 `0`。 在這個例子中， `cohort` 對於當前時段，僅包含部分資料。

#### 5.時間範圍 `Cohort` 發生

此功能允許您設定您查看的選定資料的時間範圍 `cohorts`。 例如，如果要查看24個月 `cohorts` 基於 `customer's first order date`，但您只對每個資料的前3個月感興趣 `cohort`，可以設定 `number of cohorts to view` 至 `24` 和 `time range after cohort occurrence` 至 `3`。

此值的間隔隨您在 `cohort time period` 值設定為 `12` 預設；除非按一下日曆表徵圖編輯，否則該值不會更改。

![](../../assets/cohort-time-range.png)

#### 其他說明

* [!UICONTROL Filters]:當您在以下狀態之間切換時，應用的度量仍保持不變 `Standard` 和 `Cohort` 的子菜單。

* 請參閱 [`Perspectives`](#perspectives)。

#### 示例

這是一個將它拉到一起的例子。 在此示例中，我要在 `cohort`他們是第一次購買，看看這批人是否會在未來6個月內再次購買。

![訂單隊列](../../assets/crb_example.gif)

### 舊體系結構

#### 舊體系結構 {#personalinfo}

下面是特定於舊版本的說明 `Cohort Report Builder`。 如果您對使用新版本感興趣，請參閱 [新體系結構](../../administrator/account-management/new-architecture.md) 有關遷移到的詳細資訊 [!DNL Commerce Intelligence] 新建體系結構帳戶。

#### 如何建立自己的 `cohort` 分析？ {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` 分析！ 在這裡，您可以看到收入隨著時間的推移而逐漸增長，並且以累計和按用戶計算。

本部分將指導您建立自己的 `cohort` 分析。 有關示例(以及演示該過程的動畫GIF)，請查看 [示例部分](#examples) 這個主題。

1. 按一下 **[!UICONTROL Report Builder]** 的 **[!UICONTROL Add Report** > **Create Report]** 在任何儀表板中。

1. 在 `Report Builder Selection` 螢幕，按一下 **[!UICONTROL Create Report]** 的 `Cohort Analysis` 的雙曲餘切值。

#### 添加度量

既然你在 `Cohort Report Builder`，添加度量(示例： `Revenue` 或 `Number of orders`)。

>[!NOTE]
>
>本機 [!DNL Google Analytics] 度量與 `Cohort Report Builder`。

#### 選擇隊列日期 {#date}

下一步是指定 `cohort date`。 這是用戶分組的日期。 例如，這可能 `User's first order date` 或 `User's registration date`。

>[!NOTE]
>
>不能使用度量所基於的相同日期(例如： `created at`) `cohort date`。

#### 設定間隔和時段

下一步，設定 `Interval` 和 `Time Period`。

`Interval`
的 `Interval` 選項 `length` 你 `cohorts`。 例如，如果此值設定為 `Month`，您的報告以月計量。

可以使用 **持續時間** 的子菜單。

`Time Period`
使用 `Time Period` 的子菜單。 `cohorts` 分析。 你可以展示 `cohort`，從清單中選擇，指定時間範圍，或定義滾動時間範圍 `cohorts` 包含。 例如，如果您使用 `Specific Cohorts` 選項，可以選擇要包括在分析中的特定月份：

![使用 `Time Period` 菜單以添加特定 `Cohorts`](../../assets/Cohort_Time_Period.gif)

如果要分組 `cohorts` 於2014年4月、5月和6月 `Specific Cohorts` 清單中，所有在這些月中註冊的用戶都將包括在內。

#### 定義X軸

下 `duration`，可以定義圖表的X軸設定。 即，每個資料點表示多少個時間段以及要包括在分析中的資料點。

#### 選擇 `counting members` 表

如果您選擇將用戶分組為 `cohort date` 已從另一個表聯接，您可能看到 `counting members in the … table` 的雙曲餘切值。

![](../../assets/Cohort_Counting_Members_option.png)

查看一個示例以瞭解此設定。 假設你建了一個 `Revenue` 度量 `Customer's registration date`。 您還希望使用透視 `Average value per cohort member` 查看每個買家隨時間推移的收入。 要查找每個買家的平均值，您需要確定要除以的買家數。 是否是您的 `customers` 或者是您 `orders table` 同期？

此設定可回答該問題。 正在計算 `customers` 表包括平均值中的所有客戶（無論他們是否購買過）。 正在計算 `orders` 表僅包括進行購買的客戶。

#### 選擇透視 {#perspective}

定義了度量並想要如何分析它後，可以選擇 `perspective` 你想用。

在報告可視化的正上方是 `perspective` 的子菜單。

請參閱 [透視](#perspectives)。

![](../../assets/Cohort_Perspective_Menu.png)

## 隊列分析實例 {#examples}

既然你已經經歷了如何 `cohort` 分析，看一些例子。

### 我想知道我的用戶 `cohorts` 隨著時間的推移而增長。

![用戶 `cohorts` 隨著時間的推移而增長](../../assets/cohort1.gif)

在本例中，您分析了 `Revenue` 度量，按 `customer's first order date`，並選擇了8個最新 `cohorts` (定義於 `Time Period` 菜單)，以包括在分析中。 為了觀察小伙們是如何隨著時間的推移而成長 `Cumulative Average Value per Cohort Member` `perspective`。

### 我想知道，平均而言，一個用戶在有生之年的不同點下了多少訂單。

!![Average number of orders users make at different points in their lifetimes]../../assets/cohort2.gif

對於本示例，您分析了 `Number of orders` 度量，按 `customer's first order date`，並包括最近八個組(定義於 `Time Period` )的正平方根。 要查看每個隊列的平均訂單數，請更改 `perspective` 至 `Average Value per Cohort Member`。

### 我想瞭解用戶未來的購買活動與其第一個月的業務活動有何不同。

![將用戶的未來採購活動與其第一個活動月進行比較](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
這顯示了某一群體在其生命週期中任何給定時刻的增量貢獻。 (示例：「第6週」點顯示用戶在其第6週內建立的所有資料點。)

`Average Value per Cohort Member`
這將 `Standard cohort` 第(1)項中按每個用戶數分析 `cohort` 組。 這可用於比較基於蘋果到蘋果的群體表現，因為並非所有群體都可能包括相同數量的用戶。 例如，某個特定用戶的每週6個平均收入 `cohort`。

`Cumulative`
此 `perspective` 顯示了 `cohort` 分析 `cumulative` 基礎。 換句話說，它顯示了某一群體迄今為止在其生命週期中任何給定時刻的總貢獻。 比如，某一群體在六週後累積的收入。

`Cumulative Average Value per Cohort Member`
這將 `Cumulative` 第(3)項中按每個用戶數分析 `cohort` 組。 它顯示每人的平均壽命貢獻（通常為平均壽命收入） `cohort` 成員 `cohort's` 生命。 例如，在6月加入的用戶數為6個月後，平均壽命收入。

`Percent of First Value (show first value)`
這將分析聚合 `cohort` 在某個特定時間 `cohort's` 生命週期佔其在第一個期間貢獻的百分比。 例如，第6個月的收入除以在6月加入的用戶的第1個月的收入。

`Percent of First Value (hide first value)`
這和 `perspective` 上，但是第一個100%的時段值隱藏。

## 收尾 {#finish}

的 `Cohort Report Builder` 已針對按公用分組用戶進行了優化 `cohort date`。 您可能有興趣按類似的活動或屬性對用戶進行分組。 Adobe建議簽出 [關於定性組的本教程](../dev-reports/create-qual-cohort-analysis.md) 的子例行程式。
