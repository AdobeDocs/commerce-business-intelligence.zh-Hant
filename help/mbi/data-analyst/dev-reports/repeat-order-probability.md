---
title: 重複訂購機率報表
description: 瞭解並瞭解「重複訂購機率報表」。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 重複訂購機率報表

## 何時為 `Incremental Event Probability` 有觀點嗎？

此 `incremental event probability` 「透視」僅適用於篩選條件使用對所有訂單都相等的維度時(例如 `gender`，使用者的 `age` 或使用者的 `source`)。

這是因為此觀點仰賴名為的維度 `User's order number` 適用於分段，即計算使用者的購買數（例如，John的第一次、第二次和第三次訂購）。

如果您新增的篩選器使用並非對所有訂單都相等的維度(例如， `Order's Region`)， `User's order number` 維度將不再準確。 這是因為在為使用者的訂單編號時，並未考慮特定地區（例如，John的第1、2、3筆訂單仍相同，無論其地區為何）。

## 將訂單特定維度轉換為使用者特定維度

在某些情況下，您或許可以將 `order-specific` 將維度移入 `user-specific` 要新增為篩選器的維度 `Repeat Order Probability` 圖表。 在這些情況下，您會傳回使用者第一訂單或最新訂單的訂單屬性（例如，使用者的第一訂單區域名稱）。

如果您想要建立這類新維度， [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## 比較不同屬性的訂單重複機率

若要比較不同訂單屬性(例如訂單的 `region`)，Adobe建議建立類似於 `Users by lifetime number of orders`. 這會顯示產生1、2、3...期限訂單數並新增訂單層級篩選器的使用者人數。 （換言之，這可顯示使用者是否在一個地區或另一個地區進行多次購買。）

組成此類圖表的數字可匯出至Excel以計算重複順序機率比率。 若要檢視客戶進行變更的可能性 `(x)` 要完成的訂單 `(x+1)` 訂購，簡單` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 購買。

### 範例：

| 類別 | 值 |
|---|---|
| 一生中購買1次的客戶數 | `90` |
| 一生中購買2次的客戶數 | `30` |
| 一生中購買3次的客戶數 | `10` |
| 已在其一生中購買過一次以進行第二次購買的客戶的重複訂購機率 | `(30 + 10) / (30+10+90) = 30.77%` |
