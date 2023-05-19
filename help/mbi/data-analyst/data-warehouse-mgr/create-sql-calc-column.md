---
title: 建立和使用SQL計算列
description: 瞭解如何在新的Adobe Commerce智慧體系結構上以SQL計算列的形式建立高級列。
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# 建立SQL計算列

本主題概述了 `Calculation` 列類型，可以使用 [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md)。 下面將介紹SQL計算的作用、使用原因、建立SQL計算的過程，並包括兩個示例。

**解釋**

過去，那些被認為 `advanced` 只能由此處的「客戶成功」團隊的分析師完成 [!DNL Adobe Commerce Intelligence]。 現在，所有功能都掌握在最終用戶手中，而高級列可以以 `SQL Calculation` 列 [!DNL Commerce Intelligence] 架構。

的 `Calculation` 列類型(現在在Data Warehouse管理器中可用)是同一表操作，它允許您使用PostgreSQL邏輯轉換表上的列。 有關可用於的函式和運算子的文檔 `Calculation` 列類型可在PostgreSQL網站上找到 [這裡](https://www.postgresql.org/docs/9.6/functions.html)。

可以使用 `Calculation` 列幾乎是無限的，但大多數列都可以使用IF-THEN語句和基本算術建立，下面的示例中使用了這些語句。

**示例1:客戶的最後一份訂單嗎？**

大多數帳戶都有一個名為 `Is customer's last order?` 在 `orders` 表，用於對重複採購費率和已變更的客戶執行分析。 如果帳戶位於新體系結構上，則此列使用 `Calculation` 列中，可在以下螢幕截圖中看到：

![](../../assets/Is_customer_s_last_order.png)

的 `Is customer's last order?` 列使用輸入 `Customer's lifetime number of orders` 和 `Customer's order number` 別名 `A` 和 `B` 分別進行。

逐行顯示，PostgreSQL的含義是：

* 案例：這將啟動一系列If - Then語句
* 何時 `A` 為空或 `B` 為空，然後為空：如果其中一個輸入為空，則輸出也應為空。 這是為了防止SQL錯誤
* 何時 `A=B` 然後 `Yes`:如果 `Customer's lifetime number of orders` 等於 `Customer's order number` 返回 `Yes`。 因此，如果客戶已下了4個訂單，則第4個訂單的行將返回 `Yes` 為 `Is customer's last order?`
* 其他 `No`:如果沒有其他語句在滿足聲明時返回 `No`
* 結束：這將結束If - Then語句

此列可返回的可能值(`NULL`。 `Yes`。 `No`)包含非數字字元，因此此處的資料類型為String。

**示例2:訂單物料總值（數量x價格）**

許多客戶喜歡在項目層分析收入，按欄位(如 `product name` 或 `category`。 大多數資料庫實際上並不會按順序提供產品的收入；而是提供訂單中的銷售數量和物料的價格。

要啟用產品收入分析，大多數帳戶都有一個名為 `Order item total value (quantity * price)` 在 `Orders Items` 的子菜單。 如果帳戶位於新體系結構上，則此列也使用 `Calculation` 列中，可在以下螢幕截圖中看到：

![](../../assets/Order_item_total_value.png)

在Commerce架構中， `Order item total value (quantity * price)` 列使用輸入 `qty ordered` 和 `base price` 別名 `A` 和 `B` 分別進行。

此新列返回的值以美元和美分計，因此正確的資料類型是 `Decimal(10,2)`。

**力學**

新 `Calculation` 通過導航到 **[!DNL Manage Data > Data Warehouse]** 如下所示：

![](../../assets/blobid2.png)

在此處，您可以建立 `Calculation` 按照以下步驟進行列：

1. 選擇要在其上添加的表 `Calculation` 的雙曲餘切值。
1. 在正確的表上，按一下 **[!UICONTROL Create New Column]** 右上角。
1. 從 `Select a definition` 下拉清單，選擇 `Same Table`。
1. 選擇 `Calculation` 的 `column definition equation`。
1. 輸入列名。
1. 選擇 `input` 列。 您添加的每列都會獲取字母別名，因此第一列是 `A`，第二個是 `B` 等等。
1. 在窗口中，使用輸入的字母別名為新列鍵入PostgreSQL邏輯。 SQL計算應限於單個列定義，包括SQL查詢的SELECT語句和FROM語句之間的所有邏輯。 使用任何輸入字母的SQL關鍵字應為小寫。 例如，當使用 `CASE` 語句，它應該寫成小寫 —  `case`。 系統假定大寫 `A` 指其中一個輸入。
1. 選擇適當的資料類型。
   * `Integer`  — 整數
   * `Decimal(10,2)`  — 一個小數，總位數為10，其中2位於小數點的右側
   * `String`  — 使用非數字的任何類型的文本或字元系列
   * `Datetime` -yyyy-MM-dd hh:mm:ss格式

1. 按一下 **[!UICONTROL test column]**。 這將為每個輸入生成五個test值的清單，並顯示每組test值的步驟6中的邏輯結果。 如果SQL的任何部分都生成錯誤，則返回相應的錯誤消息。 僅當所有輸入列均為本機欄位時，才能生成示例結果。 如果任何輸入列是計算列，則必須通過將列添加到度量並在可視Report Builder中查看來驗證結果

1. 對結果滿意後，按一下 **[!UICONTROL Save]**。 列可供使用。
