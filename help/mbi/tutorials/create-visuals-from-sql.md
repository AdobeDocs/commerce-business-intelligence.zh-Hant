---
title: 從SQL查詢建立視覺效果
description: 瞭解如何熟悉SQL Report Builder中使用的術語，並為您建立SQL視覺效果奠定堅實的基礎。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# 從SQL查詢建立視覺效果

本教學課程的目標是讓您熟悉[!DNL SQL Report Builder]中使用的術語，並為您建立`SQL visualizations`奠定堅實的基礎。

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md)是具有選項的Report Builder：您可以僅為了擷取資料表的目的而執行查詢，也可以將這些結果轉換為報表。 本教學課程說明如何從SQL查詢建立視覺效果。

## 術語

開始此教學課程之前，請參閱`SQL Report Builder`中使用的下列術語。

- `Series`：您要測量的資料行在SQL Report Builder中稱為序列。 常見的範例是`revenue`、`items sold`和`marketing spend`。 至少必須有一個資料行設定為`Series`才能建立視覺效果。

- `Category`：您要用來劃分資料的資料行稱為`Category`，就像`Group By`中的[`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md)功能一樣。 例如，如果您想要依客戶的贏取來源來劃分客戶期限收入，則會將包含贏取來源的欄指定為`Category`。 可以將多個資料行設定為`Category`。

>[!NOTE]
>
>日期和時間戳記也可當作`Categories`使用。 它們只是查詢中的另一欄資料，必須在查詢中視需要設定格式和排序。

- `Labels`：這些會套用為x軸標籤。 分析一段時間的資料趨勢時，會將年份和月份欄指定為標籤。 可以將多個欄設定為Label。

## 步驟1：撰寫查詢

請牢記以下事項：

- [!DNL SQL Report Builder]使用[`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html)。

- 如果您要建立具有時間序列的報告，請務必`ORDER BY`時間戳記欄。 這樣可確保時間戳記在報表上的繪製順序正確無誤。

- `EXTRACT`函式非常適合用於剖析時間戳記的日、周、月或年。 當您要在報告上使用的`time interval`是`daily`、`weekly`、`monthly`或`yearly`時，這會很有用。

若要開始，請按一下[!DNL SQL Report Builder]以開啟&#x200B;**[!UICONTROL Report Builder** > **SQL Report Builder]**。

例如，假設此查詢傳回每個產品每月的銷售專案總數：

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

此查詢會傳回此結果表：

![顯示SQL查詢結果的表格，其中包含依產品、年份和月份銷售的專案](../assets/SQL_results_table.png)

## 步驟2：建立視覺效果

使用這些結果，*您如何建立視覺效果？*&#x200B;若要開始，請按一下&#x200B;**[!UICONTROL Chart]**&#x200B;窗格中的`Results`索引標籤。 這會顯示`Chart settings`標籤。

第一次執行查詢時，報表可能看起來難以捉摸，因為查詢中的所有欄都繪製為序列：

![初始SQL報告，所有資料行均繪製為數列](../assets/SQL_initial_report_results.png)

在此範例中，您希望這會是隨時間變化的折線圖。 若要建立檔案，請使用下列設定：

- `Series`：選取`Items sold`資料行作為`Series`，因為您想要測量它。 定義`Series`欄後，您會在報表中看到繪製的單一線條。

- `Category`：在此範例中，您想要以報表中不同的行來檢視每個產品。 若要這麼做，請將`Product name`設為`Category`。

- `Labels`：使用資料行`year`和`month`做為x軸上的標籤，以便檢視`Items Sold`隨時間的趨勢。

>[!NOTE]
>
>如果標籤為`ORDER BY`/`date`欄，則查詢必須在標籤上包含`time`子句。

以下快速瞭解您如何建立此視覺效果，從執行查詢到設定報表：

![設定SQL報表視覺效果設定的動畫示範](../assets/SQL_report_settings.gif)

## 步驟3：選取`Chart Type`

此範例使用`Line`圖表型別。 若要使用其他`chart type`，請按一下圖表選項區段上方的圖示以變更它：

![可用的圖表型別圖示，包括線條、長條、區域和其他視覺化選項](../assets/Chart_types.png)

## 步驟4：儲存視覺效果

如果您想要再次使用此報表，請為報表命名，然後按一下右上角的&#x200B;**[!UICONTROL Save]**。

在下拉式清單中，選取`Chart`作為`Type`，然後選取要儲存報告的儀表板。

## 正在結束

想要更進一步嗎？ 請檢視[查詢最佳化最佳實務](../best-practices/optimizing-your-sql-queries.md)。
