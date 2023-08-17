---
title: 同類群組Report Builder
description: 瞭解分析在其生命週期內具有類似特性的使用者群組。
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# 同類群組Report Builder

您是否曾想要研究使用者的不同子集在一段時間內的行為？ 例如，曾經想知道在促銷期間註冊的使用者是否擁有比未註冊的使用者更高的平均終身收入？ 如果答案為 `Yes`，然後 `Cohort Report Builder` 是您的最佳工具。 [!DNL Adobe Commerce Intelligence] 已進行最佳化，可執行此分析並使其與您的業務相關。

## 同類群組分析是什麼？ {#what}

`Cohort` 分析可以寬泛地定義為分析在其生命週期內具有類似特性的使用者群組。 它可讓您識別不同使用者群組中的行為趨勢。

如需在上的深入入門課程 `cohort` 分析、檢閱 [此頁面](https://www.cohortanalysis.com/).

在您的 [!DNL Commerce Intelligence] 儀表板，可輕鬆建立使用者 `cohorts` 根據 `cohort` 帳戶中的日期和量度。

## 那麼，同類群組分析為何如此重要？ {#important}

如上所述， `cohort` 分析可讓您識別不同使用者群組之間的行為趨勢。 瞭解特定群組的行為之後，您就可以量身打造自己的決策與支出，將銷售量最大化。 例如，以期限收入為例 `cohort` 分析 — 雖然這種分析有很多好處，但最直接的原因就是更好的客戶贏取決策。

## 如何建立我自己的 `cohort` 分析？

### 新架構

以下是使用的相關指示 `Cohort Report Builder` 於 [新架構](../../administrator/account-management/new-architecture.md).

1. 按一下 **[!UICONTROL Report Builder]** 在左側標籤上或 **[!UICONTROL Add Report** > **Create Report]** 在任何控制面板中。

1. 在 `Report Builder` 選取畫面，按一下 **[!UICONTROL Create Report]** 在 `Visual Report Builder` 選項。

**新增量度**

現在您已在 `Report Builder`，新增您要執行分析的量度(範例： `Revenue` 或 `Orders`)。

>[!NOTE]
>
>原生 [!DNL Google Analytics] 量度與不相容 `Cohort Report Builder`.

**將量度檢視切換至`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

這將開啟一個新視窗，以配置詳細資訊 `Cohort` 報表。

### 建置需要五個規格 `Cohort` 報告：

1. 如何分組 `cohorts`
1. 此 `cohort` 時段
1. 「 」的數量 `cohorts` 以檢視
1. 每個專案的最小資料量 `cohort` 必須包含
1. 時間範圍晚於 `cohort` 發生次數

#### 1.分組 `cohorts`

`Cohorts` 依時間戳記分組，例如 **註冊日期** 或 **第一個訂單日期**.

>[!NOTE]
>
>您無法使用的時間戳記與為建置量度的時間戳記相同 `cohort` 日期。 對於需要此功能的分析，您可以使用 `Standard report builder` 而非。

#### 2. `Cohort` 時段

選擇要群組的時段 `cohorts` 作者。 換言之，您在上方選取的時間戳記中哪一部分最重要； `week`， `month`， `quarter`，或 `year`？ 您的報告會以您在此處選取的任何間隔顯示資料

#### 3.和4. 設定數量 `cohorts` 以檢視及每個資料量 `cohort` 必須具有

這些引數可協助您僅檢視 `cohorts` 您感興趣的，以及方便使用的 `Preview` 方塊會精確顯示報表中顯示的同類群組。

依預設，目前的 `cohort` 除非您變更每個專案所需的最低資料量，否則不會納入 `cohort` 至 `0`. 在此案例中， `cohort` 目前時段僅包含部分資料。

#### 5.之後的時間範圍 `Cohort` 發生次數

此功能可讓您設定檢視所選資料的時間範圍 `cohorts`. 例如，如果您每月要檢視24頁， `cohorts` 根據 `customer's first order date`，但您只對每個「 」的前3個月資料感興趣 `cohort`，您可以設定 `number of cohorts to view` 至 `24` 和 `time range after cohort occurrence` 至 `3`.

此值的間隔會隨著您在 `cohort time period` 且值設為 `12` 依預設，除非您按一下日曆圖示進行編輯，否則值不會變更。

![](../../assets/cohort-time-range.png)

#### 其他附註

* [!UICONTROL Filters]：套用至量度的專案，會在您切換時維持不變 `Standard` 和 `Cohort` 檢視。

* 另請參閱 [`Perspectives`](#perspectives).

#### 範例

以下是整合所有元素的範例。 在此範例中，我想在 `cohort`這是該同類群組首次購買，看看未來六個月中是否會再次購買。

![訂單同類群組](../../assets/crb_example.gif)

### 舊版架構

#### 舊版架構 {#personalinfo}

以下為舊版的特定指示 `Cohort Report Builder`. 如果您有興趣使用新版本，請參閱 [新架構](../../administrator/account-management/new-architecture.md) 以取得移轉至 [!DNL Commerce Intelligence] 新架構帳戶。

#### 如何建立我自己的 `cohort` 分析？ {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` 分析運作中！ 在這裡，您可以看到收入以累積和每個使用者的基礎隨著時間增長。

本節將逐步引導您建立自己的網站 `cohort` 分析。 如需範例(以及示範程式的動畫GIF)，請檢視 [範例區段](#examples) 主題的。

1. 按一下 **[!UICONTROL Report Builder]** 在左側標籤上或 **[!UICONTROL Add Report** > **Create Report]** 在任何控制面板中。

1. 在 `Report Builder Selection` 熒幕，按一下 **[!UICONTROL Create Report]** 在 `Cohort Analysis` 選項。

#### 新增量度

現在您已在 `Cohort Report Builder`，新增量度(範例： `Revenue` 或 `Number of orders`)，以對其執行分析。

>[!NOTE]
>
>原生 [!DNL Google Analytics] 量度與不相容 `Cohort Report Builder`.

#### 選取同類群組日期 {#date}

下一步是指定 `cohort date`. 這是對使用者進行分組的日期。 例如，這可能是 `User's first order date` 或 `User's registration date`.

>[!NOTE]
>
>您不能使用建立量度的相同日期(例如： `created at`)作為 `cohort date`.

#### 設定間隔和時間週期

接下來，設定 `Interval` 和 `Time Period`.

`Interval`
此 `Interval` 選項可讓您設定 `length` 的 `cohorts`. 例如，如果設定為 `Month`，您的報告會以月為單位測量。

您可以使用以下專案變更這些間隔在x軸上的顯示方式： **持續時間** 功能表。

`Time Period`
使用 `Time Period` 功能表以選擇特定使用者 `cohorts` 以分析。 您可以顯示每 `cohort`，從清單中選擇、指定時間範圍或定義滾動時間範圍 `cohorts` 以包含。 例如，如果您使用 `Specific Cohorts` 選項，您可以選取要納入分析的特定月份：

![使用 `Time Period` 功能表以新增特定 `Cohorts`](../../assets/Cohort_Time_Period.gif)

如果您正在將您分組 `cohorts` 依註冊日期，然後在中選取4月、5月和6月 `Specific Cohorts` 清單中會包含在這幾個月內註冊的任何使用者。

#### 定義X軸

在 `duration`中，您可以定義圖表的X軸設定。 也就是說，每個資料點代表多少時段，以及分析中要包含多少資料點。

#### 選取 `counting members` 表格

如果您選擇依群組使用者 `cohort date` 從另一個表格聯結的，您可能會看到 `counting members in the … table` 選項。

![](../../assets/Cohort_Counting_Members_option.png)

檢視範例以瞭解此設定。 假設您建立了一個報表同類群組 `Revenue` 量度依據 `Customer's registration date`. 您也想要使用透視 `Average value per cohort member` 若要檢視一段時間中每個購買者的收入。 若要找出每個購買者的平均值，您必須決定要除以的購買者數目。 此數字代表貴公司中 `customers` 表格，或是 `orders table` 同一期間？

此設定可回答該問題。 計算中的成員數 `customers` 表格包括平均值中的所有客戶（無論他們是否購買）。 計算中的成員數 `orders` 表格僅包含已購買的客戶。

#### 選取透視 {#perspective}

定義量度以及要如何分析量度後，您可以選取 `perspective` 您想要使用。

在報表視覺效果上方是一個下拉式清單，內含 `perspective` 設定。

另請參閱 [透視](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## 同類群組分析的範例 {#examples}

您已逐步瞭解如何建立 `cohort` 分析，檢視一些範例。

### 我想瞭解我的使用者 `cohorts` 會隨著時間而成長。

![使用者 `cohorts` 隨時間成長](../../assets/cohort1.gif)

在此範例中，您已分析 `Revenue` 量度，您的同類群組依據 `customer's first order date`，並選取最近8個 `cohorts` (定義於 `Time Period` 選單)，以包含在分析中。 若要瞭解同類群組在一段時間內的成長情形，您使用 `Cumulative Average Value per Cohort Member` `perspective`.

### 我想要瞭解使用者在其期限內的不同時間點平均下了多少訂單。

(../../assets/cohort2.gif

在此範例中，您已分析 `Number of orders` 量度，您的同類群組依據 `customer's first order date`，並包括最近的8個同類群組(定義於 `Time Period` 功能表)。 若要檢視每個同類群組的平均訂單數，您已變更 `perspective` 至 `Average Value per Cohort Member`.

### 我想要瞭解使用者的未來購買活動與他們在業務中的第一個月活動相較之下的結果。

![將使用者的未來購買活動與其第一個月的活動進行比較](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
這會顯示指定同類群組在其生命週期中任一指定點的增量貢獻。 （範例：「第6週」點會顯示使用者在其第六週提出的所有資料點。）

`Average Value per Cohort Member`
這會除以 `Standard cohort` 在(1)中依每個專案的使用者人數分析 `cohort` 群組。 這對於根據蘋果對蘋果來比較同類群組效能非常有用，因為並非所有同類群組都可能包含相同數量的使用者。 例如，來自特定使用者的平均每週6收入 `cohort`.

`Cumulative`
這個 `perspective` 顯示傳統 `cohort` 分析 `cumulative` 基礎。 換言之，它會顯示指定同類群組在其生命週期中任何指定時間點至今的總貢獻。 例如，某個同類群組中使用者連續六週後的累計收入。

`Cumulative Average Value per Cohort Member`
這會除以 `Cumulative` 在(3)中依每個專案的使用者人數分析 `cohort` 群組。 它會顯示每個報表的平均期限貢獻（通常為平均期限收入） `cohort` 中每個期間的成員 `cohort's` 期限。 例如，在6月加入的使用者六個月後的平均期限收入。

`Percent of First Value (show first value)`
這會分析彙總 `cohort` 中的特定時間貢獻 `cohort's` 生命週期在其第一個週期中的貢獻百分比。 例如，第6個月收入除以6月加入的使用者第1個月收入。

`Percent of First Value (hide first value)`
這與 `perspective` 「 」以外，但第一個時段值100%會隱藏。

## 正在結束 {#finish}

此 `Cohort Report Builder` 已最佳化為依一般使用者分組 `cohort date`. 您可能想要依類似的活動或屬性來分組使用者。 Adobe建議簽出 [此定性同類群組教學課程](../dev-reports/create-qual-cohort-analysis.md) 以開始使用。
