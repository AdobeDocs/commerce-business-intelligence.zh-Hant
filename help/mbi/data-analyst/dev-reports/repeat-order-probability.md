---
title: 重複訂單概率報表
description: 瞭解並瞭解重複訂單概率報表。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 重複訂單概率報表

## 何時 `Incremental Event Probability` 透視可用？

的 `incremental event probability` 透視僅在篩選器使用與所有訂單相等的維時可用(例如，用戶 `gender`，用戶 `age` 或用戶 `source`)。

這是因為此透視依賴於名為 `User's order number` 細分，即用戶購買量（例如，John&#39;s 1、2nd和3d訂單）。

如果添加的篩選器使用的維不等於所有訂單(例如， `Order's Region`) `User's order number` 尺寸不再準確。 這是因為在為用戶訂單編號時，它不考慮特定區域（例如，John的第1、第2、第3個訂單仍然相同，而不管其區域如何）。

## 將特定於訂單的尺寸轉換為特定於用戶的尺寸

在某些情況下，您可能 `order-specific` 維到 `user-specific` 要添加為篩選器的維 `Repeat Order Probability` 圖表。 在這些情況下，您會返回用戶的第一訂單或最新訂單的訂單屬性（例如，用戶的第一訂單區域名稱）。

如果要建立新尺寸， [聯繫人支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 不同屬性訂單重複概率的比較

比較不同訂單屬性的重複採購數(例如，訂單的 `region`),Adobe建議建立類似於 `Users by lifetime number of orders`。 這顯示了生成1、2、3的用戶數……訂單的生存期數，並添加訂單層篩選器。 （換句話說，這可以向您顯示用戶是否在一個區域或另一個區域重複購買。）

然後，可以導出構成此圖表的數字以便計算重複順序概率比。 查看客戶完成 `(x)` 訂單 `(x+1)` 命令` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 購買。

### 示例：

| 類別 | 值 |
|---|---|
| 在有生之年購買了1個產品的客戶數 | `90` |
| 在有生之年進行2次購買的客戶數 | `30` |
| 在有生之年進行3次採購的客戶數 | `10` |
| 在有生之年已進行一次購買以進行第二次購買的客戶的重複訂單概率 | `(30 + 10) / (30+10+90) = 30.77%` |
