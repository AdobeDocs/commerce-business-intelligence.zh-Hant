---
title: 使用SQLReport Builder
description: 瞭解使用SQLReport Builder的內容。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# 使用 [!DNL SQL Report Builder]

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md) 建立和編輯SQL圖表。 `Standard` 用戶可以在儀表板上重新排列這些圖表， `Read-only` 用戶擁有與傳統圖表相同的體驗。 另外， `Read-only` 用戶無權訪問查詢的文本。

查看 [培訓視頻](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) 來瞭解更多資訊。

[!DNL SQL]或「結構化查詢語言」是用於與資料庫通信的寫程式語言。 在 [!DNL Commerce Intelligence]。 [!DNL SQL] 用於查詢或檢索Data Warehouse中的資料。 查看儀表板上的報告 — 在幕後，每個報告都由 [!DNL SQL] 的子菜單。

您可以使用 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 要直接查詢Data Warehouse，請查看結果，並將其轉換為圖表。 可以開始使用 [!DNL SQL Report Builder] 按一下 **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**。

查看 [培訓視頻](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) 來瞭解更多資訊。

的 [!DNL SQL Report Builder] 允許您直接查詢Data Warehouse、查看結果，並快速將其轉換為圖表。 關於使用 [!DNL SQL] 要生成報告，您不需要等待更新週期來迭代您建立的列。 如果結果看起來不正確，您可以快速編輯並重新運行查詢，直到符合您的預期。

本主題將引導您使用 [!DNL SQL Report Builder]。 等你瞭解了自己的路，再看看 [!DNL SQL] 要獲取可視化教程，請嘗試優化您編寫的一些查詢。

本文所涵蓋：

