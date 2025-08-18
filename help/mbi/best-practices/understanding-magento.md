---
title: 瞭解您的 [!DNL Commerce Intelligence] 環境
description: 瞭解如何使用及改善您的 [!DNL Commerce Intelligence] 環境。
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# 您的[!DNL Adobe Commerce Intelligence]環境

當您分析商務資料時，請注意這些因素和常見的誤解。 若您需要協助以確保您正確使用Commerce結構描述，請立即[聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## [!DNL entity\_id]

許多資料表包含名為`entity\_id`的資料行。 在每個包含`entity\_id`的資料表中，該資料行是用來識別唯一資料列。

例如，`sales\_order`表格中的每一列都是唯一順序。 此資料表中的主索引鍵稱為`entity\_id`。 可將此資料行視為`order\_id`。 在個別表格`customer\_entity`中，每一列代表一個不重複客戶。 此資料表中的主索引鍵也稱為`entity\_id`，可以將其視為`customer\_id`。

在這些資料表中，`sales\_order.entity\_id`不等於`customer\_entity.entity\_id`。 這適用於包含`entity\_id`的所有資料表集： `table\_A.entity\_id`不等於`table\_B.entity\_id`。

## [!DNL Guest orders]

如果您允許客戶在沒有帳戶（訪客訂單）的情況下從您的網站訂購，則這些客戶不會填入為您`customer\_entity`表格中的列。 此外，客體所下的每個訂單在`customer\_id`資料表上都有空的`sales\_order`值。

因此，如果您想要追蹤來賓在一段時間內的行為，所有客戶層級的欄都必須使用客戶識別碼（例如`sales\_order`）在`customer\_email`表格上計算。

如果您使用`sales\_order`表格做為Customer表格，則在建立客戶層級量度時必須小心。 例如，考慮平均期限收入量度。 此量度用於識別整個客戶群的平均期限收入。 首先，需要新欄，讓每個客戶傳回其期限收入。 接著，您必須對此欄進行平均值，以取得客戶的平均期限收入。

如果您能使用`customer\_entity`表格，每一列都是單一客戶，而且該表格中每個客戶僅存在一次。 因此，當您有期限收入欄時，您只需要建立平均量度即可。 但是，如果您使用`sales\_order`表格作為客戶表格，則客戶可能會存在於許多列中。 設定期限收入欄後，指定客戶下的每個訂單（列）都會顯示客戶的期限收入；但您只想將該客戶納入整體平均量度一次。

訣竅在於您必須將篩選器新增至量度，確保只包含每位客戶一次。 Adobe鼓勵您建立並使用名為&#x200B;**我們計算的客戶**&#x200B;的篩選器集，該篩選器集會針對&#x200B;**客戶的訂單編號= 1**&#x200B;進行篩選（除了您可能需要排除不想要的客戶的其他篩選器之外）。 新增此篩選器可確保您將每個客戶僅納入客戶層級量度一次。

## 產品和類別

產品可以有多個類別，而類別可用於多個產品。 因此，在設定類別層級分析時，您必須小心使用正確的定義。 您要最上層類別嗎？ 第二層類別？ 如果產品可能屬於多個頂層類別，該怎麼辦？

想像一下，根據Commerce實作的定義，有一條牛仔褲屬於三個不同的類別層級：「服飾」（頂層）、「外套」（第二層）和「褲子」（第三層）。 您可能希望依售出件數來分析類別效能。 此分析所需的量度是&#x200B;_已售出專案_，這是建立在`sales\_order\_item`資料表上。 因此，您必須將類別層級資訊移至料號表格上。 `sales\_order\_item`表格上的每一列都有一個相關聯的`product\_id`，因此如果您知道與產品相關聯的類別，就可以將該資訊帶至所需的表格。

在移動任何資料之前，您必須先知道適當的連線和篩選器，以確保您抓取正確的類別。 對於某些分析，您可能需要知道「褲子」，但在其他分析中，「衣服」可能更合適。 這些是需個別識別的相異類別。 瞭解每個類別層次定義的方式，可確保您將單位銷售歸因到適合您特定分析的類別。

現在，假設您的網站首頁上也有`Our Favorites`頂層類別。 也許您已實作Commerce商店將這些牛仔褲納入`Clothing`類別和`Our Favorites`類別。 若是如此，這雙牛仔褲會有多個頂層類別。 在這種情況下，將單一最上層類別移至`sales\_order\_item`表格沒有意義，因為有多個選項。 為了說明這個問題，Adobe建議建立是/否要檢查特定類別的欄。 例如，`Is product in Clothing category?`和`Is product in Our Favorites category?`欄可讓您檢查產品是否屬於這些特定類別。
