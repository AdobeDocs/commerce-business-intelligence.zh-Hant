---
title: 使用可視Report Builder
description: 學習分析報告中特定時段的資料。
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# 使用 [!DNL Visual Report Builder]

的 [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) 使您能夠直觀地瞭解資料，以便得出見解並幫助推動業務決策。 本教程將指導您完成建立基本報告的過程。

>[!NOTE]
>
>要將報表添加到儀表板，您需要 `Standard` [用戶權限](../administrator/user-management/user-management.md) 和 `Edit` 訪問儀表板。

## 步驟1:建立報告

要開始建立報告，請按一下 **[!UICONTROL Report Builder]** 在邊欄或 **[!UICONTROL Add Report]** 在任何儀表板的頂部。 當 `Report Builder` 頁面顯示，按一下 **[!UICONTROL Visual Report Builder]** 的雙曲餘切值。

編輯在 [!DNL Visual Report Builder]，按一下任意圖表右上角的齒輪（選項）表徵圖，然後按一下 **[!UICONTROL Edit]**。

## 步驟2:添加度量

建立分析的第一步是選擇 [度量](../data-user/reports/ess-manage-data-metrics.md) 分析。 雖然度量在預設情況下按字母順序列出，但您也可以按為度量提供動力的表對它們進行分組。

在選擇初始度量後，可以添加附加度量，並將所有度量覆蓋到單個報表上，或通過添加公式來執行多度量計算。

## 第3步：添加 `Formulas`

`Formulas` 通過按一下 **[!UICONTROL Add Formula]**，位於報告中度量清單的上方。 在 [公式編輯器](../data-analyst/dev-reports/formulas-in-rpt-bldr.md)，報告中包含的任何度量都可用作輸入。 使用基本數學運算子來處理不同的度量。

假設您想建立一個報告，向我們顯示每個訂單的平均收入。 在這種情況下，你會 `Revenue` 度量 `Number of orders` 度量。

![](../assets/ave-rev-per-order.png)

## 第4步：設定 `Time Period` 和 `Interval of Analysis` {#time}

要在特定時間段中為零，可設定分析的時間段。 您還可以選擇時間間隔來分段資料（例如，按年、按季度或按月）。 使用圖表右上角的菜單設定時段和間隔。

![](../assets/Time_Options_Report_Builder.png)

在為時段設定特定日期範圍時，請確保開始日期在時間間隔的開始處，結束日期在時間間隔的結束處。

例如，設定從 `January 1st` 至 `March 1st` 選擇 `monthly` 間隔顯示 `March` 作為資料點，但每天忽略 `March` 除 `March 1`。 那樣的話，你應該 `Time Period` 從 `January 1 to March 31`。

## 第5步： `Group by` / `Segmenting the Analysis` {#groupby}

[按資料維度分段度量](../best-practices/segment-filter.md)，按一下 **[!UICONTROL Group by]** 的上界。 這將顯示一個下拉清單，其中包含清單中第一個度量的所有可用維。

您可以選擇 `None` 來防止度量被分割。 例如，您可能需要一個度量，該度量返回總收入而不進行分段，而另一個收入度量則按區域分段。

返回至每個訂單實例的平均收入，並將「組」設定為促銷代碼。 這將顯示具有促銷代碼和沒有促銷代碼的訂單的每訂單平均收入。

![](../assets/Group_By_Report_Builder.png)

如果分析中包含的度量是基於不同的資料表構建的，則彈出窗口允許您在每個表中選擇匹配的資料維。 此處的目標是查找共用分段值類型的維：

![](../assets/Dimension_Editor.png)

## 步驟6:設定 `Metric Filters`。 `Perspective`, `Time Interval` {#metric-specific}

