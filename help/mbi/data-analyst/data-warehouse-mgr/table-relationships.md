---
title: 瞭解和評估表關係
description: 瞭解如何瞭解一個表中可能出現的事件可能屬於另一個表中的實體。
exl-id: e7256f46-879a-41da-9919-b700f2691013
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# 瞭解和評估表關係

在評估兩個給定表之間的關係時，您需要瞭解一個表中可能出現的實例可能屬於另一個表中的實體，反之亦然。 例如，使用 `users` 和 `orders` 的子菜單。 在這種情況下，你想知道 **訂單** 給予 **用戶** 已放置和可能 **用戶** 一個 **訂單** 可能屬於。

瞭解關係對於維護資料完整性至關重要，因為它會影響您的 [計算列](../data-warehouse-mgr/creating-calculated-columns.md) 和 [尺寸](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。 要瞭解更多資訊，請參閱 [關係類型](#types) 和 [如何計算Data Warehouse中的表。](#eval)

## 關係類型 {#types}

兩個表之間可以存在三種關係：

1. [「一對一」](#onetoone)
1. [「一對多」](#onetomany)
1. [「多對多」](#manytomany)

### `One-to-One` {#onetoone}

在 `one-to-one` 關係，表中的記錄 `B` 只屬於表中的一條記錄 `A`。 表中的記錄 `A` 僅屬於表中的一條記錄 `B`。

例如，在人與駕照號的關係中，一個人只能有一個駕照號，一個駕照號只屬於一個人。

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

在 `one-to-many` 關係，表中的記錄 `A` 可能屬於表中的多個記錄 `B`。 想想看 `orders` 和 `items`  — 訂單可以包含許多物料，但物料屬於單個訂單。 在這個例子中， `orders` 桌子是一面 `items` 桌子是多面的。

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

在 `many-to-many` 關係，表中的記錄 `B` 可能屬於表中的多個記錄 `A`。 反之，表中的記錄 `A` 可能屬於表中的幾個記錄 `B`。

想想看 **產品** 和 **類別**:一個產品可以屬於多個類別，一個類別可以包含多個產品。

![](../../assets/many-to-many.png)

## 計算表 {#eval}

給定表之間存在的關係類型，您可以學習如何評估Data Warehouse中的表。 由於這些關係決定了多表計算列的定義方式，因此瞭解如何識別表關係和哪一方非常重要 —  `one` 或 `many`  — 表屬於。

有兩種方法可用於評估Data Warehouse中給定對表的關係。 第一種方法採用 [概念框架](#concept) 它考慮了表的圖元之間如何交互。 第二種方法使用 [表的架構](#schema)。

### 使用概念框架 {#concept}

該方法使用概念框架描述兩個表中的實體如何相互交互。 必須瞭解，考慮到這種關係，這一框架評估了可能的情況。

例如，在考慮用戶和訂單時，會考慮關係中可能的所有內容。 註冊用戶在其生命週期內不能下訂單、只能下單或下多份訂單。 如果您已啟動業務且尚未下訂單，則給定用戶在其有生之年可能會下許多訂單。 這些表是為了適應這一點而構建的。

要使用此方法：

1. 標識每個表中描述的實體。 **提示：通常是名詞**。 例如， `user` 和 `orders` 表是對用戶和訂單的顯式描述。

1. 確定一個或多個描述這些實體如何交互的動詞。 例如，在將用戶與訂單進行比較時，用戶會「下訂單」。 向另一個方向，命令「屬於」用戶。

此類框架可應用於Data Warehouse中任何表的配對。 這樣，您就可以輕鬆確定關係類型，以及哪個表是單面，哪個表是多面。

一旦確定了描述兩個表如何交互的術語，就會考慮第一個實體的一個給定實例與第二個實體的關聯方式，從而將交互框定為兩個方向。 下面是每種關係的一些示例：

### `One-to-One`

一個給定人只能有一個駕駛執照號。 給定駕照號的一個只屬於個人。

這是 `one-to-one` 關係，其中每個表是一邊。

![](../../assets/one-to-one3.png)

### `One-to-Many`

一個給定訂單可能包含許多項。 一個給定項只屬於一個訂單。

這是 `one-to-many` 關係，其中訂單表為一側，項目表為多側。

![](../../assets/one-to-many3.png)

### `Many-to-Many`

一個給定的產品可能屬於多個類別。 一個給定類別可能包含許多產品。

這是 `many-to-many` 關係，其中每個表是多邊。

![](../../assets/many-to-many3.png)

### 使用表的架構 {#schema}

第二種方法使用表模式。 架構定義哪些列是 [`Primary`](https://en.wikipedia.org/wiki/Unique_key) 和 [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) 按鈕。 您可以使用這些鍵將表連結在一起並幫助確定關係類型。

在確定將兩個表連結在一起的列後，使用列類型來評估表關係。 以下是一些示例：

### `One-to-one`

如果表使用 `primary key` 表中的唯一實體，然後在每個表中描述同一唯一實體，並且關係 `one-to-one`。

例如， `users` 表可捕獲大多數用戶屬性（如名稱），而補充屬性 `user_source` 表捕獲用戶註冊源。 在每個表中，一行表示一個用戶。

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>您接受來賓訂單嗎？請參閱 [來賓訂單](../data-warehouse-mgr/guest-orders.md) 瞭解來賓訂單如何影響表關係。

當使用 `Foreign key` 指向 `primary key`，此安裝程式說明 `one-to-many` 關係。 一側是包含 `primary key` 多邊是包含 `foreign key`。

![](../../assets/one-to-many1.png)

### `Many-to-many`

如果以下任一項為true，則關係為 `many-to-many`:

* `Non-primary key` 列用於連結兩個表
   ![](../../assets/many-to-many1.png)
* 複合的一部分 `primary key` 用於連結兩個表

![](../../assets/many-to-mnay2.png)

## 後續步驟

正確評估表關係對準確建模資料至關重要。 現在，您瞭解了表之間的關係，請參見 [可以用Data Warehouse管理器做什麼](../data-warehouse-mgr/tour-dwm.md)。