1. [寫入查詢](#writing)

1. [運行查詢並查看結果](#runquery)

1. [建立可視化](#createviz)

1. [保存報告](#save)

## [!DNL SQL Report Builder] 整合

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) 是唯一不能與 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)。 此功能正在開發中。

開始建立 [!DNL SQL] 報告，按一下 **[!UICONTROL Report Builder]** 或 **[!UICONTROL Add Report]** 在任何儀表板的頂部。 在 [!DNL Report Picker] 螢幕，按一下 **[!UICONTROL SQL Report Builder]** 開啟 [!DNL SQL] 編輯器。

## 開始

要編輯報告，請按一下齒輪(![](../../assets/gear-icon.png))表徵圖 [!DNL SQL]基於圖表，按一下 **[!UICONTROL Edit]**。

## 寫入查詢 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] 查詢區分大小寫。 確保在編寫查詢時使用了正確的大小寫，或者最終可能會出現意外的結果或錯誤。

遵循 [查詢優化准則](../../best-practices/optimizing-your-sql-queries.md)，在 [!DNL SQL] 編輯器。

>[!IMPORTANT]
>
>**指標 [!DNL SQL] 報告**  — 在SQL報告中插入度量時， `current definition` 的下界。

如果度量將來更新，則SQL報告 *不* 反映變化。 必須手動編輯報表，以使更改生效。

使用提要欄頂部的按鈕，可以在可用於 [!DNL SQL Report Builder]。 如果在清單中未看到要查找的內容，請嘗試使用邊欄頂部的搜索欄進行搜索。

您還可以使用 [!DNL SQL] 編輯器，通過將度量、表和列懸停在查詢上並按一下 **[!UICONTROL Insert]**:

![將表插入 [!DNL SQL] 編輯器。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>任意 [SELECT函式](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)，或SQLReport Builder中支援的任何不對資料進行變異的函式。 這包括但不限於AVG、COUNT、COUNT DISTINCT、MIN/MAX和SUM。

還有， `JOIN` 類型受支援，但Adobe建議僅使用INNER JOIN，因為它是最便宜的 `JOIN` 的下界。

## 運行查詢並查看結果 {#runquery}

完成編寫查詢後，按一下 **[!UICONTROL Run Query]**。 結果顯示在SQL編輯器下的表中：

![運行查詢並查看結果。](../../assets/SQL_Run_Query.gif)

如果結果中出現問題，您可以編輯查詢並重新運行查詢，直到您滿意為止。

你有時可能會看到 [編輯器下麵包含EXPLAIN的消息](../../best-practices/optimizing-your-sql-queries.md)。 如果您看到其中一個，這意味著您的查詢尚未運行，需要稍微調整。

編輯完查詢後，可以繼續建立可視化或將工作保存到儀表板。

## 建立可視化 {#createviz}

要使用查詢結果建立可視化，請按一下 **[!UICONTROL Chart]** 的 `Results` 的子菜單。 在此頁籤中，您選擇：

* 的 `Series`或要測量的列，例如 **已售物料**。
* 的 `Category`，或要用於分割資料的列，如 **採集源**。
* 的 `Labels`或X軸值。

下面快速查看可視化過程的外觀：

![](../../assets/SQL_RB_viz_overview.gif)

有關如何建立可視化的詳細說明，請參閱 [通過SQL查詢建立可視化效果教程](../../tutorials/create-visuals-from-sql.md){:target=&quot;_blank&quot;}。

## 保存報告 {#save}

在保存您的工作之前，必須為報表命名。 請記住 [命名的最佳實踐准則](../../best-practices/naming-elements.md){:target=&quot;_blank&quot;}，然後選擇明確傳達報告內容的內容！

按一下 **[!UICONTROL Save]** 在 [!DNL SQL] 編輯器並選擇報告 `Type` (`Chart` 或 `Table`)。 要對內容進行總結，請選擇要將報告保存到的儀表板，然後按一下 **[!UICONTROL Save to Dashboard]**。

![](../../assets/SQL_Save_Report.gif)

### 分析資料

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 使您能夠直接查詢Data Warehouse、查看結果並快速將結果轉換為報告。 使用 [!DNL SQL] 也允許 [使用 [!DNL SQL] 不可用的函式](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) 的 `Visual` 或 `Cohort` Report Builder，從而讓您能夠更好地控制資料。

使用 [!DNL SQL] 不依賴於更新週期，這意味著您可以根據需要迭代這些週期並立即查看結果。

>[!NOTE]
>
>這隻適用於列的結構，而不適用於資料的新鮮度。 新資料仍依賴於成功完成的更新週期。

| **這對……** | **這對……** |
|---|---|
| 中級/高級分析師 | 初學者，你要知道 [!DNL SQL]。 |
| 的 [!DNL SQL] 精明 | 簡單分析 — 編寫查詢比使用 [!UICONTROL Visual Report Builder]。 |
| 生成一次性使用的計算列 | 與他人共用 — 請考慮您的受眾：他們明白 [!DNL SQL]? 如果不是，他們可能會對報告的構建方式感到困惑。 |
| 資料 `one-to-many` 關係 |  |
| 測試新列或分析 |  |

#### 資料庫與SQL編輯器結果

大多數時間、結果差異都可歸因於更新週期。 如果 [!DNL Commerce Intelligence] 正在將資料從資料庫複製到Data Warehouse的過程中，即使使用同一查詢，您也可能看到不同的結果。

連接問題也可能導致差異。 導航到 `Connections` 按一下 **[!DNL Manage Data** > **Connections]** 檢出 — 有問題的資料庫整合是否出錯？ 如果是，你可能需要 [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) 讓事情重新運轉起來。

如果所有整合都已成功連接，並且您未處於更新週期的中間，則可能有其他問題。

#### 是否刪除 [!DNL SQL] 報告還會從我的Data Warehouse中刪除基礎列？

不，不管您如何構建列，您不會從Data Warehouse中丟失任何列。

使用 `Data Warehouse Manager` 刪除使用報表或查詢時不受影響。

使用 [!DNL SQL Report Builder] 不保存到您的Data Warehouse。


#### `Report Builder` 與 `SQL Report Builder`

的 [!DNL SQL Report Builder] 在建立和構建圖表時，您可以更靈活地選擇應在圖表上顯示的值 `X` 和 `Y` 軸。 有關在中建立圖表的詳細資訊 [!DNL SQL Report Builder]，簽出 [從建立可視化 [!DNL SQL] 查詢](../../tutorials/create-visuals-from-sql.md) 教程。

#### `Cohort Report Builder` {#cohortrb}

與 [!DNL Visual Report Builder]，也請參見Wiki頁。 [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) 僅用於單一目的 — 分析和識別隨時間推移的類似用戶組的行為趨勢。 使用 [!DNL Cohort Report Builder] 不需要 [!DNL SQL] 精明，所以如果你剛開始工作，你可以毫不猶豫地潛入。

| **這對……** | **這對……** |
|---|---|
| 中級/高級分析師 | 初學者 — 你需要定義練習的同伴。 |
| 確定隨時間推移的行為趨勢 | 定性分析 — 可 [完成](../dev-reports/create-qual-cohort-analysis.md)，但需要Adobe幫助。 |

## 更新週期後重建查詢

您不必重新生成查詢。 使用 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 被保存得跟傳統 `Report Builder`。 更新流程 [!DNL SQL] 圖表是相同的 — 更新資料後，將重新計算並重新顯示圖表中的值。

>[!NOTE]
>
>刪除 [!DNL SQL] 報表/查詢，它不會從Data Warehouse中刪除基礎列。 不管您如何構建列，您都不會丟失任何列。

* 如果刪除使用Data Warehouse管理器的報表或查詢，則使用它們建立的列不會受到影響。

* 使用SQLReport Builder建立的列不會保存到Data Warehouse。

## 收尾 {#wrapup}

如果您想嘗試一些更具挑戰性的內容，為什麼不嘗試編寫針對可視化而優化的查詢？ 查看 [從建立可視化 [!DNL SQL] 查詢教程](../../tutorials/create-visuals-from-sql.md){:target=&quot;_blank&quot;}開始。
