---
title: 瞭解 [!DNL Commerce Intelligence] 環境
description: 瞭解與您的 [!DNL Commerce Intelligence] 環境。
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# 您 [!DNL Adobe Commerce Intelligence] 環境

在分析您的商業資料時，請注意這些因素和常見的誤解。 如果您需要幫助以確保正確使用您的Commerce架構，請毫不猶豫地 [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## [!DNL entity\_id]

您的許多表包含名為 `entity\_id`。 在包含 `entity\_id`，該列用於標識唯一行。

例如， `sales\_order` 表是唯一的順序。 此表中的主鍵稱為 `entity\_id`。 此列可以視為 `order\_id`。 在單獨的桌子上， `customer\_entity`，每行代表一個唯一的客戶。 此表中的主鍵也稱為 `entity\_id`，可以認為 `customer\_id`。

在那些桌子裡， `sales\_order.entity\_id` 不等於 `customer\_entity.entity\_id`。 對於包含 `entity\_id`: `table\_A.entity\_id` 不等於 `table\_B.entity\_id`。

## [!DNL Guest orders]

如果您允許客戶在沒有帳戶的情況下從您的站點訂購（來賓訂單），則這些客戶不會在您的站點中以行的形式填寫 `customer\_entity` 的子菜單。 此外，來賓所下的每個訂單都具有空值 `customer\_id` 值 `sales\_order` 的子菜單。

因此，如果您希望跟蹤來賓的行為隨時間推移而變化，則必須在 `sales\_order` 表，使用客戶標識符，如 `customer\_email`。

如果使用 `sales\_order` 表作為客戶表，然後在建立客戶級度量時必須小心。 例如，考慮平均生命週期收入度量。 此指標用於確定整個客戶群的平均生命週期收入。 這首先需要一個新列，每個客戶都可以返回其終身收入。 然後，您必須將此列平均化，以獲得客戶的平均生命週期收入。

如果你能夠 `customer\_entity` 表，每行是單個客戶，每個客戶只存在一次。 因此，當您有生命期收入列時，您只需建立一個平均度量。 但是，如果您使用 `sales\_order` 表作為客戶表，客戶可能存在於許多行中。 在設定生存期收入列後，給定客戶的每個訂單（行）將顯示該客戶的生存期收入；但您只希望將該客戶納入總體平均指標中一次。

這裡的訣竅是，您必須在指標中添加一個篩選器，以確保您只包括每個客戶一次。 Adobe鼓勵您建立和使用名為 **客戶數量** 用於 **客戶訂單編號= 1** （除了可能需要排除不需要的客戶的其他過濾器外）。 添加此篩選器可確保您只將每個客戶一次包括在客戶級別度量中。

## 產品和類別

產品可以具有多個類別，並且類別可用於多個產品。 因此，在設定類別級分析時，必須小心使用正確的定義。 是否要頂級類別？ 二級類別？ 如果產品可以分為多個頂級類別怎麼辦？

想像一條牛仔褲，它分為三個不同的類別級別，如Commerce實施所定義：「Cloting」（頂層）、「Outerwear」（二層）和「Pants」（三層）。 您可能希望按銷售數量分析您的類別效能。 此分析所需的度量是 _已售物料_，它建立在 `sales\_order\_item` 的子菜單。 因此，您需要將類別層資訊移到物料表中。 上的每一行 `sales\_order\_item` 表具有關聯 `product\_id`，因此，如果您知道與產品關聯的類別，可以將該資訊轉到所需的表中。

在移動任何資料之前，必須先知道正確的聯接和篩選器，以確保您獲取正確的類別。 對於一些分析，你可能需要知道「褲子」，但在其他分析中，「衣服」可能更合適。 這些是單獨標識的不同類別。 瞭解如何定義每個類別層可確保您能夠將單位銷售分配給適合您特定分析的類別。

現在，假設你還有 `Our Favorites` 網站首頁上的頂級類別。 也許您已實施了Commerce商店，將這些牛仔褲 `Clothing` 的 `Our Favorites` 的子菜單。 如果是，這條牛仔褲有不止一個頂級類別。 在這種情況下，將單個頂層類別移到 `sales\_order\_item` 桌子不太合理，因為有多種選擇。 為瞭解決此問題，Adobe建議建立檢查特定類別的是/否列。 比如說， `Is product in Clothing category?` 和 `Is product in Our Favorites category?` 列允許您檢查產品是否屬於這些特定類別。
