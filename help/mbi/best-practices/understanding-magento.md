---
title: 了解您的 [!DNL MBI] 環境
description: 了解如何使用和改善 [!DNL MBI] 環境。
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# 您的 [!DNL MBI] 環境

分析商務資料時，請注意這些因素和常見的誤解。 若您需要協助以確定您正確使用商務結構，請立即 [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## [!DNL entity\_id]

許多表都包含一個名為 `entity\_id`. 在包含 `entity\_id`，該欄可用來識別不重複列。

例如， `sales\_order` 表格是唯一順序。 此表中的主鍵稱為 `entity\_id`. 本欄可視為 `order\_id`. 在另一張桌子裡， `customer\_entity`，每一列代表一個不重複客戶。 此表中的主鍵也稱為 `entity\_id`，可以認為 `customer\_id`.

在那些桌子裡， `sales\_order.entity\_id` 不等於 `customer\_entity.entity\_id`. 對於包含的所有表集，都適用這個規則 `entity\_id`: `table\_A.entity\_id` 不等於 `table\_B.entity\_id`.

## [!DNL Guest orders]

如果您允許客戶在沒有帳戶的情況下從您的網站進行訂購（來賓訂購），則這些客戶不會在您的 `customer\_entity` 表格。 此外，來賓下的每個訂單都有一個空值 `customer\_id` 值 `sales\_order` 表格。

因此，如果您想要追蹤訪客的行為並隨時間改變，則必須依 `sales\_order` 表格，使用客戶識別碼，例如 `customer\_email`.

如果您使用 `sales\_order` 表格作為客戶表格時，建立客戶層級量度時請務必小心。 例如，假設有平均期限收入量度。 此量度可用來識別整個客戶群的平均期限收入。 首先需要新欄，供每位客戶傳回其終身收入。 然後，您必須平均此欄，才能取得客戶的平均期限收入。

如果您能使用 `customer\_entity` 表格中，每一列都是單一客戶，而每個客戶只存在於該表格中一次。 因此，若您有期限收入欄，您只需建立平均量度即可。 不過，如果您使用 `sales\_order` 表格作為客戶表格，客戶可能存在於許多列中。 設定期限收入欄後，指定客戶放置的每個訂單（列）都會顯示該客戶的期限收入；但您只想將該客戶納入整體平均量度一次。

這裡的訣竅在於，您必須在量度中新增篩選器，以確保您只納入每個客戶一次。 Adobe建議您建立並使用已命名的篩選器集 **我們數** 篩選 **客戶訂單編號= 1** （除了其他篩選器，您可能需要排除不想要的客戶）。 新增此篩選器可確保您只將每位客戶納入客戶層級量度一次。

## 產品與類別

產品可以有多個類別，而類別可用於多個產品。 因此，在設定類別層級分析時，必須小心使用正確的定義。 是否要頂級類別？ 二級類別？ 如果產品可分為多個頂層類別，該怎麼辦？

試想一條牛仔褲，可分為三個不同的類別等級，由商務實施所定義：「Clothing」（頂層）、「Outerwear」（第二層）和「Pants」（第三層）。 您可能希望按售出件數分析類別績效。 此分析所需的量度為 _已售項目_，此元件建置於 `sales\_order\_item` 表格。 因此，您需要將類別層級資訊移至項目表格。 上的每一列 `sales\_order\_item` 表具有關聯 `product\_id`，因此如果您知道與產品相關聯的類別，可以將該資訊帶入所需的表格。

在移動任何資料之前，您必須先知道正確的聯接和篩選器，以確保您抓取正確的類別。 對於某些分析，您可能需要知道「褲子」，但在其他分析中，「服裝」可能更合適。 這些是個別識別的不同類別。 了解每個類別層的定義方式可確保您將單位銷售歸因於適合您特定分析的類別。

現在，假設您也有 `Our Favorites` 頂層類別。 您可能已實作您的商務商店，將這些牛仔褲加入 `Clothing` 類別和 `Our Favorites` 類別。 如果是，這條牛仔褲不止一個頂級類別。 在此情況下，將單一頂層類別移至 `sales\_order\_item` 表格並不太合理，因為有多種選項。 為了解決此問題，Adobe建議建立「是」/「否」欄，以檢查特定類別。 例如， `Is product in Clothing category?` 和 `Is product in Our Favorites category?` 欄可讓您檢查產品是否屬於這些特定類別。
