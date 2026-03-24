---
title: 合併您的表格
description: 瞭解如何整合表格和資料庫。
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
TQID: https://experienceleague.adobe.com/HC5REx483htdfFigZPxcrZeD5byyJKk-beQqnEARt1E
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---

# 合併您的表格

如果您經營多個店面或在多個市場，可能會有個別儲存的類似資料庫。 在[!DNL Adobe Commerce Intelligence]中，將來自不同資料庫的類似資料表合併在一起很容易。

例如，您可能有適用於`orders`的`Market A`資料表以及適用於`orders`的類似`Market B`資料表。 [!DNL Commerce Intelligence]可以合併兩個資料表，並可讓您檢視來自`Market A`和`B`的彙總訂單資料，以及依特定市場進行分段。

若要讓資料表的合併生效，輸入資料表必須是&#x200B;**類似結構**。 換言之，所有輸入表格都必須包含統一表格中所需的資料欄。

本主題討論整合表格的一些最常見的使用案例，以及建立自己的表格所需的後續步驟。

## 關於何時使用合併表格的建議

以下討論何時適合在系統中使用整合表格。

### 整合來自多個網站的資料

如果您在不同品牌和網站下銷售產品，每個品牌或網站的表格結構可能會類似。

例如，您可能有網站`orders`的`A`資料表，以及網站`orders`的個別但類似的`B`資料表。 在此情況下，從網站`orders`與`A`合併`B`資料表可能很有用。 這可讓您檢視網站`A`和`B`的合併收入與訂單數，以及這兩個網站劃分量度的能力。

### 整合舊資料

許多公司曾經重組過資料庫，舊資料庫中的資料並不總是會轉換為新系統。 您可以使用統一表格將舊版表格的索引鍵資料欄與作用中系統的索引鍵資料欄聯結。 這可讓您在整個歷程記錄中對資料進行統一分析。

### 結合活動使用者分析的事件

想像一個使用者可執行數項操作的網站：參加調查、玩遊戲、購物、介紹朋友等。 通常，這些事件都會儲存在其本身的表格中。 這讓您難以分析在指定時段內，有多少不同的使用者至少執行了任何種類的動作。

您可以使用整合表格來建立一個包含所有使用者以及發生其中任何事件的統一清單。 然後，您可以在整合表格上執行查詢，以輕鬆進行此類分析。

與Data Warehouse中的所有其他表格一樣，您可以新增其他欄以支援各種圖表和分析。

## 建立、檢視或更新統一表格

如果您有興趣將整合資料表新增至您的Data Warehouse，請連絡[!DNL Commerce Intelligence] [支援](../guide-overview.md#Submitting-a-Support-Ticket)。

>[!NOTE]
>
>由於無法在`Data Warehouse Manager`中檢視整合的資料表，因此檢視和更新這些資料表只能由[!DNL Commerce Intelligence]支援完成。
