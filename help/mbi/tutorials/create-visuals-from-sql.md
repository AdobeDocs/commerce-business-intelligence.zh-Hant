---
title: 從SQL查詢建立可視化
description: 瞭解如何熟悉SQLReport Builder中使用的術語，並為建立SQL可視化奠定堅實的基礎。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 從SQL查詢建立可視化

本教程的目標是讓您熟悉在 [!DNL SQL Report Builder] 為你創造一個 `SQL visualizations`。

的 [[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) 是包含選項的報表生成器：您可以運行查詢，其唯一目的是檢索資料表，也可以將這些結果轉換為報告。 本教程介紹如何從SQL查詢生成可視化。

## 術語

在開始本教程之前，請參考以下術語。 `SQL Report Builder`。

- `Series`:要度量的列在SQLReport Builder中稱為系列。 常見示例有 `revenue`。 `items sold`, `marketing spend`。 必須至少將一列設定為 `Series` 建立可視化。

- `Category`:要用於分割資料的列稱為 `Category` 這就像 `Group By` 的 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md)。 例如，如果要按客戶的採購來源劃分客戶的生命週期收入，則包含採購來源的列將指定為 `Category`。 可以將多列設定為 `Category`。

>[!NOTE]
>
>日期和時間戳也可用作 `Categories`。 它們只是查詢中的另一列資料，必鬚根據查詢本身的需要進行格式化和排序。

- `Labels`:這些作為x軸標籤應用。 分析資料隨時間推移的趨勢時，年和月列被指定為標籤。 可以將多列設定為「標籤」。

## 步驟1:編寫查詢

請牢記以下事項：

- 的 [!DNL SQL Report Builder] 使用 [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html)。

- 如果要建立帶有時間序列的報告，請確保 `ORDER BY` 時間戳列。 這可確保以正確的順序在報表上繪製時間戳。

- 的 `EXTRACT` 函式用於解析時間戳的日、周、月或年。 當 `time interval` 要在報告中使用 `daily`。 `weekly`。 `monthly`或 `yearly`。

要開始，請開啟 [!DNL SQL Report Builder] 按一下 **[!UICONTROL Report Builder** > **SQL Report Builder]**。

例如，請考慮以下查詢：

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

此查詢返回此結果表：

![](../assets/SQL_results_table.png)

## 步驟2:建立可視化

有了這些結果， *如何建立可視化？* 要開始，請按一下 **[!UICONTROL Chart]** 的 `Results` 的子菜單。 這將顯示 `Chart settings` 頁籤。

當首次執行查詢時，報表可能看起來難以理解，因為查詢中的所有列都以系列形式顯示：

![](../assets/SQL_initial_report_results.png)

對於此示例，您希望它是隨時間變化的折線圖。 要建立它，請使用以下設定：

- `Series`:選擇 `Items sold` 列 `Series` 因為你想衡量。 定義 `Series` 列中，您將在報表中看到一條圖表。

- `Category`:在此示例中，您希望將每個產品作為報表中的不同行進行查看。 要執行此操作，請設定 `Product name` 的 `Category`。

- `Labels`:使用列 `year` 和 `month` 作為x軸上的標籤，以便能夠查看 `Items Sold` 隨著時間的流逝。

>[!NOTE]
>
>查詢必須包含 `ORDER BY` 子句 `date`/`time` 的子菜單。

下面是您如何建立此可視化的快速瞭解，從運行查詢到設定報告：

![](../assets/SQL_report_settings.gif)

## 第3步：選擇 `Chart Type`

此示例使用 `Line` 圖表類型。 使用其他 `chart type`，按一下圖表選項部分上方的表徵圖以更改它：

![](../assets/Chart_types.png)

## 第4步：保存可視化

如果要再次使用此報告，請為該報告指定名稱，然後按一下 **[!UICONTROL Save]** 在右上角。

在下拉清單中，選擇 `Chart` 的 `Type` 然後是一個儀表板以將報表保存到。

## 包裝

想再往前一步嗎？ 查看 [查詢優化最佳實踐](../best-practices/optimizing-your-sql-queries.md)。
