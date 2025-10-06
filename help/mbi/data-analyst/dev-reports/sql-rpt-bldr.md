---
title: 使用SQL Report Builder
description: 瞭解使用SQL Report Builder的來去去。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# 使用[!DNL SQL Report Builder]

>[!NOTE]
>
>需要[管理員許可權](../../administrator/user-management/user-management.md)才能建立和編輯SQL圖表。 `Standard`個使用者可以在儀表板上重新排列這些圖表，並且`Read-only`個使用者具有與傳統圖表相同的體驗。 此外，`Read-only`個使用者沒有查詢文字的存取權。

請觀看[訓練影片](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=zh-Hant)以瞭解更多資訊。

[!DNL SQL]或結構化查詢語言是一種用來與資料庫通訊的程式設計語言。 在[!DNL Commerce Intelligence]中，[!DNL SQL]用於查詢或擷取您Data Warehouse中的資料。 檢視您控制面板上的報告 — 在幕後，每個報告都由[!DNL SQL]查詢提供技術支援。

您可以使用[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)直接查詢您的Data Warehouse、檢視結果，並將其轉換為圖表。 您可以按一下[!DNL SQL Report Builder]，開始使用&#x200B;**[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**&#x200B;建立報告。

請觀看[訓練影片](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html?lang=zh-Hant)以瞭解更多資訊。

[!DNL SQL Report Builder]可讓您直接查詢您的Data Warehouse、檢視結果，並快速將其轉換為圖表。 使用[!DNL SQL]建立報告的最佳部分是，您不需要等待更新週期來重複您建立的欄。 如果結果看起來不正確，您可以快速編輯並重新執行查詢，直到符合您的預期為止。

此主題將逐步說明如何使用[!DNL SQL Report Builder]。 在您熟悉使用方法後，可檢視[!DNL SQL]的視覺效果教學課程，或嘗試最佳化您撰寫的某些查詢。

本文章內容：

