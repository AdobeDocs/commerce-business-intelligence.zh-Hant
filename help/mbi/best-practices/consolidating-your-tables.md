---
title: 合併您的表格
description: 瞭解如何整合表格和資料庫。
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 合併您的表格

如果您經營多個店面或在多個市場，可能會有個別儲存的類似資料庫。 在 [!DNL Adobe Commerce Intelligence]，將不同資料庫的類似表格輕鬆整合在一起。

例如，您可能會 `orders` 表格 `Market A`和類似專案 `orders` 表格 `Market B`. [!DNL Commerce Intelligence] 可以合併兩個表格，並允許您檢視來自兩者的彙總訂單資料 `Market A` 和 `B`，以及依特定市場進行細分。

若要讓資料表合併生效，輸入資料表必須 **類似結構**. 換言之，所有輸入表格都必須包含統一表格中所需的資料欄。

本主題討論整合表格的一些最常見的使用案例，以及建立自己的表格所需的後續步驟。

## Recommendations以瞭解何時使用整合表格

以下討論何時適合在系統中使用整合表格。

### 整合來自多個網站的資料

如果您在不同品牌和網站下銷售產品，每個品牌或網站的表格結構可能會類似。

例如，您可能會 `orders` 網站的表格 `A` 和一個單獨的，但相似的， `orders` 網站的表格 `B`. 在此情況下，合併 `orders` 來自網站的表格 `A` 和 `B`. 這可讓您檢視網站的合併收入和訂單數 `A` 和 `B`，此外還能夠依這兩個網站劃分量度。

### 整合舊資料

許多公司曾經重組過資料庫，舊資料庫中的資料並不總是會轉換為新系統。 您可以使用統一表格將舊版表格的索引鍵資料欄與作用中系統的索引鍵資料欄聯結。 這可讓您在整個歷程記錄中對資料進行統一分析。

### 結合活動使用者分析的事件

想像一個使用者可執行數項操作的網站：參加調查、玩遊戲、購物、介紹朋友等。 通常，這些事件都會儲存在其本身的表格中。 這讓您難以分析在指定時段內，有多少不同的使用者至少執行了任何種類的動作。

您可以使用整合表格來建立一個包含所有使用者以及發生其中任何事件的統一清單。 然後，您可以在整合表格上執行查詢，以輕鬆進行此類分析。

與Data Warehouse中的所有其他表格一樣，您可以新增其他欄以支援各種圖表和分析。

## 建立、檢視或更新統一表格

如果您有興趣將整合表格新增至您的Data Warehouse，請聯絡 [!DNL Commerce Intelligence] [支援](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>由於無法檢視整合表格，因此 `Data Warehouse Manager`，檢視和更新這些表格只能由以下人員完成 [!DNL Commerce Intelligence] 支援。
