---
title: 建置[!DNL Google ECommerce]維度
description: 瞭解如何建立將您的電子商務資料與您的訂單和客戶資料連結的維度。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 建置[!DNL Google ECommerce]維度

>[!NOTE]
>
>需要[管理員許可權](../../administrator/user-management/user-management.md)。

現在您已完成[連線您的[!DNL Google ECommerce]帳戶](../../data-analyst/importing-data/integrations/google-ecommerce.md)，您可以在[!DNL Commerce Intelligence]中處理這些資料嗎？ 本主題將引導您建立維度，將您的電子商務資料與您的訂單和客戶資料連結在一起。

所涵蓋的維度可讓您建立分析，以[回答有關行銷管道和行銷活動的重要問題](../../data-analyst/analysis/most-value-source-channel.md)。 每個來源各佔總收入的百分比為何？ [!DNL Facebook]已取得客戶的期限值與[!DNL Google]的客戶有何不同？

## 必要條件和概覽

若要在此主題中建立維度，您需要[!DNL Google ECommerce]表格、`orders`表格和`customers`表格。 這些資料表必須先同步至[您的Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md)，才能建立維度。 已同步的資料表會顯示在`Synced Tables`的`Data Warehouse Manager`區段中。

如果您需要重新整理程式，以下快速瞭解同步表格和欄：

![](../../assets/Syncing_New_Columns.gif)

從`orders`表格建立連結至[!DNL Google eCommerce]表格之後，您會在下列清單中建立前三個維度。 接著，使用這些維度在`customers`表格中建立三個使用者/客戶維度。 若要完成，請將這些資料行加入`orders`資料表。

以下為涵蓋的維度：

* **訂單資料表**

* 訂單的[!DNL Google Analytics]來源
* 訂單的[!DNL Google Analytics]媒體
* 訂單的[!DNL Google Analytics]行銷活動
* 客戶第一筆訂單的[!DNL Google Analytics]來源
* 客戶第一筆訂單的[!DNL Google Analytics]媒體
* 客戶第一筆訂單的[!DNL Google Analytics]行銷活動

* **客戶資料表**

* 客戶第一筆訂單的[!DNL Google Analytics]來源
* 客戶第一筆訂單的[!DNL Google Analytics]媒體
* 客戶第一筆訂單的[!DNL Google Analytics]行銷活動

## 建立維度

若要建立維度，請按一下[ > ](../data-warehouse-mgr/tour-dwm.md)以開啟&#x200B;**[!UICONTROL Data]** Data Warehouse管理員&#x200B;**[!UICONTROL Data Warehouse]**。

### 訂單表格，第1回合

此範例會建置&#x200B;**訂單的[!DNL Google Analytics] Source**&#x200B;維度。

1. 從Data Warehouse中的表格清單中，按一下包含訂單資訊的表格（在此例中為`orders`）。
1. 按一下&#x200B;**[!UICONTROL Create a Column]**。
1. 為欄命名。
1. 從`Joined Column`定義下拉式清單[中選取](../data-warehouse-mgr/calc-column-types.md)。 此範例適用於[一對一關係](../data-warehouse-mgr/table-relationships.md)，將`eCommerce.transactionID`資料行與`orders`資料表的一列相符。
1. 接下來，您需要定義路徑，或定義所使用的表格和欄的連線方式。 按一下`Select a table and column`下拉式清單。
1. 您需要的路徑無法使用，因此您需要建立新的路徑。 按一下&#x200B;**[!UICONTROL Create new Path]**。
1. 在顯示的視窗中，將`Many`端設定為`orders.order\_id`，或將`orders`表格中包含訂單ID的欄設定為。
1. 在`One`端，找到`Google ECommerce`資料表，然後將資料行設定為`transactionID`。

   ![](../../assets/google-ecommerce-table.png)

1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以建立路徑。
1. 新增路徑後，再按一下&#x200B;**[!UICONTROL Select table and column]**&#x200B;下拉式清單。
1. 找到`ECommerce`資料表，然後按一下`Source`資料行。 這會將訂單連結至來源資訊。
1. 回到表格結構描述後，再按一下「**[!UICONTROL Save]**」以建立維度。

以下是整個程式的概況：

![](../../assets/help_center.gif)

接下來，嘗試建立&#x200B;**訂單的[!DNL Google Analytics]媒體**&#x200B;和`campaign`。 這些維度沒有太多變更，所以請嘗試一下。 但如果您卡住了，可以檢視[本文結尾](#stuck)，看看有什麼不同之處。

