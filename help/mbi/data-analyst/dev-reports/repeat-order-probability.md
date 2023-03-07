---
title: 重複順序機率報表
description: 了解並了解「重複順序機率」報表。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 重複順序機率報表

## 何時為 `Incremental Event Probability` 透視圖可用？

此 `incremental event probability` 只有當篩選器使用所有訂單相等的維度時(例如使用者的 `gender`，使用者的 `age` 或使用者的 `source`)

這是因為此觀點仰賴以下維度： `User's order number` 用於細分，會將使用者的購買數量（例如，John的第1、第2和第3訂單）。

如果您新增的篩選器使用的維度不等於所有訂單(例如 `Order's Region`), `User's order number` 維度將不再準確。 這是因為在為使用者的訂單編號時，它不會計入特定區域（例如，無論其地區為何，John的第1、第2、第3訂單仍相同）。

## 將訂單特定維度轉換為使用者特定維度

在某些情況下，您可以將 `order-specific` 維度 `user-specific` 要新增為篩選器的維度 `Repeat Order Probability` 圖表。 在這些情況下，您會傳回使用者首次訂購或最新訂購的訂購屬性（例如，使用者的首次訂購地區名稱）。

如果要建立這樣的新維， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## 不同屬性下訂單重複概率的比較

比較不同訂單屬性(例如，訂單的 `region`),Adobe建議建立類似的圖表 `Users by lifetime number of orders`. 這會顯示下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數、下單數。 （換句話說，這可顯示使用者是否在一個地區或另一個地區重複購買。）

然後，組成此圖表的數字可匯出至excel以計算重複順序機率比。 查看客戶完成 `(x)` 訂購 `(x+1)` 命令` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 購買。

### 範例：

|  |  |
|---|---|
| 在其有限期內購買1次的客戶數 | `90` |
| 終身購買2次的客戶數 | `30` |
| 終身購買3次的客戶數 | `10` |
| 在有生之年曾購買過一次以進行第二次購買的客戶重複訂購的可能性 | `(30 + 10) / (30+10+90) = 30.77%` |
