---
title: 建置[!DNL Google ECommerce]維度
description: 了解如何建立維度，將您的電子商務資料與訂單和客戶資料連結。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# 建置 [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md).

現在你完成了 [連接[!DNL Google ECommerce]帳戶](../../data-analyst/importing-data/integrations/google-ecommerce.md)，您在 [!DNL MBI]? 本文會逐步帶您了解如何建立維度，將您的電子商務資料與訂單和客戶資料建立連結。

涵蓋的尺寸使您能夠建立分析， [回答與行銷管道和行銷活動相關的重要問題](../../data-analyst/analysis/most-value-source-channel.md). 每個來源的收入百分比是多少？ facebook所贏取客戶的期限值與 [!DNL Google]?

## 必要條件與概觀

若要在本文中建立維度，您需要 [!DNL Google ECommerce] 表格， `orders` 表格和 `customers` 表格。 那些表必須 [同步至Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 之後才能建立維度。 同步的表格會顯示在 `Synced Tables` 區段 `Data Warehouse Manager`.

如果您需要重新整理，以下提供同步的表格和欄的快速資訊：

![](../../assets/Syncing_New_Columns.gif)

從建立連結之後 `orders` 表格 [!DNL Google eCommerce] 表格中，您可在下方清單中建立前三個維度。 接下來，您可使用這些維度，在 `customers` 表格。 最後，您將這些欄連結至 `orders` 表格。

涵蓋的維度如下：

* **訂購表**

* 訂購 [!DNL Google Analytics] 來源
* 訂購 [!DNL Google Analytics] 媒體
* 訂購 [!DNL Google Analytics]行銷活動
* 客戶的首次訂購 [!DNL Google Analytics] 來源
* 客戶的首次訂購 [!DNL Google Analytics] 媒體
* 客戶的首次訂購 [!DNL Google Analytics] 行銷活動

* **客戶表**

* 客戶的首次訂購 [!DNL Google Analytics] 來源
* 客戶的首次訂購 [!DNL Google Analytics] 媒體
* 客戶的首次訂購 [!DNL Google Analytics] 行銷活動

## 建立維度

若要建立維度，請開啟 [Data Warehouse管理員](../data-warehouse-mgr/tour-dwm.md) 按一下 **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 訂單表，第1回合

此範例會建置 **訂購 [!DNL Google Analytics] 來源** 維度。

1. 從Data Warehouse的表清單中，按一下表(在本例中， `orders`)，其中包含您的訂單資訊。
1. 按一下 **[!UICONTROL Create a Column]**.
1. 為欄命名。
1. 選擇 `Joined Column` 從 [定義下拉式清單](../data-warehouse-mgr/calc-column-types.md). 此範例適用於 [一對一關係](../data-warehouse-mgr/table-relationships.md)，符合 `eCommerce.transactionID` 一列 `orders` 表格。
1. 接下來，您需要定義路徑，或所使用的表格和欄的連線方式。 按一下 `Select a table and column` 下拉式清單。
1. 您需要的路徑不可用，因此您需要建立新路徑。 按一下 **[!UICONTROL Create new Path]**.
1. 在顯示的視窗中，設定 `Many` 側向 `orders.order\_id`，或 `orders` 包含訂單ID的表格。
1. 在 `One` 側，查找 `Google ECommerce` 表格，然後將欄設定為 `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. 按一下 **[!UICONTROL Save]** 來建立路徑。
1. 新增路徑後，按一下 **[!UICONTROL Select table and column]** 再次下拉式清單。
1. 找出 `ECommerce` 表格，然後按一下 `Source` 欄。 這會將訂單系結至來源資訊。
1. 返回表架構後，按一下 **[!UICONTROL Save]** 再次，以建立維度。

以下是整個程式：

![](../../assets/help_center.gif)

接下來，嘗試建立 **訂購 [!DNL Google Analytics] 媒體** 和 `campaign`. 這些維度沒有太多變更，請試一試。 但如果你被卡住了，你可以檢查 [本文的結尾](#stuck) 看看有什麼不同。

### 客戶表 {#customers}

此範例會建置 **客戶的首次訂購 [!DNL Google Analytics] 來源** 維度。

1. 從Data Warehouse的表清單中，按一下表(在本例中， `customers`)，其中包含您的客戶資訊。
1. 按一下 **[!UICONTROL Create a Column]**.
1. 為欄命名。
1. 在此範例中，選取 `is MAX` 定義 [定義下拉式清單](../../data-analyst/data-warehouse-mgr/calc-column-types.md). 此 `is MIN` 如果套用至只有一個可能值的文字欄，定義也可能有效。 重要的部分是確保已設定正確的篩選器，您稍後會這麼做。
1. 按一下 **[!UICONTROL Select a table and column]** 下拉式清單，然後選取 `orders` 表格，然後 `Order's [!DNL Google Analytics] source` 欄。
1. 按一下 **[!UICONTROL Save]**.
1. 回到表格架構後，按一下 `Options` 下拉式清單，然後 `Filters`.
1. 按一下 **[!UICONTROL Add Filter Set]** ，然後選取 `Orders we count` 設定。 您只希望包含在計數篩選器集的訂單中，因此請務必選取此篩選器集。
1. 按一下 **[!UICONTROL Add Filter]**. 您想要找到客戶的首筆訂單 [!DNL Google Analytics] 來源，因此您需要新增篩選器：

   _orders.客戶的訂單編號= 1

   _
1. 按一下 **[!UICONTROL Save]** 來建立維度。

接下來，嘗試建立 **客戶的首次訂購 [!DNL Google Analytics] 媒體** 和 `campaign`. 這些維度沒有太多變更，請試一試。 但如果你被卡住了，你可以檢查 [本文的結尾](#stuck) 看看有什麼不同。

### 額外好處：訂單表，第2回合

您可以視需要停止於此處，但本節會將 **客戶的首次訂購 [!DNL Google Analytics] 維度** 您在 [最後一節](#customers) 進入 `orders` 表格。 在此區段中建立維度，可讓您分析所有建置在 `orders` 表格 —  `Revenue`, `Number of orders`, `Distinct buyers`、等 — 使用 [!DNL Google Analytics] 客戶首次訂購的屬性。

此範例連結 `Customer's first order's [!DNL Google Analytics] source` 維度 `orders` 表格。

1. 從Data Warehouse的表清單中，按一下表(在本例中， `orders`)，其中包含您的訂單資訊。
1. 按一下 **[!UICONTROL Create a Column]**.
1. 為欄命名。
1. 選擇 `Joined Column` 從「定義」下拉式清單。 這會將您在上一節中建立的客戶維度連結至 `orders` 表格。
1. 按一下 **[!UICONTROL Select a table and column]** 下拉式清單，然後選取 `customers` 表格和 `Customer's first order's [!DNL Google Analytics] source` 欄。
1. 如果路徑未自動填入，請選取最能連接客戶和訂單表格的路徑。
1. 按一下 **[!UICONTROL Save]** 來建立維度。

以下是整個程式：

![](../../assets/help_center2.gif)

最後，加入 `Customer's first order's` 中型 `campaign` 維度 `orders` 表格。 連接維，如果有問題，請簽出 [文章結尾](#stuck) 如果你需要幫助。

### 包裝

您已完成維度的建立，這表示您現在可以建立功能強大的分析，以追蹤各個管道和促銷活動的效能。 請記住 **下次更新完成後，新欄才可用**.

本文涵蓋一些較熱門的維度，但天空是限制 — 嘗試建立自己的維度，或者如果您想在探索其他選項時提供協助，就可以隨時向我們提示。 

### 我被卡住了！ 有什麼不同？ {#stuck}

**`Orders`表#1:** 建立 `Order's [!DNL Google Analytics]` 中型 `campaign` 維度中，差異為步驟12中選取的欄。 在此範例中，欄是 `Source`.

**`Customers`表格：** 建立 `Customer's first order's [!DNL Google Analytics]` 中型 `campaign` 維度中，差異為在步驟5中選取的欄。 在此範例中，欄是 `Order's [!DNL Google Analytics]` 來源。

**`Orders`表#2:** 加入 `Customer's first order's [!DNL Google Analytics]` 中型 `campaign` 欄 `orders` 表格中，差異為在步驟5中選取的欄。 在此範例中，欄是 `Customer's first order's [!DNL Google Analytics]` 來源。
