---
title: 重複訂購機率報表
description: 瞭解並瞭解「重複訂購機率報表」。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 343
ht-degree: 0%

---

# 重複訂購機率報表

## 何時可以使用`Incremental Event Probability`觀點？

只有當篩選器使用對所有訂單都相等的維度（例如，使用者的`incremental event probability`、使用者的`gender`或使用者的`age`）時，`source`透視才可用。

這是因為此觀點仰賴名為`User's order number`的維度來分段，該維度會計算使用者的購買數（例如John的第一次、第二次和第三次訂購）。

如果您新增的篩選器所使用的維度並非對所有訂單都相等（例如，`Order's Region`），`User's order number`維度將不再正確。 這是因為在為使用者的訂單編號時，並未考慮特定地區（例如，John的第1、2、3筆訂單仍相同，無論其地區為何）。

## 將訂單特定維度轉換為使用者特定維度

在某些情況下，您或許可以將`order-specific`維度轉換為`user-specific`維度，以新增為`Repeat Order Probability`圖表中的篩選器。 在這些情況下，您會傳回使用者第一訂單或最新訂單的訂單屬性（例如，使用者的第一訂單區域名稱）。

若要建立這類新維度，[請連絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 比較不同屬性的訂單重複機率

若要比較不同訂單屬性（例如訂單的`region`）的重複購買次數，Adobe建議建立類似於`Users by lifetime number of orders`的圖表。 這會顯示產生1、2、3...期限訂單數並新增訂單層級篩選器的使用者人數。 （換言之，這可顯示使用者是否在一個地區或另一個地區進行多次購買。）

組成此類圖表的數字可匯出至Excel以計算重複順序機率比率。 若要檢視客戶下達`(x)`份訂單以發出`(x+1)`份訂單的可能性，只需購買` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)`份即可。

### 範例：

| 類別 | 值 |
|---|---|
| 一生中購買1次的客戶數 | `90` |
| 一生中購買2次的客戶數 | `30` |
| 一生中購買3次的客戶數 | `10` |
| 已在其一生中購買過一次以進行第二次購買的客戶的重複訂購機率 | `(30 + 10) / (30+10+90) = 30.77%` |