### 客戶表格 {#customers}

此範例會建置&#x200B;**客戶第一個訂單的[!DNL Google Analytics]來源**&#x200B;維度。

1. 從Data Warehouse中的表格清單中，按一下包含客戶資訊的表格（在此例中為`customers`）。
1. 按一下&#x200B;**[!UICONTROL Create a Column]**。
1. 為欄命名。
1. 在此範例中，從`is MAX`定義下拉式清單[中選取](../../data-analyst/data-warehouse-mgr/calc-column-types.md)定義。 如果套用至只有一個可能值的文字欄，`is MIN`定義也可以運作。 重要部分是確保設定正確的篩選器，您稍後再執行。
1. 按一下&#x200B;**[!UICONTROL Select a table and column]**&#x200B;下拉式清單，選取`orders`資料表，然後選取`Order's [!DNL Google Analytics] source`資料行。
1. 按一下&#x200B;**[!UICONTROL Save]**。
1. 回到表格結構描述後，按一下`Options`下拉式清單，然後`Filters`。
1. 按一下&#x200B;**[!UICONTROL Add Filter Set]**，然後選取`Orders we count`集。 您只希望納入您盤點篩選集之訂單中的訂單，因此請務必選取此篩選集。
1. 按一下&#x200B;**[!UICONTROL Add Filter]**。 您想要尋找客戶的第一個訂單[!DNL Google Analytics]來源，因此您需要新增篩選器：

   _orders.客戶的訂單編號= 1

   _
1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以建立維度。

接下來，嘗試建立&#x200B;**客戶第一張訂單的[!DNL Google Analytics]媒體**&#x200B;和`campaign`。 這些維度沒有太多變更，所以請嘗試一下。 但如果您卡住了，可以檢視[本文結尾](#stuck)，看看有什麼不同之處。

### 額外優點：訂單表格，第2回合

您可以視需要在此停止，但此區段會將您在&#x200B;**最後一個區段[!DNL Google Analytics]中建立的**&#x200B;客戶第一訂單的[維度](#customers)帶入`orders`表格，以啟用進一步分析。 在此區段中建立維度可讓您使用客戶第一張訂單的`orders`屬性，分析在`Revenue`表格（`Number of orders`、`Distinct buyers`、[!DNL Google Analytics]等等）上建置的所有量度。

此範例將`Customer's first order's [!DNL Google Analytics] source`維度聯結至`orders`資料表。

1. 從Data Warehouse中的表格清單中，按一下包含訂單資訊的表格（在此例中為`orders`）。
1. 按一下&#x200B;**[!UICONTROL Create a Column]**。
1. 為欄命名。
1. 從定義下拉式清單中選取`Joined Column`。 這會將您在上一節建立的客戶維度加入`orders`表格。
1. 按一下&#x200B;**[!UICONTROL Select a table and column]**&#x200B;下拉式清單，然後選取`customers`表格和`Customer's first order's [!DNL Google Analytics] source`欄。
1. 如果路徑未自動填入，請選取最能連線客戶和訂單表格的路徑。
1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以建立維度。

以下是整個程式的概況：

![](../../assets/help_center2.gif)

將`Customer's first order's`媒體和`campaign`維度加入`orders`表格以完成作業。 加入維度，如果發生問題，則在您需要協助時檢視[文章結尾](#stuck)。

### 正在結束

您已建立完維度，這表示您現在可以建立強大的分析，以追蹤各種管道和行銷活動的績效。 請記住，在下次更新完成&#x200B;**之前，**&#x200B;新資料行將無法使用。

本主題會介紹一些較受歡迎的維度，但天空是極限 — 請嘗試建立您自己的維度，或如果您想尋求探索其他選項的協助，請隨時試試看。 

### 其他附註

**`Orders`資料表#1**：建立`Order's [!DNL Google Analytics]`媒體和`campaign`維度時，差異在於步驟12中選取的資料行。 在此範例中，資料行是`Source`。

**`Customers`資料表**：建立`Customer's first order's [!DNL Google Analytics]`媒體和`campaign`維度時，差異是步驟5中選取的資料行。 在此範例中，資料行是`Order's [!DNL Google Analytics]`來源。

**`Orders`資料表#2**：將`Customer's first order's [!DNL Google Analytics]`個媒體和`campaign`個資料行加入`orders`資料表時，差異是步驟5中選取的資料行。 在此範例中，資料行是`Customer's first order's [!DNL Google Analytics]`來源。