對於添加到分析的每個度量，可以添加篩選器、選擇相關資料透視並設定 `time interval` 頁籤 要訪問這些功能，請按一下漏斗(`Filter`)，眼睛(`Perspective`)和時鐘(`Time`)表徵圖，位於報告中包含的度量旁邊。

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` 限制分析中包含的資料集。 例如，在評估單個獲取通道和刪除離群值時，過濾器非常有用。

除了下拉菜單和文本框之外，還可以使用特殊的篩選器運算子，如 `LIKE` 或 `IN` 來修改標籤元素的屬性。

使用通配符(`%` 或 `_`與 `LIKE` 支援語句。 的 `%` 通配符匹配多個字元，而 `_` 只與任何單個字元匹配。 例如：

- `affiliate's name Like B%` 僅允許名稱開頭的客戶的資料 `B`。

- `affiliate's name Like _ake` 僅允許來自名稱類似 `Jake`。 `Rake`或 `Bake` 但 `Drake` 或 `Blake`。

添加多個篩選器可以嚴格控製圖表資料。 預設情況下，要包括的某段資料的所有篩選條件必須為true，但可以通過編輯「篩選規則」文本框來建立OR關係。

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` 允許您輕鬆在資料的不同視圖之間切換。 查看可用內容：

- `Standard perspective`:標準透視顯示x軸上匹配日期的結果（例如，1月的收入）。 這是您在「每訂單平均收入」實例中使用的透視。

![](../assets/Standard.png)

- `Amount` 或 `Percent Change` 與 `Previous Period` 透視：此透視顯示從一個時間間隔到下一個時間間隔的更改量或更改百分比，對於測量快速更改度量中的更改率非常有用。 還有一個觀點可以比較與去年同期相比的間隔，以顯示每年的增長。

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`:的 `cumulative perspective` 顯示一段時間內度量的持續或累計總和金額。 這通常用於分析總客戶和規劃未來容量。

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`:此透視以分析中包含的第一次時間間隔的百分比形式顯示資料。 這有助於測量特定動作相對於第一週期效能的有效性。

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`:「累計平均值」窗口透視顯示指定時間範圍內度量的累計平均值。 間隔必須與在報告級別上設定的間隔相同。 例如，如果報表按周顯示收入的最後一個完整季度，則可以將累計平均窗口時間範圍設定為四周。 這樣，前三個值為空，第四個值表示收入前四週的平均值。 為了清晰起見，請確保關閉 `Multiple Y-Axes` 複選框。

![](../assets/rolling_avg_window.png)

### 特定於度量的時間選項

報表中使用的度量有兩個選項：它們可以根據全局時間選項隨時間而變化，或者不根據全局時間選項進行變化，而全局時間選項會將它們顯示為標量數。

將度量時間間隔更改為 `None` 返回 `scalar` 編號，在建立涉及將時間趨勢度量除以 `scalar` 數。 此外，您還可以更改 `scalar` 度量到獨立於報告的時間範圍。

比如，你希望看到2019年月收入佔2019年總收入的百分比。 可以添加兩個 `Revenue` 按月間隔分段的全球時間範圍為2019年1月1日至2019年12月31日的報告。

>[!NOTE]
>
>如果添加 `group by` 維，選擇新的可視化，或調整時間間隔，然後僅保存數字(`scalar`)。 下次從儀表板開啟該報表時，不會保留這些調整 — 只保留時間範圍。

要瞭解有關在報告中使用時間選項的詳細資訊，請參閱 [教程](../tutorials/time-options-visual-rpt-bldr.md)。

## 第7步：保存報告

建立圖表時，可通過按一下 **[!UICONTROL Save]** 在 `Visual Report Builder`。

您可以選擇保存圖表、表或數字(`scalar`)使用 `Type` 下拉清單和使用 `Location` 下拉清單。

然後，可通過按一下 **[!UICONTROL Save to Dashboard]**。

![](../assets/save-to-dashboard.png)

## 報告輸出

要幫助您確定要選擇的報表輸出，請參閱：

### 圖表

![](../assets/RB_Chart.png)

### 表格

![](../assets/RB_Table.png)

### 編號(`scalar`)

![](../assets/RB_Scalar.png)

恭喜！ 你完了。
