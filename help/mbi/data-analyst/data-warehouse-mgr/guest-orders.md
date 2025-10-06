---
title: 來賓訂單
description: 瞭解訪客訂單對您資料的影響，以及在 [!DNL Commerce Intelligence] Data Warehouse中正確說明訪客訂單的選項。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 賓客訂單

在檢閱您的訂單時，如果您發現許多`customer\_id`值為空，或沒有可連線回`customers`表格的值，這表示您的商店允許訪客訂單。 這表示您的`customers`資料表很可能並未包含您的所有客戶。

此主題討論訪客訂單對您資料的影響，以及在[!DNL Commerce Intelligence] Data Warehouse中正確說明訪客訂單的選項。

## 訪客訂單對資料的影響

在一般商務資料庫中，有`orders`資料表聯結至`customers`資料表。 `orders`表格的每一列都有一個`customer\_id`欄，它對`customers`表格中的一列而言是唯一的。

* **如果所有客戶皆已註冊**，且不允許來賓訂單，則表示`orders`資料表中的每筆記錄在`customer\_id`資料行中都有一個值。 因此，每個訂單都會聯結回`customers`表格。

  ![客服訂單資料表顯示客戶資訊](../../assets/guest-orders-4.png)

* **如果允許來賓訂單**，這表示某些訂單在`customer\_id`欄中沒有值。 在`customer\_id`資料表上，`orders`資料行的值只提供給已註冊客戶。 未註冊的客戶會收到此欄的`NULL` （或空白）值。 因此，並非所有訂單記錄在`customers`資料表中都有相符的記錄。

  >[!NOTE]
  >
  >若要識別發出訂單的唯一個人，必須在訂單所附的`customer\_id`旁有另一個唯一的使用者屬性。 通常會使用客戶的電子郵件地址。

## 如何在Data Warehouse設定中說明來賓訂單

實作您帳戶的銷售工程師在建立Data Warehouse的基礎時，通常會考量訪客訂單。

說明訪客訂單的最佳方式是以`orders`表格作為所有客戶層級量度的基礎。 此設定使用所有客戶擁有的唯一客戶ID，包括來賓（通常使用客戶電子郵件）。 這會忽略來自`customers`表格的註冊資料。 使用此選項時，客戶層級報表中只會包含至少購買過一次的客戶。 尚未購買一次的註冊使用者不包括在內。 透過此選項，您的`New customer`量度會以`orders`表格中客戶的第一個訂購日期為基礎。

您可能會注意到，在此設定型別中設定的`Customers we count`篩選器有`Customer's order number = 1`的篩選器。

![用於排除來賓訂單的篩選器集組態](../../assets/guest-orders-filter-set.png)

在沒有訪客訂單的情況下，每個客戶在客戶表格中都以唯一資料列存在（請參閱圖1）。 `New customers`之類的量度可以僅根據`created\_at`日期計算此資料表的ID，以根據註冊日期瞭解新客戶。

在來賓訂單設定中，所有客戶量度都以`orders`資料表為基礎，以說明來賓訂單，您必須確保您是`not counting customers twice`。 如果您計算訂單表格的ID，則會計算每個訂單。 如果您改為計算`orders`資料表上的ID並使用篩選器`Customer's order number = 1`，則您將會計算每個唯一客戶`only one time`。 這適用於所有客戶層級的量度，例如`Customer's lifetime revenue`或`Customer's lifetime number of orders`。

您可以在上方看到`customer\_ids`資料表中有Null `orders`。 如果您使用`customer\_email`識別不重複客戶，可以看到`erin@test.com`已下三(3)份訂單。 因此，您可以根據下列條件在`New customers`資料表上建置`orders`量度：

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
