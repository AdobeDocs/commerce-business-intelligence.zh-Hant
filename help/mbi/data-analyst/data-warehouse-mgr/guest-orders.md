---
title: 來賓訂單
description: 了解來賓訂單對您的資料的影響，以及您必須正確計算來賓訂單的選項 [!DNL MBI] Data Warehouse。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 來賓訂單

在檢閱訂單時，若您發現 `customer\_id` 值為null或沒有值要重新連接到 `customers` 表格，這表示您的商店允許訪客訂單。 這表示您的 `customers` 表格很可能不包含所有客戶。

本主題討論來賓訂單對您的資料的影響，以及您必須正確計算來賓訂單的選項 [!DNL MBI] Data Warehouse。

## 訪客訂單對資料的影響

在一般的商務資料庫中， `orders` 連接到 `customers` 表格。 在 `orders` 表具有 `customer\_id` 欄，此欄對上的一列是唯一的 `customers` 表格。

* **如果所有客戶都已註冊** 和來賓訂單不允許，這意味著 `orders` 表格中有值 `customer\_id` 欄。 因此，每個訂單會重新連結至 `customers` 表格。 您可以在下圖中看到這個。

   ![](../../assets/guest-orders-4.png)

* **如果允許來賓訂單**，這表示某些訂單在 `customer\_id` 欄。 只有註冊客戶會獲得 `customer\_id` 欄 `orders` 表格。 未註冊的客戶會收到 `NULL` （或空白）值。 因此，並非所有訂單記錄都在 `customers` 表格。

   >[!NOTE]
   >
   >若要識別下訂單的不重複個人，除了以外，還需要有另一個不重複的使用者屬性 `customer\_id` 附加至訂單。 通常會使用客戶的電子郵件地址。

## 如何在Data Warehouse設定中說明來賓訂單

通常，實施您帳戶的銷售工程師在建立Data Warehouse的基礎時會考慮來賓訂單。

考慮來賓訂單的最佳方式，是將所有客戶層級量度設為 `orders` 表格。 此設定使用所有客戶都擁有的不重複客戶ID，包括來賓（通常會使用客戶電子郵件）。 這會忽略來自 `customers` 表格。 透過此選項，只有已購買至少一次的客戶才會納入客戶層級報表中。 尚未購買過一次的註冊使用者不包含在內。 使用此選項，您的 `New customer` 量度是根據 `orders` 表格。

您可能會注意到 `Customers we count` 此類型設定中的篩選器集具有 `Customer's order number = 1`. 想想為什麼會這樣。

![](../../assets/guest-orders-filter-set.png)

在沒有訪客訂單的情況下，每個客戶在客戶表格中都以唯一列的形式存在（請參閱圖1）。 量度，例如 `New customers` 只需根據 `created\_at` 根據註冊日期了解新客戶的日期。

在客戶訂單設定中，所有客戶量度均以 `orders` 表來說明來賓訂單，您必須確保 `not counting customers twice`. 如果計算訂單表的id，則會計算每筆訂單。 若您改為計算 `orders` 表格，並使用篩選器， `Customer's order number = 1`，則您會計算每個不重複客戶 `only one time`. 這適用於所有客戶層級量度，例如 `Customer's lifetime revenue` 或 `Customer's lifetime number of orders`.

在上方的影像2中，您會看到有null `customer\_ids` 在 `orders` 表格。 如果您使用 `customer\_email` 若要識別不重複客戶，您可以看到 `erin@test.com` 下了三(3)份訂單。 因此，您可以建置 `New customers` 量度 `orders` 表格，依據下列條件：

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
