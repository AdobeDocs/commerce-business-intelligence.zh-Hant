---
title: 了解和評估表關係
description: 了解如何了解一個表格中可能發生的次數可能屬於另一個表格中的實體。
exl-id: e7256f46-879a-41da-9919-b700f2691013
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# 了解和評估表關係

在評估兩個指定表之間的關係時，您需要了解一個表中可能出現的次數有多少可能屬於另一個表中的實體，反之亦然。 例如，使用 `users` 表格和 `orders` 表格。 在這種情況下，您想知道 **訂購** 給予 **使用者** 已放置，可能的數量 **使用者** an **訂購** 屬於。

了解關係對於維護資料完整性至關重要，因為它會影響您的 [計算欄](../data-warehouse-mgr/creating-calculated-columns.md) 和 [維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md). 若要進一步了解，請參閱 [關係類型](#types) 和 [如何評估Data Warehouse中的表格。](#eval)

## 關係類型 {#types}

兩個表之間可以存在三種關係：

* [「一對一」](#onetoone)
* [「一對多」](#onetomany)
* [「多對多」](#manytomany)

### `One-to-One` {#onetoone}

在 `one-to-one` 關係，表中的記錄 `B` 僅屬於表中的一條記錄 `A`. 還有一張表格 `A` 僅屬於表中的一條記錄 `B`.

例如，在人與駕照號之間的關係中，一個人只能擁有一個駕照號，而駕照號只屬於一個人。

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

在 `one-to-many` 關係，表中的記錄 `A` 可能屬於表中的數條記錄 `B`. 想想 `orders` 和 `items`  — 訂單可包含許多項目，但某個項目屬於單一訂單。 在此情況下， `orders` 桌子是一面 `items` 桌子是多面的。

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

在 `many-to-many` 關係，表中的記錄 `B` 可能屬於表中的數條記錄 `A`. 反之，表格中的記錄 `A` 可能屬於表中的數條記錄 `B`.

想想 **產品** 和 **類別**:產品可以屬於許多類別，而類別可以包含許多產品。

![](../../assets/many-to-many.png)

## 評估表 {#eval}

給定表之間存在的關係類型，您可以了解如何評估Data Warehouse中的表。 由於這些關係決定了多表計算列的定義方式，因此您必須了解如何標識表關係以及哪一邊 —  `one` 或 `many`  — 表所屬。

您可以使用兩種方法來評估Data Warehouse內指定對表的關係。 第一種方法採用 [概念框架](#concept) 考量表格實體彼此互動的方式。 第二個方法使用 [表的架構](#schema).

### 使用概念框架 {#concept}

此方法使用概念框架來說明兩個表格中的實體如何彼此互動。 必須理解，鑒於這種關係，這一框架評估了哪些可能。

例如，思考使用者和訂單時，會考量關係中可能的所有條件。 註冊用戶在其期限內不得下任何訂單、只能下一訂單或多個訂單。 如果您已啟動業務且尚未下訂單，則指定使用者在有生命週期中可能會下許多訂單。 這些表是為了適應這一情況而構建的。

若要使用此方法：

1. 標識每個表中描述的實體。 **提示：通常是名詞**. 例如， `user` 和 `orders` 表格會明確說明使用者和順序。
1. 識別描述這些實體如何互動的一或多個動詞。 例如，在比較使用者與訂單時，使用者會「下」訂單。 向另一個方向，訂單「屬於」使用者。

此類型的框架可應用於Data Warehouse中任何表的配對。 這可讓您輕鬆識別關係的類型，以及哪個表是一側，哪個表是多側。

一旦確定了描述兩個表如何交互的術語後，請考慮第一個實體的一個給定實例與第二個實例的關係，以雙向框架交互。 以下是每種關係的一些範例：

### `One-to-One`

一個指定的人只能有一個駕駛執照號。 一個給定的駕照號只屬於人。

這是 `one-to-one` 關係，其中每個表是一邊。

![](../../assets/one-to-one3.png)

### `One-to-Many`

一個訂單可能包含許多項。 一個指定項目只屬於一個訂單。

這是 `one-to-many` 關係，其中orders表為一側，items表為多側。

![](../../assets/one-to-many3.png)

### `Many-to-Many`

一個特定產品可能屬於許多類別。 一個給定的類別可能包含許多產品。

這是 `many-to-many` 關係，其中每個表是多邊。

![](../../assets/many-to-many3.png)

### 使用表的架構 {#schema}

第二個方法使用表架構。 架構會定義 [`Primary`](https://en.wikipedia.org/wiki/Unique_key) 和 [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) 鍵。 您可以使用這些鍵將表連結在一起，並幫助確定關係類型。

在確定將兩個表連結在一起的列後，請使用列類型來評估表關係。 以下是一些範例：

### `One-to-one`

如果表使用 `primary key` ，則每個表中都描述相同的唯一實體，且關係為 `one-to-one`.

例如， `users` 表可以捕獲大多數用戶屬性（如名稱），而補充 `user_source` 表捕獲用戶註冊源。 在每個表格中，一列代表一個使用者。

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>你接受客人的訂單嗎？請參閱 [來賓訂單](../data-warehouse-mgr/guest-orders.md) 了解來賓訂單如何影響您的表關係。

使用 `Foreign key` 指向 `primary key`，此設定說明 `one-to-many` 關係。 一側是包含 `primary key` 多邊是包含 `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

如果下列其中一項為真，則關係為 `many-to-many`:

* `Non-primary key` 欄來連結兩個表格
   ![](../../assets/many-to-many1.png)
* 複合材料的一部分 `primary key` 用於連結兩個表

![](../../assets/many-to-mnay2.png)

## 後續步驟

正確評估表關係對於準確建模資料至關重要。 現在，您已了解表格彼此的關聯方式，請參閱 [您可以對Data Warehouse管理員執行什麼動作](../data-warehouse-mgr/tour-dwm.md).
