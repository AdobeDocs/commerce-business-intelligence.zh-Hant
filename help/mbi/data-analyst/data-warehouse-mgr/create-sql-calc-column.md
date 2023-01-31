---
title: 建立和使用SQL計算列
description: 了解如何以新MBI體系結構上的SQL計算列的形式建立高級列。
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 建立SQL計算列

本主題概述 `Calculation` 欄類型：可使用 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md). 以下說明SQL計算的作用、使用原因、建立SQL計算的過程以及兩個示例。

**說明**

過去， `advanced` 只能由客戶成功團隊的分析師在此完成 [!DNL MBI]. 現在，所有功能都掌握在最終用戶手中，而高級列可以以 `SQL Calculation` 欄 [!DNL MBI] 架構。

此 `Calculation` 列類型(現在在「Data Warehouse管理器」中可用)是同一表操作，允許您使用PostgreSQL邏輯轉換表上的列。 關於可在 `Calculatio`在PostgreSQL網站上可以找到n列類型 [此處](https://www.postgresql.org/docs/9.6/static/functions.html).

可使用 `Calculation` 欄幾乎無限制，但大部分欄可使用IF-THEN陳述式和基本算術來建立，這些將用於以下範例中。

**範例1:客戶的最後訂單？**

大部分帳戶都有一欄稱為 `Is customer's last order?` 在 `orders` 表格，用於對重複購買率和週轉客戶執行分析。 如果您的帳戶位於新架構，則此欄會使用 `Calculation` 欄，並可在下方的螢幕擷取中看到：

![](../../assets/Is_customer_s_last_order.png)

此 `Is customer's last order?` 欄使用輸入 `Customer's lifetime number of orders` 和 `Customer's order number` 已將 `A` 和 `B` 分別為5個。

逐行顯示，PostgreSQL的含義是：

* 案例：這會啟動一系列If - Then陳述式
* when `A` 為null或 `B` 為null，然後為null。如果其中一個輸入為空，則輸出也應為空。 這是為了防止SQL錯誤
* when `A=B` then `Yes`:若 `Customer's lifetime number of orders` 等於 `Customer's order number` 然後返回 `Yes`. 因此，如果客戶下了4個訂單，則第4個訂單的行將返回 `Yes` for `Is customer's last order?`
* else `No`:如果沒有其他語句在滿足時返回 `No`
* 結束：這會結束If - Then陳述式

此欄可傳回的可能值(`NULL`, `Yes`, `No`)包含非數字字元，因此此處的資料類型為字串。

**範例2:訂單項目總值（數量*價格）**

我們的許多客戶喜歡在項目層級分析收入，依欄位(例如 `product name` 或 `category`. 實際上，大多數資料庫並不會按訂單提供某產品的收入；而是提供訂單中的銷售數量和項目價格。

為了啟用產品收入分析，大部分帳戶都有一個名為 `Order item total value (quantity * price)` 在 `Orders Items` 表格。 如果您的帳戶位於新架構，則此欄也會使用 `Calculation` 欄，並可在下方的螢幕擷取中看到：

![](../../assets/Order_item_total_value.png)

在商務結構中， `Order item total value (quantity * price)` 欄使用輸入 `qty ordered` 和 `base price` 已將 `A` 和 `B` 分別為5個。

此新欄所傳回的值會是美金和美分，因此正確的資料類型為 `Decimal(10,2)`.

**力學**

新 `Calculation` 欄可導覽至 **[!DNL Manage Data > Data Warehouse]** 如下所示：

![](../../assets/blobid2.png)

您可以從此處建立新 `Calculation` 欄，請依照下列步驟執行：

1. 選取要在其上新增 `Calculation` 欄。
1. 在正確的表格上，按一下 **[!UICONTROL Create New Column]** 在畫面右上角。
1. 從 `Select a definition` 下拉式清單，選取 `Same Table`.
1. 選擇 `Calculation` 作為 `column definition equation`.
1. 輸入列名。
1. 選擇 `input` 表中用於新列邏輯的列。 您新增的每欄都會收到字母別名，因此第一欄會是 `A`，第二個是 `B` 等等。
1. 在視窗中，使用輸入項的字母別名為新列鍵入PostgreSQL邏輯。 SQL計算應限於單個列定義，包括SQL查詢的SELECT和FROM語句之間的所有邏輯。 請注意，使用任何輸入字母的SQL關鍵字應為小寫。 例如，使用 `CASE` 語句，應以小寫寫 —  `case`. 系統假設大寫 `A` 是指其中一個輸入。
1. 選擇相應的資料類型。
   * `Integer`  — 整數
   * `Decimal(10,2)`  — 小數位數，總位數為10，其中2位於小數點的右側
   * `String`  — 使用非數字的任何類型的文本或字元系列
   * `Datetime` - yyyy-MM-dd hh:mm:ss格式

1. 按一下 **[!UICONTROL test column]**. 這會為每個輸入產生5個測試值的清單，並顯示每組測試值之步驟6的邏輯結果。 如果SQL的任何部分生成錯誤，則將返回相應的錯誤消息。 請注意，只有當所有輸入列均為本機欄位時，才能產生範例結果。 如果任何輸入欄是計算欄，則您需要將欄新增至量度並在視覺化Report Builder中檢視，以驗證結果
1. 對結果滿意後，按一下 **[!UICONTROL Save]**，您的欄將可供使用。
