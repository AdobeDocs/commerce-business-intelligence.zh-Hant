---
title: 瞭解並評估表格關係
description: 瞭解如何瞭解一個表格中可能屬於另一個實體多少個事件。
exl-id: e7256f46-879a-41da-9919-b700f2691013
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# 瞭解並評估表格關係

評估兩個給定表格之間的關係時，您需要瞭解一個表格中可能屬於另一個實體可能的出現次數，反之亦然。 例如，使用`users`表格和`orders`表格。 在此案例中，您想要瞭解指定的&#x200B;**使用者**&#x200B;已下多少&#x200B;**訂單**，以及可能屬於多少個&#x200B;**使用者** **訂單**。

瞭解關聯性對於維護資料完整性至關重要，因為它會影響您[計算的資料行](../data-warehouse-mgr/creating-calculated-columns.md)和[維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)的正確性。 若要深入瞭解，請參閱[關聯性型別](#types)和[如何評估Data Warehouse中的資料表。](#eval)

## 關係型別 {#types}

兩個資料表之間可以存在三種關聯性：

1. [&#39;一對一&#39;](#onetoone)
1. [&#39;一對多&#39;](#onetomany)
1. [&#39;多對多&#39;](#manytomany)

### `One-to-One` {#onetoone}

在`one-to-one`關聯性中，資料表`B`中的記錄只屬於資料表`A`中的一個記錄。 而且資料表`A`中的記錄只屬於資料表`B`中的一個記錄。

例如，在人與駕照號碼之間的關係中，一個人只能有一個駕照號碼，而一個駕照號碼只屬於個人。

![顯示兩個實體間一對一關係的圖表](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

在`one-to-many`關聯性中，資料表`A`中的記錄可能屬於資料表`B`中的數個記錄。 想一想`orders`與`items`之間的關係 — 一個訂單可以包含許多專案，但一個專案屬於單一訂單。 在這種情況下，`orders`表格是一面，`items`表格是多面。

![顯示訂單與專案之間一對多關係的圖表](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

在`many-to-many`關聯性中，資料表`B`中的記錄可能屬於資料表`A`中的數個記錄。 反之亦然，資料表`A`中的記錄可能屬於資料表`B`中的數個記錄。

想一想&#x200B;**產品**&#x200B;和&#x200B;**類別**&#x200B;之間的關係：一個產品可以屬於許多類別，而一個類別可以包含許多產品。

![顯示產品與類別之間多對多關係的圖表](../../assets/many-to-many.png)

## 評估表格 {#eval}

根據表格之間存在的關係型別，您可以瞭解如何評估Data Warehouse中的表格。 由於這些關係塑造了多資料表計算資料行的定義方式，因此請務必瞭解如何識別資料表關係，以及資料表屬於哪一邊 — `one`或`many`。

在Data Warehouse中，有兩種方法可用來評估指定表格組的關係。 第一個方法採用[概念架構](#concept)，考量資料表的實體彼此互動的方式。 第二個方法使用[資料表的結構描述](#schema)。

### 使用概念架構 {#concept}

此方法使用概念架構來說明兩個表格中的實體如何彼此互動。 重要的是，要瞭解此框架會評估在給定關係下可能的情況。

例如，在考慮使用者和訂單時，考慮關係中可能的所有條件。 註冊使用者在存留期內不得下任何訂單、僅能下一份訂單或多份訂單。 如果您已啟動業務，但尚未下訂單，則特定使用者可以在其存留期內下許多訂單。 建置表格就是為了因應這種情況。

若要使用此方法：

1. 識別每個表格中描述的實體。 **提示：它通常是名詞**。 例如，`user`和`orders`資料表明確說明使用者和順序。

1. 識別一或多個描述這些實體如何互動的動詞。 例如，將使用者與訂單比較時，使用者會「下單」。 另一方面，訂單「屬於」使用者。

此型別的架構可套用至Data Warehouse中的任何表格配對。 這可讓您輕鬆識別關係的型別、哪個表格是一側而哪個表格是多側。

一旦確定了描述兩個表格如何互動的術語，就可以考慮第一個實體的一個特定例項如何與第二個實體相關，以雙向設定互動的框架。 以下是每種關係的一些範例：

### `One-to-One`

一個指定人員只能有一個駕駛執照號碼。 一個特定駕照號碼只屬於個人。

這是`one-to-one`關係，其中每個資料表都是單面。

![個人與駕駛執照之間一對一關係的概念圖表](../../assets/one-to-one3.png)

### `One-to-Many`

一個特定訂單可能包含許多專案。 一個指定專案只屬於一個訂單。

這是一種`one-to-many`關係，其中訂購表格是一面，而料號表格是多面。

![訂單與專案之間一對多關係的概念圖表](../../assets/one-to-many3.png)

### `Many-to-Many`

一個特定產品可能屬於多個類別。 一個指定類別可以包含許多產品。

這是`many-to-many`關係，其中每個資料表都是多面。

![產品與類別之間多對多關係的概念圖表](../../assets/many-to-many3.png)

### 使用表格的綱要 {#schema}

第二個方法使用表格結構描述。 結構描述會定義哪些資料行是[`Primary`](https://en.wikipedia.org/wiki/Unique_key)和[`Foreign`](https://en.wikipedia.org/wiki/Foreign_key)索引鍵。 您可以使用這些鍵將表格連結在一起，並協助判斷關係型別。

識別將兩個表格連結在一起的欄之後，請使用欄型別來評估表格關係。 以下是一些範例：

### `One-to-one`

如果使用兩個資料表的`primary key`連結資料表，則每個資料表中會說明相同的唯一實體，而且關聯性為`one-to-one`。

例如，`users`表格可能會擷取大部分的使用者屬性（例如名稱），而補充`user_source`表格則會擷取使用者註冊來源。 在每個表格中，一列代表一位使用者。

![使用主索引鍵顯示一對一關係的結構描述圖表](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>您接受客服訂單嗎？ 請參閱[訪客訂單](../data-warehouse-mgr/guest-orders.md)，瞭解訪客訂單如何影響您的資料表關係。

使用指向`Foreign key`的`primary key`連結資料表時，此設定會說明`one-to-many`關係。 一方是包含`primary key`的資料表，而多面是包含`foreign key`的資料表。

![使用外部索引鍵顯示一對多關聯性的結構描述圖表](../../assets/one-to-many1.png)

### `Many-to-many`

如果下列任一專案為true，則關聯性為`many-to-many`：

* `Non-primary key`欄正用於連結兩個資料表
  ![結構描述圖表顯示使用非主索引鍵的多對多關係](../../assets/many-to-many1.png)
* 複合`primary key`的一部分用於連結兩個資料表

![結構描述圖表顯示使用複合主索引鍵的多對多關係](../../assets/many-to-mnay2.png)

## 後續步驟

正確評估表格關係是精確建立資料模型的關鍵。 現在您已瞭解資料表如何相互關聯，請參閱[您可以使用Data Warehouse管理員做什麼](../data-warehouse-mgr/tour-dwm.md)。