1. [撰寫查詢](#writing)

1. [執行查詢並檢視結果](#runquery)

1. [建立視覺效果](#createviz)

1. [儲存報告](#save)

## [!DNL SQL Report Builder]整合

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md)是唯一無法與[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)搭配使用的整合。 此功能正在開發中。

若要開始建立[!DNL SQL]報告，請按一下任何儀表板頂端的&#x200B;**[!UICONTROL Report Builder]**&#x200B;或&#x200B;**[!UICONTROL Add Report]**。 在[!DNL Report Picker]畫面中，按一下&#x200B;**[!UICONTROL SQL Report Builder]**&#x200B;以開啟[!DNL SQL]編輯器。

## 開始使用

若要編輯報表，請按一下![圖表右上角的齒輪（](../../assets/gear-icon.png)齒輪圖示[!DNL SQL]）圖示，然後按一下&#x200B;**[!UICONTROL Edit]**。

## 撰寫查詢 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder]個查詢區分大小寫。 在撰寫查詢時，請務必使用正確的大小寫，否則可能會出現非預期的結果或錯誤。

依照查詢最佳化[的](../../best-practices/optimizing-your-sql-queries.md)准則，在[!DNL SQL]編輯器中寫入查詢。

>[!IMPORTANT]
>
>**[!DNL SQL]報表中的量度** — 當您在SQL報表中插入量度時，會使用量度的`current definition`。

如果度量未來已更新，則SQL報表&#x200B;*不會*&#x200B;反映變更。 您必須手動編輯報告，變更才會生效。

使用側邊欄頂端的按鈕，您可以在表格清單與[!DNL SQL Report Builder]中可用的量度之間切換。 如果您在清單中看不到要尋找的內容，請嘗試使用側邊欄頂端的搜尋列來搜尋。

您也可以使用[!DNL SQL]編輯器中的側邊欄，將滑鼠懸停在量度、表格和欄上並按一下&#x200B;**[!UICONTROL Insert]**，直接將其插入您的查詢：

![正在將資料表插入[!DNL SQL]編輯器中。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>SQL Report Builder支援PostgreSQL支援的任何[SELECT函式](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)，或任何不會變更資料的函式。 這包含但不限於AVG、COUNT、COUNT DISTINCT、MIN/MAX和SUM。

此外，也支援任何`JOIN`型別，但Adobe建議僅使用INNER JOIN，因為這是`JOIN`型別中最便宜的型別。

## 執行查詢並檢視結果 {#runquery}

當您完成查詢的撰寫時，請按一下&#x200B;**[!UICONTROL Run Query]**。 結果會顯示在SQL編輯器下方的表格中：

![正在執行查詢並檢視結果。](../../assets/SQL_Run_Query.gif)

如果結果中出現錯誤，您可以編輯查詢並重新執行，直到滿意為止。

您有時會在編輯器中看到[封含有EXPLAIN的訊息](../../best-practices/optimizing-your-sql-queries.md)。 如果您看到其中一項，表示您的查詢尚未執行，需要微調。

編輯完查詢後，您可以繼續建立視覺效果或儲存工作到儀表板。

## 建立視覺效果 {#createviz}

若要使用查詢結果建立視覺效果，請按一下&#x200B;**[!UICONTROL Chart]**&#x200B;窗格中的`Results`標籤。 在此索引標籤中，您選取：

* `Series`或您要測量的資料行，例如&#x200B;**售出的專案**。
* `Category`或您要用來劃分資料的資料行，例如&#x200B;**贏取來源**。
* `Labels`或X軸值。

以下是視覺化流程的外觀：

![SQL Report Builder視覺效果概觀的動畫示範](../../assets/SQL_RB_viz_overview.gif)

如需如何建立視覺效果的詳細逐步解說，請參閱[從SQL查詢建立視覺效果教學課程](../../tutorials/create-visuals-from-sql.md){: target="_blank"}。

## 儲存報告 {#save}

您必須先為報表命名，才能儲存作業。 請記得遵循[命名](../../best-practices/naming-elements.md){: target="_blank"}的最佳實務准則，並選擇能明確傳達報表內容的專案！

按一下&#x200B;**[!UICONTROL Save]**&#x200B;編輯器右上角的[!DNL SQL]，然後選取報告`Type` （`Chart`或`Table`）。 若要完成工作，請選取要儲存報告的儀表板，然後按一下&#x200B;**[!UICONTROL Save to Dashboard]**。

![將SQL報告儲存到儀表板的動畫示範](../../assets/SQL_Save_Report.gif)

### 分析您的資料

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)讓您能夠直接查詢Data Warehouse、檢視結果，並快速將其轉換為報表。 使用[!DNL SQL]也可讓您[使用 [!DNL SQL] 或](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) Report Builder中不可用的`Visual`函式`Cohort`，讓您更能掌控資料。

使用[!DNL SQL]建立的已計算欄不依存於更新週期，這表示您可以視需要重複這些欄並立即檢視結果。

>[!NOTE]
>
>這僅適用於欄的結構，不適用於資料的時效性。 新的資料仍取決於成功完成的更新週期。

| **這是最適合的……** | **這不太適合……** |
|---|---|
| 中級/進階分析師 | 初學者 — 您需要知道[!DNL SQL]。 |
| [!DNL SQL]精通 | 簡單分析 — 撰寫查詢可能比單純使用[!UICONTROL Visual Report Builder]更有效。 |
| 建立一次性使用的計算欄 | 與他人共用 — 考慮您的對象：他們瞭解[!DNL SQL]嗎？ 如果沒有，他們可能會對報告的建置方式感到困惑。 |
| 具有`one-to-many`關係的資料 |  |
| 測試新欄或分析 |  |

#### 資料庫與SQL編輯器結果

大多數時間，結果的差異可歸因於更新週期。 如果[!DNL Commerce Intelligence]正在將資料從您的資料庫復寫到Data Warehouse，即使使用相同的查詢，您也可能會看到不同的結果。

連線問題也可能導致不一致。 按一下「`Connections`」以瀏覽至「**[!DNL Manage Data** > **Connections]**」頁面以將其簽出 — 有問題的資料庫整合是否有錯誤？ 若是如此，您可能需要[重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)，才能重新執行專案。

如果所有的整合都已成功連線，而且您並未處於更新週期中，則可能有其他問題發生。

#### 刪除[!DNL SQL]報告也會從我的Data Warehouse中刪除基礎欄嗎？

不會，無論您如何建立Data Warehouse的任何欄，都不會遺失這些欄。

如果您刪除使用`Data Warehouse Manager`的報表或查詢，則使用建立的欄不會受到影響。

使用[!DNL SQL Report Builder]建立的欄不會儲存至您的Data Warehouse。


#### `Report Builder`與`SQL Report Builder`

[!DNL SQL Report Builder]可讓您在建立及建構圖表時擁有更多彈性，例如，您可以選取應該顯示在`X`與`Y`軸上的值。 如需在[!DNL SQL Report Builder]中建立圖表的詳細資訊，請參閱[從 [!DNL SQL] 查詢建立視覺效果](../../tutorials/create-visuals-from-sql.md)教學課程。

#### `Cohort Report Builder` {#cohortrb}

與[!DNL Visual Report Builder]不同，[[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md)只有一個用途 — 分析和識別一段時間內類似使用者群組的行為趨勢。 使用[!DNL Cohort Report Builder]不需要任何[!DNL SQL]知識，因此如果您剛開始使用，可以毫不猶豫地直接開始使用。

| **這是最適合的……** | **這不太適合……** |
|---|---|
| 中級/進階分析師 | 初學者 — 您需要定義練習的同類群組。 |
| 識別一段時間的行為趨勢 | 定性分析 — 可以是[完成](../dev-reports/create-qual-cohort-analysis.md)，但需要Adobe協助。 |

## 在更新週期後重建查詢

您不需要重新建置查詢。 使用[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)建立的報告會像在傳統`Report Builder`中建立的報告一樣儲存。 [!DNL SQL]個圖表的更新程式相同 — 您的資料更新後，圖表中的值將會重新計算並重新顯示。

>[!NOTE]
>
>刪除[!DNL SQL]報表/查詢時，它不會從Data Warehouse中刪除基礎欄。 無論您如何建立欄，都不會遺失任何欄。

* 如果您刪除使用這些欄的報表或查詢，使用Data Warehouse Manager建立的欄不會受到影響。

* 使用SQL Report Builder建立的欄不會儲存至您的Data Warehouse。

## 正在結束 {#wrapup}

如果您想要嘗試更具挑戰性的工作，為什麼不嘗試編寫針對視覺效果最佳化的查詢？ 請檢視[從 [!DNL SQL] 查詢教學課程](../../tutorials/create-visuals-from-sql.md){: target="_blank"}建立視覺效果以開始。
